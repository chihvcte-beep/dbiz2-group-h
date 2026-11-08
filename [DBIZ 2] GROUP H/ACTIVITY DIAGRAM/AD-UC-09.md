# Activity Diagram: AD-UC-09 Automatic personalised book recommendations

| Field | Value |
|---|---|
| AD ID | AD-UC-09 |
| Use case | UC-09 Automatic personalised book recommendations |
| Feature | F-03 Discovery, Reading History & Recommendation |
| Primary actor | Reader |
| Lanes | Reader · Library Core System (the AI Service step sits inside this lane) |
| Inputs (L3-L5) | Context Diagram (Reader flow "Recommendations & chatbot answers"; system function "AI chatbot & recommendations") · Use Case Diagram (UC-09, includes Sign in UC-11) · Sequence: Reader Interaction Flow (UC-07 with UC-09) · W0 Table 1 (login required), Table 4 (Reading history & preferences, Chatbot conversations, Book QR codes) · W1 rows FR-03-11, FR-03-19, FR-03-20, FR-03-21, FR-04-08 |
| Trigger | The reader opens the recommendations section |
| Preconditions | The reader may not be signed in yet: the flow checks the session and shows a sign-in prompt (FR-03-21). |
| Success end state | The reader sees a list of recommended books: personalised, topped up with trending books when short, or popular books when there is no reader data. |
| Failure end state | The reader is not signed in and chooses not to sign in: no recommendations are shown. |
| FRs covered | FR-03-11, FR-03-19, FR-03-20, FR-03-21, FR-04-08; FR-04-01, FR-01-01 and FR-03-05 through the calls to UC-11, UC-01 and UC-07 |
| Business rules applied | Personalised recommendations need a library card account (FR-03-21). With no reading history, preferences or chatbot conversations, popular books by QR scan count are shown and the reader is asked to set preferences (FR-03-19). Fewer than three matching titles are topped up with trending books of the same subjects (FR-03-20). |
| Version / status | v1.2 · Draft |
| Author | Owner D (F-03) |

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
    r1("Open the recommendations section (FR-03-11)")
    d1{"Sign in now?"}
    c1[["Sign in (UC-11) (FR-04-01)"]]
    r2("View the recommended books (FR-03-11)")
    d4{"What does the reader do next?"}
    c2[["View book shelf location (UC-01) (FR-01-01)"]]
    c3[["Update reading preferences (UC-07) (FR-03-05)"]]
    stop1@{ shape: fr-circ }
    stop2@{ shape: fr-circ }
    stop3@{ shape: fr-circ }
  end
  subgraph SYS["Library Core System"]
    m0{" "}
    s0("Check the reader's session (FR-04-08)")
    d0{"Valid signed-in session?"}
    s1("Display a sign-in prompt: personalised recommendations<br/>require a library card account (FR-03-21)")
    s2("Retrieve the reader's Reading history & preferences<br/>and chatbot conversations (FR-03-11)")
    d2{"Any reading history, preferences<br/>or chatbot conversations?"}
    s3("Select popular books by QR scan count and<br/>prompt the reader to set reading preferences (FR-03-19)")
    d3{"At least three matching titles?"}
    s4("Add trending books from the same subject categories (FR-03-20)")
    m1{" "}
    s5("Display the recommended book list (FR-03-11)")
    a1("AI Service: compute recommendation scores (FR-03-11)")
  end

  start --> r1 --> m0 --> s0 --> d0
  d0 -->|"[No]"| s1 --> d1
  d1 -->|"[Yes]"| c1 --> m0
  d1 -->|"[No]"| stop1
  d0 -->|"[Yes]"| s2 --> d2
  d2 -->|"[No]"| s3 --> m1
  d2 -->|"[Yes]"| a1 --> d3
  d3 -->|"[Yes]"| m1
  d3 -->|"[No]"| s4 --> m1
  m1 --> s5 --> r2 --> d4
  d4 -->|"[Open a physical book]"| c2 --> stop3
  d4 -->|"[Set reading preferences]"| c3 --> m0
  d4 -->|"[Finish]"| stop2
