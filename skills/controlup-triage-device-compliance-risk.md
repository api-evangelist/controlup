---
name: Triage endpoint compliance risk for a ControlUp-managed device
description: >-
  Find a managed device in ControlUp for Compliance and pull its complete security posture — score, agent status,
  detected CVEs, missing OS and application patches, failed compliance controls and misconfigurations — so an agent
  can rank what to remediate first.
api: openapi/controlup-compliance-openapi.yml
base_url: https://api.controlup.com/compliance
operations:
  - getDevices
  - getDeviceDetails
  - getDeviceVulnerabilities
  - getDevicePatches
  - getDeviceCompliance
  - getDeviceMisconfig
mcp_tools:
  - list-devices
  - get-device-details
  - list-device-vulnerabilities
  - list-device-patches
  - list-device-compliance
  - list-device-misconfigurations
generated: '2026-08-04'
method: generated
---

# Triage endpoint compliance risk

## Before you start

- **Auth.** Every call carries `Authorization: Bearer <API_KEY>`. The key is created in the ControlUp ONE console
  under **API Key Management** and has an expiry duration set at creation time.
- **Permissions.** An API key inherits the permissions of the user who created it, and only permissions assigned
  **directly** to that ControlUp user account apply — permissions inherited through an identity-provider group do
  **not** grant API access. A 403 here usually means the permission is group-derived, not that the key is wrong.
- **Rate budget.** 60 requests/minute per user, 200/minute per organization, shared across every key that user
  owns. This skill makes 1 + 5N calls for N devices — page the device list and batch, do not fan out.
- **No idempotency key exists.** Every operation in this skill is a `GET`, so retries are safe by method, not by
  contract.

## Steps

1. **Find the device.** `getDevices` — `GET /devices`. Supports filtering by device property and paging. The
   platform paging convention here is `_page` and `_limit`; filters are **contains** matchers, case-insensitive,
   OR-ed within one parameter and AND-ed across parameters. Repeat the same parameter to widen, add a different
   parameter to narrow. Use `_search` to match any field when you only have a fragment of a hostname.

2. **Read the posture summary.** `getDeviceDetails` — `GET /devices/{device_id}`. Returns the device's security
   score and agent status. Treat the score as the ranking key across devices; treat agent status as a validity
   gate — a stale or offline agent means the findings below are stale too, and should be reported as
   *unknown*, not as *clean*.

3. **Pull the four finding sets.** These are independent and can be read in any order:
   - `getDeviceVulnerabilities` — `GET /devices/{device_id}/vulnerabilities` — detected CVEs.
   - `getDevicePatches` — `GET /devices/{device_id}/patches` — missing OS and application patches.
   - `getDeviceCompliance` — `GET /devices/{device_id}/compliance` — failed security controls and benchmarks.
   - `getDeviceMisconfig` — `GET /devices/{device_id}/misconfig` — security settings deviating from policy.

4. **Rank.** Cross-reference: a CVE from step 3 that is closed by a patch already listed in
   `getDevicePatches` is a single remediation, not two. Report the patch as the action and the CVEs as its
   justification.

## Error handling

Error bodies are plain `application/json`, not RFC 9457 problem details, and no stable machine-readable error
code is published — branch on HTTP status.

| Status | Meaning | Do |
|---|---|---|
| 400 | Bad request | Check `_page`/`_limit` and filter parameter names against the spec. |
| 401 | Bad or expired key | The key duration elapsed, the key was revoked, or the owning user was disabled or deleted. |
| 403 | Permission missing | Verify the permission is assigned directly to the user, not via an IdP group. |
| 404 | Unknown `device_id` | Ids are organization-scoped; re-resolve through `getDevices`. |
| 429 | Rate limited | No `Retry-After` or `RateLimit-*` header is published — back off against the documented 60/min per-user budget. |
| 500 | Server error | Retry with backoff, then open a ticket at support.controlup.com. |

## Related

- `conventions/controlup-conventions.yml` — filtering, paging and auth semantics in full.
- `errors/controlup-problem-types.yml` — the derived status catalog.
- `mcp/controlup-tool-crosswalk.yml` — the six MCP `cu4c` tools that bind one-to-one to these operations.
