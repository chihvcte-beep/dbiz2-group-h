# Screen Lists — UC-11, UC-01 and UC-02

This document consolidates the screen lists for UC-11, UC-01 and UC-02. The screen IDs follow the `S-<feature>-<nn>` convention. Shared platform screens use the `S-F00-<nn>` convention shown in the group's existing Screen List example.

**Priority rule.** A screen's priority is the highest priority of the in-scope functional requirements it serves in W1 (W1_FunctionList, column "Initial priority").

---

# UC-11 — Register and sign in (library card with email OTP)

**Actor:** Reader  
**Feature:** F-04 Platform, Access & Operations  
**Login required:** No — this use case is the sign-in flow.

**Feature ownership and screen classification:** UC-11 belongs to F-04 Platform, Access & Operations. Its sign-in screens are classified under F-00 Shared Platform because they provide reusable authentication functionality across the OPAC system. Therefore, the screen IDs remain S-F00-01 and S-F00-02.

## Screen List

| Screen ID | Screen name | Actor | Feature | Shown when (purpose) | Entry points | Use cases / FRs served | Priority | Screen spec |
|---|---|---|---|---|---|---|---|---|
| S-F00-01 | Sign in — Library card number | Reader | F-00 Shared Platform | A reader starts the sign-in process and needs to submit their library card number. | Shared sign-in entry point; invoked as `Sign in (UC-11)` by use cases that require authentication. | UC-11 · FR-04-01, FR-04-04, FR-04-16 | Must | Provide an input for the library card number and an action to submit it. The system checks the card number against the reader account data from Library Internal System. If the card number is not found, show the general sign-in rejection message. If found, generate an OTP and send it by email, then continue to the OTP screen. |
| S-F00-02 | Verify email OTP | Reader | F-00 Shared Platform | The reader's library card number has been found. The OTP email has been sent, or its delivery has failed and the reader can ask for a new OTP. | From S-F00-01 after the library card number is found. | UC-11 · FR-04-01, FR-04-04, FR-04-12, FR-04-16, FR-04-17 | Must | Provide an OTP input, a submit action and a request-new-OTP action. An OTP expires after five minutes and can be used once. An incorrect code can be re-entered while fewer than five incorrect attempts have been made. After five incorrect attempts, invalidate the OTP and reject sign-in. Requesting a new OTP invalidates the previous OTP. If delivery fails, show an email-send error and offer the request-new-OTP action. On successful verification, start the signed-in session and write an audit entry. |

## Modals and overlays

No modals or overlays are identified in the supplied AD-UC-11.

## What is deliberately not a screen

| Candidate | Why it is not a screen |
|---|---|
| Request a new OTP | An action available on the Verify email OTP screen; it does not require a separate screen. |
| Incorrect, expired or already-used OTP message | An error state/message on the Verify email OTP screen, not a separate screen. |
| OTP email delivery failure message | An error state/message on the Verify email OTP screen, not a separate screen. |
| Start a signed-in session | A system action after successful OTP verification, not a screen. |
| Write an audit entry | A backend/system action, not a screen. |
| Register an online account or link an external account | The supplied AD states that online-account registration/linking is out of scope for this release. |
| Sign in inside another use case | A shared platform flow. Other authenticated use cases should show only the collapsed step `Sign in (UC-11)`, not duplicate this detailed flow. |

---

# UC-01 — View book shelf location

**Actor:** Reader  
**Feature:** F-01 Book Location & Library Map  
**Login required:** No

## Screen List

| Screen ID | Screen name | Actor | Feature | Shown when (purpose) | Entry points | Use cases / FRs served | Priority | Screen spec |
|---|---|---|---|---|---|---|---|---|
| S-F01-01 | Book Detail — Shelf location | Reader | F-01 Book Location & Library Map | The reader opens a book's detail page and requests its physical shelf location. The screen shows the floor, room and shelf code of every physical copy that has complete and consistent location data. | From the existing catalogue/search results when the reader opens a book's detail page; the exact originating control is not specified in the supplied activity diagram. | UC-01 · FR-01-01, FR-01-03, FR-01-06, FR-01-07 | Must | Display the floor, room and shelf code for every physical copy of the book, with one line per copy. If a book has copies in different rooms or on different floors, display each copy's location separately; do not display only one representative location. For an online-only book, state that the book is available electronically and that no physical shelf location applies. If location codes are missing or inconsistent, state that the shelf location is unavailable and direct the reader to the information desk on the ground floor. If the reader chooses to view the book on the map, open S-F01-02, keep the shelf details visible and identify the room or rooms of the book. Each copy line is linked to its own room on the map (proposed rule, see AD-UC-01 open question 4). |
| S-F01-02 | Interactive Digital Library Map | Reader | F-01 Book Location & Library Map | The reader requests to view the book's room on the map from the shelf-location details. | From S-F01-01 when the reader chooses to view the book on the map. | UC-01 · FR-01-03, FR-01-09, FR-01-10 | Must | Shared with UC-02. The master specification is in the UC-02 section below. In UC-01 the map opens as a separate screen from S-F01-01, highlights the room or rooms of the book when found on the plan, and keeps the book's floor, room and shelf code visible in every outcome. |

