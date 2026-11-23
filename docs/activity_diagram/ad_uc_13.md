# Activity Diagram: AD-UC-13 Remove reviews that violate rules

| Field | Value |
|---|---|
| AD ID | AD-UC-13 |
| Use case | UC-13 Remove reviews that violate rules |
| Feature | F-02 Reviews & QR |
| Primary actor | On-site Staff |
| Lanes | On-site Staff · Library Core System |
| Inputs (L3-L5) | Context Diagram (On-site Staff flows "Reported reviews", "Remove review", "Staff sign-in"; Library Internal System flow "Staff accounts") · Use Case Diagram (UC-13) · Sequence: [SD-UC-13](../system_design/sequence_diagram/sd_uc_13.md) · W0 Table 1 (staff login), Table 4 (Book review, ILF) · W1 rows FR-02-10, FR-02-14, FR-02-19, FR-02-20, FR-04-07, FR-04-08, FR-04-12, FR-04-18, FR-04-21 (D7) (FR-04-05 and FR-04-06 are not part of UC-13: AD-UC-13 Q3) |
| Trigger | On-site Staff open the staff page to handle the reported reviews |
| Preconditions | Staff have an internal library account (FR-04-07). Readers have reported reviews through UC-14. |
| Success end state | Every reported review the staff handled is either removed from public display (with an audit entry) or kept public with its report dismissed; staff stop when they choose. |
| Failure end state | No reported reviews are waiting (FR-02-19), or staff cannot sign in (wrong account or no staff role) and stop trying. |
| FRs covered | FR-02-10, FR-02-14, FR-02-19, FR-02-20, FR-04-07, FR-04-08, FR-04-12, FR-04-18, FR-04-21 |
| Business rules applied | Removal needs a confirmation (FR-02-10). Every review removal and every successful staff sign-in writes an audit entry (FR-04-12; D30). A dismissed review stays public and leaves the reported list (FR-02-20). Staff judge whether a review breaks the rules (`d3`) against exactly the three criteria shown to readers in the hint under the review field on S-F02-01 and S-F02-02 (MSG-14): no offensive language, no advertising, no personal information (D20); the system does not judge content. The staff page opens only with a staff session and role: staff sign in before the page opens (FR-04-08, FR-04-07). A wrong account or an account without the staff role is rejected with an error message, and staff may try again (FR-04-18). The staff session does not end by time: it ends only when staff choose Sign out (FR-04-21, D7). |
| Version / status | v1.5 · Draft |
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
    a0("Open the staff page (FR-04-08)")
    m0{" "}
    a2("Sign in with the internal library account (FR-04-07)")
    d1{"Try again?"}
    mA{" "}
    a1("Open the reported reviews (FR-02-14)")
    a3("Select a reported review (FR-02-10)")
    d3{"Does the review violate the rules?"}
    a4("Choose Remove on the review (FR-02-10)")
    d4{"Confirm the removal?"}
    a5("Dismiss the report (FR-02-20)")
    d5{"Handle another reported review?"}
    d7{"Sign out?"}
    a6("Choose Sign out (FR-04-21)")
    stop1@{ shape: fr-circ }
    stop3@{ shape: fr-circ }
  end
  subgraph SYS["Library Core System"]
    s0("Check the staff session and role (FR-04-08)")
    d0{"Valid staff session and role?"}
    s1("Deny the request and show the staff sign-in (FR-04-08)")
    s8("Verify the account and the staff role<br/>against the internal library accounts (FR-04-07)")
    d6{"Valid account with the staff role?"}
    s9("Reject the sign-in and show an error message (FR-04-18)")
    s10("Start a staff session and open the staff page (FR-04-07)")
    s12("Write an audit entry for the staff sign-in (FR-04-12)")
    m1{" "}
    s2("Retrieve the reported reviews (FR-02-14)")
    d2{"Are there reported reviews?"}
    s3("Display that no reported reviews are waiting (FR-02-19)")
    s4("Display the reported-reviews list (FR-02-14)")
    s5("Remove the review from public display (FR-02-10)")
    s6("Write an audit entry for the review removal (FR-04-12)")
    s7("Keep the review public and remove it<br/>from the reported-reviews list (FR-02-20)")
    m2{" "}
    s11("End the staff session and show the staff sign-in (FR-04-21)")
    stop2@{ shape: fr-circ }
    stop4@{ shape: fr-circ }
  end

  start --> a0 --> s0 --> d0
  d0 -->|"[No]"| s1 --> m0 --> a2 --> s8 --> d6
  d6 -->|"[No]"| s9 --> d1
  d1 -->|"[Yes]"| m0
  d1 -->|"[No]"| stop1
  d6 -->|"[Yes]"| s10 --> s12 --> mA
  d0 -->|"[Yes]"| mA
  mA --> a1 --> m1 --> s2 --> d2
  d2 -->|"[No]"| s3 --> stop2
  d2 -->|"[Yes]"| s4 --> a3 --> d3
  d3 -->|"[Yes]"| a4 --> d4
  d4 -->|"[Yes]"| s5 --> s6 --> m2
  d4 -->|"[No]"| m2
  d3 -->|"[No]"| a5 --> s7 --> m2
  m2 --> d5
  d5 -->|"[Yes]"| m1
  d5 -->|"[No]"| d7
  d7 -->|"[Yes]"| a6 --> s11 --> stop4
  d7 -->|"[No]"| stop3
