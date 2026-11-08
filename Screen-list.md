# UC-08 \-- AI-Based Conversational Book Search

**Actor:** Reader  
 **Feature:** F-03  
 **Login required:** Yes  
 **Activity Diagram trace:** Action `r1` in `AD-UC-08.md` ("Send an inquiry message to the chatbot")

## Screen List

| Screen ID | Screen name | Actor | Feature | Shown when (purpose) | Entry points | Use cases / FRs served | Priority | Screen spec |
| ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| S-F03-06 | AI Chatbot Book Search | Reader | F-03 | A signed-in reader interacts with a conversational AI chatbot to find catalogue books using natural language inquiries, and views conversational replies accompanied by book result cards. | OPAC Header / Floating Chatbot Widget on bottom-right of pages → AI Chatbot Search | UC-08 · FR-03-09, FR-03-10, FR-03-16, FR-03-17, FR-03-18 | Could | `screens/screen-spec-S-F03-06.md` |

## Modals and overlays

| Modal / Overlay | Opened from screen | Purpose |
| ----- | ----- | ----- |
| M-F03-06-01 (Sign-in Prompt Modal) | S-F03-06 | Displayed when an unauthenticated reader attempts to send a chatbot message, prompting them to log in with a library card account (FR-03-18). |

## What is deliberately not a screen

| Candidate | Why it is not a screen |
| ----- | ----- |
| Send inquiry message | An input action performed inside the chat window on screen `S-F03-06`, not a separate screen. |
| Save conversation history | A background data persistence function (`FR-03-10`); it has no separate user interface. |
| AI Service catalogue search | Internal backend and AI service processing (`FR-03-09`, `FR-03-09-INT`); no direct user screen. |
| Sign in | A shared platform screen (`S-F00-01`), serving `UC-11` (`FR-04-01`). |
| AI Error / Timeout warning | An error state of screen `S-F03-06` (`FR-03-17`); not divided into a separate screen. |
| No results found notice | An empty/no-match state displayed within the conversational stream of `S-F03-06` (`FR-03-16`). |

## Screen States (Design System mapping for S-F03-06)

* **Default / Initial State:** Chat history displays past messages (if any) or a welcome prompt with suggested topic chips (e.g., "Find books on Macroeconomics", "Machine Learning in Business").  
* **Typing / Loading State:** A subtle typing indicator (animated three dots) is shown while the AI service in the Library Core System is processing the inquiry.  
* **Success State (Result Cards):** Chatbot response message displayed together with compact book result cards showing title, author, call number/shelf location link, and access format badge.  
* **Hover / Interactive State:** Hovering over a book card elevates the card with a soft shadow and surfaces quick actions ("View Shelf Location", "Save Book").  
* **No-Match State (FR-03-16):** The chatbot replies conversationally stating that no catalogue books match the exact inquiry, suggesting related alternative keywords or subjects.  
* **Error / Timeout State (FR-03-17):** An inline warning banner appears explaining that AI search is temporarily unavailable and providing a one-click shortcut to the format filter (`S-F03-05`).

# **UC-09 \-- Automatic Personalised Book Recommendations**

**Actor:** Reader  
 **Feature:** F-03  
 **Login required:** Yes  
 **Activity Diagram trace:** Actions `r1` ("Open the recommendations section") and `r2` ("View the recommended books") in `AD-UC-09.md`

## **Screen List**

| Screen ID | Screen name | Actor | Feature | Shown when (purpose) | Entry points | Use cases / FRs served | Priority | Screen spec |
| ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| S-F03-07 | Book Recommendations | Reader | F-03 | A signed-in reader opens the recommendation section to view a personalized list of book suggestions computed from their reading history, declared preferences, and past chatbot conversations. | OPAC Navigation bar ("Recommended for You") or Reader Dashboard → Book Recommendations | UC-09 · FR-03-11, FR-03-19, FR-03-20, FR-03-21 | Could | `screens/screen-spec-S-F03-07.md` |

## **Modals and overlays**

| Modal / Overlay | Opened from screen | Purpose |
| ----- | ----- | ----- |
| M-F03-07-01 (Sign-in Prompt Modal) | S-F03-07 | Displayed when an unauthenticated visitor opens the recommendation page, explaining that personalized suggestions require a library card account (FR-03-21). |

## **What is deliberately not a screen**

| Candidate | Why it is not a screen |
| ----- | ----- |
| Compute recommendation scores | Background backend processing (`FR-03-11-BE`); it has no separate user interface. |
| Add trending books | An algorithmic fallback rule (`FR-03-20`) when fewer than three titles match; rendered directly within the book list of `S-F03-07`. |
| Select popular books by QR scans | A fallback data aggregation rule (`FR-03-19`) for readers with no profile history; rendered as a cold-start state within `S-F03-07`. |
| Sign in | A shared platform screen (`S-F00-01`), serving `UC-11` (`FR-04-01`). |

## **Screen States (Design System mapping for S-F03-07)**

* **Loading State:** Skeleton card loaders simulate the recommendation grid while scores are computed.  
* **Personalised Success State (FR-03-11):** A responsive grid of book recommendation cards with recommendation context badges (e.g., "Based on your recent reads", "Matches your Interest: Technology").  
* **Topped-Up State (FR-03-20):** If personalized results yield fewer than three books, additional trending books from the same subject category are appended with a "Trending in Subject" badge.  
* **Cold-Start / Fallback State (FR-03-19):** For new readers without reading history, preferences, or chat logs, popular books ranked by QR scan count are displayed alongside a prompt banner encouraging the reader to configure Reading Preferences (`S-F03-02`).  
* **Hover / Interactive State:** Hovering over a book card reveals cover zoom, author metadata, and quick action buttons ("View Shelf Location", "Save to Personal List").  
* **Error State:** A failure message with a "Retry" button appears if the backend data retrieval encounters an unhandled exception.

