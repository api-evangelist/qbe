# QBE Insurance (qbe)

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

QBE Insurance Group Limited is a Sydney-headquartered, ASX-listed global general insurance and reinsurance group, tracing back to 1886 in Townsville, Queensland, and operating today across Australia Pacific, North America and International divisions including a Lloyd's of London syndicate. QBE writes commercial and personal property and casualty lines — property, liability, motor and compulsory third party (CTP), workers compensation, marine, aviation, trade credit, crop and specialty — distributed overwhelmingly through brokers and agents rather than direct to consumers.

Its API posture reflects that distribution model and is partner-gated by design: QBE Australia runs a real, publicly browsable Azure API Management developer portal at [connect.api-au.qbe.com](https://connect.api-au.qbe.com/) whose catalogue, operations, schemas and examples can be read anonymously, but every product requires an approved subscription and the broker API is keyed to named partner platforms. The portal exposes genuine quote, bind, endorse, renew, cancel and refer operations for the commercial policy lifecycle — the four real insurance verbs, minus claims/FNOL, which QBE does not expose publicly.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/qbe/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/qbe/refs/heads/main/apis.yml)

## Tags

- Insurance
- Australia
- Property and Casualty
- Commercial Insurance
- Underwriting
- Policy Administration
- Quote
- Broker
- Reinsurance
- Carrier
- Partner API

## Timestamps

- **Created:** 2026-07-25
- **Modified:** 2026-07-25

## APIs

### QBE Australia ANZO Digital Brokers Experience API

QBE Australia's broker-facing policy lifecycle API, published in the QBE Australia API Hub as the "ANZO Digital Brokers" product. QBE describes it as providing access to the insurance policy lifecycle with QBE from creating quotes to policy binding, endorsements, renewals and more. Fifteen documented operations cover create/modify/abandon quote, bind a quote into a policy (issuing a policy number), endorse, renew, cancel, abandon and refer a policy to a QBE underwriter, plus quote and policy document upload and a health check. No claims or FNOL operations are exposed.

- **Human URL:** [https://connect.api-au.qbe.com/apis](https://connect.api-au.qbe.com/apis)
- **Base URL:** `https://gateway.api-au.qbe.com/x-digital-brokers-qbe-anzo/api`

#### Properties

- [Documentation](https://connect.api-au.qbe.com/)
- [API Reference](https://connect.api-au.qbe.com/apis)
- [OpenAPI](openapi/qbe-anzo-digital-brokers-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

### QBE Australia CTP Switch Service

A small QBE Australia service published in the same API Hub as the "ANZO CTP Service" product, supporting the compulsory third party (CTP) motor insurance switching flow. Two documented operations append data to and retrieve saved data for a CTP document, keyed by a code parameter.

- **Human URL:** [https://connect.api-au.qbe.com/apis](https://connect.api-au.qbe.com/apis)
- **Base URL:** `https://gateway.api-au.qbe.com/ctp-service`

#### Properties

- [Documentation](https://connect.api-au.qbe.com/)
- [API Reference](https://connect.api-au.qbe.com/apis)
- [OpenAPI](openapi/qbe-ctp-switch-service-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

## API Posture Notes

- **Developer portal:** [https://connect.api-au.qbe.com/](https://connect.api-au.qbe.com/) — HTTP 200, a real Azure API Management developer portal with browsable reference documentation, not a login wall. Access to the gateway, however, is partner-gated: both products carry `subscriptionRequired: true` and `approvalRequired: true`.
- **Auth model:** Azure APIM subscription key (`Ocp-Apim-Subscription-Key` header or `subscription-key` query), plus `X-ClientID` / `X-ClientSecret` and a required `X-Partner-Id` limited to QBE's named broker partners. No OAuth2 or OIDC — `/.well-known/openid-configuration` returns 404.
- **ACORD posture:** No ACORD reference found. The broker API uses QBE's own proprietary JSON canonical policy model over REST, not ACORD XML or AL3 agency download.
- **Insurance verbs:** quote ✔, bind ✔, issue ✔, FNOL ✘.
- **Webhooks / events:** none published. No AsyncAPI, no event catalogue, no callbacks.
- **Other regions:** QBE North America's [API Product Hub](https://partnerportal-api.qbena.com/) is live but publishes no anonymous catalogue; QBE Hong Kong's partner API pages sit on `qbe.com`, which returns HTTP 403 to anonymous fetchers and could not be verified.
- **Regulatory context:** Australia's Consumer Data Right was designated to extend to general insurance and then deferred, so nothing QBE publishes here is compelled by an open-insurance mandate.

## Review

See [review.yml](review.yml) for the full API Evangelist review, including probe results, HTTP statuses and spec provenance.

## Links

- **Website:** [https://www.qbe.com/](https://www.qbe.com/)
- **Developer Portal:** [https://connect.api-au.qbe.com/](https://connect.api-au.qbe.com/)
- **API Catalogue:** [https://connect.api-au.qbe.com/apis](https://connect.api-au.qbe.com/apis)
- **Partner Portal (North America):** [https://partnerportal-api.qbena.com/](https://partnerportal-api.qbena.com/)
