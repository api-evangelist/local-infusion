# Local Infusion

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

Local Infusion is a tech-enabled outpatient infusion-therapy provider operating ambulatory infusion centers across thirteen US states — Connecticut, Florida, Maine, Maryland, Massachusetts, New Hampshire, New Jersey, New York, North Carolina, Ohio, South Carolina, Texas and Virginia — where patients with autoimmune, neurological, gastrointestinal and other chronic conditions receive specialty biologic infusions in private suites, supported by a dedicated Infusion Guide who handles referrals, prior authorization, benefits investigation and financial assistance. It sells care, not software: there is no developer programme, no product API, no SDK and no published pricing for any machine surface. It is catalogued here because its corporate WordPress site serves a live, self-describing REST API of 282 routes — including a publicly readable `location` custom post type carrying the company's 75-center directory — because the same install fronts two Model Context Protocol servers guarded by an OAuth 2.1 authorization server the host advertises through RFC 8414 and RFC 9728 metadata, and because the site carries an unusually deliberate agent-discovery layer: llms.txt, llms-full.txt, and .well-known ai-manifest, brand-facts and llm-sitemap documents, with a robots.txt that explicitly allows GPTBot, ClaudeBot, PerplexityBot and Google-Extended.

**Areas:** Company · Healthcare · Health Services · Infusion Therapy · Specialty Pharmacy · Ambulatory Care · Patient Services · Autoimmune · Chronic Care · MCP · WordPress

## Local Infusion on APIs.io

Everything profiled for Local Infusion is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/local-infusion/](https://apis.io/providers/local-infusion/)** — or go straight to one of the APIs or properties below.

### APIs (2)

- [Local Infusion Website (WordPress REST)](https://apis.io/apis/local-infusion/mylocalinfusion-com-website-wordpress-rest/) — The public WordPress REST API (wp-json) of the Local Infusion website at mylocalinfusion.com: the route index of the site's content management system,…
- [Local Infusion MCP API](https://apis.io/apis/local-infusion/local-infusion-mcp-api/) — Two Model Context Protocol servers exposed by the WordPress MCP adapter. Both require authentication — mcp-oauth-server returned HTTP 401 with a correct RFC…

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [local-infusion-mcp.yml](https://apis.io/servers/local-infusion/local-infusion-mcp-yml/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Local Infusion Wp Rest Overlay](https://apis.io/overlays/local-infusion/local-infusion-wp-rest-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Local Infusion Authentication](https://apis.io/security/local-infusion/local-infusion-authentication/)
- [Local Infusion Domain Security](https://apis.io/security/local-infusion/local-infusion-domain-security/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Local Infusion Scopes](https://apis.io/scopes/local-infusion/local-infusion-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Local Infusion Plans Pricing](https://apis.io/plans/local-infusion/local-infusion-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Local Infusion Rate Limits](https://apis.io/rate-limits/local-infusion/local-infusion-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://mylocalinfusion.com/)
- [Blog](https://mylocalinfusion.com/blog/)
- [Privacy policy](https://mylocalinfusion.com/privacy-policy/)

## API Evangelist rating

**Kin Score 22.3** — emerging · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 67.5 |
| Contract quality | 17.0 |
| Contract governance | 4.5 |
| Operational transparency | 0.0 |
| Developer ergonomics | 25.6 |
| Access clarity | 10.5 |

**Agent readiness 42.1** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | platform (partial credit) |
| Auth Clarity | served (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | — |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | yes |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | distinct |

**Regulatory alignment 40.6** — Health

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/local-infusion/](https://apis.io/providers/local-infusion/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Local Infusion: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/local-infusion/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
