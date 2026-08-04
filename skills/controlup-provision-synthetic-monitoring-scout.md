---
name: Provision a Synthetic Monitoring Scout and its alert policy
description: >-
  Stand up a ControlUp Synthetic Monitoring Scout (EUC or network), attach an alert policy with a webhook
  notification, verify it is running, and read back test results and triggered alerts.
api: openapi/controlup-synthetic-monitoring-openapi.yml
base_url: https://api.controlup.com/synthetic-monitoring/v2/
operations:
  - honeycomb.api.custom_hives
  - honeycomb.api.cloud_hives
  - app.create_scout
  - app.get_scouts
  - app.get_scout_by_id
  - app.edit_scout
  - app.disable_scout
  - app.create_scout_alert
  - app.get_scout_alert_policies
  - app.get_scout_alert
  - app.update_scout_alert
  - app.get_tests
  - app.get_alerts
  - app.get_alert_for_scout
  - honeycomb.api.get_org_integrations
mcp_tools:
  - list-hives
  - list-cloud-hives
  - create-scout-euc
  - create-scout-net
  - get-scout
  - toggle-scout
  - create-alert-policy
  - list-alert-policies
  - list-tests
  - list-alerts
  - list-integrations
generated: '2026-08-04'
method: generated
---

# Provision a Synthetic Monitoring Scout

A **Scout** is a scheduled synthetic test. An **EUC Scout** logs into a virtual desktop stack (Citrix, Omnissa
Horizon, AVD and others) on an interval; a **Network Scout** tests HTTP endpoints, DNS, ping and traceroute. A
**Hive** is where the Scout runs from — a Cloud Hive hosted by ControlUp, or a Custom Hive you run on-premises.

## Before you start

- **Auth.** `Authorization: Bearer <API_KEY>` on every call.
- **Rate budget — this surface has its own limits, tighter than the rest of the estate.**
  `app.create_scout` and `app.create_scout_alert` are each capped at **10 requests per minute**. Everything else
  on this API is **100 per minute**. Bulk provisioning must be paced.
- **Paging dialect.** Synthetic Monitoring uses `page`/`pageSize`, **not** the `_page`/`_limit` pair used by the
  platform, Desktops and Compliance APIs. Reusing the platform dialect here silently returns page one.
- **No idempotency key.** `app.create_scout` has no replay protection. If a create times out, list scouts with
  `app.get_scouts` and match on name before retrying, or you will create a duplicate that bills and alerts twice.

## Steps

1. **Pick where it runs.** `honeycomb.api.cloud_hives` — `GET /cloud_hives` for ControlUp-hosted locations, or
   `honeycomb.api.custom_hives` — `GET /hives` for your own on-premises hives. Location matters: an EUC Scout must
   run from a hive with network reach to the broker or gateway it is testing.

2. **Create the Scout.** `app.create_scout` — `POST /scouts`. The single published operation covers both Scout
   families; the MCP server splits it into `create-scout-euc` and `create-scout-net` for ergonomics, but the REST
   contract is one operation whose body shape selects the type. Set the name, the test interval, the target
   address, and — for EUC Scouts — the credentials the Scout authenticates with.

3. **Confirm it registered.** `app.get_scout_by_id` — `GET /scouts/{scoutId}`. Returns the configuration plus a
   summary of test results, so it doubles as the post-create assertion.

4. **Attach an alert policy.** `app.create_scout_alert` — `POST /scouts/{scoutId}/alerts`. The policy defines the
   condition that fires (a test failure, a threshold breach, a recovery), the trigger sensitivity, and the
   notification methods.
   - To notify an external system, add a **webhook** notification method. The endpoint URL, auth mode
     (none / basic / API token), custom headers and the JSON payload shape are **all yours to define** — ControlUp
     has no canonical event envelope. Payload values may embed webhook variables such as `{scout.name}`,
     `{test.status}` and `{test.latency}`. See `asyncapi/controlup-webhooks.yml` for the full variable table.
   - **Security caveat from ControlUp's own docs:** custom headers and custom fields are stored and transmitted as
     clear, unencrypted text. Do not put a long-lived bearer token in a custom header if you can avoid it.
   - To notify an already-connected system instead, read `honeycomb.api.get_org_integrations` —
     `GET /integrations` — for the active notification integrations.

5. **Verify the policy.** `app.get_scout_alert_policies` — `GET /scouts/{scoutId}/alerts`, then
   `app.get_scout_alert` — `GET /scouts/{scoutId}/alerts/{alertId}` for full detail.

6. **Read results.** `app.get_tests` — `GET /tests`, filtered by date range, Scout id and test status. Triggered
   alerts come from `app.get_alerts` — `GET /alerts` across the org, or `app.get_alert_for_scout` —
   `GET /alerts/{scoutId}` for one Scout.

7. **Pause rather than delete.** `app.disable_scout` — `POST /scouts/{scoutId}/disabled` toggles a Scout off and
   back on. `app.delete_scout` — `DELETE /scouts/{scoutId}` is **irreversible and removes all test history**. An
   agent should never call delete without explicit human confirmation.

## Error handling

| Status | Meaning | Do |
|---|---|---|
| 400 | Invalid body or paging | Check `page`/`pageSize` (not `_page`/`_limit`) and the Scout body shape. |
| 401 / 403 | Key or permission | See `authentication/controlup-authentication.yml`. |
| 404 | Unknown `scoutId` / `alertId` | Re-resolve via `app.get_scouts`. |
| 429 | Rate limited | You most likely hit the 10/min create cap. No `Retry-After` header is published — pace to the documented number. |

## Related

- `asyncapi/controlup-webhooks.yml` — the webhook notification surface and its variable table.
- `rate-limits/controlup-rate-limits.yml` — the per-endpoint caps on this API.
- `conventions/controlup-conventions.yml` — the two pagination dialects and why they matter.
