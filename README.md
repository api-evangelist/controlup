# ControlUp

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

ControlUp is a Digital Employee Experience (DEX) and Autonomous Endpoint Management (AEM) platform that monitors, scores and remediates the end-user computing estate — physical desktops and laptops, VDI and DaaS (Citrix CVAD / Citrix Cloud, Omnissa Horizon, Azure Virtual Desktop, Windows 365, Parallels RAS), the applications and sessions running on them, and the network path in between. The ControlUp ONE platform spans ControlUp for Desktops, for VDI, for Apps, for Frontline Workers and for Compliance, plus Synthetic Monitoring (Scouts and Hives), Workflows, and Pulse AI. It publishes a public REST API surface at api.controlup.com documented on a ReadMe hub at api.controlup.io, an RFC 9727 /.well-known/api-catalog linkset enumerating twelve OpenAPI definitions, an official Model Context Protocol server on npm (@controlup-ai/mcp) exposing 106 tools across six product domains, PowerShell cmdlets for monitor and agent automation, and llms.txt indexes on both the documentation and API hosts.

**Areas:** Digital Employee Experience · Endpoint Management · VDI · DaaS · Virtual Desktop · Observability · Monitoring · Synthetic Monitoring · Device Management · Compliance · Vulnerability Management · Workflow Automation

## ControlUp on APIs.io

