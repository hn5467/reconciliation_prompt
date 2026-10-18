# Reconciliation_Prompt


# AI Prompt for Purchases vs. Bank Statement Reconciliation

A ready-to-use prompt that turns an AI assistant into a **financial manager / internal auditor** to reconcile your accounting system's purchases against your bank statements. It handles exact **one-to-one** matches and harder **many-to-one** cases, where several invoices are paid with a single transfer.

Test data is included so you can try it in minutes.

## Why this exists

Reconciliation has been a core finance task for decades. In telecom, for example, operators routinely reconciled the interconnect invoices other carriers claimed against the call events they had actually registered. Today the same logic applies at every scale, from large enterprises to small businesses and personal finances. A well-structured prompt lets AI do much of the heavy lifting while keeping the result auditable.

## What's in this repo

| File | Description |
|---|---|
| `bank_reconciliation_prompt_EN.md` | The prompt (English) |
| `purchases_accounting_system.xlsx` | Test data: 20 purchase records |
| `bank_statement.xlsx` | Test data: 15 bank transactions |
| `Gemini Auto Example Output.docx` | Output from Gemini Auto |
| `Copilot example Output reconciliation_report.xlsx` | Output from Copilot Auto - Basic License |
| `Claude Sonnet 5.5 Med example reconciliation_report_EN.md/.xlsx` | Output from Claude Sonnet 5.5 Medium |

## How to test it

1. Open your AI assistant of choice (Claude, ChatGPT, Gemini, etc.).
2. Paste the contents of `bank_reconciliation_prompt_EN.md`.
3. Attach both Excel files (`purchases_accounting_system.xlsx` and `bank_statement.xlsx`).
4. Confirm or adjust the assumptions the assistant proposes (amount tolerance, date window).
5. Review the reconciliation report and compare it with the expected results below.

## Test data design

The data was built on purpose to cover the typical scenarios:

- **One-to-one matches (9 cases)**: Suppliers D (x2), E, F, G, H, I, J, and one invoice from Supplier B.
- **Many-to-one matches (3 payments covering 9 invoices)**:
  - Supplier A: 4 invoices paid in one transfer of 102,000
  - Supplier B: 2 invoices paid in one transfer of 39,500
  - Supplier C: 3 invoices paid in one transfer of 25,000
- **Purchases without payment (2)**: one invoice from Supplier E and one from Supplier K.
- **Bank transactions without a purchase (3)**: an account fee, an insurance direct debit and an incoming customer transfer.
- **Built-in trap**: Supplier K's pending invoice (25,000) has the same amount as the Supplier C transfer. A good reconciliation should not match them, because the bank description and the invoice sums point to Supplier C.


## Tips for real-world use

- Always review the **"Cases to review"** section. The prompt is designed to flag ambiguity instead of forcing a match.
- Define your **tolerance and date window** up front for reproducible results.
- Do not paste sensitive data (account numbers, personal information) into tools your organization has not approved. Anonymize first.
- Treat the output as a **first-pass reconciliation** to be reviewed by a person, not as a final audit opinion.

## Feedback

Tried it on your own data? Found a case where it fails? Open an issue or send a message. Improvements and new test scenarios are welcome.

