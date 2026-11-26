# Scope: Group H Library Core System

What the product covers, how it is split into features, what is left out on purpose, and which data it keeps or only reads. The use case list itself is in [use-case.md](../use-case/use-case.md).

| Field | Value |
|---|---|
| Version | v1.0 · 23/11/2026 |
| Exported from | Sheet W0_Scope of [GROUP-H_UC_FR_COST.xlsx @ cd61897](https://github.com/chihvcte-beep/dbiz2-group-h/blob/cd61897/%5BDBIZ%202%5D%20GROUP%20H/GROUP-H_UC_FR_COST.xlsx) (frozen). Source of truth from 23/11/2026 (D51). |
| Inputs | [cvca.md](../context/cvca.md), [context-diagram.md](../context/context-diagram.md), [use-case.md](../use-case/use-case.md) |
| Where the W0 tables went | Table 1 (use case inventory): [use-case.md](../use-case/use-case.md#3-use-case-inventory-w0-table-1). Tables 2, 3 and 4: this file. Function points of Table 4: [cost.md](cost.md). |

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

## Business rules

Domain rules and constraints that govern the system across features, traced to functional requirements in [fr-list.md](fr-list.md) or group decisions in [decision-index.md](../project/decision-index.md).

| BR | Rule | Source |
|---|---|---|
| BR-01 | Only library card holders can sign in to reader features, using a 7-digit library card number (stored as text to preserve leading zeros) and a 6-digit email OTP sent to the email registered on the card. | [FR-04-01](fr-list.md#fr-04-01), [FR-04-04](fr-list.md#fr-04-04), [UI Q8](../project/decision-index.md#ui-conventions), [UI Q11](../project/decision-index.md#ui-conventions) |
| BR-02 | Each OTP is valid for 5 minutes, can be used only once, and is invalidated immediately after 5 incorrect attempts or when a new OTP is requested. | [FR-04-04](fr-list.md#fr-04-04), [FR-04-17](fr-list.md#fr-04-17) |
| BR-03 | On-site Staff sign in with their internal library credentials and stay signed in without session time-out until they explicitly sign out. | [FR-04-07](fr-list.md#fr-04-07), [FR-04-21](fr-list.md#fr-04-21), [D7](../project/decision-index.md#group-decisions-22112026) |
| BR-04 | A reader's pending protected action (such as saving a book, posting a review, or reporting a review) is preserved and automatically completed after OTP sign-in succeeds, or kept waiting if sign-in is cancelled. | [D1](../project/decision-index.md#group-decisions-22112026) |
| BR-05 | The system only reads data from the Library Internal System via scheduled daily syncs and never writes back to internal catalogue, shelf, loan, or account records. | [FR-04-09](fr-list.md#fr-04-09), [FR-04-10](fr-list.md#fr-04-10), [D48](../project/decision-index.md#group-decisions-22112026) |
| BR-06 | Online-only books have no physical shelf location and are never assigned a QR code. | [FR-01-06](fr-list.md#fr-01-06), [FR-02-07](fr-list.md#fr-02-07) |
| BR-07 | Every physical book title in the synced catalogue gets exactly one unique QR code shared across all physical copies of that title. | [FR-02-07](fr-list.md#fr-02-07), [D4](../project/decision-index.md#group-decisions-22112026), [D40](../project/decision-index.md#group-decisions-22112026) |
| BR-08 | New QR labels display the title's primary shelf location from the sync, whereas reprinted QR labels omit the shelf location because additional copies may sit on different shelves. | [FR-02-23](fr-list.md#fr-02-23), [FR-02-25](fr-list.md#fr-02-25), [D13](../project/decision-index.md#group-decisions-22112026), [D40](../project/decision-index.md#group-decisions-22112026) |
| BR-09 | Physical books are marked as label-printed only when On-site Staff confirm printing («Đã in xong»), which also triggers the audit log entry; closing or failing to print leaves them unprinted. | [FR-02-08](fr-list.md#fr-02-08), [D12](../project/decision-index.md#group-decisions-22112026), [D32](../project/decision-index.md#group-decisions-22112026) |
| BR-10 | QR label sheets are formatted as 24 labels (3 columns × 8 rows) per A4 page and span multiple pages when more than 24 books are selected. | [FR-02-08](fr-list.md#fr-02-08), [D4](../project/decision-index.md#group-decisions-22112026), [D41](../project/decision-index.md#group-decisions-22112026) |
| BR-11 | Book reviews must be non-empty plain text of at most 2,000 characters, and readers may post them either under their registered library card name or anonymously («Bạn đọc ẩn danh»). | [FR-02-01](fr-list.md#fr-02-01), [FR-02-22](fr-list.md#fr-02-22) |
| BR-12 | Reviews must not contain offensive language, advertising, or personal information; On-site Staff evaluate reported reviews strictly against these three criteria. | [FR-02-10](fr-list.md#fr-02-10), [D20](../project/decision-index.md#group-decisions-22112026) |
| BR-13 | Readers can only edit or delete their own reviews, and removed reviews are hidden from public display while remaining stored internally with a Removed state. | [FR-02-03](fr-list.md#fr-02-03), [FR-02-04](fr-list.md#fr-02-04), [FR-02-11](fr-list.md#fr-02-11), [FR-02-13](fr-list.md#fr-02-13), [AD-UC-04 Q3](../project/decision-index.md#ad-uc-04) |
| BR-14 | Readers cannot report their own reviews and cannot submit more than one report for the same review. | [FR-02-21](fr-list.md#fr-02-21), [FR-02-24](fr-list.md#fr-02-24), [D39](../project/decision-index.md#group-decisions-22112026) |
| BR-15 | A reported review remains publicly visible until On-site Staff explicitly confirm its removal. | [FR-02-10](fr-list.md#fr-02-10), [FR-02-13](fr-list.md#fr-02-13), [AD-UC-14 Q3](../project/decision-index.md#ad-uc-14) |
| BR-16 | Only physical books can be added to a reader's saved books list, and the same book cannot be saved twice. | [FR-03-06](fr-list.md#fr-03-06), [FR-03-24](fr-list.md#fr-03-24) |
| BR-17 | Reading history entries are created automatically with initial status Reading and 0% progress whenever a signed-in reader selects an online book to open on the OPAC or borrows a physical book in synced loan records. | [FR-03-02](fr-list.md#fr-03-02), [FR-03-03](fr-list.md#fr-03-03), [D42](../project/decision-index.md#group-decisions-22112026), [AD-UC-07 Q1](../project/decision-index.md#ad-uc-07) |
| BR-18 | Reading progress must be an integer between 0 and 100 percent, and a book can be marked Finished even when progress is below 100%. | [FR-03-04](fr-list.md#fr-03-04), [AD-UC-07 Q4](../project/decision-index.md#ad-uc-07) |
| BR-19 | Every selection of an online book to open on the OPAC is logged anonymously (book ID and timestamp only, without reader identity) to support usage analysis and AI training. | [FR-03-13](fr-list.md#fr-03-13), [D42](../project/decision-index.md#group-decisions-22112026) |
| BR-20 | Personalized recommendations display up to 10 books, fall back to popular books (ranked by QR scan count or loan count) when a reader has no data, and supplement lists of fewer than 3 titles with trending books from the same subject in the last 30 days. | [FR-03-19](fr-list.md#fr-03-19), [FR-03-20](fr-list.md#fr-03-20), [AD-UC-09 Q1](../project/decision-index.md#ad-uc-09), [AD-UC-09 Q2](../project/decision-index.md#ad-uc-09), [AD-UC-09 Q3](../project/decision-index.md#ad-uc-09) |