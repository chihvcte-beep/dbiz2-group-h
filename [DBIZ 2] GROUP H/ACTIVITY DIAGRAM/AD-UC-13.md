# Activity Diagram: AD-UC-13 Remove reviews that violate rules

| Field | Value |
|---|---|
| AD ID | AD-UC-13 |
| Use case | UC-13 Remove reviews that violate rules |
| Feature | F-02 Reviews & QR |
| Primary actor | On-site Staff |
| Lanes | On-site Staff · Library Core System |
| Inputs (L3-L5) | Context Diagram (On-site Staff flows "Reported reviews", "Remove review", "Staff sign-in"; Library Internal System flow "Staff accounts") · Use Case Diagram (UC-13) · Sequence: User Review Reporting Flow (UC-14 with UC-13) · W0 Table 1 (staff login), Table 4 (Book review, ILF) · W1 rows FR-02-10, FR-02-14, FR-02-19, FR-02-20, FR-04-07, FR-04-08, FR-04-12 (FR-04-05 and FR-04-06 were traced to UC-13 by mistake; W1 corrected, see open question 3) |
| Trigger | On-site Staff open the reported reviews |
| Preconditions | Staff have an internal library account (FR-04-07). Readers have reported reviews through UC-14. |
| Success end state | Every reported review the staff handled is either removed from public display (with an audit entry) or kept public with its report dismissed; staff stop when they choose. |
| Failure end state | No reported reviews are waiting (FR-02-19), or staff are not signed in and do not sign in. |
| FRs covered | FR-02-10, FR-02-14, FR-02-19, FR-02-20, FR-04-07, FR-04-08, FR-04-12 |
| Business rules applied | Removal needs a confirmation (FR-02-10). Every removal writes an audit entry (FR-04-12). A dismissed review stays public and leaves the reported list (FR-02-20). Staff judge whether a review breaks the rules; the system does not judge content. The staff page needs a staff session and role (FR-04-08). |
| Version / status | v1.2 · Draft |
| Author | Owner C (F-02) |

## 1. Diagram

Notation follows the DBIZ2 activity profile and the GeeksforGeeks notation sheet the team uses.
Rendered with `swimlane-beta`, which needs Mermaid 11.16 or later.

```mermaid
---
config:
  theme: base
  themeVariables:
    primaryColor: "#d5e8d4"
    primaryBorderColor: "#333333"
    lineColor: "#000000"
    clusterBkg: "#ffffff"
    clusterBorder: "#333333"
---
swimlane-beta TB
  subgraph STF["On-site Staff"]
    start@{ shape: sm-circ }
    m0{" "}
    a1("Open the reported reviews (FR-02-14)")
    d1{"Sign in now?"}
    a2("Sign in with the internal library account (FR-04-07)")
    a3("Select a reported review (FR-02-10)")
    d3{"Does the review violate the rules?"}
    a4("Choose Remove on the review (FR-02-10)")
    d4{"Confirm the removal?"}
    a5("Dismiss the report (FR-02-20)")
    d5{"Handle another reported review?"}
    stop1@{ shape: fr-circ }
    stop3@{ shape: fr-circ }
  end
  subgraph SYS["Library Core System"]
    s0("Check the staff session and role (FR-04-08)")
    d0{"Valid staff session and role?"}
    s1("Deny access to the moderation page (FR-04-08)")
    m1{" "}
    s2("Retrieve the reported reviews (FR-02-14)")
    d2{"Are there reported reviews?"}
    s3("Display that no reported reviews are waiting (FR-02-19)")
    s4("Display the reported-reviews list (FR-02-14)")
    s5("Remove the review from public display (FR-02-10)")
    s6("Write an audit entry for the review removal (FR-04-12)")
    s7("Keep the review public and remove it<br/>from the reported-reviews list (FR-02-20)")
    m2{" "}
    stop2@{ shape: fr-circ }
  end

  start --> m0 --> a1 --> s0 --> d0
  d0 -->|"[No]"| s1 --> d1
  d1 -->|"[Yes]"| a2 --> m0
  d1 -->|"[No]"| stop1
  d0 -->|"[Yes]"| m1 --> s2 --> d2
  d2 -->|"[No]"| s3 --> stop2
  d2 -->|"[Yes]"| s4 --> a3 --> d3
  d3 -->|"[Yes]"| a4 --> d4
  d4 -->|"[Yes]"| s5 --> s6 --> m2
  d4 -->|"[No]"| m2
  d3 -->|"[No]"| a5 --> s7 --> m2
  m2 --> d5
  d5 -->|"[Yes]"| m1
  d5 -->|"[No]"| stop3
```

Reading notes:

- `d3` is a staff judgement, not a system rule: it sits in the staff lane.
- `d4 [No]` (removal not confirmed) changes nothing; the review stays in the reported list.
- `m1` is the merge the staff come back through to handle the next reported review; the list is
  loaded again each time, so a review handled by a colleague in the meantime is gone.

## 2. Node trace

