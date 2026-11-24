# Scope: Group H Library Core System

What the product covers, how it is split into features, what is left out on purpose, and which data it keeps or only reads. The use case list itself is in [use_case.md](../use_case/use_case.md).

| Field | Value |
|---|---|
| Version | v1.0 · 23/11/2026 |
| Exported from | Sheet W0_Scope of [GROUP-H_UC_FR_COST.xlsx @ cd61897](https://github.com/chihvcte-beep/dbiz2-group-h/blob/cd61897/%5BDBIZ%202%5D%20GROUP%20H/GROUP-H_UC_FR_COST.xlsx) (frozen). Source of truth from 23/11/2026 (D51). |
| Inputs | [cvca.md](../context/cvca.md), [context_diagram.md](../context/context_diagram.md), [use_case.md](../use_case/use_case.md) |
| Where the W0 tables went | Table 1 (use case inventory): [use_case.md](../use_case/use_case.md#3-use-case-inventory-w0-table-1). Tables 2, 3 and 4: this file. Function points of Table 4: [cost.md](cost.md). |

## Product in one paragraph

An add-on to the library's existing OPAC ([opac.nlv.gov.vn](https://opac.nlv.gov.vn)) for two groups of people: **Readers** and **On-site Staff**. Readers find the exact shelf of a book, browse a map of the library, read and write reviews, scan a QR code on a physical book, keep a reading history and a saved list, and get AI search and recommendations. On-site Staff print QR labels and remove reviews that break the rules. Catalogue, shelf placement, loans and accounts stay in the Library Internal System; this product only reads them.

## Table 2: Feature list

A feature name is a business noun the client recognises, never a screen name or a technical module.

| Feature | Name | Scope in one sentence | Actors served | Use cases |
|---|---|---|---|---|
| F-01 | Book Location & Library Map | Readers see the exact shelf location of each book and browse a digital map of floors and reading rooms. | Reader | UC-01, UC-02 |
| F-02 | Reviews & QR | Readers write, edit, delete and read reviews of books, including by scanning a QR code on a physical book, and On-site Staff print the QR labels and remove reviews that violate rules. | Reader, On-site Staff | UC-04, UC-05, UC-06, UC-10, UC-13, UC-14 |
| F-03 | Discovery, Reading History & Recommendation | Readers filter books by access format (online, physical or both), keep a reading history and a saved-books list, and get AI chatbot search and recommendations based on their preferences. | Reader | UC-03, UC-07, UC-08, UC-09, UC-12 |
| F-04 | Platform, Access & Operations | Readers sign in (library card with email OTP), On-site Staff sign in with their internal library accounts to reach their minimal page, and the platform syncs data from the library's internal system, is deployed and keeps an audit log. | All actors | UC-11, UC-15 |

## Table 3: Won't have

Excluded on purpose. Never drop an item silently: add it here with the reason.

| Excluded from scope | How it surfaced | Reason |
|---|---|---|
| Automatic tracking of reading progress and finished books | Stated in the note under UC-07 | The library records borrow/return of physical books but not pages read. Online books opened by library card readers and borrowed physical books enter the history automatically; readers mark Reading or Finished and enter progress manually in release 1 |
| Borrowing, returning and renewing loans | Implied by former UC-05 ('ready for borrowing', removed from the diagram); no loan use case in the diagram | Stays in the library's internal system; this platform does not handle loans. The current OPAC already shows copy availability and the Borrow action |
| Reading online content inside the platform | Implied by UC-03 (Online format); no viewer use case in the diagram | Confirmed: online books can be opened or downloaded without sign-in on the existing OPAC; this platform builds no viewer and no download of its own |
| Assigning or editing shelf codes and the library layout | Implied by the original UC-01 (Manage book locations) | Done in the library's internal system; this platform only reads the data and publishes it to readers |
| Full librarian/admin workspace in the OPAC | Implied by the original actor Librarian/Admin | Staff use only a minimal page (QR label printing, review removal) with their internal accounts; catalogue, shelf codes and loans are managed in the internal system |
| Traditional keyword search | Not in any use case | Already provided by the current OPAC; this platform adds filtering and AI chatbot search only |
| QR codes for online-only books | Business rule on UC-06 | Online-only books have no physical copy to attach a QR code to; readers download the PDF instead |
| Sending reader reviews and feedback to the library's internal system, or a report/dashboard of them for library staff | Implied by the CVCA flow 'reader feedback & rate books' to the library (flow to be removed from the CVCA) | Reviews and feedback stay in this platform and are not sent to the internal system |
| Screen for library staff to edit floor plans and rooms | Implied by UC-02 (digital library map) | No digital floor plan exists today; the team prepares it once. Changes to the room layout are made by the team, not through a screen in release 1 |
| Features not rebuilt: (a) like/dislike rating, list of books in a room, copy availability and borrow status, already on the current OPAC; (b) viewing and filtering by collection status (In collection / Coming soon) | (a) Confirmed on the current OPAC (document location panel shows each copy, its circulation point and status); (b) former UC-03, dropped after team review | (a) Not rebuilt. This platform keeps text reviews only and does not read copy circulation status. (b) The internal system holds the field, but readers do not need it on the web |
| Showing the access format of each book on the book detail page (FR-03-14) and downloading PDFs on this platform (FR-03-15) | Scope cut after the W4 capacity review (UC-03 reduced to the access-format filter) | Download PDF: the current OPAC already has this function and online books can be downloaded without sign-in, so it is not rebuilt. Access format display: for physical books the OPAC already shows the number of copies and the shelf location; for online books it already shows a download button. This platform only adds the online / physical / both filter (FR-03-12) |
| Online reader accounts: register or sign in with email OTP (FR-04-02), Google sign-in (FR-04-03), linking an online account to a library card and its check (FR-04-05, FR-04-06) | Scope cut after the W4 capacity review (UC-11 online part) | Only library card holders sign in (library card + email OTP, FR-04-01). Online books are opened or downloaded without any account, so there is nothing to link |
| Error tracking, health check and alerts to the project team (FR-04-15) | Hidden work in F-04, cut after the W4 capacity review | Deferred to fit team capacity; the team checks the system by hand in release 1 |

## Table 4: Data functions

ILF = data this product keeps and changes. EIF = data it only reads from another system, never writes.

| Data group | ILF / EIF | Why |
|---|---|---|
| Book placement & library layout | EIF | Rooms, shelf codes and book-to-shelf assignments, plus the list of floors and rooms, read from the library's internal system, never written (UC-01, UC-02). The floor-plan drawing is a fixed asset built once by the project team, not a data function; its room codes must match the internal system |
| Book review | ILF | Written by readers, stored and shown by the system; readers can report a review and staff can remove reviews that violate rules (UC-04 to UC-06, UC-13, UC-14) |
| Reading history & preferences | ILF | History entries are added automatically (opening of an online book by a library card reader; borrow of a physical book, library card accounts only); status Reading/Finished, progress and preferences are entered by readers (UC-07, UC-09) |
| Book catalogue | EIF | Titles, authors, subjects, summaries and access formats read from the library's internal system, never written (UC-03, UC-06) |
| Reader accounts | EIF | Reader identity, library card number and the email declared when the card was made (used to send the OTP) read from the library's existing reader accounts, never written (UC-11) |
| Book QR codes | ILF | QR codes generated automatically for each new physical book, with scan counts kept for analysis and AI training; also the entry point for writing reviews (UC-06, UC-10) |
| Saved books list | ILF | Physical books that readers save, with a library card account, to find them later in the library (UC-12) |
| Reader loan records | EIF | Borrow/return history of each library card account, read from the library's internal system, never written (UC-07) |
| Chatbot conversations | ILF | Messages and needs readers state to the chatbot, saved per reader to personalise search and recommendations (UC-08, UC-09) |
| Staff accounts | EIF | On-site Staff identity read from the library's internal accounts, never written (sign-in to the staff page) |
| Online book read log | ILF | Book ID and time of each online-book read, stored without any reader identity, kept to analyse use and to train the AI features (UC-03) |
