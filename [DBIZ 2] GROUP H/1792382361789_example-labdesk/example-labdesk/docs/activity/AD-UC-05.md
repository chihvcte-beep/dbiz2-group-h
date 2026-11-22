# Activity Diagram: AD-UC-05 Release no-show seats

> **Worked example for teaching (LabDesk).** Not a student submission and not a real product.

| Field | Value |
|---|---|
| AD ID | AD-UC-05 |
| Use case | UC-05 Release no-show seats |
| Feature | F-02 Check-in and No-show |
| Primary actor | none: started by time (system-initiated) |
| Lanes | LabDesk system · Email service |
| Inputs (L3-L5) | Context Diagram v2 (Email service) · Use Case Diagram v2 (UC-05 added, started by time) · Architecture v2 + ADR-004 (scheduler) · W1 rows FR-02-04 to FR-02-06, BR-04 |
| Trigger | 15 minutes have passed since a slot started |
| Preconditions | The slot has at least one booking. |
| Success end state | Every booking of the slot that was still `Confirmed` is now `No-show`, its seat is free, and the student has been notified. |
| FRs covered | FR-02-04, FR-02-05, FR-02-06 |
| Business rules applied | BR-04 |
| Version / status | v1.0 · Reviewed |

## 1. Diagram

The hourglass is a **time event**: the activity starts by itself when the time expression on the
first arrow becomes true. No person clicks anything. This is the kind of flow that a coding agent
never builds unless a document asks for it.

```mermaid
swimlane-beta TB
  subgraph SYS["LabDesk system"]
    t1@{ shape: hourglass }
    s1("Find bookings of the slot still Confirmed (FR-02-04)")
    d1{"Any found?"}
    stop1@{ shape: fr-circ }
    m0{" "}
    s2("Set booking to No-show and free the seat (FR-02-04)")
    o1["Booking [No-show]"]
    f1@{ shape: fork }
    d2{"3 no-shows<br>in 30 days?"}
    s3("Suspend booking rights for 7 days (FR-02-06)")
    m1{" "}
    j1@{ shape: join }
    d3{"More bookings<br>to process?"}
    stop2@{ shape: fr-circ }
  end
  subgraph MAIL["Email service"]
    e1("Send no-show notice (FR-02-05)")
  end
  t1 -->|"15 min after slot start"| s1 --> d1
  d1 -->|"[no]"| stop1
  d1 -->|"[yes]"| m0 --> s2 --> o1 --> f1
  f1 --> e1 --> j1
  f1 --> d2
  d2 -->|"[yes]"| s3 --> m1
  d2 -->|"[no]"| m1
  m1 --> j1 --> d3
  d3 -->|"[yes]"| m0
  d3 -->|"[no]"| stop2
```

Reading notes:

- The loop `d3 [yes] → s2` processes one booking at a time. UML has a richer notation for this
  (an expansion region); the course profile uses a simple loop because it renders everywhere and
  reads the same way.
- The loop re-enters through the merge `m0`, never straight into `s2`, for the same reason as in
  AD-UC-01: an action with two incoming control flows would wait for both.

## 2. Node trace

| Node | Kind | Text | Traces to |
|---|---|---|---|
| t1 | Time event | 15 min after slot start | FR-02-04 |
| s1 | Action | Find bookings of the slot still Confirmed | FR-02-04 |
| s2 | Action | Set booking to No-show and free the seat | FR-02-04 |
| o1 | Object node | Booking [No-show] | FR-02-04 (state value) |
| d2 | Decision | 3 no-shows in 30 days? | BR-04 |
| s3 | Action | Suspend booking rights for 7 days | FR-02-06, BR-04 |
| e1 | Action (external lane) | Send no-show notice | FR-02-05 |

## 3. Branches and acceptance tests

| Branch | Given | When | Then |
|---|---|---|---|
| d1 [no] | every booking of the 09:00 slot is Checked-in or Cancelled | it is 09:15 | nothing changes |
| d1 [yes], d2 [no] | one booking of the 09:00 slot is Confirmed and the student has no earlier no-show | it is 09:15 | the booking is No-show, the seat is free, one notice is sent, booking rights are unchanged |
| d1 [yes], d2 [yes] | the student already has 2 no-shows in the last 30 days | their third booking becomes No-show at 09:15 | booking rights are suspended until 7 days later and the notice says so |
| d3 [yes] | two bookings of the slot are still Confirmed | it is 09:15 | both become No-show and two notices are sent |

## 4. Object states used

| Object | States in this diagram |
|---|---|
| Booking | Confirmed (read), No-show (written) |

## 5. Open questions

| # | Question | Blocking? | Default applied |
|---|---|---|---|
| 1 | [NEEDS CLARIFICATION: does a student who arrives at minute 16 get the seat back if it is still free?] | No | No; they book again like anyone else. |
