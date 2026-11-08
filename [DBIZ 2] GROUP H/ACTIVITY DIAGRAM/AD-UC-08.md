# Activity Diagram: AD-UC-08 AI-based conversational book search

| Field | Value |
|---|---|
| AD ID | AD-UC-08 |
| Use case | UC-08 AI-based conversational book search |
| Feature | F-03 Discovery, Reading History & Recommendation |
| Primary actor | Reader |
| Lanes | Reader · Library Core System (the AI Service step sits inside this lane) |
| Inputs (L3-L5) | Context Diagram (Reader flows "Chatbot questions", "Recommendations & chatbot answers"; system function "AI chatbot & recommendations") · Use Case Diagram (UC-08, includes Sign in UC-11) · Sequence: AI Service Chatbot · W0 Table 1 (login required), Table 4 (Chatbot conversations, ILF) · W1 rows FR-03-09, FR-03-10, FR-03-16, FR-03-17, FR-03-18, FR-04-08 |
| Trigger | The reader sends an inquiry message to the chatbot |
| Preconditions | The reader may not be signed in yet: the flow checks the session and prompts sign-in with a library card (FR-03-18). |
| Success end state | Each message got a reply: book result cards, or a no-results message with other search terms. The reader message and the chatbot reply are saved in that reader's conversation history (FR-03-10). |
| Failure end state | The AI Service did not answer in time or returned an error: the reader is told AI search is temporarily unavailable and advised to use the format filter (FR-03-17). Or the reader chose not to sign in. |
| FRs covered | FR-03-09, FR-03-10, FR-03-16, FR-03-17, FR-03-18, FR-04-08; FR-04-01, FR-01-01 and FR-03-12 through the calls to UC-11, UC-01 and UC-03 |
| Business rules applied | The chatbot is only for signed-in library card readers (FR-03-18). Every reader message and chatbot reply is saved per reader (FR-03-10). If the AI fails, the reader is pointed to the format filter (FR-03-17). |
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
    m0{" "}
    r1("Send an inquiry message to the chatbot (FR-03-09)")
    d1{"Sign in now?"}
    c1[["Sign in (UC-11) (FR-04-01)"]]
    d4{"What does the reader do next?"}
    c2[["View book shelf location (UC-01) (FR-01-01)"]]
    c3[["Filter books by access format (UC-03) (FR-03-12)"]]
    stop1@{ shape: fr-circ }
    stop2@{ shape: fr-circ }
    stop3@{ shape: fr-circ }
    stop4@{ shape: fr-circ }
  end
  subgraph SYS["Library Core System"]
    s0("Check the reader's session (FR-04-08)")
    d0{"Valid signed-in session?"}
    s1("Deny the request and prompt the reader<br/>to sign in with a library card (FR-03-18)")
    s2("Save the reader message to the conversation history (FR-03-10)")
    s3("Forward the message and reader context<br/>to the AI Service (FR-03-09)")
    d2{"Did the AI Service reply in time without error?"}
    s4("Display that AI search is temporarily unavailable<br/>and advise using the format filter (FR-03-17)")
    s5("Save the chatbot reply to the conversation history (FR-03-10)")
    d3{"Are there matching catalogue books?"}
    s6("Display the reply with book result cards (FR-03-09)")
    s7("Display that no results were found and suggest<br/>alternative search terms or subjects (FR-03-16)")
    m2{" "}
    a1("AI Service: find matching catalogue books<br/>and compose the reply (FR-03-09)")
  end

  start --> m0 --> r1 --> s0 --> d0
  d0 -->|"[No]"| s1 --> d1
  d1 -->|"[Yes]"| c1 --> m0
  d1 -->|"[No]"| stop1
  d0 -->|"[Yes]"| s2 --> s3 --> a1 --> d2
  d2 -->|"[No]"| s4 --> m2
  d2 -->|"[Yes]"| s5 --> d3
  d3 -->|"[Yes]"| s6 --> m2
  d3 -->|"[No]"| s7 --> m2
  m2 --> d4
  d4 -->|"[Send another message]"| m0
  d4 -->|"[Open a physical book from a result card]"| c2 --> stop3
  d4 -->|"[Use the format filter]"| c3 --> stop4
  d4 -->|"[Close the chat]"| stop2
