---
name: Govern organization access, roles and API keys
description: >-
  Audit and manage who can reach a ControlUp organization — users, invitations, roles and permissions, SAML SSO
  and SSO group mappings, the IP allowlist, organization settings and the audit log — including revoking every API
  key a departing user created.
api: openapi/controlup-dex-platform-openapi.yml
base_url: https://api.controlup.com/v1
operations:
  - OrgUsersPublicController_getAll
  - OrgUsersPublicController_getOneById
  - OrgUsersPublicController_update
  - OrgUsersPublicController_delete
  - OrgUsersPublicController_revoke
  - OrgInvitationPublicController_create
  - OrgInvitationPublicController_update
  - OrgRolesPublicController_getAll
  - OrgRolesPublicController_getOneById
  - OrgRolesPublicController_create
  - OrgRolesPublicController_update
  - OrgRolesPublicController_delete
  - OrgSettingsPublicController_getOneById
  - OrgSettingsPublicController_update
  - OrgSamlPublicController_getOneById
  - OrgSamlPublicController_create
  - OrgSamlPublicController_update
  - OrgSamlPublicController_configureByIdp
  - OrgSsoGroupsPublicController_getAll
  - OrgSsoGroupsPublicController_create
  - OrgIpAllowlistPublicController_getAll
  - OrgIpAllowlistPublicController_create
  - OrgIpAllowlistPublicController_update
  - OrgIpAllowlistPublicController_delete
  - OrgAuditLogPublicController_getAll
  - OrgLicensePublicController_getLicenseUsage
mcp_tools:
  - list-users
  - get-user
  - update-user
  - delete-user
  - revoke-user-api-keys
  - invite-users
  - list-roles
  - create-role
  - update-role
  - get-organization-settings
  - update-organization-settings
  - get-saml-settings
  - create-saml-settings
  - list-sso-groups
  - list-ip-allowlist
  - get-audit-log
generated: '2026-08-04'
method: generated
---

# Govern organization access

Every operation here is addressed as `/v1/organizations/{orgId}/…`. The `orgId` is the tenancy boundary for the
whole ControlUp estate; it is shown on the **API Key Management** page in the ONE console and is the `ORG_ID` the
MCP server requires.

## Before you start

- **Auth.** `Authorization: Bearer <API_KEY>` plus the `orgId` path parameter. Both are required.
- **The permission trap.** API keys inherit the permissions of the user who created them, and **permissions
  granted through an identity-provider group do not apply to API access**. A user who can do something in the
  console may get 403 through the API. Before diagnosing a key problem, check whether the permission is assigned
  directly to the account.
- **No idempotency key.** `OrgInvitationPublicController_create`, `OrgRolesPublicController_create` and
  `OrgIpAllowlistPublicController_create` have no replay protection. On a timeout, re-list before re-posting.
- **PATCH is a partial update.** Across this API, parameters you do not send are left unchanged — but the IP
  allowlist is the documented exception: `OrgIpAllowlistPublicController_update` **overwrites** the entire
  allowlist array on the entry with whatever you send. Read it first, merge, then write.

## Flows

### Audit who has access

1. `OrgUsersPublicController_getAll` — `GET /organizations/{orgId}/users`. Returns active users **and** users with
   a pending invitation, so this is the complete access surface, not just accepted accounts.
2. `OrgUsersPublicController_getOneById` — `GET /organizations/{orgId}/users/{id}` with the roles/settings
   inclusion for per-user detail.
3. `OrgRolesPublicController_getAll` — `GET /organizations/{orgId}/roles` for the permission model, and
   `OrgRolesPublicController_getOneById` for a single role's permissions plus its assigned users and groups.
4. `OrgSsoGroupsPublicController_getAll` — `GET /organizations/{orgId}/sso-groups` for the SAML group→role
   mappings, which is where console access frequently comes from without a direct assignment.
5. `OrgAuditLogPublicController_getAll` — `GET /organizations/{orgId}/audit-log`. Defaults to the last 24 hours,
   newest first, all timestamps UTC. Widen the window explicitly for a real audit.

### Offboard a user

1. `OrgUsersPublicController_revoke` — `POST /organizations/{orgId}/users/{id}/revoke-api-keys`. Revokes **every**
   key that user created. **This cannot be undone.** Do it first — it closes the programmatic door immediately.
2. `OrgUsersPublicController_update` — `PATCH /organizations/{orgId}/users/{id}` to disable, if you want the
   account retained. Disabling temporarily suspends their API keys rather than destroying them.
3. `OrgUsersPublicController_delete` — `DELETE /organizations/{orgId}/users/{id}` to remove permanently. Deleting
   a user automatically revokes their API keys.

An agent should treat steps 2 and 3 as requiring explicit human confirmation — both are destructive and neither is
reversible through the API.

### Onboard

1. `OrgRolesPublicController_create` — `POST /organizations/{orgId}/roles` if the right role does not exist.
   Permissions are organised by category.
2. `OrgInvitationPublicController_create` — `POST /organizations/{orgId}/invitations`. Multiple users can be
   invited in one request by sending multiple objects in the body.
3. `OrgInvitationPublicController_update` — `PATCH /organizations/{orgId}/invitations` resends an invitation that
   has not been accepted.

### Harden the tenant

- `OrgSettingsPublicController_getOneById` / `_update` — login methods, MFA options, session timeouts, default
  settings, and whether the IP allowlist is enforced.
- `OrgIpAllowlistPublicController_getAll` / `_create` / `_update` / `_delete` — entries hold one or more IPs or
  CIDR ranges. **You cannot delete the first entry** that was auto-added when the allowlist was first enabled;
  that guard exists so the enabling user cannot lock themselves out.
- `OrgSamlPublicController_getOneById` / `_create` / `_update` — SAML SSO. `_create` **replaces** the whole
  configuration; any existing SAML config is overwritten. `OrgSamlPublicController_configureByIdp` —
  `POST /organizations/{orgId}/saml/{idpName}` derives the configuration from an existing Entra ID integration
  instead of entering IdP metadata by hand, and likewise overwrites what is there.
- Note: the MCP server exposes a `delete-saml-settings` tool that calls `DELETE /organizations/{orgId}/saml`, but
  **no DELETE operation is declared on that path in the published OpenAPI**. Treat removing SAML as
  console-only until ControlUp documents it.

### Check licence headroom before provisioning

`OrgLicensePublicController_getLicenseUsage` — `GET /organizations/{orgId}/license/usage`. Worth reading before a
bulk invite; the DaaS IQ surface returns `402 Payment Required` when an organization has no active licence for a
capability, and retrying will not clear it.

## Error handling

| Status | Meaning | Do |
|---|---|---|
| 400 | Bad request | Validate the body against the spec; paging here is `_page`/`_limit`. |
| 401 | Key expired or revoked | Keys carry a duration set at creation and die when the owner is disabled or deleted. |
| 403 | Permission not directly assigned, or wrong `orgId` | See the permission trap above. |
| 404 | Unknown id | Ids are organization-scoped. |
| 409 | Name collision or concurrent update | Re-read and retry — there is no idempotency key to make this safe. |
| 429 | Rate limited | 60/min per user, 200/min per org, no `Retry-After` header published. |

## Related

- `authentication/controlup-authentication.yml`
- `conventions/controlup-conventions.yml` — tenancy, filtering, paging.
- `errors/controlup-problem-types.yml`