```

Reading notes:

- `d3` is a staff judgement, not a system rule: it sits in the staff lane.
- `d4 [No]` (removal not confirmed) changes nothing; the review stays in the reported list.
- `m1` is the merge the staff come back through to handle the next reported review; the list is
  loaded again each time, so a review handled by a colleague in the meantime is gone.
- The session is checked at the start: the staff page opens only for a signed-in staff member
  (FR-04-08, L8-02), so staff sign in before they open the reported reviews. `m0` is the merge
  staff come back through after a rejected sign-in; `mA` gathers the two signed-in paths before `a1`.
- `d6 [No]` covers a wrong account and an account without the staff role (FR-04-18, L8-03). Staff
  sign in with their own action, not with UC-11 (the reader sign-in).
- A successful staff sign-in writes an audit entry (`s12`, FR-04-12, D30), as the reader sign-in
  does in AD-UC-11 `s8`. A rejected sign-in writes none.
- The staff session does not end by time (D7). Sign out (`d7`, `a6`, `s11`) is drawn once, when
  staff stop handling reviews; «Đăng xuất» is on every staff screen, so staff can sign out at any
  time (FR-04-21).

## 2. Node trace

| Node | Kind | Text | Traces to |
|---|---|---|---|
| a0 | Action (Staff) | Open the staff page | FR-04-08 |
| s0 | Action | Check the staff session and role | FR-04-08 |
| d0 | Decision | Valid staff session and role? | FR-04-08 |
| s1 | Action | Deny the request and show the staff sign-in | FR-04-08 |
| a2 | Action (Staff) | Sign in with the internal library account | FR-04-07 |
| s8 | Action | Verify the account and the staff role against the internal library accounts | FR-04-07 |
| d6 | Decision | Valid account with the staff role? | FR-04-07, FR-04-18 |
| s9 | Action | Reject the sign-in and show an error message | FR-04-18 |
| d1 | Decision (Staff) | Try again? | FR-04-18 |
| s10 | Action | Start a staff session and open the staff page | FR-04-07 |
| s12 | Action | Write an audit entry for the staff sign-in | FR-04-12 |
| a1 | Action (Staff) | Open the reported reviews | FR-02-14 |
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
| d7 | Decision (Staff) | Sign out? | FR-04-21 |
| a6 | Action (Staff) | Choose Sign out | FR-04-21 |
| s11 | Action | End the staff session and show the staff sign-in | FR-04-21 |

## 3. Branches and acceptance tests

| Branch | Given | When | Then |
|---|---|---|---|
| d0 [No] → d6 [Yes] | the staff member is not signed in | they open the staff page and sign in with internal account "staff.lan", which has the staff role | a staff session starts, an audit entry "staff.lan, staff sign-in, time" is written and the staff page opens; they can open the reported reviews |
| d6 [No] → d1 [Yes] | the staff member is not signed in | they enter a wrong password for "staff.lan", then the right one | the first try is rejected with an error message; the second try opens the staff page |
| d6 [No] → d1 [No] | internal account "lib.reader" exists but has no staff role | they sign in with it and then give up | the sign-in is rejected with an error message; no audit entry is written; the staff page does not open |
| d0 [Yes] → d2 [No] | no review has an open report | signed-in staff open the reported reviews | a message says no reported reviews are waiting |
| d2 [Yes] | reviews #91 and #95 have open reports | signed-in staff open the reported reviews | #91 and #95 are listed |
| d3 [Yes] → d4 [Yes] | review #91 contains insults | staff choose Remove and confirm | #91 is no longer shown publicly, leaves the list, and an audit entry "staff.lan, review removal, time" is written |
| d4 [No] | review #91 is selected | staff choose Remove and then cancel | #91 stays public and stays in the list |
| d3 [No] | review #95 follows the rules | staff dismiss the report | #95 stays public and leaves the reported list |
| d5 [Yes] | #91 has been handled | staff choose to handle another review | the list reloads with #95 only |
| d5 [No] → d7 [No] | a review has been handled | staff stop and leave the page open | the activity ends; the staff session stays valid with no time-out |
| d5 [No] → d7 [Yes] | a review has been handled | staff stop and choose «Đăng xuất» | the staff session ends and the staff sign-in opens |

## 4. Object states used

| Object | States in this diagram |
|---|---|
| Review | Published (kept by `s7`), Removed (written by `s5`) |
| Review report | Open (read by `s2`), Dismissed (written by `s7`), Upheld (when `s5` removes the review) (AD-UC-13 Q5) |
| Audit entry | written by `s6` (review removal) and `s12` (staff sign-in) |
| Staff session | Signed-in (written by `s10`), Ended (written by `s11`) |

## 5. Screens touched

Filled in during Lesson 8, from the Screen List.

| On-site Staff action | Screen ID |
|---|---|
| Open the staff page (a0) | S-F04-01 when signed in; S-F00-03 when not (s1) |
| Sign in with the internal library account (a2), Try again? (d1) | S-F00-03 |
| See that the sign-in was rejected (s9) | S-F00-03 (error state) |
| Staff page opens after sign-in (s10) | S-F00-03 → S-F04-01 |
| Open the reported reviews (a1) | S-F04-01 ("Reported reviews") → S-F02-04 |
| Select a reported review (a3), Does the review violate the rules? (d3), Choose Remove on the review (a4), Dismiss the report (a5), Handle another reported review? (d5) | S-F02-04 |
| Confirm the removal? (d4) | S-F02-04 (modal M-F02-04-01 "Remove this review?") |
| See the list without the handled review (s5, s7) | S-F02-04 (list reloaded) |
| See that no reported reviews are waiting (s3) | S-F02-04 (empty state) |
| Sign out? (d7), Choose Sign out (a6), staff sign-in shown (s11) | «Đăng xuất» in the header of S-F02-04 or S-F04-01 → S-F00-03 |

## 6. Open questions

None. Decisions: see [decision_index.md](../project_brief/decision_index.md#ad-uc-13).

## 7. Verification log

| Check | Result | By | Date |
|---|---|---|---|
| Renders (Mermaid 12.3.0, swimlane-beta) | Pass (re-checked after the v1.3 sign-in change) | AI assistant | 2026-11-08 |
| Every decision has guards on all outgoing flows | Pass | AI assistant | 2026-11-04 |
| No action or decision has two incoming flows without a merge | Pass | AI assistant | 2026-11-04 |
| Every fork has a matching join | Not applicable (no fork) | AI assistant | 2026-11-04 |
| Every action cites one FR | Pass | AI assistant | 2026-11-04 |
| Every FR of UC-13 appears in the diagram | Pass (5 of 5 non-Won't W1 rows whose source trace names UC-13, after the W1 trace correction, plus FR-04-18) | AI assistant | 2026-11-08 |
| Lane names match the Context Diagram | Pass | AI assistant | 2026-11-04 |
| v1.4 sign out (D7): guards on `d7`, each new action cites one FR | Pass (checked by reading) | AI assistant | 2026-11-22 |
| Renders (Mermaid 12.3.0, swimlane-beta, Chrome) | Pass | AI assistant | 2026-11-22 |
| Review criteria (D20): business rule for `d3` updated; diagram and node trace unchanged | Pass (checked by reading) | AI assistant | 2026-11-22 |
| v1.5 (D30): `s12` added between `s10` and `mA`, the new action cites one FR | Pass (checked by reading) | AI assistant | 2026-11-23 |
| Renders after v1.5 (Mermaid 12.3.0, swimlane-beta, Chrome) | Pass | AI assistant | 2026-11-23 |
| AI critic prompt run, findings resolved or logged | Not yet run by the team | | |
