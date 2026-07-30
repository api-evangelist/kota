---
name: Reconcile and finalize contribution reports
description: Pull Kota contribution reports and their per-employee breakdowns into payroll, then
  finalize the report so premiums are billed against the agreed contributions.
api: openapi/kota-openapi-original.json
base_url: https://api.kota.io
test_base_url: https://test.api.kota.io
operations:
  - ListContributionReports
  - RetrieveContributionReport
  - ListEmployeeBreakdownsForContributionReport
  - RetrieveEmployeeBreakdownForContributionReport
  - FinalizeContributionReport
  - RetrieveEmployee
---

# Reconcile and finalize contribution reports

Contribution reporting is how a payroll or benefits-administration platform tells Kota what each
employee actually contributed toward their benefit premiums for a period, and closes the period.

## Steps

1. **Find the open report.** Call `ListContributionReports`, filtering to the employer and period
   you are closing. Results paginate with `page` and `page_size` and return `items`, `page`,
   `page_size`, `total_count`.
2. **Read the report header.** Call `RetrieveContributionReport` for its status, period and
   totals. Only act on a report that is still open.
3. **Pull the per-employee breakdown.** Call `ListEmployeeBreakdownsForContributionReport` and page
   through all of it — do not stop at the first page. Use
   `RetrieveEmployeeBreakdownForContributionReport` for a single employee when investigating a
   discrepancy.
4. **Reconcile against payroll.** Match each breakdown line to your payroll deduction for the same
   employee and period. Resolve mismatches before finalizing: employees missing from the breakdown
   usually mean an unsynced employee or an enrolment that has not completed.
5. **Finalize.** Call `FinalizeContributionReport`. This is the irreversible commit for the period.
   Send `Idempotency-Key: <uuid-v4>` so a network failure can be retried without double-finalizing.
6. **Confirm downstream.** Handle the `contribution_report.finalized` webhook to trigger your own
   post-close work rather than assuming success from the HTTP response alone.

## Rules

- Finalize once per report. Replaying the identical request with the same `Idempotency-Key`
  returns the original response; changing parameters under the same key returns
  `409 idempotency_error`.
- `400 invalid_state` means the report is not in a finalizable status — usually already finalized.
  Re-read it rather than retrying.
- Retry only `429` and `5xx`, with exponential backoff.
- Reconcile before you finalize. There is no published un-finalize operation.
