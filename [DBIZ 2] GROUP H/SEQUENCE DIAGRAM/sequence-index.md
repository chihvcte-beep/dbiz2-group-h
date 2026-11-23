# Sequence Diagram Index: Group H Library Core System

One sequence diagram per use case, 15 in total. Each file pairs with the activity diagram of the same
number: `SD-UC-xx.md` and `AD-UC-xx.md`.

| Field | Value |
|---|---|
| Version | v2.3 · 23/11/2026 |
| Sources | The 10 original diagrams of 12/10/2026 · `GROUP-H_UC_FR_COST.xlsx` W0, W1 · AD-UC-01 … AD-UC-14 · `EXTERNAL DESIGN/decision-index.md` |
| Status | Draft, waiting for group review |

## Diagrams

| Sequence diagram | Use case | Name | Redrawn from | Messages | FRs |
|---|---|---|---|---|---|
| [SD-UC-01](SD-UC-01.md) | UC-01 | View book shelf location | `User Interface Flow-2026-10-12-031728.png` | 19 | 6 |
| [SD-UC-02](SD-UC-02.md) | UC-02 | Browse interactive digital library map | `User Interface Flow-2026-10-12-031728.png` | 22 | 6 |
| [SD-UC-03](SD-UC-03.md) | UC-03 | Filter books by access format (online, physical or both) | `User Interface Flow-2026-10-12-032159.png` | 22 | 4 |
| [SD-UC-04](SD-UC-04.md) | UC-04 | Write, edit and delete own book reviews | `User Review Interaction Flow-2026-10-12-032334.png` · `Book Review API Interaction-2026-10-12-032039.png` | 42 | 7 |
| [SD-UC-05](SD-UC-05.md) | UC-05 | View book reviews | `User Review Interaction Flow-2026-10-12-032334.png` | 18 | 3 |
| [SD-UC-06](SD-UC-06.md) | UC-06 | Access book information and reviews via QR code (physical books; reviews via UC-04) | `Book Review API Interaction-2026-10-12-032039.png` | 19 | 5 |
| [SD-UC-07](SD-UC-07.md) | UC-07 | Update and view personal reading history and preferences | `Reader Interaction Flow-2026-10-12-031246.png` | 30 | 7 |
| [SD-UC-08](SD-UC-08.md) | UC-08 | AI-based conversational book search | `AI Service Chatbot-2026-10-12-032513.png` | 18 | 6 |
| [SD-UC-09](SD-UC-09.md) | UC-09 | Automatic personalised book recommendations | `Reader Interaction Flow-2026-10-12-031246.png` | 20 | 5 |
| [SD-UC-10](SD-UC-10.md) | UC-10 | Print QR code labels for physical books (QR codes are generated automatically) | `QR Code Label Printing-2026-10-12-033525.png` | 80 | 11 |
| [SD-UC-11](SD-UC-11.md) | UC-11 | Register and sign in (library card with email OTP) | `Library Sign-In OTP Pipeline-2026-10-12-035036.pdf` | 30 | 6 |
| [SD-UC-12](SD-UC-12.md) | UC-12 | Save physical books to a personal list for finding them later in the library, and remove them from the list | `Reader API Saved List-2026-10-12-033031.png` | 29 | 7 |
| [SD-UC-13](SD-UC-13.md) | UC-13 | Remove reviews that violate rules | `User Review Reporting Flow-2026-10-12-035252.pdf` | 41 | 9 |
| [SD-UC-14](SD-UC-14.md) | UC-14 | Report a review that violates rules | `User Review Reporting Flow-2026-10-12-035252.pdf` | 21 | 4 |
| [SD-UC-15](SD-UC-15.md) | UC-15 | Sync data from the library internal system | New on 23/11/2026 (D48) | 10 | 5 |

## Original files and their new diagrams

The original images and PDFs, and the one-page copy `SEQUENCE DIAGRAM.pdf` from the parent folder, were
removed on 23/11/2026. They remain in Git history at commit `4e55347`.

| Original file | New diagram(s) |
|---|---|
| `AI Service Chatbot-2026-10-12-032513.png` | SD-UC-08 |
| `Book Review API Interaction-2026-10-12-032039.png` | SD-UC-04, SD-UC-06 |
| `Library Sign-In OTP Pipeline-2026-10-12-035036.pdf` | SD-UC-11 |
| `QR Code Label Printing-2026-10-12-033525.png` | SD-UC-10 |
| `Reader API Saved List-2026-10-12-033031.png` | SD-UC-12 |
| `Reader Interaction Flow-2026-10-12-031246.png` | SD-UC-07, SD-UC-09 |
| `SEQUENCE DIAGRAM.pdf` (one-page copy of Reader Interaction Flow) | SD-UC-07, SD-UC-09 |
| `User Interface Flow-2026-10-12-031728.png` | SD-UC-01, SD-UC-02 |
| `User Interface Flow-2026-10-12-032159.png` | SD-UC-03 |
| `User Review Interaction Flow-2026-10-12-032334.png` | SD-UC-04, SD-UC-05 |
| `User Review Reporting Flow-2026-10-12-035252.pdf` | SD-UC-13, SD-UC-14 |

## Drawing rules

- **File name:** `SD-UC-xx.md`, where `xx` is the use case number. One use case has one diagram (Inputs check 4).
- **Participant names:** Reader, On-site Staff, Web App, Backend, AI Service, Reader database, Book database and
  Library Internal System, spelled the same in every file.
- **Message label:** the text, then exactly one FR at the end, for example `Save the review (FR-02-01)`.
- **`alt` / `opt`:** only for system or interaction conditions (Inputs check 5).
- **Blue section:** a choice of the actor, which is a decision in the activity diagram of the same number.
- **Grey section:** a flow started automatically, by a daily sync or by another use case.
- **`ref` note:** a call to another use case, drawn once in that use case's own file. The sign-in step is
  "Sign in (UC-11)".
- **FR-04-20 (network or loading error):** applies to every call between Web App and Backend, so it is stated here
  and not repeated in each diagram.
- **Staff session ended elsewhere (D36):** applies to every staff request: it changes nothing and the staff sign-in
  opens. It is stated here and not repeated in each diagram.
- **FR-02-23, FR-04-21 and the new FR-02-08 text:** decided on 22/11/2026 and added to W1 on 23/11/2026.

## Verification log

| Check | Result | Date |
|---|---|---|
| All 14 diagrams render (Mermaid 12.3.0, Chrome) | Pass | 2026-11-23 |
| Every message carries exactly one FR, at the end of its label | Pass | 2026-11-23 |
| Every FR cited exists in W1 | Pass | 2026-11-23 |
| Every FR a use case owns in its activity diagram appears in its sequence diagram | Pass | 2026-11-23 |
| v2.1: SD-UC-03, 04, 05, 06, 08, 10, 11, 12 match the activity diagrams of 23/11/2026; all 14 render (Mermaid 12.3.0, Chrome) and every message carries one FR | Pass | 2026-11-23 |
| v2.2: SD-UC-10 and SD-UC-14 match AD-UC-10 v1.7 and AD-UC-14 v1.4 (D39, D40, D41); every message carries one FR (script); all 14 render (Mermaid 12.3.0, Chrome) | Pass | 2026-11-23 |
| v2.3: SD-UC-01, 08, 09, 10, 11, 12, 13 updated and SD-UC-15 added (D42, D48, L8-21); counts measured by script; all 15 render (Mermaid 12.3.0, Chrome) | Pass | 2026-11-23 |
| Group review | Not yet done | |
