# Activity Diagram Index: Group H Library Core System

One row per use case in the Use Case inventory (W0 Table 1). Every use case appears, even when it
needs no diagram, so a reader can see that the decision was made on purpose.

## Inputs check (Block 1: what Lesson 3 and Lesson 4 gave us)

| # | Finding | Source to fix | Action | Owner | Status |
|---|---|---|---|---|---|
| 1 | The AI Service appears as a lifeline "inside Library Core System" in the sequences AI Service Chatbot and Reader Interaction Flow, and was drawn as a box nested in the system lane in UC-08 and UC-09. It is not an outside party on the Context Diagram, and `swimlane-beta` does not draw nested lanes | Activity diagrams | AI steps drawn in the Library Core System lane with the prefix "AI Service:" (AD-UC-08, AD-UC-09) | Owner D | Done |
| 2 | The system emails the OTP (FR-04-04), but the Context Diagram has no email service: "Email OTP" goes straight to the Reader | Context Diagram | Decided 2026-11-04: no outside email service; the Context Diagram and AD-UC-11 stay as they are | Owner A | Done |
| 3 | Processes started by time have no use case of their own: daily sync of catalogue, shelf placement, floors and rooms (FR-04-09), loan records (FR-04-10), sync failures (FR-04-11), room-code check (FR-01-05). The Library Internal System is used as a lane only by UC-11. Two timed steps are drawn inside other use cases as time events: QR generation (FR-02-07) in AD-UC-10 and history entries from loans (FR-03-03) in AD-UC-07 | Use Case Diagram | Decided 2026-11-04: QR generation stays in AD-UC-10 and loan history entries stay in AD-UC-07. Still to do: add a use case "Sync data from the library internal system" (started by time) for FR-04-09, FR-04-10, FR-04-11 and FR-01-05, and draw its activity diagram | Integrator | Open (sync use case) |
| 4 | Several sequence diagrams tell two use cases: User Interface Flow (UC-01 + UC-02), User Review Interaction Flow (UC-05 + UC-04), Book Review API Interaction (UC-06 + UC-04), Reader Interaction Flow (UC-07 + UC-09), User Review Reporting Flow (UC-14 + UC-13) | Sequence Diagrams | Split into one sequence per use case | Owners A, C, D | Open |
| 5 | `opt` / `alt` used for a reader's choice: map link (User Interface Flow), edit or delete own review (User Review Interaction Flow), view history or set preferences (Reader Interaction Flow) | Sequence Diagrams | The choices are now decisions in AD-UC-02, AD-UC-04 and AD-UC-07; in the sequences keep `alt` only for interaction conditions such as an API error | Owners A, C, D | Open |
| 6 | W1 source traces that name the wrong use case: FR-04-05 and FR-04-06 → UC-13 (old account-linking use case, Won't); FR-02-10 → UC-14 (removal is done by staff in UC-13) | W1 | AD-UC-13 and AD-UC-14 leave these rows out and say why (v1.1). W1 corrected on 2026-11-04: FR-04-05 and FR-04-06 now trace to UC-11 (online part, cut in W4; W0 Table 3), FR-02-10 traces to UC-13 only | Integrator | Done |
| 7 | The sequence User Review Reporting Flow cites FR-02-10 for opening the reported-reviews list; W1 has FR-02-14 for that step | Sequence Diagrams | Change the step to FR-02-14 | Owner C | Open |
| 8 | FRs missing from their diagrams: FR-03-02 and FR-03-13 (UC-03) and FR-03-02 and FR-03-03 (UC-07). FR-03-02 and FR-03-13 need an online book to be opened "from this platform", but the viewer and download were cut (FR-03-14, FR-03-15 Won't) | Activity diagrams; client | Drawn in v1.1: AD-UC-03 adds "Open an online book from the results" with the anonymous read log and the history entry; AD-UC-07 adds a time event (loan sync, FR-03-03) and an accept event (online book opened, FR-03-02). Both rest on online books in the results linking to the current OPAC, with the click recorded; the team confirmed on 2026-11-04 that the current OPAC opens and downloads online books (AD-UC-03 open question 1) | Owner D | Done |

## Use cases

Rule used in this course: draw an activity diagram for every **Must** use case that has at least
one decision, more than one lane, or a time trigger. A use case that is a single display step gets
"not needed" and a one-line reason. A use case has at most one diagram, and one diagram never
covers two use cases.

All 14 use cases have at least one decision and two lanes, so all have a diagram, including the
Should and Could ones (drawn now rather than marked "later").

Priority: W0 Table 1 has no priority column, so the column below shows the effective priority (W4)
of the use case's main FR.

Business rules: the workbook has no separate business-rule IDs (BR-xx). Each AD file names the rule
in words and cites the FR that states it.

| Use case | Name | Feature | Priority | Activity diagram | Status | Reason if not needed |
|---|---|---|---|---|---|---|
| UC-01 | View book shelf location | F-01 | Must (FR-01-01) | `AD-UC-01.md` | Draft | |
| UC-02 | Browse interactive digital library map | F-01 | Must (FR-01-02) | `AD-UC-02.md` | Draft | |
| UC-03 | Filter books by access format (online, physical or both) | F-03 | Should (FR-03-12) | `AD-UC-03.md` | Draft | |
| UC-04 | Write, edit and delete own book reviews | F-02 | Must (FR-02-01) | `AD-UC-04.md` | Draft | |
| UC-05 | View book reviews | F-02 | Must (FR-02-02) | `AD-UC-05.md` | Draft | |
| UC-06 | Access book information and reviews via QR code | F-02 | Must (FR-02-05) | `AD-UC-06.md` | Draft | |
| UC-07 | Update and view personal reading history and preferences | F-03 | Should (FR-03-01) | `AD-UC-07.md` | Draft | |
| UC-08 | AI-based conversational book search | F-03 | Could (FR-03-09) | `AD-UC-08.md` | Draft | |
| UC-09 | Automatic personalised book recommendations | F-03 | Could (FR-03-11) | `AD-UC-09.md` | Draft | |
| UC-10 | Print QR code labels for physical books (QR codes are generated automatically) | F-02 | Must (FR-02-08) | `AD-UC-10.md` | Draft | |
| UC-11 | Register and sign in (library card with email OTP) | F-04 | Must (FR-04-01) | `AD-UC-11.md` | Draft | |
| UC-12 | Save physical books to a personal list, and remove them | F-03 | Should (FR-03-06) | `AD-UC-12.md` | Draft | |
| UC-13 | Remove reviews that violate rules | F-02 | Could (FR-02-10) | `AD-UC-13.md` | Draft | |
| UC-14 | Report a review that violates rules | F-02 | Could (FR-02-09) | `AD-UC-14.md` | Draft | |

All open questions in the AD files were decided on 2026-11-04 by adopting their defaults; only the
work items in the Inputs check above stay open.

Object state lists collected from all diagrams (copy into the data model in DBIZ3):

| Object | States |
|---|---|
| Review | Published, Removed |
| Review report | Open, Dismissed, Upheld |
| OTP | Active, Used, Expired, Invalidated |
| Reader session | Signed-in |
| Reading history entry | Reading, Finished (automatic entries start as Reading, 0 percent) |
| Online book read log entry | Recorded |
| Saved book entry | Saved |
| QR code | Generated |
| Chatbot message | Saved |

## Exit ticket (one per team)

To be filled in by the team after the peer review.

1. Which use case surprised you most when you drew it, and why?
2. One FR you added, changed or questioned because of a diagram.
3. One open question you will take to your client.
