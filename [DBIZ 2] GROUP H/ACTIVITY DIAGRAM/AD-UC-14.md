# Activity Diagram: AD-UC-14 Report a review that violates rules

| Field | Value |
|---|---|
| AD ID | AD-UC-14 |
| Use case | UC-14 Report a review that violates rules |
| Feature | F-02 Reviews & QR |
| Primary actor | Reader |
| Lanes | Reader · Library Core System |
| Inputs (L3-L5) | Context Diagram (Reader flow "Report reviews") · Use Case Diagram (UC-14, from View book reviews UC-05; includes Sign in UC-11) · Sequence: [SD-UC-14](../SEQUENCE%20DIAGRAM/SD-UC-14.md) · W0 Table 1 (login required), Table 4 (Book review, ILF) · W1 rows FR-02-09, FR-02-21, FR-02-24, FR-04-08 (FR-02-10 is not part of UC-14: AD-UC-14 Q3) |
| Trigger | The reader selects Report on a review (usually from UC-05) |
| Preconditions | The review is on public display. The reader may not be signed in yet: the flow checks the session (FR-04-08) and calls Sign in (UC-11). |
| Success end state | A report is saved against the selected review and the reader sees a confirmation. The review waits for staff in UC-13. |
| Failure end state | The reader wrote this review (FR-02-24), has already reported it (FR-02-21), or chose not to sign in. No report is saved. |
| FRs covered | FR-02-09, FR-02-21, FR-02-24, FR-04-08; FR-04-01 through the call to UC-11 |
| Business rules applied | A reader cannot report their own review, also when the report was requested before sign-in (FR-02-24; D39). One report per reader per review (FR-02-21). Reporting needs a signed-in reader (FR-04-08). A reported review stays public until staff remove it (FR-02-10, UC-13). |
| Version / status | v1.4 · Draft |
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
  subgraph RDR["Reader"]
    start@{ shape: sm-circ }
    r1("Select Report on a review (FR-02-09)")
    d1{"Sign in now?"}
    c1[["Sign in (UC-11) (FR-04-01)"]]
    r2("Submit the report for the selected review (FR-02-09)")
    stop1@{ shape: fr-circ }
  end
  subgraph SYS["Library Core System"]
    m0{" "}
    s0("Check the reader's session (FR-04-08)")
    d0{"Valid session?"}
    s1("Deny the request (FR-04-08)")
    d3{"Did the reader write this review?"}
    s5("Display that a reader cannot report<br/>their own review (FR-02-24)")
    d2{"Has the reader already reported this review?"}
    s2("Display that the review has already been reported (FR-02-21)")
    s3("Save the report against the selected review (FR-02-09)")
    s4("Display a confirmation (FR-02-09)")
    stop2@{ shape: fr-circ }
    stop3@{ shape: fr-circ }
    stop4@{ shape: fr-circ }
  end

  start --> r1 --> m0 --> s0 --> d0
  d0 -->|"[No]"| s1 --> d1
  d1 -->|"[Yes]"| c1 --> m0
  d1 -->|"[No]"| stop1
  d0 -->|"[Yes]"| d3
  d3 -->|"[Yes]"| s5 --> stop4
  d3 -->|"[No]"| r2 --> d2
  d2 -->|"[Yes]"| s2 --> stop2
  d2 -->|"[No]"| s3 --> s4 --> stop3
