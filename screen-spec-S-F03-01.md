# Screen Spec: S-F03-01 Access-format filter and results

| Field | Value |
|---|---|
| Screen ID | `S-F03-01` |
| Screen name | Access-format filter and results |
| Actor | Reader |
| Priority | Should |
| Feature | `F-03` Discovery, Reading History & Recommendation |
| Activity diagrams | `AD-UC-03` (v1.2) |
| Mockup image | `img/S-F03-01-default.png` |
| Status | Draft — pending v0.8 mockup review |
| Frame width | 360px (exported at 3x = 1080px) |
| Wireframe source | `screens/src/S-F03-01.html` [NEEDS CLARIFICATION: Nhi's notes do not specify the source path; confirm whether this file is present] |
| Wireframe author | Nhi |
| Screen spec author | Linh |
| UI conventions | v0.8 |

## 1. Purpose

**Shown when:** The reader opens the `Filter by access format` link on the existing OPAC catalogue/search results, or follows the `use the format filter` link from `S-F03-06` when AI search is unavailable.

**The user leaves this screen when:** The reader opens an online book on the current OPAC, opens a physical book on the existing OPAC Book Detail page, or returns to the existing OPAC catalogue/search results using Back. Choosing another format or finishing the filtering activity keeps the reader on this screen.

## 2. Mockup

**Current numbered wireframe (for group review; not yet approved against UI Conventions v0.8):**

![S-F03-01 — existing numbered wireframe](https://raw.githubusercontent.com/chihvcte-beep/dbiz2-group-h/main/%5BDBIZ%202%5D%20GROUP%20H/EXTERNAL%20DESIGN/screens/img/S-F03-01-numbered.png)

[Open original numbered image on GitHub](https://github.com/chihvcte-beep/dbiz2-group-h/blob/main/%5BDBIZ%202%5D%20GROUP%20H/EXTERNAL%20DESIGN/screens/img/S-F03-01-numbered.png)

> **Draft review note:** This is the wireframe owner's existing image, linked from the repository rather than edited or copied. Replace/verify the mockup after the owner updates the export. State-specific image paths below are pending confirmation.

![S-F03-01](img/S-F03-01-default.png)

**Numbered reference (supplied GitHub image):** `img/S-F03-01-numbered.png`.

| State | Image |
|---|---|
| Default | `img/S-F03-01-default.png`; `img/S-F03-01-numbered.png` (numbered file supplied; verify default export in repo) |
| Empty | `img/S-F03-01-empty.png` |
| Loading | `img/S-F03-01-loading.png` |
| Error | Not applicable for UC-03 at present: AD-UC-03 defines the no-results branch, not a system/network-error branch. The exported Error image is a placeholder, not a confirmed UC-03 requirement. |
| Success / results | `img/S-F03-01-success.png` [NEEDS CLARIFICATION: include only if this image is retained in Nhi's final export] |

Use `ui-conventions.md` v0.8 §6 for all design tokens. Reader frame: 360px, exported at 3x (1080px). Titles use SVN-Gilroy; other text uses Inter.

## 3. Element inventory

**Numbering check:** Items 1–4 are the main numbered Default wireframe elements. Conditional results, empty, loading and error UI must be reconciled against their corresponding state images; system logging/history actions are not visible numbered controls. The initial selected format is still an open team decision (Q5).

| # | Element | Type | Content / data source | Required | Validation |
|---|---|---|---|---|---|
| 1 | Back navigation | Screen header | Returns to the existing OPAC catalogue / search results from which the reader opened the filter. | Yes | Navigation only; preserve the originating OPAC destination. |
| 2 | Screen title | Screen header | `Lọc theo hình thức`. | Yes | Static text; title is confirmed in `ui-conventions.md` v0.7 §1. |
| 3 | Access-format selector | Segmented control | Exactly three choices: `Trực tuyến`, `Bản giấy`, and `Cả hai`. `Cả hai` means books that have both a physical copy and an online version. | Yes | Exactly one option can be selected at a time. Initial selected state is unresolved; do not assume a default until Q5 is confirmed. |
| 4 | Matching book results | Book row | Book catalogue (W0 Table 4) › book title, author, cover placeholder, and applicable access-format label(s). Each format label uses an icon + Vietnamese word (`Trực tuyến` and/or `Bản giấy`). | No (shown when results exist) | Read-only catalogue data. Only display the format information returned for each book; do not infer availability or stock status. |
| 5 (empty state) | No-results message | Empty state | `Không tìm thấy sách. Hãy chọn hình thức khác.` (shared example wording in `ui-conventions.md` §4; confirm as final approved copy because Nhi's notes leave exact wording open). | No (shown when no matches exist) | Not an input. Keep the selector available so the reader can choose another format. |
| 6 (results state) | Online-book link | Text link | Opens the selected online book on the current OPAC. No new online reader or download function is part of this product. | No (shown for online book results) | Open the matching book's existing OPAC online-book page. |
| — (system) | Anonymous online-read log | Background system action; not a visible UI element | Online read log › book and read time only; no reader identity. | Yes (system action) | Create an anonymous record each time an online book is opened; do not include reader identity. |
| — (system) | Signed-in reader history update | Background system action; not a visible UI element | Reader reading history › book entry. | Conditional (system action) | Add the book to reading history only if the reader is signed in with a library card; otherwise do not create a history entry. |

## 4. States

| State | What the user sees | Trigger |
|---|---|---|
| Default | `Lọc theo hình thức` and the three-option selector. The initially selected option must be taken from Nhi's final Default wireframe after Q5 is resolved; the activity diagram does not define a default. | Reader opens the access-format filter. |
| Empty (no data) | An empty state tells the reader that no matching books were found and invites them to choose another format. The selector remains available on this screen. Use the shared example wording only after the group confirms it. | No books match the selected format (`AD-UC-03 d1 [No]`, `s3`; FR-03-23). |
| Loading | Skeleton placeholders while the system retrieves books matching the selected format (`MSG-05`; no loading text by default). | Reader selects an access format and matching books are retrieved. |
| Error | Not applicable for the current UC-03 scope: AD-UC-03 does not define a system/network-error branch. The `-error.png` in the notes is a design placeholder. If the group confirms that this screen must handle a load failure, use shared `MSG-04` / FR-04-20 and update the wireframe and interaction inventory first. | — |
| Success / confirmation | Matching books appear with their access-format labels. This is the results outcome, not a separate toast or confirmation message. | The selected format has matching books (`AD-UC-03 d1 [Yes]`, `s2`; FR-03-12). |

## 5. Interactions and navigation

| # | Element | User action | System response | Goes to screen |
|---|---|---|---|---|
| 1 | Entry | Open the access-format filter from the existing OPAC catalogue/search results, or follow the format-filter link from `S-F03-06` when AI search is unavailable. | Load the filter screen and make the three access-format choices available. | `S-F03-01` |
| 2 | Access-format selector | Choose `Trực tuyến`, `Bản giấy`, or `Cả hai`. | Retrieve matching books from the whole synced catalogue, not only the current OPAC search-result subset; display matching results or the no-results state. | stays |
| 3 | Matching book results — physical book | Open a physical book result. | Hand off to the selected book's existing OPAC Book Detail page. | Existing OPAC Book Detail (exit) |
| 4 | Online-book link | Open an online book result. | Open the selected online book on the current OPAC. Trigger the anonymous online-read log. | Existing OPAC online-book page (exit) |
| 5 | Anonymous online-read log | System records the online-book opening. | Record the book and read time only; do not include reader identity. | stays (background action) |
| 6 | Signed-in reader history update | System checks whether the reader is signed in with a library card after an online book is opened. | If signed in, add the book to reading history; otherwise do not create a history entry. | stays (background action) |
| 7 | No-results state / Access-format selector | Choose another format after seeing no results. | Retrieve results for the newly selected format and update the same screen. | stays |
| 8 | Back navigation | Select Back. | Return to the existing OPAC catalogue/search results that opened the filter. | Existing OPAC catalogue / search results (exit) |
| 9 | Finish | Stop filtering. | End the activity; the current result list remains displayed. | stays |

## 6. Screen-level rules

| Rule ID | Rule | Source |
|---|---|---|
| SR-001 | The access-format filter does not require reader sign-in. | AD-UC-03 preconditions; Nhi-wireframe-2.md §2.3 |
| SR-002 | The selector contains exactly three choices: `Trực tuyến`, `Bản giấy`, and `Cả hai`; `Cả hai` means the book has both a physical copy and an online version. | FR-03-12; AD-UC-03; `ui-conventions.md` §2 |
| SR-003 | Retrieve matches from the whole synced catalogue, not only the current OPAC search results. | FR-03-12; L8-12 |
| SR-004 | Each result displays the applicable access-format label using an icon and a Vietnamese word; colour must not be the only signal. | FR-03-12; `ui-conventions.md` §§2, 3, 5 |
| SR-005 | If no books match, display the no-results state and allow another format to be selected without leaving this screen. | FR-03-23; AD-UC-03 `d1`, `s3`, `d2` |
| SR-006 | Opening an online book hands off to the current OPAC; this product does not build an online-book viewer or download function. | FR-03-13; W0 Table 3; AD-UC-03 |
| SR-007 | Every online-book opening creates an anonymous read-log record containing the book and time only; no reader identity is stored in that log. | FR-03-13; AD-UC-03 `s4` |
| SR-008 | Add an online-book opening to reading history only when the reader is signed in with a library card. | FR-03-02; AD-UC-03 `d3`, `s5` |
| SR-009 | The initial selected option must follow the final group decision for Q5; do not infer a default from AD-UC-03. | Q5 in `screen-spec-chung.md`; S-F03-01 wireframe notes |
| SR-010 | Do not add keyword search, collection-status filtering, an online reader, or PDF download controls. | W0 Table 3; Nhi-wireframe-2.md §2.3 |

## 7. Linked requirements

| FR ID | What this screen does for it |
|---|---|
| FR-03-12 | Filters the whole synced catalogue by Online, Physical, or Both and displays each result's access-format label. |
| FR-03-23 | Displays a no-results state and lets the reader choose another format on the same screen. |
| FR-03-13 | Records each opened online book and read time without reader identity. |
| FR-03-02 | Adds an online-book opening to reading history only for a reader signed in with a library card. This is a background action, not a separate UI element. |

## 8. Responsive and accessibility notes

- Smallest supported width: 360px.
- Reader frame: 360px, exported at 3x (1080px).
- Preserve Nhi's approved selector and result-row grouping; do not introduce a different layout without updating the wireframe.
- Access-format labels must use an icon plus the Vietnamese word `Trực tuyến` and/or `Bản giấy`; never communicate format by colour alone.
- Interactive targets on Reader screens must be at least 44×44px; all controls must have a visible 2px focus ring.
- Text contrast: at least 4.5:1; control borders: at least 3:1.
- Body and input text: at least 16px; title: 20px; use SVN-Gilroy for titles and Inter for other text, per `ui-conventions.md` v0.7 §§5–6.
- Book title and author follow the catalogue and are truncated after two lines with an ellipsis, per `ui-conventions.md` §2.

## 9. Open questions

| # | Question | Blocking? | Status |
|---|---|---|---|
| 1 | [NEEDS CLARIFICATION: Q5 — Which option is selected when S-F03-01 first opens? Confirm with Nhi and the group, then record the group decision. Do not infer a default.] | Yes | Open |
| 2 | [NEEDS CLARIFICATION: What is the final approved Vietnamese wording for the no-results message? `Không tìm thấy sách. Hãy chọn hình thức khác.` is the shared example in `ui-conventions.md` §4, but Nhi's notes leave the exact wording open.] | No | Open |
| 3 | [NEEDS CLARIFICATION: Is the Error image a retained state? Nhi's notes identify it as a placeholder and AD-UC-03 has no system-error branch. If approved as a network/load state, use `MSG-04` / FR-04-20 and add the corresponding interaction and element to the wireframe first.] | Yes | Open |
| 4 | [NEEDS CLARIFICATION: Confirm the exact W0 Table 4 field names / group names for book title, author, cover placeholder and access format.] | Yes | Open |
| 5 | [NEEDS CLARIFICATION: Confirm whether `img/S-F03-01-success.png` is retained in Nhi's final export; the notes mark it as optional.] | No | Open |
| 6 | [NEEDS CLARIFICATION: Nhi's notes omit Frame, UI conventions version and Author in their metadata row; confirm/add `Reader · 360px · v0.7 · Nhi`.] | No | Open |
| 7 | [NEEDS CLARIFICATION: Confirm the source path for Nhi's wireframe; `screens/src/S-F03-01.html` is the expected path if the HTML has been committed.] | No | Open |

---

## Completion checklist

- [ ] The Default mockup is a separate cropped image file named with the Screen ID and is 1080px wide; the current notes name it `img/S-F03-01-default.png`.
- [x] Every element in Nhi's notes appears in the element inventory, retaining the original `#`.
- [x] Every input element has a validation rule or an explicit `none` (there are no text-entry fields).
- [x] All five states are filled in or marked not applicable with a reason; Error is provisional and explicitly marked not applicable for current UC-03 scope.
- [x] Every navigation target is an existing Screen ID, `stays`, or an existing OPAC destination marked `(exit)`.
- [x] Every element that displays data names its data source; exact W0 Table 4 field names remain open.
- [x] Linked FRs are drawn from the Screen List and Nhi's notes; all listed user/system actions are represented in the interaction table.
