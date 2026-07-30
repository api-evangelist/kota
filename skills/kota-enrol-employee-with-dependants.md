---
name: Enrol an employee and manage dependants
description: Run the employee-side benefits flow — check eligibility, drive an enrolment intent to
  completion, attach dependants or beneficiaries, and issue the individual policy.
api: openapi/kota-openapi-original.json
base_url: https://api.kota.io
test_base_url: https://test.api.kota.io
operations:
  - CheckGroupEligibility
  - CreateEnrolmentIntent
  - RetrieveEnrolmentIntent
  - ListEnrolmentIntentRequirements
  - UpdateEnrolmentIntentConfiguration
  - SubmitEnrolmentIntentCoverageSelections
  - CreateDependentsManagementIntentForEnrolmentIntent
  - CreateAssociatedPerson
  - ListAssociatedPersons
  - AddDependentsToDependentsManagementIntent
  - RemoveDependentFromDependentsManagementIntent
  - GetAssociatedPersonsEligibility
  - ConfirmDependentsManagementIntent
  - CancelDependentsManagementIntent
  - ConfirmEnrolmentIntent
  - RejectEnrolmentIntent
  - RetrievePolicy
  - ListEmployeeHealthInsurancePolicies
---

# Enrol an employee and manage dependants

Once a group policy is active, each eligible employee either enrols — receiving their own policy
derived from the group policy — or opts out within the cooling-off window.

## Steps

1. **Check eligibility.** Call `CheckGroupEligibility` for the employee and group before offering
   anything in your UI.
2. **Start enrolment.** An enrolment intent is created either automatically when you call
   `AddEmployeeToGroup`, or explicitly with `CreateEnrolmentIntent`. Read it back with
   `RetrieveEnrolmentIntent`.
3. **Fulfil requirements.** Call `ListEnrolmentIntentRequirements` and render the returned fields
   and schemas. Submit answers incrementally and re-check until nothing is outstanding.
4. **Capture coverage choices.** Call `SubmitEnrolmentIntentCoverageSelections` with the employee's
   selections. Use `UpdateEnrolmentIntentConfiguration` if the policy configuration for the intent
   needs to change.
5. **Add dependants or beneficiaries** (optional). Create the people with `CreateAssociatedPerson`
   (spouse, partner, children), then open a dependants management intent with
   `CreateDependentsManagementIntentForEnrolmentIntent`. Check who qualifies with
   `GetAssociatedPersonsEligibility`, attach them with
   `AddDependentsToDependentsManagementIntent`, drop any with
   `RemoveDependentFromDependentsManagementIntent`, and finish with
   `ConfirmDependentsManagementIntent`. `CancelDependentsManagementIntent` abandons it. Adding
   dependants changes coverage and premiums.
6. **Confirm.** Call `ConfirmEnrolmentIntent`. This issues the individual **Policy** under the
   group policy. Read it with `RetrievePolicy` or `ListEmployeeHealthInsurancePolicies`.
7. **Or opt out.** Call `RejectEnrolmentIntent` within the cooling-off window. Surface the deadline
   prominently — opt-out windows are time-limited and once the window closes the policy stands.

## After issuance

Dependants can still be added during the cooling-off period by opening a dependants management
intent against the issued policy. Later changes go through a policy amendment intent
(`CreatePolicyAmendmentIntent` → `ConfirmPolicyAmendmentIntent`).

## Rules

- Send `Idempotency-Key: <uuid-v4>` on every POST.
- Handle `employee.health_insurance.offer.action_required` immediately: its `required_action`
  object (`reason`, `reason_description`, `due_at`) is time-sensitive for the employee. Present
  Kota's wording rather than your own — this is regulated communication.
- `400 invalid_state` means the intent or policy is not in a status that permits the call. Re-read
  the intent before retrying.
- Errors are RFC 9457 problem documents; on `400 invalid_request` the `errors` object names the
  exact invalid fields by JSON path.
