# Activity Diagram: AD-UC-11 Register and sign in (library card with email OTP)

| Field | Value |
|---|---|
| AD ID | AD-UC-11 |
| Use case | UC-11 Register and sign in (library card with email OTP) |
| Feature | F-04 Platform, Access & Operations |
| Primary actor | Reader |
| Lanes | Reader · Library Core System · Library Internal System |
| Inputs (L3-L5) | Context Diagram (Reader flows "Library card info", "OTP code", "Email OTP"; Library Internal System flow "Reader accounts") · Use Case Diagram (UC-11, included by UC-04, UC-07, UC-08, UC-09, UC-12, UC-14) · Sequence: Library Sign-In OTP Pipeline · W0 Table 3 (online accounts and Google sign-in cut), Table 4 (Reader accounts, EIF) · W1 rows FR-04-01, FR-04-04, FR-04-12, FR-04-16, FR-04-17 |
| Trigger | The reader submits their library card number, directly or from the "Sign in (UC-11)" step of another use case |
| Preconditions | The reader holds a library card whose record in the Library Internal System has an email address. |
| Success end state | A signed-in session has started for the reader, and an audit entry with actor, action and time is written. |
| Failure end state | No session: the card number is not found; or the OTP is expired or already used; or 5 incorrect attempts were made; or the OTP email could not be sent; and the reader does not ask for a new OTP. |
| FRs covered | FR-04-01, FR-04-04, FR-04-12, FR-04-16, FR-04-17 |
| Business rules applied | An OTP expires after 5 minutes and works only once (FR-04-04). A new OTP cancels the previous one (FR-04-04). After 5 incorrect attempts the OTP is cancelled (FR-04-17). Every sign-in writes an audit entry (FR-04-01, FR-04-12). Reader accounts are read, never written (W0 Table 4). |
| Version / status | v1.3 · Draft |
| Author | Owner A (F-04) |

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
    r1("Submit the library card number (FR-04-01)")
    m2{" "}
    r2("Submit the OTP received by email (FR-04-01)")
    d5{"Request a new OTP?"}
    r3("Request a new OTP (FR-04-04)")
    stop3@{ shape: fr-circ }
  end
  subgraph SYS["Library Core System"]
    s1("Request the reader account for the card number (FR-04-01)")
    d1{"Is the card number found?"}
    s2("Reject the sign-in and display an error message (FR-04-01)")
    m1{" "}
    s3("Generate an OTP that expires after 5 minutes<br/>and can be used only once (FR-04-04)")
    s4("Email the OTP to the email declared on the card (FR-04-04)")
    d2{"Was the OTP email sent?"}
    s5("Display that the code could not be sent (FR-04-16)")
    s6("Verify the submitted OTP (FR-04-04)")
    d3{"What is the OTP result?"}
    s7("Start a signed-in session for the reader (FR-04-01)")
    s8("Write an audit entry with actor, action and time (FR-04-12)")
    d4{"Fewer than 5 incorrect attempts for this OTP?"}
    s9("Display that the code is incorrect<br/>and let the reader enter it again (FR-04-17)")
    s10("Invalidate the OTP and reject the sign-in (FR-04-17)")
    s11("Reject the sign-in and display an error message (FR-04-01)")
    m3{" "}
    s12("Invalidate the previous OTP (FR-04-04)")
    stop1@{ shape: fr-circ }
    stop2@{ shape: fr-circ }
  end
  subgraph INT["Library Internal System"]
    i1("Return the reader account for the card number (FR-04-01)")
  end

  start --> r1 --> s1 --> i1 --> d1
  d1 -->|"[No]"| s2 --> stop1
  d1 -->|"[Yes]"| m1 --> s3 --> s4 --> d2
  d2 -->|"[No]"| s5 --> m3
  d2 -->|"[Yes]"| m2 --> r2 --> s6 --> d3
  d3 -->|"[Correct, not expired, not used]"| s7 --> s8 --> stop2
  d3 -->|"[Incorrect]"| d4
  d4 -->|"[Yes]"| s9 --> m2
  d4 -->|"[No]"| s10 --> m3
  d3 -->|"[Expired or already used]"| s11 --> m3
  m3 --> d5
  d5 -->|"[Yes]"| r3 --> s12 --> m1
  d5 -->|"[No]"| stop3
