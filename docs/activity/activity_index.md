# Activity Diagram Index: Group H Library Core System

One row per use case in the Use Case inventory (W0 Table 1). Every use case appears, even when it
needs no diagram, so a reader can see that the decision was made on purpose.

## Inputs check (Block 1: what Lesson 3 and Lesson 4 gave us)

None. Decisions: see [decision_index.md](../project/decision_index.md#activity-index).

## Use cases

Rule used in this course: draw an activity diagram for every **Must** use case that has at least
one decision, more than one lane, or a time trigger. A use case that is a single display step gets
"not needed" and a one-line reason. A use case has at most one diagram, and one diagram never
covers two use cases.

All 15 use cases have at least one decision and two lanes, so all have a diagram, including the
Should and Could ones (drawn now rather than marked "later").

Priority: W0 Table 1 has no priority column, so the column below shows the effective priority (W4)
of the use case's main FR.

Business rules: the workbook has no separate business-rule IDs (BR-xx). Each AD file names the rule
in words and cites the FR that states it.

| Use case | Name | Feature | Priority | Activity diagram | Status | Reason if not needed |
|---|---|---|---|---|---|---|
| UC-01 | View book shelf location | F-01 | Must (FR-01-01) | [ad_uc_01.md](ad_uc_01.md) | Draft | |
| UC-02 | Browse interactive digital library map | F-01 | Must (FR-01-02) | [ad_uc_02.md](ad_uc_02.md) | Draft | |
| UC-03 | Filter books by access format (online, physical or both) | F-03 | Should (FR-03-12) | [ad_uc_03.md](ad_uc_03.md) | Draft | |
| UC-04 | Write, edit and delete own book reviews | F-02 | Must (FR-02-01) | [ad_uc_04.md](ad_uc_04.md) | Draft | |
| UC-05 | View book reviews | F-02 | Must (FR-02-02) | [ad_uc_05.md](ad_uc_05.md) | Draft | |
| UC-06 | Access book information and reviews via QR code | F-02 | Must (FR-02-05) | [ad_uc_06.md](ad_uc_06.md) | Draft | |
| UC-07 | Update and view personal reading history and preferences | F-03 | Should (FR-03-01) | [ad_uc_07.md](ad_uc_07.md) | Draft | |
| UC-08 | AI-based conversational book search | F-03 | Could (FR-03-09) | [ad_uc_08.md](ad_uc_08.md) | Draft | |
| UC-09 | Automatic personalised book recommendations | F-03 | Could (FR-03-11) | [ad_uc_09.md](ad_uc_09.md) | Draft | |
| UC-10 | Print QR code labels for physical books (QR codes are generated automatically) | F-02 | Must (FR-02-08) | [ad_uc_10.md](ad_uc_10.md) | Draft | |
| UC-11 | Register and sign in (library card with email OTP) | F-04 | Must (FR-04-01) | [ad_uc_11.md](ad_uc_11.md) | Draft | |
| UC-12 | Save physical books to a personal list, and remove them | F-03 | Should (FR-03-06) | [ad_uc_12.md](ad_uc_12.md) | Draft | |
| UC-13 | Remove reviews that violate rules | F-02 | Could (FR-02-10) | [ad_uc_13.md](ad_uc_13.md) | Draft | |
| UC-14 | Report a review that violates rules | F-02 | Could (FR-02-09) | [ad_uc_14.md](ad_uc_14.md) | Draft | |
| UC-15 | Sync data from the library internal system (started by time, D48) | F-04 | Must (FR-04-09) | [ad_uc_15.md](ad_uc_15.md) | Draft | |

Decisions on the open questions of the AD files and on the Lesson 8 questions (L8-01 … L8-22): see
[decision_index.md](../project/decision_index.md#activity-index).

Object state lists collected from all diagrams (copy into the data model in DBIZ3):

| Object | States |
|---|---|
| Review | Published, Removed |
| Review report | Open, Dismissed, Upheld |
| OTP | Active, Used, Expired, Invalidated |
| Reader session | Signed-in |
| Staff session | Signed-in, Ended (only by «Đăng xuất»; no time-out) |
| Reading history entry | Reading, Finished (automatic entries start as Reading, 0 percent) |
| Online book read log entry | Recorded |
| Saved book entry | Saved |
| QR code | Generated, Label printed |
| Chatbot message | Saved |

## Exit ticket (one per team)

1. Which use case surprised you most when you drew it, and why?
2. One FR you added, changed or questioned because of a diagram.
3. One open question you will take to your client.
