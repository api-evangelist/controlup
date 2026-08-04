---
name: Discover and execute a ControlUp Workflows integration action
description: >-
  Enumerate the flows, forms and integrations in a ControlUp Workflows tenant, read an integration action's
  input/output schema, execute that action directly without running a full flow, and check flow-run status.
api: openapi/controlup-workflows-openapi.yml
base_url: https://api.controlup.com
operations:
  - get_flows_workflows_v1_flows_get
  - get_flow_workflows_v1_flows__flowId__get
  - update_flow_status_workflows_v1_flows__flowId__patch
  - get_flow_runs_workflows_v1_flows__flowId__runs_get
  - launch_flow_workflows_v1_flows_launch_post
  - get_all_forms_workflows_v1_forms_get
  - get_form_workflows_v1_forms__formId__get
  - get_all_integrations_workflows_v1_integrations_get
  - get_integration_workflows_v1_integrations__integrationId__get
  - get_integration_actions_workflows_v1_integrations__integration_id__actions_get
  - get_integration_action_workflows_v1_integrations__integration_id__actions__node_type__get
  - execute_integration_action_workflows_v1_integrations__integration_id__actions__node_type__execute_post
mcp_tools:
  - list-flows
  - get-flow
  - update-flow-status
  - list-flow-runs
  - list-forms
  - get-form
  - list-integrations
  - get-integration
  - list-integration-actions
  - get-integration-action
  - execute-integration-action
generated: '2026-08-04'
method: generated
---

# Discover and execute a Workflows integration action

ControlUp Workflows is the orchestration layer: a **flow** is an automation, a **form** collects input for it, and
an **integration** is a connected external system exposing **actions** addressed by a `nodeType`. The interesting
property for an agent is that an integration action publishes its **own input/output schema at runtime** — so this
API is self-describing beyond what the OpenAPI alone declares.

## Before you start

- **Auth.** `Authorization: Bearer <API_KEY>`.
- **Paths carry the `/workflows` prefix on the gateway.** The published spec's servers entry is
  `https://api.controlup.com` and its paths already begin `/workflows/v1/…`.
- **No idempotency key.** `execute_integration_action…` and `launch_flow…` are both side-effecting POSTs with no
  replay protection. A timeout is genuinely ambiguous — check `get_flow_runs…` before retrying a launch, and
  treat a retried integration action as potentially duplicated.
- **Rate budget.** 60/min per user, 200/min per organization.

## Steps

### Discover the surface

1. `get_all_integrations_workflows_v1_integrations_get` — `GET /workflows/v1/integrations`: every integration in
   the organization.
2. `get_integration_workflows_v1_integrations__integrationId__get` — `GET /workflows/v1/integrations/{integrationId}`
   for one integration's detail.
3. `get_integration_actions_workflows_v1_integrations__integration_id__actions_get` —
   `GET /workflows/v1/integrations/{integration_id}/actions`: the actions that integration exposes.

### Read the contract before you call it

4. `get_integration_action_workflows_v1_integrations__integration_id__actions__node_type__get` —
   `GET /workflows/v1/integrations/{integration_id}/actions/{node_type}`. Returns the action's **input and output
   schema**. An agent must call this before executing — the request body for step 5 has to match this schema, and
   it is not knowable from the OpenAPI, which describes the envelope rather than the per-action payload.

### Execute

5. `execute_integration_action_workflows_v1_integrations__integration_id__actions__node_type__execute_post` —
   `POST /workflows/v1/integrations/{integration_id}/actions/{node_type}/execute`. Runs the single action
   directly, bypassing flow orchestration. The body must match the schema from step 4.

   This is a real side effect in a third-party system. An agent should surface what the action does — read from
   step 4 — and get confirmation before executing anything that is not a pure read.

### Or run the whole flow

6. `get_flows_workflows_v1_flows_get` — `GET /workflows/v1/flows`, then
   `get_flow_workflows_v1_flows__flowId__get` — `GET /workflows/v1/flows/{flowId}`.
7. `launch_flow_workflows_v1_flows_launch_post` — `POST /workflows/v1/flows/launch`.
8. `get_flow_runs_workflows_v1_flows__flowId__runs_get` — `GET /workflows/v1/flows/{flowId}/runs`: status and
   detail of runs. Poll this after a launch rather than assuming success from the launch response.
9. `update_flow_status_workflows_v1_flows__flowId__patch` — `PATCH /workflows/v1/flows/{flowId}` enables or
   disables a flow. Prefer disabling over
   `delete_flow_workflows_v1_flows__flowId__delete` — `DELETE /workflows/v1/flows/{flowId}` — which is permanent.

### Forms

`get_all_forms_workflows_v1_forms_get` — `GET /workflows/v1/forms` and
`get_form_workflows_v1_forms__formId__get` — `GET /workflows/v1/forms/{formId}` describe the input surface a flow
presents to an end user, which is often where the required fields for a launch are actually documented.

## Destructive operations — require confirmation

- `delete_flow_workflows_v1_flows__flowId__delete`
- `delete_form_workflows_v1_forms__formId__delete`
- `delete_integration_workflows_v1_integrations__integrationId__delete` — removes the connection, breaking every
  flow that depends on it.

## Error handling

| Status | Meaning | Do |
|---|---|---|
| 400 | Body does not match the action schema | Re-read step 4; the schema is per-action, not per-integration. |
| 401 / 403 | Key or permission | Permissions must be assigned directly to the user. |
| 404 | Unknown `integrationId`, `node_type`, `flowId` or `formId` | Re-enumerate; ids are organization-scoped. |
| 422 | Validation failure | Usually an unknown key or stale stored credentials on the integration. |
| 429 | Rate limited | Back off to the documented per-user budget; no `Retry-After` is published. |

## Related

- `mcp/controlup-tool-crosswalk.yml` — all 14 `workflows` MCP tools bind one-to-one to these operations.
- `conventions/controlup-conventions.yml`
- `errors/controlup-problem-types.yml`