## Modals and overlays

No modals or overlays are identified in the supplied AD-UC-01.

## What is deliberately not a screen

| Candidate | Why it is not a screen |
|---|---|
| Display an online-only book message | A message/state on S-F01-01; it does not require a separate screen. |
| Display missing or inconsistent shelf-location message | An error/information state on S-F01-01, not a separate screen. |
| Choose whether to view the room on the map | A reader decision/action from the book detail screen, not a separate screen by itself. |
| Map-unavailable message | A message/state while using S-F01-02; it is not a separate screen. |
| Room-cannot-be-identified message | A message/state while using S-F01-02; it is not a separate screen. |
| Keep shelf details visible | A display-preservation requirement across the map branch, not a separate screen. |
| Sign in | Not required for UC-01 according to the supplied activity-diagram preconditions. |

---

# UC-02 — Browse interactive digital library map

**Actor:** Reader  
**Feature:** F-01 Book Location & Library Map  
**Login required:** No

## Screen List

| Screen ID | Screen name | Actor | Feature | Shown when (purpose) | Entry points | Use cases / FRs served | Priority | Screen spec |
|---|---|---|---|---|---|---|---|---|
| S-F01-02 | Interactive Digital Library Map | Reader | F-01 Book Location & Library Map | The reader opens the digital library map from the menu or arrives from UC-01 to view a book's room. The reader can view available floors and reading rooms, switch floors, and select a room. | From the existing main menu/map entry point; from S-F01-01 when the reader chooses to view the book on the map. Both entry points are kept because the screen serves UC-01 and UC-02. | UC-01, UC-02 · FR-01-02, FR-01-03, FR-01-09, FR-01-10, FR-01-11 | Must | Master specification for this screen, shared with UC-01. A separate screen, not a modal or overlay. When opened from the menu, show the ground floor (lowest floor number) first, with the available floors and reading rooms. When opened from S-F01-01, show the map with the room or rooms of the book highlighted when found on the plan, and carry forward and keep displaying the book's floor, room and shelf code in all outcomes: room highlighted, room cannot be identified (then show the plain map), or floor plan unavailable or unreadable (then show a map-unavailable message). Allow the reader to request another floor. If the selected floor plan is readable, show that floor's map and rooms; otherwise show a map-unavailable message for that floor while retaining the previous floor's map. When a reader selects a room, highlight it and display its room name, room code and floor. The reader can repeat floor switching and room selection, then finish. |

## Modals and overlays

No modals or overlays are identified in the supplied AD-UC-02.

## What is deliberately not a screen

| Candidate | Why it is not a screen |
|---|---|
| Request to view another floor | An action performed from S-F01-02; it does not require a separate screen. |
| Select a reading room | An action performed on S-F01-02; it does not require a separate screen. |
| Display another floor's map | A content/state change within the same interactive map screen. |
| Highlight a selected room and display its details | A selected state within S-F01-02, not a separate screen. |
| Map-unavailable message for a floor | A message/state on S-F01-02. The supplied AD says the previous floor's map remains visible. |
| Plain map after a room cannot be identified | A display state of S-F01-02, not a separate screen. |
| Sign in | Not required for UC-02 according to the supplied activity-diagram preconditions. |

---

## Screen ID Summary

| Screen ID | Screen name | Use case(s) |
|---|---|---|
| S-F00-01 | Sign in — Library card number | UC-11; shared entry for authenticated use cases |
| S-F00-02 | Verify email OTP | UC-11 |
| S-F01-01 | Book Detail — Shelf location | UC-01 |
| S-F01-02 | Interactive Digital Library Map | UC-01, UC-02 |
