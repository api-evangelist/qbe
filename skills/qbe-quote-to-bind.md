---
name: QBE quote to bound policy
description: Create a commercial quote with QBE Australia, modify it if needed, refer it to an underwriter when required, then convert it into a bound policy.
api: openapi/qbe-anzo-digital-brokers-openapi.yml
operations:
  - Create-a-new-Quote
  - Modify-an-existing-Quote
  - Refer-a-quote-to-QBE-Underwriter
  - Convert-a-Quote-to-Policy
  - To-Abandon-an-existing-quote
generated: '2026-07-25'
method: generated
source: openapi/qbe-anzo-digital-brokers-openapi.yml
---

# QBE quote to bound policy

The core broker flow on the QBE Australia ANZO Digital Brokers Experience API. Every step posts the
same canonical policy document (`PolicyType`); the operation and the transaction headers decide what
QBE does with it.

## Before you start

You cannot run this without an approved QBE partnership. Required on every call:

- `Ocp-Apim-Subscription-Key` — approved Azure APIM subscription to the **ANZO Digital Brokers** product
  (`approvalRequired: true`, max 10 subscriptions).
- `X-ClientID` and `X-ClientSecret` — partner credentials issued by QBE.
- `X-Partner-Id` — one of `AUSTBROKERS`, `MARSH`, `PSC`. There is no value for an unlisted broker.
- `X-TrackingID` — your own tracing id for this call.
- `X-Mockable` — required boolean. Set it `true` (optionally with `X-Mock-Scenario`) to run against
  QBE's MuleSoft WireMock scenarios instead of live underwriting while you build.

Base URL: `https://gateway.api-au.qbe.com/x-digital-brokers-qbe-anzo/api`

## Steps

1. **Create the quote** — `POST /auth/quotes` (`Create-a-new-Quote`). Body is a `policy` object with
   `policyHeader.policyTransactionInformation` (`product` — one of `BPK`, `MSA`, `MPA`, `MVA` — and
   `inceptionDate` are required; set `transactionType: NEW_QUOTE`), a `customerParty` with a required
   `location`, and one or more `risks[]` carrying `riskClassCode`, dates and `riskMode: A`. On `201`
   you get the quote back with a quote identifier. Anything else, read step 5.
2. **Amend if the customer changes their mind** — `PUT /auth/quotes/{quoteId}`
   (`Modify-an-existing-Quote`). Returns `201`; QBE re-issues the quote. Use `riskMode: M` to modify an
   existing risk and `riskMode: T` to terminate one.
3. **Refer when QBE needs to look at it** — `POST /auth/quotes/{quoteId}/refer`
   (`Refer-a-quote-to-QBE-Underwriter`). Supply `referral.reasons[]` (1–10 strings). Use this rather
   than retrying a quote that keeps returning a business exception.
4. **Bind** — `POST /auth/quotes/{quoteId}/bind` (`Convert-a-Quote-to-Policy`). This is the money step:
   `201` issues a policy number (format like `145U475933BPK`, where the trailing three characters are
   the product code). Capture the returned `x-master-ref-id` — every later endorse / cancel / renew
   round trip replays it.
5. **Walk away cleanly** — `POST /auth/quotes/{quoteId}/abandon` (`To-Abandon-an-existing-quote`) if the
   quote is dead. Do not leave quotes hanging.

## Rules

- **No idempotency.** There is no `Idempotency-Key` on this API. A failed-but-possibly-applied bind must
  be resolved by reading state or contacting QBE, never by blind retry. Treat step 4 as non-repeatable.
- **Errors are not RFC 9457.** Every 4xx/5xx is `{"errors":[{"code","message","details"}]}`.
  `APIKIT_BAD_REQUEST` means your JSON failed schema validation — fix the payload.
  `INTERNAL_BUSINESS_EXCEPTION` / `CCHANGE_BUSINESS_EXCEPTION` mean the policy data broke an
  underwriting rule (the message and `extendedMessages[]` carry the reason, e.g. "Start Date too long
  ago. Please Amend.") — amend the data, do not retry unchanged. `HTTP_UNAUTHORISED` is a credential
  problem; `HTTP_FORBIDDEN` is a subscription or `X-Partner-Id` mismatch.
- **No claims.** There is no FNOL or claims operation on this API; do not look for one.
- Full detail: `conventions/qbe-conventions.yml`, `errors/qbe-problem-types.yml`,
  `vocabulary/qbe-vocabulary.yml`, `data-model/qbe-data-model.yml`.
