---
name: QBE renewal and cancellation
description: Take a QBE policy invited for renewal through to a bound renewal, or cancel an in-force policy with the correct QBE reason code.
api: openapi/qbe-anzo-digital-brokers-openapi.yml
operations:
  - Generate-a-quote-request-for-a-policy-that-has-been-invited-for-renewal
  - Cancel-an-existing-policy
  - Bind-a-policy-to-save-change-after-endoresement-cancellation-or-renewal-has
  - To-Abandon-a-policy-before-it-has-been-bound
  - Policy-Document-Upload-API
generated: '2026-07-25'
method: generated
source: openapi/qbe-anzo-digital-brokers-openapi.yml
---

# QBE renewal and cancellation

Both ends of the policy year, on the same two-step open-then-bind transaction as an endorsement.

## Renew

1. `POST /auth/policies/{policyId}/renew`
   (`Generate-a-quote-request-for-a-policy-that-has-been-invited-for-renewal`) — generates the renewal
   quote request for a policy QBE has invited for renewal. Set
   `policyHeader.policyTransactionInformation.transactionType` to `RENEWAL` (or `RENEWAL_AMEND` when the
   broker is changing terms at renewal), and send an `x-master-ref-id`.
2. `POST /auth/policies/{policyId}/bind` with `x-bind-policy-transaction: RENEWAL` and the same
   `x-master-ref-id` to commit the renewal.
3. `POST /auth/policies/{policyId}/documents?type=renewal_schedule` to attach the renewal schedule
   (`effectiveDate` + `primaryFile`).
4. Not proceeding? `POST /auth/policies/{policyId}/abandon` with
   `x-abandon-policy-transaction: RENEWAL` and the same reference.

## Cancel

1. `POST /auth/policies/{policyId}/cancel` (`Cancel-an-existing-policy`) — set
   `transactionType: CANCEL`, the cancellation `effectiveDate`, and
   `policyHeader.cancelReasonCode` from QBE's published list. Send an `x-master-ref-id`.
2. `POST /auth/policies/{policyId}/bind` with `x-bind-policy-transaction: CANCEL` and the same
   `x-master-ref-id`.
3. `POST /auth/policies/{policyId}/documents?type=cancellation_schedule` for the cancellation schedule.

### QBE cancellation reason codes

`CL` Cancelled (Payout) · `PR` Policy Replaced · `DC` Declined by Company · `TL` Total Loss ·
`IC` Found cheaper Policy · `OG` Outside Guidelines · `IE` Insured Elsewhere · `LR` Loan Refinance ·
`ER` Error Correction · `NR` Not Required · `CO` Cooling Off · `NP` Non-Payment · `PS` Property Sold.

Pick the true reason — this code drives QBE's retention reporting, and `ER` (Error Correction) is not a
catch-all for a mistaken cancellation you meant to abandon instead.

## Rules

- Cancellation is committing and there is no idempotency key. If step 2 times out, read state or contact
  QBE; do not re-fire.
- Same credentials and tracing headers as every call: `Ocp-Apim-Subscription-Key`, `X-ClientID`,
  `X-ClientSecret`, `X-Partner-Id`, `X-TrackingID`, `X-Mockable`.
- Errors are `{"errors":[{"code","message","details"}]}`; business rejections arrive as
  `INTERNAL_BUSINESS_EXCEPTION` or `CCHANGE_BUSINESS_EXCEPTION` with the reason in the message.
- Full detail: `vocabulary/qbe-vocabulary.yml` (all controlled values),
  `conventions/qbe-conventions.yml`, `errors/qbe-problem-types.yml`.
