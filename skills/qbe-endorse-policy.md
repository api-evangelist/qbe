---
name: QBE mid-term endorsement
description: Amend an in-force QBE policy mid-term and confirm the change, using the two-step endorse-then-bind transaction with x-master-ref-id correlation.
api: openapi/qbe-anzo-digital-brokers-openapi.yml
operations:
  - Amend-an-existing-policy-endorsement
  - Bind-a-policy-to-save-change-after-endoresement-cancellation-or-renewal-has
  - To-Abandon-a-policy-before-it-has-been-bound
  - Refer-an-existing-Policy
generated: '2026-07-25'
method: generated
source: openapi/qbe-anzo-digital-brokers-openapi.yml
---

# QBE mid-term endorsement

QBE models every post-issue policy change as a **two-step transaction**: open it, then confirm it. The
open call returns a pending change; nothing is committed until you bind. This is the pattern for
endorsements, cancellations and renewals alike — only the opening operation differs.

## Steps

1. **Open the endorsement** — `POST /auth/policies/{policyId}/endorse`
   (`Amend-an-existing-policy-endorsement`). Post the canonical policy document with
   `policyHeader.policyTransactionInformation.transactionType: ENDORSEMENT`, the `effectiveDate` of the
   change, and the affected `risks[]` using `riskMode`: `A` to add a risk, `M` to modify one, `T` to
   terminate one, `V` to carry an existing risk through unchanged. Required headers include
   `x-master-ref-id` — this is the correlation reference that ties the whole transaction together.
2. **Confirm it** — `POST /auth/policies/{policyId}/bind`
   (`Bind-a-policy-to-save-change-after-endoresement-cancellation-or-renewal-has`) with
   `x-bind-policy-transaction: ENDORSEMENT` and **the same `x-master-ref-id` you sent in step 1**.
   Sending a different reference, or omitting it, breaks the pairing.
3. **Or back it out** — `POST /auth/policies/{policyId}/abandon`
   (`To-Abandon-a-policy-before-it-has-been-bound`) with
   `x-abandon-policy-transaction: ENDORSEMENT` and the same `x-master-ref-id`. Use this whenever you
   opened a change you are not going to confirm; do not leave pending transactions on a policy.
4. **Or escalate it** — `POST /auth/policies/{policyId}/refer` (`Refer-an-existing-Policy`) with
   `x-refer-policy-transaction: ENDORSEMENT` and `referral.reasons[]`, when the change needs a QBE
   underwriter.
5. **Attach the paperwork** — `POST /auth/policies/{policyId}/documents`
   (`Policy-Document-Upload-API`) with `?type=endorsement_schedule` and a body carrying `effectiveDate`
   and `primaryFile`.

## Rules

- The same three headers govern all three policy transaction types: `ENDORSEMENT`, `CANCEL`, `RENEWAL`.
  Swap the opening operation (`/endorse`, `/cancel`, `/renew`) and the header value together — a
  mismatch between the transaction you opened and the value you bind with is a business exception.
- **There is no idempotency key.** Step 2 is the committing call; never fire it twice on a timeout.
- Errors are `{"errors":[{"code","message","details"}]}`. `CCHANGE_BUSINESS_EXCEPTION` carries
  `extendedMessages[]` with the QBE policy-system reason code — surface that text to the broker rather
  than a generic failure.
- Same credential set as every call on this API: `Ocp-Apim-Subscription-Key`, `X-ClientID`,
  `X-ClientSecret`, `X-Partner-Id` (`AUSTBROKERS` | `MARSH` | `PSC`), `X-TrackingID`, `X-Mockable`.
- Full detail: `conventions/qbe-conventions.yml`, `errors/qbe-problem-types.yml`.
