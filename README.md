# Browser Use

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

Browser Use makes websites accessible to AI agents. It ships two commercial products on one managed browser platform — Browser Use Agents, which take a natural-language goal and return completed web work, and Browser Infrastructure, which rents stealth cloud Chromium browsers over SDK, REST, or CDP to automation you already own. The public Cloud API is versioned (v4 for long-horizon agent runs, v3 for sessions and workspaces, v2 for low-cost step-based tasks), authenticates with an X-Browser-Use-API-Key header, and is complemented by an OAuth-protected remote MCP server, signed webhooks, an A2A agent card, a published agent skill, first-party Python and TypeScript SDKs, and a CLI. The open-source browser-use Python library is a separate developer tool with its own API.

**Areas:** AI Automation · Browser Automation · Web Agents · Web Scraping · Agent Infrastructure · MCP · Cloud Browser · A2A

## Browser Use on APIs.io

Everything profiled for Browser Use is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/browser-use/](https://apis.io/providers/browser-use/)** — or go straight to one of the APIs or properties below.

### APIs (12)

- [Browser Use MCP Server](https://apis.io/apis/browser-use/browser-use-mcp/) — Browser Use's hosted remote Model Context Protocol server. An anonymous tools/list returns six real tools — browser_task, monitor_task, list_skills,…
- [Browser Use Billing API](https://apis.io/apis/browser-use/browser-use-billing-api/) — The Billing API from Browser Use — 1 operation(s) for billing.
- [Browser Use Browsers API](https://apis.io/apis/browser-use/browser-use-browsers-api/) — The Browsers API from Browser Use — 3 operation(s) for browsers.
- [Browser Use Files API](https://apis.io/apis/browser-use/browser-use-files-api/) — The Files API from Browser Use — 3 operation(s) for files.
- [Browser Use Profiles API](https://apis.io/apis/browser-use/browser-use-profiles-api/) — The Profiles API from Browser Use — 2 operation(s) for profiles.
- [Browser Use Runs API](https://apis.io/apis/browser-use/browser-use-runs-api/) — The Runs API from Browser Use — 6 operation(s) for runs.
- [Browser Use Sessions API](https://apis.io/apis/browser-use/browser-use-sessions-api/) — The Sessions API from Browser Use — 8 operation(s) for sessions.
- [Browser Use Skills API](https://apis.io/apis/browser-use/browser-use-skills-api/) — The Skills API from Browser Use — 8 operation(s) for skills.
- [Browser Use Skills Marketplace API](https://apis.io/apis/browser-use/browser-use-skills-marketplace-api/) — The Skills Marketplace API from Browser Use — 4 operation(s) for skills marketplace.
- [Browser Use Tasks API](https://apis.io/apis/browser-use/browser-use-tasks-api/) — The Tasks API from Browser Use — 4 operation(s) for tasks.
- [Browser Use Workspaces API](https://apis.io/apis/browser-use/browser-use-workspaces-api/) — The Workspaces API from Browser Use — 5 operation(s) for workspaces.
- [Browser Use X402 API](https://apis.io/apis/browser-use/browser-use-x402-api/) — The x402 API from Browser Use — 1 operation(s) for x402.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Browser Use Webhooks](https://apis.io/asyncapis/browser-use/browser-use-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [browser-use-mcp.yml](https://apis.io/servers/browser-use/browser-use-mcp-yml/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Browser Use Agentic Access](https://apis.io/agentic-access/browser-use/browser-use-agentic-access/)

#### Overlays (12)

OpenAPI overlays, including conversational phrasing for each operation.

- [Browser Use Api V4 Overlay](https://apis.io/overlays/browser-use/browser-use-api-v4-overlay/)
- [Browser Use Billing Api Phrasing Overlay](https://apis.io/overlays/browser-use/browser-use-billing-api-phrasing-overlay/)
- [Browser Use Browsers Api Phrasing Overlay](https://apis.io/overlays/browser-use/browser-use-browsers-api-phrasing-overlay/)
- [Browser Use Files Api Phrasing Overlay](https://apis.io/overlays/browser-use/browser-use-files-api-phrasing-overlay/)
- [Browser Use Profiles Api Phrasing Overlay](https://apis.io/overlays/browser-use/browser-use-profiles-api-phrasing-overlay/)
- [Browser Use Runs Api Phrasing Overlay](https://apis.io/overlays/browser-use/browser-use-runs-api-phrasing-overlay/)
- [Browser Use Sessions Api Phrasing Overlay](https://apis.io/overlays/browser-use/browser-use-sessions-api-phrasing-overlay/)
- [Browser Use Skills Api Phrasing Overlay](https://apis.io/overlays/browser-use/browser-use-skills-api-phrasing-overlay/)
- [Browser Use Skills Marketplace Api Phrasing Overlay](https://apis.io/overlays/browser-use/browser-use-skills-marketplace-api-phrasing-overlay/)
- [Browser Use Tasks Api Phrasing Overlay](https://apis.io/overlays/browser-use/browser-use-tasks-api-phrasing-overlay/)
- [Browser Use Workspaces Api Phrasing Overlay](https://apis.io/overlays/browser-use/browser-use-workspaces-api-phrasing-overlay/)
- [Browser Use X402 Api Phrasing Overlay](https://apis.io/overlays/browser-use/browser-use-x402-api-phrasing-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Browser Use Authentication](https://apis.io/security/browser-use/browser-use-authentication/)
- [Browser Use Domain Security](https://apis.io/security/browser-use/browser-use-domain-security/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Browser Use Scopes](https://apis.io/scopes/browser-use/browser-use-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Browser Use Plans Pricing](https://apis.io/plans/browser-use/browser-use-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Browser Use Rate Limits](https://apis.io/rate-limits/browser-use/browser-use-rate-limits/)

#### FinOps (1)

What the API costs to run, by operation.

- [Browser Use Finops](https://apis.io/finops/browser-use/browser-use-finops/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://browser-use.com)
- [Documentation](https://docs.browser-use.com)
- [Getting started](https://docs.browser-use.com/cloud/quickstart)
- [API reference](https://browser-use.com/api)
- [Pricing](https://browser-use.com/pricing)
- [Sign up](https://cloud.browser-use.com)
- [Support](https://link.browser-use.com/discord)
- [Blog](https://browser-use.com/posts)
- [Terms of service](https://browser-use.com/legal/terms-of-service)
- [Privacy policy](https://browser-use.com/privacy/)
- [GitHub](https://github.com/browser-use)
- [Status](https://status.browser-use.com)

## API Evangelist rating

**Kin Score 69.3** — exemplar · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 80.0 |
| Contract quality | 60.8 |
| Contract governance | 18.2 |
| Operational transparency | 65.8 |
| Developer ergonomics | 77.9 |
| Access clarity | 84.2 |

**Agent readiness 61.8** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | verified |
| Auth Clarity | served (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | — |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | unknown |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | paginated |
| Operation Distinctiveness | distinct |

**Regulatory alignment 39.2** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/browser-use/](https://apis.io/providers/browser-use/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Browser Use: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/browser-use/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