Everything profiled for ControlUp is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/controlup/](https://apis.io/providers/controlup/)** — or go straight to one of the APIs or properties below.

### APIs (61)

- [ControlUp MCP Server](https://apis.io/apis/controlup/controlup-mcp-server/) — Official Model Context Protocol server published by ControlUp as the npm package @controlup-ai/mcp. Runs locally over stdio via npx, authenticates with a…
- [ControlUp Alerts API](https://apis.io/apis/controlup/controlup-alerts-api/) — Alerts let you receive notifications or automatically run an action when certain conditions occur on a device.
- [ControlUp Alerts - Devices API](https://apis.io/apis/controlup/controlup-alerts-devices-api/) — The Alerts - Devices API from ControlUp — 2 operation(s) for alerts - devices.
- [ControlUp Applications API](https://apis.io/apis/controlup/controlup-applications-api/) — Applications usage reports
- [ControlUp Audit Log API](https://apis.io/apis/controlup/controlup-audit-log-api/) — The Audit Log API from ControlUp — 1 operation(s) for audit log.
- [ControlUp Cloud providers API](https://apis.io/apis/controlup/controlup-cloud-providers-api/) — The Cloud providers API from ControlUp — 3 operation(s) for cloud providers.
- [ControlUp Dal API](https://apis.io/apis/controlup/controlup-dal-api/) — The DAL (data access layer) is an advanced way to get data from an index.
- [ControlUp Data API](https://apis.io/apis/controlup/controlup-data-api/) — These endpoints are for interacting with the raw data stored in data indices.
- [ControlUp Devices API](https://apis.io/apis/controlup/controlup-devices-api/) — Get information about devices.
- [ControlUp Dynamic Query API](https://apis.io/apis/controlup/controlup-dynamic-query-api-api/) — Dynamic SQL transformation and execution
- [ControlUp Events API](https://apis.io/apis/controlup/controlup-events-api/) — The System Events log reports important events and alerts in your ControlUp for Desktops environment.
- [ControlUp Features API](https://apis.io/apis/controlup/controlup-features-api/) — The Features API from ControlUp — 2 operation(s) for features.
- [ControlUp Health API](https://apis.io/apis/controlup/controlup-health-api/) — The Health API from ControlUp — 3 operation(s) for health.
- [ControlUp Hives API](https://apis.io/apis/controlup/controlup-hives-api/) — Hives are the locations from which Scouts (tests) are initiated. Custom Hives allow you to test internal resources from within your network. They must be…
- [ControlUp Host API](https://apis.io/apis/controlup/controlup-host-api/) — Host usage reports
- [ControlUp Host pool cost API](https://apis.io/apis/controlup/controlup-host-pool-cost-api/) — The Host pool cost API from ControlUp — 4 operation(s) for host pool cost.
- [ControlUp Host pool deployments API](https://apis.io/apis/controlup/controlup-host-pool-deployments-api/) — The Host pool deployments API from ControlUp — 1 operation(s) for host pool deployments.
- [ControlUp Host pool scaling policies API](https://apis.io/apis/controlup/controlup-host-pool-scaling-policies-api/) — The Host pool scaling policies API from ControlUp — 2 operation(s) for host pool scaling policies.
- [ControlUp Host pool session host deployments API](https://apis.io/apis/controlup/controlup-host-pool-session-host-deployments-api/) — The Host pool session host deployments API from ControlUp — 1 operation(s) for host pool session host deployments.
- [ControlUp Host pool session hosts API](https://apis.io/apis/controlup/controlup-host-pool-session-hosts-api/) — The Host pool session hosts API from ControlUp — 1 operation(s) for host pool session hosts.
- [ControlUp Host pool user sessions API](https://apis.io/apis/controlup/controlup-host-pool-user-sessions-api/) — The Host pool user sessions API from ControlUp — 1 operation(s) for host pool user sessions.
- [ControlUp Host pool VM settings API](https://apis.io/apis/controlup/controlup-host-pool-vm-settings-api/) — The Host pool VM settings API from ControlUp — 2 operation(s) for host pool vm settings.
- [ControlUp Host pools API](https://apis.io/apis/controlup/controlup-host-pools-api/) — The Host pools API from ControlUp — 6 operation(s) for host pools.
- [ControlUp Integrations API](https://apis.io/apis/controlup/controlup-integrations-api/) — The Integrations API from ControlUp — 1 operation(s) for integrations.
- [ControlUp Invitations API](https://apis.io/apis/controlup/controlup-invitations-api/) — The Invitations API from ControlUp — 1 operation(s) for invitations.
- [ControlUp IP Allowlist API](https://apis.io/apis/controlup/controlup-ip-allowlist-api/) — The IP Allowlist API from ControlUp — 2 operation(s) for ip allowlist.
- [ControlUp Jobs API](https://apis.io/apis/controlup/controlup-jobs-api/) — The Jobs API from ControlUp — 8 operation(s) for jobs.
- [ControlUp License API](https://apis.io/apis/controlup/controlup-license-api/) — The License API from ControlUp — 1 operation(s) for license.
- [ControlUp License Usage API](https://apis.io/apis/controlup/controlup-license-usage-api/) — The License Usage API from ControlUp — 1 operation(s) for license usage.
- [ControlUp Machine API](https://apis.io/apis/controlup/controlup-machine-api/) — Machine usage reports
- [ControlUp Machines API](https://apis.io/apis/controlup/controlup-machines-api/) — Endpoints to manage and query machines
- [ControlUp Master images API](https://apis.io/apis/controlup/controlup-master-images-api/) — The Master images API from ControlUp — 20 operation(s) for master images.
- [ControlUp Metrics API](https://apis.io/apis/controlup/controlup-metrics-api/) — Endpoints to manage and query metrics
- [ControlUp MF As API](https://apis.io/apis/controlup/controlup-mfas-api/) — Multi-factor authentication (MFA) is supported for gateway access on all EUC platforms except Citrix Storefront. Use this resource to retrieve the sets of…
- [ControlUp Net Scaler API](https://apis.io/apis/controlup/controlup-netscaler-api/) — Netscaler usage reports
- [ControlUp Onboarding API](https://apis.io/apis/controlup/controlup-onboarding-api/) — The Onboarding API from ControlUp — 5 operation(s) for onboarding.
- [ControlUp Organization Settings API](https://apis.io/apis/controlup/controlup-organization-settings-api/) — The Organization Settings API from ControlUp — 1 operation(s) for organization settings.
- [ControlUp Organizations API](https://apis.io/apis/controlup/controlup-organizations-api/) — The Organizations API from ControlUp — 2 operation(s) for organizations.
- [ControlUp Overview API](https://apis.io/apis/controlup/controlup-overview-api/) — The Overview API from ControlUp — 11 operation(s) for overview.
- [ControlUp Processes API](https://apis.io/apis/controlup/controlup-processes-api/) — Process usage reports
- [ControlUp Public API](https://apis.io/apis/controlup/controlup-public-api-api/) — The Public API API from ControlUp — 11 operation(s) for public api.
- [ControlUp Roles API](https://apis.io/apis/controlup/controlup-roles-api/) — The Roles API from ControlUp — 2 operation(s) for roles.
- [ControlUp SAML API](https://apis.io/apis/controlup/controlup-saml-api/) — The SAML API from ControlUp — 2 operation(s) for saml.
- [ControlUp Scaling profiles API](https://apis.io/apis/controlup/controlup-scaling-profiles-api/) — The Scaling profiles API from ControlUp — 3 operation(s) for scaling profiles.
- [ControlUp Scouts API](https://apis.io/apis/controlup/controlup-scouts-api/) — Scouts are the proactive tests that you configure to monitor the availability and health of various resources. There are different types of Scouts,…
- [ControlUp Scripts API](https://apis.io/apis/controlup/controlup-scripts-api/) — The Scripts API from ControlUp — 1 operation(s) for scripts.
- [ControlUp Session API](https://apis.io/apis/controlup/controlup-session-api/) — Session statistics report
- [ControlUp Session hosts API](https://apis.io/apis/controlup/controlup-session-hosts-api/) — The Session hosts API from ControlUp — 2 operation(s) for session hosts.
- [ControlUp SSO Groups API](https://apis.io/apis/controlup/controlup-sso-groups-api/) — The SSO Groups API from ControlUp — 2 operation(s) for sso groups.
- [ControlUp Subscriptions API](https://apis.io/apis/controlup/controlup-subscriptions-api/) — The Subscriptions API from ControlUp — 27 operation(s) for subscriptions.
- [ControlUp Support endpoint API](https://apis.io/apis/controlup/controlup-support-endpoint-api/) — Provides an additional information about customer's data
- [ControlUp Surveys API](https://apis.io/apis/controlup/controlup-surveys-api/) — These endpoints are for interacting with Employee Sentiment surveys.
- [ControlUp Tags API](https://apis.io/apis/controlup/controlup-tags-api/) — The Tags API from ControlUp — 2 operation(s) for tags.
- [ControlUp Tenants API](https://apis.io/apis/controlup/controlup-tenants-api/) — The Tenants API from ControlUp — 23 operation(s) for tenants.
- [ControlUp Tests API](https://apis.io/apis/controlup/controlup-tests-api/) — The output of the scout tests
- [ControlUp Triggers API](https://apis.io/apis/controlup/controlup-triggers-api/) — The Triggers API from ControlUp — 2 operation(s) for triggers.
- [ControlUp Trigger Schedules API](https://apis.io/apis/controlup/controlup-triggerschedules-api/) — The TriggerSchedules API from ControlUp — 2 operation(s) for triggerschedules.
- [ControlUp User API](https://apis.io/apis/controlup/controlup-user-api/) — User activity reports
- [ControlUp User sessions API](https://apis.io/apis/controlup/controlup-user-sessions-api/) — The User sessions API from ControlUp — 1 operation(s) for user sessions.
- [ControlUp Users API](https://apis.io/apis/controlup/controlup-users-api/) — The Users API from ControlUp — 4 operation(s) for users.
- [ControlUp Windows Events API](https://apis.io/apis/controlup/controlup-windowsevents-api/) — Windows Event Log Monitoring history

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Controlup Webhooks](https://apis.io/asyncapis/controlup/controlup-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [controlup](https://apis.io/servers/controlup/controlup/)

#### Collections (60)

Postman and Open Collection request collections.

- [Controlup Alerts API](https://apis.io/collections/controlup/open-controlup-alerts-api/)
- [Dex Alerts Alerts - Devices API](https://apis.io/collections/controlup/open-controlup-alerts-devices-api/)
- [VDI & DAAS Applications API](https://apis.io/collections/controlup/open-controlup-applications-api/)
- [Dex Audit Log API](https://apis.io/collections/controlup/open-controlup-audit-log-api/)
- [DaaS IQ Cloud providers API](https://apis.io/collections/controlup/open-controlup-cloud-providers-api/)
- [ControlUp for Desktops Dal API](https://apis.io/collections/controlup/open-controlup-dal-api/)
- [ControlUp for Desktops Data API](https://apis.io/collections/controlup/open-controlup-data-api/)
- [Controlup Devices API](https://apis.io/collections/controlup/open-controlup-devices-api/)
- [VDI & DAAS Dynamic Query API API](https://apis.io/collections/controlup/open-controlup-dynamic-query-api-api/)
- [Controlup Events API](https://apis.io/collections/controlup/open-controlup-events-api/)
- [DaaS IQ Features API](https://apis.io/collections/controlup/open-controlup-features-api/)
- [DaaS IQ Health API](https://apis.io/collections/controlup/open-controlup-health-api/)
- [Synthetic Monitoring Hives API](https://apis.io/collections/controlup/open-controlup-hives-api/)
- [VDI & DAAS Host API](https://apis.io/collections/controlup/open-controlup-host-api/)
- [DaaS IQ Host pool cost API](https://apis.io/collections/controlup/open-controlup-host-pool-cost-api/)
- [DaaS IQ Host pool deployments API](https://apis.io/collections/controlup/open-controlup-host-pool-deployments-api/)
- [DaaS IQ Host pool scaling policies API](https://apis.io/collections/controlup/open-controlup-host-pool-scaling-policies-api/)
- [DaaS IQ Host pool session host deployments API](https://apis.io/collections/controlup/open-controlup-host-pool-session-host-deployments-api/)
- [DaaS IQ Host pool session hosts API](https://apis.io/collections/controlup/open-controlup-host-pool-session-hosts-api/)
- [DaaS IQ Host pool user sessions API](https://apis.io/collections/controlup/open-controlup-host-pool-user-sessions-api/)
- [DaaS IQ Host pool VM settings API](https://apis.io/collections/controlup/open-controlup-host-pool-vm-settings-api/)
- [DaaS IQ Host pools API](https://apis.io/collections/controlup/open-controlup-host-pools-api/)
- [Synthetic Monitoring Integrations API](https://apis.io/collections/controlup/open-controlup-integrations-api/)
- [Dex Invitations API](https://apis.io/collections/controlup/open-controlup-invitations-api/)
- [Dex IP Allowlist API](https://apis.io/collections/controlup/open-controlup-ip-allowlist-api/)
- …and 35 more published on APIs.io

#### Overlays (72)

OpenAPI overlays, including conversational phrasing for each operation.

- [Controlup Alerts Api Phrasing Overlay](https://apis.io/overlays/controlup/controlup-alerts-api-phrasing-overlay/)
- [Controlup Alerts Devices Api Phrasing Overlay](https://apis.io/overlays/controlup/controlup-alerts-devices-api-phrasing-overlay/)
- [Controlup Applications Api Phrasing Overlay](https://apis.io/overlays/controlup/controlup-applications-api-phrasing-overlay/)
- [Controlup Audit Log Api Phrasing Overlay](https://apis.io/overlays/controlup/controlup-audit-log-api-phrasing-overlay/)
- [Controlup Cloud Providers Api Phrasing Overlay](https://apis.io/overlays/controlup/controlup-cloud-providers-api-phrasing-overlay/)
- [Controlup Compliance Overlay](https://apis.io/overlays/controlup/controlup-compliance-overlay/)
- [Controlup Daas Iq Overlay](https://apis.io/overlays/controlup/controlup-daas-iq-overlay/)
- [Controlup Dal Api Phrasing Overlay](https://apis.io/overlays/controlup/controlup-dal-api-phrasing-overlay/)
- [Controlup Data Api Phrasing Overlay](https://apis.io/overlays/controlup/controlup-data-api-phrasing-overlay/)
- [Controlup Desktops Overlay](https://apis.io/overlays/controlup/controlup-desktops-overlay/)
- [Controlup Devices Api Phrasing Overlay](https://apis.io/overlays/controlup/controlup-devices-api-phrasing-overlay/)
- [Controlup Dex Alerts Overlay](https://apis.io/overlays/controlup/controlup-dex-alerts-overlay/)
- [Controlup Dex Events Overlay](https://apis.io/overlays/controlup/controlup-dex-events-overlay/)
- [Controlup Dex Platform Overlay](https://apis.io/overlays/controlup/controlup-dex-platform-overlay/)
- [Controlup Dynamic Query Api Api Phrasing Overlay](https://apis.io/overlays/controlup/controlup-dynamic-query-api-api-phrasing-overlay/)
- [Controlup Events Api Phrasing Overlay](https://apis.io/overlays/controlup/controlup-events-api-phrasing-overlay/)
- [Controlup Features Api Phrasing Overlay](https://apis.io/overlays/controlup/controlup-features-api-phrasing-overlay/)
- [Controlup Health Api Phrasing Overlay](https://apis.io/overlays/controlup/controlup-health-api-phrasing-overlay/)
- [Controlup Hives Api Phrasing Overlay](https://apis.io/overlays/controlup/controlup-hives-api-phrasing-overlay/)
- [Controlup Host Api Phrasing Overlay](https://apis.io/overlays/controlup/controlup-host-api-phrasing-overlay/)
- [Controlup Host Pool Cost Api Phrasing Overlay](https://apis.io/overlays/controlup/controlup-host-pool-cost-api-phrasing-overlay/)
- [Controlup Host Pool Deployments Api Phrasing Overlay](https://apis.io/overlays/controlup/controlup-host-pool-deployments-api-phrasing-overlay/)
- [Controlup Host Pool Scaling Policies Api Phrasing Overlay](https://apis.io/overlays/controlup/controlup-host-pool-scaling-policies-api-phrasing-overlay/)
- [Controlup Host Pool Session Host Deployments Api Phrasing Overlay](https://apis.io/overlays/controlup/controlup-host-pool-session-host-deployments-api-phrasing-overlay/)
- [Controlup Host Pool Session Hosts Api Phrasing Overlay](https://apis.io/overlays/controlup/controlup-host-pool-session-hosts-api-phrasing-overlay/)
- …and 47 more published on APIs.io

#### Security (4)

Authentication, trust centre, and vulnerability disclosure.

- [Controlup Authentication](https://apis.io/security/controlup/controlup-authentication/)
- [Controlup Domain Security](https://apis.io/security/controlup/controlup-domain-security/)
- [Controlup Trust Center](https://apis.io/security/controlup/controlup-trust-center/)
- [Controlup Vulnerability Disclosure](https://apis.io/security/controlup/controlup-vulnerability-disclosure/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Controlup Plans Pricing](https://apis.io/plans/controlup/controlup-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Controlup Rate Limits](https://apis.io/rate-limits/controlup/controlup-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.controlup.com/)
- [Documentation](https://support.controlup.com/docs)
- [Getting started](https://api.controlup.io/reference/how-to-make-api-requests-1)
- [API reference](https://api.controlup.io/reference)
- [Pricing](https://www.controlup.com/pricing/)
- [Sign up](https://www.controlup.com/free-trial/)
- [Support](https://support.controlup.com/)
- [Changelog](https://support.controlup.com/docs/release-notes)
- [Blog](https://www.controlup.com/resources/blog/)
- [Security](https://trustcenter.controlup.com/)
- [Compliance](https://trustcenter.controlup.com/)
- [Trust centre](https://trustcenter.controlup.com/)
- [Terms of service](https://www.controlup.com/terms/)
- [Privacy policy](https://www.controlup.com/privacy-policy/controlup-privacy-policy/)
- [GitHub](https://github.com/controlup)
- [Status](https://status.controlup.com/)

## API Evangelist rating

**Kin Score 75.6** — exemplar · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 78.6 |
| Contract quality | 63.8 |
| Contract governance | 4.5 |
| Operational transparency | 97.4 |
| Developer ergonomics | 58.9 |
| Access clarity | 92.1 |

**Agent readiness 37.5** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | documented (partial credit) |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | verified |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | partial |
| Operation Distinctiveness | distinct |

**Regulatory alignment 35.3** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/controlup/](https://apis.io/providers/controlup/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for ControlUp: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/controlup/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
