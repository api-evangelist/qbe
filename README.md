# QBE Insurance

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

QBE Insurance Group Limited is a Sydney-headquartered, ASX-listed global general insurance and reinsurance group, tracing back to 1886 in Townsville, Queensland, and operating today across Australia Pacific, North America and International divisions including a Lloyd's of London syndicate. QBE writes commercial and personal property and casualty lines — property, liability, motor and compulsory third party (CTP), workers compensation, marine, aviation, trade credit, crop and specialty — distributed overwhelmingly through brokers and agents rather than direct to consumers. Its API posture reflects that distribution model and is partner-gated by design: QBE Australia runs a real, publicly browsable Azure API Management developer portal at connect.api-au.qbe.com whose catalogue, operations, schemas and examples can be read anonymously, but every product requires an approved subscription (approvalRequired true) and the broker API is keyed to named partner platforms. The portal exposes genuine quote, bind, endorse, renew, cancel and refer operations for the commercial policy lifecycle — the four real insurance verbs, minus claims/FNOL, which QBE does not expose publicly. A separate QBE North America partner API hub at partnerportal-api.qbena.com serves an empty Azure APIM catalogue to anonymous callers but does publish seven named API products in its own content pages — Quote, Bind, Master Liability, Property Inquiry, Zip Code Validate and Reconciliation and Cancellation for Renters, plus Quote for Homeowners — behind a documented client-id/secret to JWT token exchange; no endpoints or specs are exposed. QBE Hong Kong documents a partner API behind qbe.com pages that are bot-blocked to anonymous fetchers. Australia is the home market; the Consumer Data Right was designated for general insurance and then deferred, so nothing here is compelled by regulation.

**Areas:** Insurance · Australia · Property and Casualty · Commercial Insurance · Underwriting · Policy Administration · Quotes · Reinsurance · Carrier · Partner API

## QBE Insurance on APIs.io

Everything profiled for QBE Insurance is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/qbe/](https://apis.io/providers/qbe/)** — or go straight to one of the APIs or properties below.

### APIs (3)

- [QBE Insurance CTP Switch API](https://apis.io/apis/qbe/qbe-ctp-switch-api/) — The CTP Switch API from QBE Insurance — 2 operation(s) for ctp switch.
- [QBE Insurance Digital Brokers API](https://apis.io/apis/qbe/qbe-digital-brokers-api/) — The Digital Brokers API from QBE Insurance — 15 operation(s) for digital brokers.
- [QBE North America Partner API Hub](https://apis.io/apis/qbe/qbe-north-america-partner-api/) — QBE North America's API Product Hub for agency and property-manager partners, offering Renters (HO4, multi-dwelling unit) and Homeowners APIs such as the…

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### Arazzo workflows (3)

Multi-step workflows that chain operations into a business task.

- [QBE policy cancellation](https://apis.io/arazzos/qbe/qbe-cancel-policy/)
- [QBE mid-term endorsement, confirmed](https://apis.io/arazzos/qbe/qbe-endorse-and-bind/)
- [QBE quote to bound policy](https://apis.io/arazzos/qbe/qbe-quote-to-bind/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [qbe-anzo-digital-brokers](https://apis.io/servers/qbe/qbe-anzo-digital-brokers/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Qbe Agentic Access](https://apis.io/agentic-access/qbe/qbe-agentic-access/)

#### JSON Schema (6)

The data models the API reads and writes.

- [AuthPoliciesPolicyIdEndorsePost200ApplicationJsonResponse](https://apis.io/schemas/qbe/qbe-auth-policies-policy-id-endorse-post200-application-json-response/)
- [AuthPoliciesPolicyIdReferPost200ApplicationJsonResponse](https://apis.io/schemas/qbe/qbe-auth-policies-policy-id-refer-post200-application-json-response/)
- [AuthQuotesPost201ApplicationJsonResponse](https://apis.io/schemas/qbe/qbe-auth-quotes-post201-application-json-response/)
- [AuthQuotesQuoteIdBindPost201ApplicationJsonResponse](https://apis.io/schemas/qbe/qbe-auth-quotes-quote-id-bind-post201-application-json-response/)
- [AuthQuotesQuoteIdReferPost200ApplicationJsonResponse](https://apis.io/schemas/qbe/qbe-auth-quotes-quote-id-refer-post200-application-json-response/)
- [Generated-2](https://apis.io/schemas/qbe/qbe-generated-2/)

#### JSON-LD (1)

Linked-data contexts for the provider's vocabulary.

- [Qbe Context](https://apis.io/jsonld/qbe/qbe-context/)

#### Vocabulary (1)

The provider's domain terms, defined.

- [QBE Australia ANZO Digital Brokers controlled vocabulary](https://apis.io/vocabularies/qbe/qbe-vocabulary/)

#### Collections (2)

Postman and Open Collection request collections.

- [ANZO Digital Brokers Experience API](https://apis.io/collections/qbe/open-qbe-anzo-digital-brokers/)
- [CTP Switch Service](https://apis.io/collections/qbe/open-qbe-ctp-switch-service/)

#### Overlays (2)

OpenAPI overlays, including conversational phrasing for each operation.

- [Qbe Ctp Switch Api Overlay](https://apis.io/overlays/qbe/qbe-ctp-switch-api-overlay/)
- [Qbe Digital Brokers Api Overlay](https://apis.io/overlays/qbe/qbe-digital-brokers-api-overlay/)

#### Governance rules (1)

Spectral rulesets for the provider's contracts.

- [QBE Insurance API Rules](https://apis.io/rules/qbe/qbe-rules/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Qbe Authentication](https://apis.io/security/qbe/qbe-authentication/)
- [Qbe Domain Security](https://apis.io/security/qbe/qbe-domain-security/)
- [Qbe Vulnerability Disclosure](https://apis.io/security/qbe/qbe-vulnerability-disclosure/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Qbe Plans Pricing](https://apis.io/plans/qbe/qbe-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Qbe Rate Limits](https://apis.io/rate-limits/qbe/qbe-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.qbe.com/)
- [Documentation](https://connect.api-au.qbe.com/getting-started)
- [Getting started](https://connect.api-au.qbe.com/getting-started)
- [API reference](https://connect.api-au.qbe.com/apis)
- [Support](https://www.qbe.com/au/contact-us)
- [Blog](https://www.qbe.com/newsroom)
- [Security](https://www.qbe.com/responsible-disclosure-program)
- [Terms of service](https://www.qbe.com/us/legal/api-terms-of-use)
- [Privacy policy](https://www.qbe.com/au/about/governance/privacy-policy)
- [GitHub](https://github.com/qbegroup)

## API Evangelist rating

**Kin Score 41.1** — developing · rubric 0.24.0 · scored 2026-10-20

| Facet | Score |
|---|---|
| Discoverability | 57.1 |
| Contract quality | 28.8 |
| Contract governance | 57.4 |
| Operational transparency | 13.2 |
| Developer ergonomics | 66.1 |
| Access clarity | 27.6 |

**Agent readiness 28.2** — agent-aware

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | derived (partial credit) |
| OpenAPI Examples | verified |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |

**Regulatory alignment 27.2** — Insurance

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/qbe/](https://apis.io/providers/qbe/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for QBE Insurance: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/qbe/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
