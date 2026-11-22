# Activity Diagram: AD-UC-01 Reserve a seat

> **Worked example for teaching (LabDesk).** LabDesk is the small reservation system used as the
> class example in DBIZ2. It is not a student submission and not a real product.

| Field | Value |
|---|---|
| AD ID | AD-UC-01 |
| Use case | UC-01 Reserve a seat |
| Feature | F-01 Seat Booking |
| Primary actor | Student |
| Lanes | Student · LabDesk system · Email service |
| Inputs (L3-L5) | Context Diagram v2 (Student, Email service) · Use Case Diagram v2 · Sequence: SD-UC-01 · Architecture v2 · W1 rows FR-01-01 to FR-01-06 |
| Trigger | The student opens the booking page |
| Preconditions | The student is signed in. Booking rights are not suspended (BR-04). |
| Success end state | One `Booking` in state `Confirmed` exists for the student, the slot and the seat; a confirmation email has been requested. |
| Failure end state | No new booking is created; the student sees why (existing booking, or seat taken). |
| FRs covered | FR-01-01, FR-01-02, FR-01-03, FR-01-04, FR-01-05, FR-01-06 |
| Business rules applied | BR-01, BR-03 |
| Version / status | v1.0 · Reviewed |
| Author | (team member) |

## 1. Diagram

Notation follows the DBIZ2 activity profile (`mermaid-activity-patterns.md`). Rendered with
`swimlane-beta`, which needs Mermaid 11.16 or later.

```mermaid
swimlane-beta TB
  subgraph STU["Student"]
    start@{ shape: sm-circ }
    a1("Open the booking page")
    a2("Choose lab and time slot")
    a3("Choose a seat")
    a4("Confirm the seat")
    a6("Choose another seat and confirm")
    a5("See booking confirmed")
    stop1@{ shape: fr-circ }
    stop2@{ shape: fr-circ }
  end
  subgraph SYS["LabDesk system"]
    s1("Show slots with free-seat counts (FR-01-01)")
    s2("Show seat map (FR-01-02)")
    m2{" "}
    d1{"Already booked<br>this slot?"}
    s3("Show the existing booking (FR-01-05)")
    d2{"Seat still free?"}
    s4("Refresh seat map, explain seat was taken (FR-01-04)")
    s5("Save booking (FR-01-03)")
    o1["Booking [Confirmed]"]
    f1@{ shape: fork }
    s6("Update free-seat count")
    j1@{ shape: join }
  end
  subgraph MAIL["Email service"]
    e1("Send confirmation email with check-in QR (FR-01-06)")
  end
  start --> a1 --> s1 --> a2 --> s2 --> a3 --> a4 --> m2 --> d1
  d1 -->|"[yes]"| s3 --> stop2
  d1 -->|"[no]"| d2
  d2 -->|"[no]"| s4 --> a6 --> m2
  d2 -->|"[yes]"| s5 --> o1 --> f1
  f1 --> s6 --> j1
  f1 --> e1 --> j1
  j1 --> a5 --> stop1
```

Reading notes:

- `m2` is a **merge** node. The flow coming back after "Choose another seat and confirm" enters a
  merge, not the decision `d1` or an action directly. A decision may legally have several incoming
  flows only through a merge in this course profile, and an action with two incoming control flows
  would wait for both (OMG UML 2.5.1, sub clause 15.2.3.2).
- The fork `f1` and join `j1` say that updating the seat count and sending the email have no
  required order. The student sees the confirmation only after both are done.
- The seat map shows blocked seats as unavailable, so BR-03 is enforced before the decision `d2`.

## 2. Node trace

Every action in the system lane cites a requirement. Every decision cites the rule or requirement
that decides it.

| Node | Kind | Text | Traces to |
|---|---|---|---|
| s1 | Action | Show slots with free-seat counts | FR-01-01 |
| s2 | Action | Show seat map | FR-01-02, BR-03 |
| d1 | Decision | Already booked this slot? | FR-01-05, BR-01 |
| s3 | Action | Show the existing booking | FR-01-05 |
| d2 | Decision | Seat still free? | FR-01-04 |
| s4 | Action | Refresh seat map, explain seat was taken | FR-01-04 |
| s5 | Action | Save booking | FR-01-03 |
| o1 | Object node | Booking [Confirmed] | FR-01-03 (state value) |
| s6 | Action | Update free-seat count | FR-01-01 (count must stay correct) |
| e1 | Action (external lane) | Send confirmation email with check-in QR | FR-01-06 |

## 3. Branches and acceptance tests

One row per outgoing branch of every decision. DBIZ3 turns each row into at least one test.

| Branch | Given | When | Then |
|---|---|---|---|
| d1 [yes] | the student holds a Confirmed booking in slot 09:00 to 11:00 | they confirm another seat in the same slot | no booking is created and the existing booking is shown |
| d1 [no] → d2 [no] | seat B-07 was free when the map loaded, then another student booked it | the first student confirms B-07 | no booking is created; the seat map reloads with B-07 marked booked and a message says the seat was just taken |
| d1 [no] → d2 [yes] | seat B-07 is free and the student has no booking in the slot | the student confirms B-07 | one Booking in state Confirmed exists, the free-seat count drops by one, and a confirmation email is requested |

## 4. Object states used

| Object | States that appear in this diagram | Full state list (all diagrams) |
|---|---|---|
| Booking | Confirmed | Confirmed, Checked-in, Cancelled, No-show |

These state names become the allowed values of `booking.status` in the DBIZ3 data model. Keep the
spelling identical everywhere.

## 5. Screens touched

Filled in during Lesson 8, from the Screen List.

| Student action | Screen ID |
|---|---|
| Open the booking page, Choose lab and time slot | S-F01-01 |
| Choose a seat, Confirm the seat, Choose another seat and confirm | S-F01-02 |
| See booking confirmed | S-F01-02 (success state) |
| See the existing booking (branch d1 [yes]) | S-F01-02 (message with link to S-F01-03) |

## 6. Open questions

| # | Question | Blocking? | Default applied |
|---|---|---|---|
| 1 | [NEEDS CLARIFICATION: if the email service is down, is the booking still Confirmed?] | No | Yes: the booking stays Confirmed; the email is retried. The student sees the QR in My bookings. |
| 2 | [NEEDS CLARIFICATION: how long before the slot starts does booking close?] | Yes | Booking closes when the slot starts (BR-02). |

## 7. Verification log

| Check | Result | By | Date |
|---|---|---|---|
| Renders on mermaid.live | Pass | | |
| Every decision has guards on all outgoing flows | Pass | | |
| Every fork has a matching join | Pass | | |
| Every system action cites an FR | Pass | | |
| Every FR of UC-01 appears in the diagram | Pass (6 of 6) | | |
| Lane names match the Context Diagram | Pass | | |
| AI critic prompt run, findings resolved or logged | Pass, 2 findings → open questions 1 and 2 | | |