```

Reading notes:

- The AI Service is part of the Library Core System, so its step `a1` sits in the system lane with
  the prefix "AI Service:" (same reason as AD-UC-08).
- `m1` gathers the three ways of building the list (popular fallback, enough titles, topped-up list)
  before the one display action `s5`.
- v1.2 adds the reader's next choice `d4` with two calls: `c2` opens a recommended physical book
  on the existing OPAC Book Detail and asks for its shelf location (UC-01, drawn in AD-UC-01); `c3`
  follows the prompt of `s3` (or the reader's own wish) to set reading preferences (UC-07, drawn in
  AD-UC-07). After `c3` the flow re-enters through the merge `m0`, so the list is built again with
  the new preferences. They back the usage-flow arrows UC-09 to UC-01, UC-09 to UC-07 and UC-07 to
  UC-09.

## 2. Node trace

| Node | Kind | Text | Traces to |
|---|---|---|---|
| r1 | Action (Reader) | Open the recommendations section | FR-03-11 |
| s0 | Action | Check the reader's session | FR-04-08 |
| d0 | Decision | Valid signed-in session? | FR-03-21, FR-04-08 |
| s1 | Action | Display a sign-in prompt: personalised recommendations require a library card account | FR-03-21 |
| d1 | Decision (Reader) | Sign in now? | FR-03-21 |
| c1 | Call (Reader) | Sign in (UC-11) | FR-04-01 |
| s2 | Action | Retrieve the reader's Reading history & preferences and chatbot conversations | FR-03-11 |
| d2 | Decision | Any reading history, preferences or chatbot conversations? | FR-03-19 |
| s3 | Action | Select popular books by QR scan count and prompt the reader to set reading preferences | FR-03-19 |
| a1 | Action (AI Service, in the system) | Compute recommendation scores | FR-03-11 |
| d3 | Decision | At least three matching titles? | FR-03-20 |
| s4 | Action | Add trending books from the same subject categories | FR-03-20 |
| s5 | Action | Display the recommended book list | FR-03-11 |
| r2 | Action (Reader) | View the recommended books | FR-03-11 |
| d4 | Decision (Reader) | What does the reader do next? | FR-03-11, FR-01-01, FR-03-19 |
| c2 | Call (Reader) | View book shelf location (UC-01) | FR-01-01 |
| c3 | Call (Reader) | Update reading preferences (UC-07) | FR-03-05 |

## 3. Branches and acceptance tests

| Branch | Given | When | Then |
|---|---|---|---|
| d0 [No] → d1 [No] | the visitor is not signed in | they open recommendations and decline to sign in | a prompt says personalised recommendations need a library card account; no list is shown |
| d0 [No] → d1 [Yes] | the visitor is not signed in | they sign in with card 0012345 | the session is checked again and the flow goes on |
| d0 [Yes] → d2 [No] | a new signed-in reader has no history, no preferences and no chatbot messages | they open recommendations | the books with the highest QR scan counts are shown with a prompt to set reading preferences |
| d2 [Yes] → d3 [Yes] | the reader's history and preferences give 8 matching titles | they open recommendations | 8 personalised titles are shown |
| d3 [No] | the reader's data gives only 2 matching titles, both in Economics | they open recommendations | the 2 titles are shown, topped up with the most borrowed Economics books of the last 30 days |
| d4 [Open a physical book] | the recommended list is shown | the reader opens a recommended physical book | the book opens on the existing OPAC Book Detail and UC-01 starts (shelf location) |
| d4 [Set reading preferences] | a new reader sees popular books and the prompt to set preferences | they set "Economics" as a preference and come back | the session is checked again and the list is rebuilt with Economics titles |
| d4 [Finish] | the recommended list is shown | the reader leaves the section | the activity ends |

## 4. Object states used

| Object | States in this diagram | Note |
|---|---|---|
| Reading history entry | Reading, Finished (read) | |
| Chatbot message | Saved (read) | |
| QR code | Generated (read) | scan counts read by `s3` |

## 5. Screens touched

Filled in during Lesson 8, from the Screen List.

| Reader action | Screen ID |
|---|---|
| Open the recommendations section (r1) | S-F03-07 (from a link on the existing OPAC main menu) |
| Sign in now? (d1) | S-F03-07 (modal M-F00-01 "Sign in to continue?", text FR-03-21) |
| Sign in (UC-11) (c1) | S-F00-01 → S-F00-02, then back to S-F03-07 |
| View the recommended books (r2), What does the reader do next? (d4) | S-F03-07 |
| View book shelf location (UC-01) (c2) | S-F03-07 → existing OPAC Book Detail → S-F01-01 |
| Update reading preferences (UC-07) (c3) | S-F03-07 → S-F03-02, then back to S-F03-07 |
| See popular books and the prompt to set reading preferences (s3) | S-F03-07 (no-history state) |

## 6. Open questions

On 2026-11-04 the team adopted the default answer for every question below, unless the row
says otherwise.

| # | Question | Blocking? | Default applied |
|---|---|---|---|
| 1 | FR-03-19 ranks popular books by QR scan count, but counting scans (FR-02-06) was moved to Could. If it is cut, what decides "popular"? | No (decided) | Decided 2026-11-04 (default adopted): The number of loans in the synced loan records (FR-04-10). |
| 2 | what counts as "trending" in FR-03-20? | No (decided) | Decided 2026-11-04 (default adopted): The most borrowed books of the same subject in the last 30 days. |
| 3 | how many books does the list show? | No (decided) | Decided 2026-11-04 (default adopted): 10. |

## 7. Verification log

| Check | Result | By | Date |
|---|---|---|---|
| Renders (Mermaid 12.3.0, swimlane-beta) | Pass (re-checked after the new calls); still to open once on mermaid.live | AI assistant | 2026-11-08 |
| Every decision has guards on all outgoing flows | Pass | AI assistant | 2026-11-04 |
| No action or decision has two incoming flows without a merge | Pass | AI assistant | 2026-11-04 |
| Every fork has a matching join | Not applicable (no fork) | AI assistant | 2026-11-04 |
| Every action cites one FR | Pass | AI assistant | 2026-11-04 |
| Every FR of UC-09 appears in the diagram | Pass (4 of 4 W1 rows whose source trace names UC-09) | AI assistant | 2026-11-04 |
| Lane names match the Context Diagram | Pass (AI Service step moved into the system lane) | AI assistant | 2026-11-04 |
| AI critic prompt run, findings resolved or logged | Not yet run by the team | | |
