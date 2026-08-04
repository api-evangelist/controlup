---
name: Analyze VDI and DaaS session experience and right-size the estate
description: >-
  Investigate a virtual desktop performance complaint end to end — host and folder metrics, user activity, session
  statistics, a single session's timeline, application and process usage, NetScaler health — then pull ControlUp's
  sizing recommendations for virtualization and Azure.
api: openapi/controlup-vdi-daas-historical-openapi.yml
base_url: https://api.controlup.com/historical
operations:
  - getHostMetrics
  - getHostCounts
  - getUserActivity
  - getSessionsStatistics
  - getSessionDetails
  - getSessionTimeline
  - getSessionsAggregated
  - getMachineStatsByMachine
  - getMachinesAggregated
  - getAppStats
  - getAppUsage
  - getAppUsageSingle
  - getProcessUsageAll
  - getProcessUsageSingle
  - getWindowsEvents
  - getNetscalerUsage
  - getGatewayUsage
  - getLoadbalancerUsage
  - getNetscalerUsageWithTimeSeries
  - getGatewayUsageTimeSeries
  - getLoadbalancerUsageWithTimeSeries
  - getRecommendationVirtualization
  - getRecommendationAzure
  - getStartUploadDate
  - getSchema
  - execute
mcp_tools:
  - get-host-metrics-per-folder
  - get-host-counts
  - get-user-activity
  - get-session-statistics
  - get-individual-session-details
  - get-session-timeline
  - get-machine-statistics
  - get-machine-sizing-virt
  - get-machine-sizing-recommendation-azure
  - get-application-statistics
  - get-usage-details-for-all-applications
  - get-usage-details-for-an-application
  - get-netscaler-metrics
  - get-netscaler-gateway-metrics
  - get-netscaler-load-balancer-metrics
  - get-start-upload-date
generated: '2026-08-04'
method: generated
---

# Analyze VDI and DaaS session experience

## Before you start

- **Auth.** `Authorization: Bearer <API_KEY>`.
- **Concurrency is the binding constraint here, not the per-minute rate.** The VDI APIs allow **15 requests in
  flight at once**; a 16th fails immediately with 429, and long-running queries hold their slot for the whole
  execution. Serialise the investigation, do not fan out.
- **Bound every query.** These operations take an explicit `_timeFrom` / `_timeTo` window, with fixed presets
  (`1W`, `1M`) and granularity selectors (`5m`, `1h`) on the activity endpoints. Granularity degrades as the window
  widens. An unbounded query is the usual cause of a 504.
- **Check the data floor first.** `getStartUploadDate` — `GET /v1/uploadstartstatus` returns the date the first
  historical upload began. Anything before that date has no data, and an empty result set from a pre-floor window
  is not evidence of a healthy estate.

## Investigation path

### 1. Is it the estate or the user?

- `getHostMetrics` — `GET /v1/hosts/metrics`: average host resource consumption per folder over the period.
  Granularity depends on window length.
- `getHostCounts` — `GET /v1/hosts/counts`: users, sessions or machines per host.
- `getUserActivity` — `GET /v1/users/activity`: users and their activity status across the window.

If host metrics are flat and only one user is affected, go to the session path. If several hosts in one folder
degrade together, go to the infrastructure path.

### 2. The session path

- `getSessionsStatistics` — `GET /v1/sessions`: historical statistics for **individual user sessions**. This is
  the entry point when you have a user and a time, not a machine.
- `getSessionDetails` — `GET /v1/sessions/details`: full activity detail for a session identified from the step
  above.
- `getSessionTimeline` — `GET /v1/sessions/timeline/{sessionUid}`: the ordered state changes for that session.
  This is where a logon-duration or disconnect complaint resolves.
- `getSessionsAggregated` — `GET /v1/sessions/aggregated` when you want the shape of the population rather than
  one session.

### 3. Application and process attribution

- `getAppStats` — `GET /v1/applications/statistics`: usage and resource consumption for all applications.
- `getAppUsage` — `GET /v1/applications/usage/all`: peak concurrent users/instances across all applications.
- `getAppUsageSingle` — `GET /v1/applications/usage/single`: the same for **one** named application. Use this
  when you already know the application — it is far cheaper than filtering the "all" response.
- `getProcessUsageAll` / `getProcessUsageSingle` — `GET /v1/processes/usage/{all,single}` for process-level
  attribution beneath the application.
- `getWindowsEvents` — `GET /v1/windowsEvents` to correlate against OS-level events.

### 4. The infrastructure path

- `getNetscalerUsage`, `getGatewayUsage`, `getLoadbalancerUsage` — `GET /v1/netscaler/usage/{system,gateway,loadbalancer}`:
  aggregated NetScaler ADC, Gateway and Load Balancer metrics.
- `getNetscalerUsageWithTimeSeries`, `getGatewayUsageTimeSeries`, `getLoadbalancerUsageWithTimeSeries` —
  the `/v2/netscaler/usage/*` siblings, which return the same metrics **with time-series points** for trend
  analysis. Prefer v2 when you need to show change over time; v1 remains live for the aggregate.

### 5. Right-size

- `getMachineStatsByMachine` — `GET /v1/machines/statistics/{grouping}`: performance and resource statistics for
  monitored machines, grouped by the segment you pass in the path.
- `getMachinesAggregated` — `GET /v1/machines/aggregated` for the estate-level roll-up.
- `getRecommendationVirtualization` — `GET /v1/machines/sizing_recommendation/virtualization`: CPU, RAM and disk
  allocation recommendations for virtual machines.
- `getRecommendationAzure` — `GET /v1/machines/sizing_recommendation/azure`: Azure cost-optimization
  recommendations with specific VM and disk SKU suggestions.

Recommendations are advisory outputs, not applied changes — nothing in this API resizes anything. An agent should
present them for approval, never treat them as executed.

### 6. When the fixed endpoints do not answer it

- `getSchema` — `GET /v1/dynamic-query/schema` describes the queryable fields.
- `execute` — `POST /v1/dynamic-query/execute` runs a custom query against that schema. Read the schema first;
  this is the only write-method operation in the skill and it is a read in disguise.

## Error handling

| Status | Meaning | Do |
|---|---|---|
| 400 | Bad request | Check `_timeFrom`/`_timeTo`, granularity and the `{grouping}` path value. |
| 401 / 403 | Key or permission | Permissions must be assigned directly to the user, not via an IdP group. |
| 429 | Concurrency or rate | Most likely the 15-in-flight ceiling, not the per-minute budget. Serialise. |
| 504 | Upstream timeout | Narrow the time window; long queries hold their concurrency slot while they run. |

## Related

- `rate-limits/controlup-rate-limits.yml` — the parallel-request limit in detail.
- `conventions/controlup-conventions.yml` — time-range and field-selection parameters.
- `data-model/controlup-data-model.yml` — the resource graph these operations sit on.