```

Reading notes:

- The Library Internal System lane only returns the reader account; the platform never writes to
  it (W0 Table 4).
- Three merges keep the loops legal: `m1` re-enters OTP generation after a new OTP is requested,
  `m2` re-enters OTP entry after a wrong code, and `m3` gathers every outcome after which the reader
  may ask for a new OTP.
- "Register" stays in the use case name, but no registration step is left: online accounts
  (FR-04-02, FR-04-03) are Won't, and library card accounts already exist in the Library Internal
  System. See open question 1.

## 2. Node trace

| Node | Kind | Text | Traces to |
|---|---|---|---|
| r1 | Action (Reader) | Submit the library card number | FR-04-01 |
| s1 | Action | Request the reader account for the card number | FR-04-01 |
| i1 | Action (Library Internal System) | Return the reader account for the card number | FR-04-01 |
| d1 | Decision | Is the card number found? | FR-04-01 |
| s2 | Action | Reject the sign-in and display an error message | FR-04-01 |
| s3 | Action | Generate an OTP that expires after 5 minutes and can be used only once | FR-04-04 |
| s4 | Action | Email the OTP to the email declared on the card | FR-04-04 |
| d2 | Decision | Was the OTP email sent? | FR-04-16 |
| s5 | Action | Display that the code could not be sent | FR-04-16 |
| r2 | Action (Reader) | Submit the OTP received by email | FR-04-01 |
| s6 | Action | Verify the submitted OTP | FR-04-04 |
| d3 | Decision | What is the OTP result? | FR-04-01, FR-04-04, FR-04-17 |
| s7 | Action | Start a signed-in session for the reader | FR-04-01 |
| s8 | Action | Write an audit entry with actor, action and time | FR-04-12 |
| d4 | Decision | Fewer than 5 incorrect attempts for this OTP? | FR-04-17 |
| s9 | Action | Display that the code is incorrect and let the reader enter it again | FR-04-17 |
| s10 | Action | Invalidate the OTP and reject the sign-in | FR-04-17 |
| s11 | Action | Reject the sign-in and display an error message | FR-04-01 |
| d5 | Decision (Reader) | Request a new OTP? | FR-04-04, FR-04-16 |
| r3 | Action (Reader) | Request a new OTP | FR-04-04 |
| s12 | Action | Invalidate the previous OTP | FR-04-04 |

## 3. Branches and acceptance tests

| Branch | Given | When | Then |
|---|---|---|---|
| d1 [No] | card number 9999999 is not in the Library Internal System | the reader submits it | the sign-in is rejected with an error message; no OTP is sent |
| d1 [Yes] → d2 [No] | card 0012345 exists but its email server refuses the message | the reader submits 0012345 | a message says the code could not be sent and offers a new OTP |
| d2 [Yes] → d3 [Correct, not expired, not used] | an OTP 482913 was sent 2 minutes ago | the reader submits 482913 | a signed-in session starts and an audit entry "reader 0012345, sign-in, time" is written |
| d3 [Incorrect] → d4 [Yes] | the reader has made 1 incorrect attempt | they submit 111111 | a message says the code is incorrect and the reader can enter it again |
| d4 [No] | the reader has made 4 incorrect attempts | they submit a fifth incorrect code | the OTP is cancelled and the sign-in is rejected |
| d3 [Expired or already used] | OTP 482913 was sent 6 minutes ago | the reader submits 482913 | the sign-in is rejected with an error message |
| d5 [Yes] | the sign-in was rejected because the OTP expired | the reader asks for a new OTP | the old OTP is cancelled and a new one is generated and emailed |
| d5 [No] | the sign-in was rejected | the reader does not ask for a new OTP | the activity ends without a session |

## 4. Object states used

| Object | States in this diagram |
|---|---|
| OTP | Active (written by `s3`), Used (by `s7`), Expired (read by `d3`), Invalidated (by `s10`, `s12`) |
| Reader session | Signed-in (written by `s7`) |
| Audit entry | written by `s8` |

## 5. Screens touched

Filled in from the Screen List (Lesson 8).

| Reader action | Screen ID |
|---|---|
| Submit the library card number | S-F00-01 |
| Submit the OTP received by email, Request a new OTP | S-F00-02 |

## 6. Open questions

On 2026-11-04 the team adopted the default answer for every question below, unless the row
says otherwise.

| # | Question | Blocking? | Default applied |
|---|---|---|---|
| 1 | "Register" is in the use case name, but online registration and account linking (FR-04-02, FR-04-03, FR-04-05, FR-04-06) are Won't. Rename UC-11 to "Sign in with library card and email OTP"? | No (decided) | Decided 2026-11-04 (default adopted): The name "Register and sign in (library card with email OTP)" is kept. |
| 2 | who sends the OTP email? The Context Diagram shows "Email OTP" going straight to the Reader and has no email service. | No (decided) | Decided 2026-11-04 (default adopted): No outside email service and no separate lane; the Context Diagram stays as it is. |
| 3 | is there a limit on how many new OTPs a reader may request? | No (decided) | Decided 2026-11-04 (default adopted): No limit in release 1; the 5-attempt rule applies to each OTP. |
| 4 | should the "card not found" message avoid saying whether a card number exists? | No (decided) | Decided 2026-11-04 (default adopted): Yes, one general message for every rejection. |

## 7. Verification log

| Check | Result | By | Date |
|---|---|---|---|
| Renders (Mermaid 12.2.0, swimlane-beta) | Pass; still to open once on mermaid.live | AI assistant | 2026-11-04 |
| Every decision has guards on all outgoing flows | Pass | AI assistant | 2026-11-04 |
| No action or decision has two incoming flows without a merge | Pass | AI assistant | 2026-11-04 |
| Every fork has a matching join | Not applicable (no fork) | AI assistant | 2026-11-04 |
| Every action cites one FR | Pass | AI assistant | 2026-11-04 |
| Every FR of UC-11 appears in the diagram | Pass (4 of 4 non-Won't W1 rows whose source trace names UC-11; FR-04-02, FR-04-03, FR-04-05, FR-04-06 are Won't online-account rows) | AI assistant | 2026-11-04 |
| Lane names match the Context Diagram | Pass | AI assistant | 2026-11-04 |
| AI critic prompt run, findings resolved or logged | Not yet run by the team | | |