| Node | Kind | Text | Traces to |
|---|---|---|---|
| a1 | Action (Staff) | Open the reported reviews | FR-02-14 |
| s0 | Action | Check the staff session and role | FR-04-08 |
| d0 | Decision | Valid staff session and role? | FR-04-08 |
| s1 | Action | Deny access to the moderation page | FR-04-08 |
| d1 | Decision (Staff) | Sign in now? | FR-04-07 |
| a2 | Action (Staff) | Sign in with the internal library account | FR-04-07 |
| s2 | Action | Retrieve the reported reviews | FR-02-14 |
| d2 | Decision | Are there reported reviews? | FR-02-19 |
| s3 | Action | Display that no reported reviews are waiting | FR-02-19 |
| s4 | Action | Display the reported-reviews list | FR-02-14 |
| a3 | Action (Staff) | Select a reported review | FR-02-10 |
| d3 | Decision (Staff) | Does the review violate the rules? | FR-02-10, FR-02-20 |
| a4 | Action (Staff) | Choose Remove on the review | FR-02-10 |
| d4 | Decision (Staff) | Confirm the removal? | FR-02-10 |
| s5 | Action | Remove the review from public display | FR-02-10 |
| s6 | Action | Write an audit entry for the review removal | FR-04-12 |
| a5 | Action (Staff) | Dismiss the report | FR-02-20 |
| s7 | Action | Keep the review public and remove it from the reported-reviews list | FR-02-20 |
| d5 | Decision (Staff) | Handle another reported review? | FR-02-14 |

## 3. Branches and acceptance tests

| Branch | Given | When | Then |
|---|---|---|---|
| d0 [No] → d1 [No] | the staff member is not signed in | they open the reported reviews and decline to sign in | access to the moderation page is denied |
| d0 [No] → d1 [Yes] | the staff member is not signed in | they sign in with internal account "staff.lan" | the session is checked again and the list loads |
| d0 [Yes] → d2 [No] | no review has an open report | signed-in staff open the reported reviews | a message says no reported reviews are waiting |
| d2 [Yes] | reviews #91 and #95 have open reports | signed-in staff open the reported reviews | #91 and #95 are listed |
| d3 [Yes] → d4 [Yes] | review #91 contains insults | staff choose Remove and confirm | #91 is no longer shown publicly, leaves the list, and an audit entry "staff.lan, review removal, time" is written |
| d4 [No] | review #91 is selected | staff choose Remove and then cancel | #91 stays public and stays in the list |
| d3 [No] | review #95 follows the rules | staff dismiss the report | #95 stays public and leaves the reported list |
| d5 [Yes] | #91 has been handled | staff choose to handle another review | the list reloads with #95 only |
| d5 [No] | a review has been handled | staff stop | the activity ends |

## 4. Object states used

| Object | States in this diagram |
|---|---|
| Review | Published (kept by `s7`), Removed (written by `s5`) |
| Review report | Open (read by `s2`), Dismissed (written by `s7`), Upheld (when `s5` removes the review); names confirmed 2026-11-04 (question 5) |
| Audit entry | written by `s6` |

## 5. Screens touched

Filled in during Lesson 8, from the Screen List.

| Staff action | Screen ID |
|---|---|
| Open the reported reviews, Select a reported review | (Lesson 8) |
| Choose Remove and confirm, Dismiss the report | (Lesson 8) |
| Sign in with the internal library account | (Lesson 8) |

## 6. Open questions

On 2026-11-04 the team adopted the default answer for every question below, unless the row
says otherwise.

| # | Question | Blocking? | Default applied |
|---|---|---|---|
| 1 | where are "the rules" written that staff judge reviews against? | No (decided) | Decided 2026-11-04 (default adopted): The library's review guideline, linked from the review form. |
| 2 | is the author told when their review is removed? | No (decided) | Decided 2026-11-04 (default adopted): No notice in release 1. |
| 3 | Wrong W1 source trace: FR-04-05 (link an online account to a library card) and FR-04-06 (reject linking when both profiles hold data) name UC-13, but they belong to an older use case for account linking, are Won't, and have nothing to do with removing reviews. | No (resolved) | They are not part of UC-13 and are not drawn or counted here. W1 corrected on 2026-11-04: their source trace now names UC-11 (online part, cut in W4). |
| 4 | The sequence User Review Reporting Flow uses FR-02-10 for opening the reported-reviews list; this diagram uses FR-02-14, as W1 does. | No (open work item) | Owner C changes the sequence step to FR-02-14 (index, Inputs check finding 7). |
| 5 | confirm the state names of a review report: Open, Dismissed, Upheld. | No (decided) | Decided 2026-11-04 (default adopted): These three names are used until the data model is set in DBIZ3. |

## 7. Verification log

| Check | Result | By | Date |
|---|---|---|---|
| Renders (Mermaid 12.2.0, swimlane-beta) | Pass; still to open once on mermaid.live | AI assistant | 2026-11-04 |
| Every decision has guards on all outgoing flows | Pass | AI assistant | 2026-11-04 |
| No action or decision has two incoming flows without a merge | Pass | AI assistant | 2026-11-04 |
| Every fork has a matching join | Not applicable (no fork) | AI assistant | 2026-11-04 |
| Every action cites one FR | Pass | AI assistant | 2026-11-04 |
| Every FR of UC-13 appears in the diagram | Pass (5 of 5 non-Won't W1 rows whose source trace names UC-13, after the W1 trace correction) | AI assistant | 2026-11-04 |
| Lane names match the Context Diagram | Pass | AI assistant | 2026-11-04 |
| AI critic prompt run, findings resolved or logged | Not yet run by the team | | |
