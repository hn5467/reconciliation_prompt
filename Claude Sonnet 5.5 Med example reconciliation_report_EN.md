# Reconciliation Report: Purchases vs. Bank Statement

*Output of running `bank_reconciliation_prompt_EN.md` on the included test data (`purchases_accounting_system.xlsx` and `bank_statement.xlsx`) with the default assumptions listed at the end. Use it as a reference to compare against your own run.*

## 1. Executive summary

| Metric | Records | Amount (UYU) |
|---|---|---|
| Total purchases | 20 | 432,750.00 |
| Purchases reconciled | 18 | 394,000.00 |
| Purchases unreconciled | 2 | 38,750.00 |
| % purchases reconciled | 90.0% | 91.0% |
| Total bank outflows | 14 | 397,650.00 |
| Outflows matched to purchases | 12 | 394,000.00 |
| % outflows reconciled | 85.7% | 99.1% |
| Unreconciled bank transactions (all) | 3 | 146,350.00 (net) |
| Net bank movement (inflows - outflows) | 15 | -247,650.00 |

Reconciled purchases equal matched payments (difference 0.00), so the two sides tie out.

## 2. One-to-one reconciliations

| Purchase_ID | Transaction_ID | Supplier | Amount | Purchase date | Payment date | Days to pay | Difference |
|---|---|---|---|---|---|---|---|
| P014 | T003 | Supplier B | 6,300.00 | 2026-08-09 | 2026-08-15 | 6 | 0.00 |
| P005 | T005 | Supplier D | 22,300.00 | 2026-08-05 | 2026-08-16 | 11 | 0.00 |
| P018 | T006 | Supplier D | 9,400.00 | 2026-08-11 | 2026-08-17 | 6 | 0.00 |
| P007 | T007 | Supplier E | 60,000.00 | 2026-08-06 | 2026-08-15 | 9 | 0.00 |
| P009 | T008 | Supplier F | 9,800.00 | 2026-08-07 | 2026-08-16 | 9 | 0.00 |
| P011 | T009 | Supplier G | 33,400.00 | 2026-08-08 | 2026-08-18 | 10 | 0.00 |
| P013 | T010 | Supplier H | 27,500.00 | 2026-08-09 | 2026-08-17 | 8 | 0.00 |
| P015 | T011 | Supplier I | 41,200.00 | 2026-08-10 | 2026-08-19 | 9 | 0.00 |
| P017 | T012 | Supplier J | 17,600.00 | 2026-08-11 | 2026-08-18 | 7 | 0.00 |

## 3. Many-to-one reconciliations

| Transaction_ID | Purchase_IDs | Supplier | Purchases sum | Bank amount | Difference | Payment date |
|---|---|---|---|---|---|---|
| T001 | P001, P003, P006, P012 | Supplier A | 102,000.00 | 102,000.00 | 0.00 | 2026-08-13 |
| T002 | P002, P010 | Supplier B | 39,500.00 | 39,500.00 | 0.00 | 2026-08-14 |
| T004 | P004, P008, P016 | Supplier C | 25,000.00 | 25,000.00 | 0.00 | 2026-08-14 |

Invoice detail:

| Transaction_ID | Purchase_ID | Invoice_No | Purchase date | Amount |
|---|---|---|---|---|
| T001 | P001 | FA-1001 | 2026-08-03 | 45,000.00 |
| T001 | P003 | FA-1002 | 2026-08-04 | 30,000.00 |
| T001 | P006 | FA-1003 | 2026-08-05 | 15,000.00 |
| T001 | P012 | FA-1004 | 2026-08-08 | 12,000.00 |
| T002 | P002 | FB-2001 | 2026-08-03 | 18,500.00 |
| T002 | P010 | FB-2002 | 2026-08-07 | 21,000.00 |
| T004 | P004 | FC-3001 | 2026-08-04 | 8,750.00 |
| T004 | P008 | FC-3002 | 2026-08-06 | 11,250.00 |
| T004 | P016 | FC-3003 | 2026-08-10 | 5,000.00 |

## 4. Unreconciled purchases

| Purchase_ID | Supplier | Invoice_No | Amount | Date | Days outstanding (as of 2026-08-20) | Comment |
|---|---|---|---|---|---|---|
| P019 | Supplier K | FK-1201 | 25,000.00 | 2026-08-12 | 8 | No payment to this supplier found in the statement; check due date and payment terms. |
| P020 | Supplier E | FE-5002 | 13,750.00 | 2026-08-12 | 8 | Supplier has other invoices paid in this statement; check payment terms for this one. |

## 5. Unreconciled bank transactions

| Transaction_ID | Description | Amount | Date | Likely nature |
|---|---|---|---|---|
| T013 | Account maintenance fee | -450.00 | 2026-08-20 | Bank fee |
| T014 | Incoming transfer - Customer XYZ | 150,000.00 | 2026-08-14 | Customer receipt (inflow, not a purchase) |
| T015 | Direct debit - Insurance | -3,200.00 | 2026-08-19 | Direct debit (non-purchase) |

## 6. Cases to review

No ambiguous matches were found. The items below are a near-miss and matches inferred from sums.

| Priority | Type | Transaction | Purchases | Issue | Suggested follow-up |
|---|---|---|---|---|---|
| Medium | Near-miss (not matched) | T004 | P019 | P019 (Supplier K, 25,000.00) has the same amount as T004, but that transfer is to Supplier C and already reconciles to that supplier's invoices. | Do not match. Confirm payment status of the invoice with Treasury. |
| Low | Inferred match (verify) | T001 | P001, P003, P006, P012 | T001 reconciles only by the sum of 4 invoices from Supplier A; the bank reference does not list the invoice numbers. | Verify against the supplier's remittance advice or payment proposal. |
| Low | Inferred match (verify) | T002 | P002, P010 | T002 reconciles only by the sum of 2 invoices from Supplier B; the bank reference does not list the invoice numbers. | Verify against the supplier's remittance advice or payment proposal. |
| Low | Inferred match (verify) | T004 | P004, P008, P016 | T004 reconciles only by the sum of 3 invoices from Supplier C; the bank reference does not list the invoice numbers. | Verify against the supplier's remittance advice or payment proposal. |

## 7. Assumptions and tolerances used

| Parameter | Value | Note |
|---|---|---|
| Currency | UYU | All amounts are in a single currency; no FX applied. |
| Amount tolerance | 1.0 | A match requires |purchase amount - bank amount| <= tolerance. |
| Payment window (days) | 30 | Bank date must be 0 to 30 days after the purchase date. |
| Statement cut-off (as-of date) | 2026-08-20 | Latest transaction date in the statement; used for days outstanding. |
| Supplier identification | Bank description | Supplier name is parsed from the description (e.g. 'Outgoing transfer - Supplier A'). |
| Many-to-one scope | Same supplier only | Combinations of 2+ invoices from one supplier; cross-supplier grouping not attempted. |
| Matching order | 1-to-1, then many-to-one | Many-to-one is attempted only on invoices left after the one-to-one pass. |
| Ambiguity rule | Unique solution required | If several candidates fit, the case goes to Review instead of being auto-matched. |
| Bank items considered as payments | Outflows only | Inflows and non-purchase debits are listed as unreconciled, never forced into a match. |