```

Reading notes:

- After sign-in (`c1`) the flow re-enters through the merge `m0` and the session is checked again.
- `d3` runs after the session check because a signed-out reader sees Report on every review: the system knows who wrote the review only after sign-in (D39).
- What happens to the report afterwards (remove or dismiss) is drawn in AD-UC-13.

## 2. Node trace

| Node | Kind | Text | Traces to |
|---|---|---|---|
| r1 | Action (Reader) | Select Report on a review | FR-02-09 |
| s0 | Action | Check the reader's session | FR-04-08 |
| d0 | Decision | Valid session? | FR-04-08 |
| s1 | Action | Deny the request | FR-04-08 |
| d1 | Decision (Reader) | Sign in now? | FR-04-08 |
| c1 | Call (Reader) | Sign in (UC-11) | FR-04-01 |
| d3 | Decision | Did the reader write this review? | FR-02-24 |
| s5 | Action | Display that a reader cannot report their own review | FR-02-24 |
| r2 | Action (Reader) | Submit the report for the selected review | FR-02-09 |
| d2 | Decision | Has the reader already reported this review? | FR-02-21 |
| s2 | Action | Display that the review has already been reported | FR-02-21 |
| s3 | Action | Save the report against the selected review | FR-02-09 |
| s4 | Action | Display a confirmation | FR-02-09 |

## 3. Branches and acceptance tests

| Branch | Given | When | Then |
|---|---|---|---|
| d0 [No] → d1 [No] | the reader is not signed in | they select Report on review #91 and decline to sign in | the request is denied; no report is saved |
| d0 [No] → d1 [Yes] | the reader is not signed in | they sign in with card 0012345 | the session is checked again and the report form opens |
| d0 [No] → d1 [Yes] → d3 [Yes] | the signed-out reader with card 0012345 wrote review #88 | they select Report on #88 and sign in | no report is saved; a message says a reader cannot report their own review |
| d3 [No] → d2 [Yes] | reader 0012345 reported review #91 yesterday | they submit a report on #91 again | no second report is saved; a message says the review has already been reported |
| d2 [No] | reader 0012345 has not reported review #91 | they submit a report on #91 | one report is saved against #91 and a confirmation is shown |

## 4. Object states used

| Object | States in this diagram |
|---|---|
| Review report | Open (written by `s3`) |
| Review | Published (read; unchanged by reporting) |

## 5. Screens touched

Filled in during Lesson 8, from the Screen List.

| Reader action | Screen ID |
|---|---|
| Select Report on a review (r1) | S-F02-01 |
| Sign in now? (d1) | S-F02-01 (modal M-F00-01 "Sign in to continue?") |
| Sign in (UC-11) (c1) | S-F00-01 → S-F00-02, then back to S-F02-01 |
| Submit the report for the selected review (r2) | S-F02-01 (modal M-F02-01-02 "Report this review?") |
| See the confirmation (s4) | S-F02-01 (success state) |
| See that the review has already been reported (s2) | S-F02-01 (already-reported state) |
| See that a reader cannot report their own review (s5) | S-F02-01 (Error-3 Banner) |

## 6. Open questions

None. Decisions: see [decision-index.md](../EXTERNAL%20DESIGN/decision-index.md#ad-uc-14).

## 7. Verification log

| Check | Result | By | Date |
|---|---|---|---|
| Renders (Mermaid 12.2.0, swimlane-beta) | Pass | AI assistant | 2026-11-04 |
| Every decision has guards on all outgoing flows | Pass | AI assistant | 2026-11-04 |
| No action or decision has two incoming flows without a merge | Pass | AI assistant | 2026-11-04 |
| Every fork has a matching join | Not applicable (no fork) | AI assistant | 2026-11-04 |
| Every action cites one FR | Pass | AI assistant | 2026-11-04 |
| Every FR of UC-14 appears in the diagram | Pass (2 of 2 W1 rows whose source trace names UC-14, after the W1 trace correction) | AI assistant | 2026-11-04 |
| Lane names match the Context Diagram | Pass | AI assistant | 2026-11-04 |
| Renders (Mermaid 12.3.0, swimlane-beta, Chrome) | Pass | AI assistant | 2026-11-22 |
| v1.4 (D39): `d3`, `s5` and `stop4` added, each new action cites one FR | Pass (checked by script and by reading) | AI assistant | 2026-11-23 |
| AI critic prompt run, findings resolved or logged | Not yet run by the team | | |
