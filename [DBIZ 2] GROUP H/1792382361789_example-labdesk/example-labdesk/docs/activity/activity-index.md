# Activity Diagram Index: LabDesk (worked example)

One row per use case in the Use Case inventory. Every use case appears, even when it needs no
diagram, so a reader can see that the decision was made on purpose.

## Inputs check (Block 1: what Lesson 3 and Lesson 4 gave us)

| # | Finding | Source to fix | Action | Owner | Status |
|---|---|---|---|---|---|
| 1 | Seats left unused must be released 15 minutes after the slot starts, but no use case covered it | Use Case Diagram | Added UC-05 "Release no-show seats" (started by time) | Integrator | Done |
| 2 | Email service sends confirmations (seen in the sequence for UC-01) but was missing from the Context Diagram | Context Diagram | Added "Email service" as an external entity | Owner A | Done |
| 3 | A timed job needs a scheduler that the Lesson 4 architecture did not have | Architecture | ADR-004 "Add a scheduler for timed jobs" | Integrator | Done |
| 4 | Sequence "Booking flow" told UC-01 and UC-02 together; cancel was an `opt` | Sequence Diagrams | Split into SD-UC-01 and SD-UC-02; the choice moved to the activity diagrams | Owner A | Open |

## Use cases

Rule used in this course: draw an activity diagram for every **Must** use case that has at least
one decision, more than one lane, or a time trigger. A use case that is a single display step gets
"not needed" and a one-line reason. A use case has at most one diagram, and one diagram never
covers two use cases.

| Use case | Name | Feature | Priority | Activity diagram | Status | Reason if not needed |
|---|---|---|---|---|---|---|
| UC-01 | Reserve a seat | F-01 | Must | `AD-UC-01.md` | Reviewed | |
| UC-02 | Cancel a booking | F-01 | Must | `AD-UC-02.md` | Draft | |
| UC-03 | View my bookings | F-01 | Must | not needed | | Single display step; no decision, one lane |
| UC-04 | Check in at the lab | F-02 | Must | `AD-UC-04.md` | Draft | |
| UC-05 | Release no-show seats | F-02 | Must | `AD-UC-05.md` | Reviewed | |
| UC-06 | Block a seat for maintenance | F-03 | Should | `AD-UC-06.md` | Draft | |
| UC-07 | View lab occupancy | F-03 | Should | not needed | | Single display step |

Object state lists collected from all diagrams (copy into the data model in DBIZ3):

| Object | States |
|---|---|
| Booking | Confirmed, Checked-in, Cancelled, No-show |
| Seat | Free, Booked, Blocked |
| Booking right (per student) | Active, Suspended |