```

Reading notes:

- The AI Service is part of the Library Core System (FR-03-09 says "the AI service in the Library
  Core System"), and the Context Diagram does not show it as an outside party. So its step `a1` sits
  in the system lane with the prefix "AI Service:". The old flowchart drew it as a box inside the
  system lane; `swimlane-beta` does not draw nested lanes.
- `m0` is the merge the reader comes back through for each new message, and after signing in.
- When the AI fails (`d2 [No]`), the reader message is already saved (`s2`) but no reply is saved.
- v1.2 turns `d4` into the reader's next choice and adds two calls: `c2` opens a physical book from
  a result card on the existing OPAC Book Detail and asks for its shelf location (UC-01, drawn in
  AD-UC-01); `c3` follows the advice of `s4` and opens the format filter (UC-03, drawn in AD-UC-03).
  They back the usage-flow arrows UC-08 to UC-01 and UC-08 to UC-03.

## 2. Node trace

| Node | Kind | Text | Traces to |
|---|---|---|---|
| r1 | Action (Reader) | Send an inquiry message to the chatbot | FR-03-09 |
| s0 | Action | Check the reader's session | FR-04-08 |
| d0 | Decision | Valid signed-in session? | FR-03-18, FR-04-08 |
| s1 | Action | Deny the request and prompt the reader to sign in with a library card | FR-03-18 |
| d1 | Decision (Reader) | Sign in now? | FR-03-18 |
| c1 | Call (Reader) | Sign in (UC-11) | FR-04-01 |
| s2 | Action | Save the reader message to the conversation history | FR-03-10 |
| s3 | Action | Forward the message and reader context to the AI Service | FR-03-09 |
| a1 | Action (AI Service, in the system) | Find matching catalogue books and compose the reply | FR-03-09 |
| d2 | Decision | Did the AI Service reply in time without error? | FR-03-17 |
| s4 | Action | Display that AI search is temporarily unavailable and advise using the format filter | FR-03-17 |
| s5 | Action | Save the chatbot reply to the conversation history | FR-03-10 |
| d3 | Decision | Are there matching catalogue books? | FR-03-16 |
| s6 | Action | Display the reply with book result cards | FR-03-09 |
| s7 | Action | Display that no results were found and suggest alternative search terms or subjects | FR-03-16 |
| d4 | Decision (Reader) | What does the reader do next? | FR-03-09, FR-01-01, FR-03-17 |
| c2 | Call (Reader) | View book shelf location (UC-01) | FR-01-01 |
| c3 | Call (Reader) | Filter books by access format (UC-03) | FR-03-12 |

## 3. Branches and acceptance tests

| Branch | Given | When | Then |
|---|---|---|---|
| d0 [No] → d1 [No] | the reader is not signed in | they send "books about supply chains" and decline to sign in | the message is not sent; a prompt to sign in with a library card is shown |
| d0 [No] → d1 [Yes] | the reader is not signed in | they sign in with card 0012345 and send the message again | the session is checked again and the message goes on |
| d0 [Yes] → d2 [No] | the AI Service does not answer within 10 seconds | the signed-in reader sends "books about supply chains" | the message is saved; a notice says AI search is temporarily unavailable and suggests the format filter |
| d2 [Yes] → d3 [Yes] | the catalogue holds 4 books on supply chains | the reader sends "books about supply chains" | message and reply are saved; the reply shows 4 book cards |
| d3 [No] | the catalogue holds no book on "underwater basket weaving" | the reader sends that inquiry | message and reply are saved; the reply says no results were found and suggests other terms or subjects |
| d4 [Send another message] | a reply is shown | the reader sends another message | the flow starts again from `r1` |
| d4 [Open a physical book from a result card] | the reply shows 4 book cards | the reader opens the card of a physical book | the book opens on the existing OPAC Book Detail and UC-01 starts (shelf location) |
| d4 [Use the format filter] | the notice says AI search is temporarily unavailable | the reader follows the advice to use the format filter | the access-format filter opens and UC-03 starts |
| d4 [Close the chat] | a reply is shown | the reader closes the chat | the activity ends; the conversation stays saved |

## 4. Object states used

| Object | States in this diagram |
|---|---|
| Chatbot message | Saved (reader message by `s2`, chatbot reply by `s5`) |

## 5. Screens touched

Filled in during Lesson 8, from the Screen List.

| Reader action | Screen ID |
|---|---|
| Send an inquiry message to the chatbot (r1), What does the reader do next? (d4) | S-F03-06 |
| View book shelf location (UC-01) (c2) | S-F03-06 → existing OPAC Book Detail → S-F01-01 |
| Filter books by access format (UC-03) (c3) | S-F03-06 → S-F03-01 |
| Sign in now? (d1) | S-F03-06 (modal M-F00-01 "Sign in to continue?", text FR-03-18) |
| Sign in (UC-11) (c1) | S-F00-01 → S-F00-02, then back to S-F03-06 |
| See the reply with book result cards (s6) | S-F03-06 |
| See that no results were found (s7) | S-F03-06 (no-results state) |
| See that AI search is temporarily unavailable (s4) | S-F03-06 (error state) |

## 6. Open questions

On 2026-11-04 the team adopted the default answer for every question below, unless the row
says otherwise.

| # | Question | Blocking? | Default applied |
|---|---|---|---|
| 1 | what is "in time" for an AI reply (FR-03-17)? | No (decided) | Decided 2026-11-04 (default adopted): 10 seconds. |
| 2 | is the "temporarily unavailable" notice saved in the conversation history? | No (decided) | Decided 2026-11-04 (default adopted): No; only the reader message is saved. |
| 3 | how long are chatbot conversations kept, and can a reader delete them? | No (decided) | Decided 2026-11-04 (default adopted): Kept for the whole release; no delete function in release 1. |

## 7. Verification log

| Check | Result | By | Date |
|---|---|---|---|
| Renders (Mermaid 12.3.0, swimlane-beta) | Pass (re-checked after the new calls); still to open once on mermaid.live | AI assistant | 2026-11-08 |
| Every decision has guards on all outgoing flows | Pass | AI assistant | 2026-11-04 |
| No action or decision has two incoming flows without a merge | Pass | AI assistant | 2026-11-04 |
| Every fork has a matching join | Not applicable (no fork) | AI assistant | 2026-11-04 |
| Every action cites one FR | Pass | AI assistant | 2026-11-04 |
| Every FR of UC-08 appears in the diagram | Pass (5 of 5 W1 rows whose source trace names UC-08) | AI assistant | 2026-11-04 |
| Lane names match the Context Diagram | Pass (AI Service step moved into the system lane) | AI assistant | 2026-11-04 |
| AI critic prompt run, findings resolved or logged | Not yet run by the team | | |
