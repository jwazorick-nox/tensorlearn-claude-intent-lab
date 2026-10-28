# Intent: Results-ready notification

Sources: `inputs/01-approved-prd.md` (PRD N-17, approved 2026-09-18), `inputs/02-current-meeting.md` (discovery notes, 2026-09-20). `inputs/03-superseded-request.md` is superseded by PRD N-17 and is history only; nothing below is approved by it.

## Problem

- **I-1.** The clinic receives avoidable calls from patients checking whether their results are ready. (PRD, "Problem and outcome")

## Proposed outcome

- **I-2.** When a result is ready, the patient is notified and directed to review it in the existing authenticated portal. The notification channel is still open (see OPEN-1). (PRD, "Problem and outcome")
- **I-3.** "Ready" means a doctor has reviewed **and** released the result. Completion of the laboratory upload alone never makes a notification eligible. (PRD, "Approved constraints"; product owner, discovery notes)

**How success will be observed**

- **I-4.** A reduction in status-only calls about whether results are ready, counted separately from clinical questions and compared against a measured baseline. (PRD; support lead, discovery notes)
- **I-5.** Delivery failures are measured. (PRD, "Problem and outcome")
- **I-6.** No baseline or numeric target is approved yet; both are to be agreed during discovery. This intent sets no target. (PRD, "Problem and outcome")

## Affected users and systems

- **Patients:** receive the notification and view the released result in the portal.
- **Reviewing doctors:** their review and release of a result is the gate for any notification.
- **Clinic support staff:** handle the results-status calls this work aims to reduce, and help count them against the baseline.
- **Existing authenticated portal and its result route:** the destination the notification points to. It is reused, not redesigned.
- **Laboratory result upload:** affected only as an event that must not trigger a notification by itself.
- **Notification delivery and operational logs:** must carry no clinical or sensitive content.

## Scope

In scope: notifying the patient through the existing portal result route, preventing duplicate notifications, and handling delivery failures. (PRD, "Scope" and "Approved constraints")

## Out of scope

Excluded from this work:

- **X-1.** Portal redesign. (PRD, "Scope")
- **X-2.** Appointment scheduling. (PRD, "Scope")
- **X-3.** Clinical interpretation of results. (PRD, "Scope")
- **X-4.** Notifying third parties. (PRD, "Scope")
- **X-5.** A new or rebuilt patient dashboard; it is a separate project. (Engineering lead, discovery notes)
- **X-6.** Referring-doctor notification is not approved and is not part of this scope until OPEN-2 is decided. (PRD, "Unresolved decisions"; clinical owner, discovery notes)

## Constraints

- **C-1.** A doctor must review and release the result before any notification is eligible. (PRD)
- **C-2.** The notification says only that an update is available and directs the patient to the existing authenticated portal. No diagnosis, test result, clinical measurement or treatment detail appears in the message or in notification and operational logs. (PRD; privacy owner, discovery notes)
- **C-3.** Access to results is authenticated in the existing portal. No results are attached and no public result link is introduced. (PRD)
- **C-4.** No duplicate notifications for the same released result version. (PRD)
- **C-5.** Delivery failures are handled without sending duplicate patient messages. The mechanism is left to the spec. (PRD)

## Open questions

- **OPEN-1. Notification channel** (SMS, email, portal push). Owners: **product owner** and **privacy owner**, to decide after the consent and delivery review. (PRD, "Unresolved decisions"; privacy owner, discovery notes)
- **OPEN-2. Notifying the referring doctor.** Owners: **clinical owner** and **privacy owner**, who must decide recipient authorization. Not approved by the PRD, and approval must not be inferred from the superseded request. (PRD, "Unresolved decisions"; clinical owner, discovery notes)
- **OPEN-3. Baseline and numeric target** for the reduction in status-only calls, to be agreed during discovery. None is approved. (PRD, "Problem and outcome")

## Decision record

```json
{
  "notifyWhen": ["doctor-reviewed", "released"],
  "messageMayInclude": ["update-available"],
  "inScope": ["existing-portal-route", "duplicate-prevention", "delivery-failure-handling"],
  "openDecisions": [
    {"topic": "channel", "owners": ["product", "privacy"]},
    {"topic": "referring-doctor-notification", "owners": ["clinical", "privacy"]}
  ],
  "successMeasures": ["status-only-calls", "delivery-failures"],
  "numericTarget": null
}
```
