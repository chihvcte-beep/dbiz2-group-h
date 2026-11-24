# Wireframe notes: S-F03-01 Access-format filter and results

Actor: Reader · Frame: 360px · UI conventions: v0.8 · Author: Nhi

## Elements

| # | Element | Component | Content / data source | FR |
|---|---|---|---|---|
| 1 | Back button | Screen header | Accessible name: “Quay lại”. Return to where the reader opened the filter: the existing OPAC catalogue / search results, or `S-F03-06` (D35). | — |
| 2 | Screen title | Screen header | “Lọc theo hình thức”. | — |
| 3 | Instruction label | Section title | “Chọn hình thức truy cập”. | FR-03-12 |
| 4 | Access-format selector | Segmented control | Exactly three choices: “Trực tuyến”, “Bản giấy”, “Cả hai”. “Cả hai” means books that have both a physical copy and an online version. | FR-03-12 |
| 5 | Matching book results | Book row | Retrieve matching books from the whole synced catalogue, not only the current OPAC search results. Each row opens the corresponding existing OPAC book detail destination. | FR-03-12 |
| 6 | Access-format label | Format label | Show the format with an icon and word: “Bản giấy” and/or “Trực tuyến”. Never rely on colour alone. | FR-03-12 |
| 7 | No-results message | Empty state | “Không tìm thấy sách. Hãy chọn hình thức khác.” Keep the selector available so the reader can choose another format. | FR-03-23 |
| 8 | Load error | Banner | MSG-04: “Không tải được trang. Bạn kiểm tra kết nối mạng rồi thử lại.” Keep data already shown. | FR-04-20 |
| 9 | Retry action | Secondary button | “Thử lại”. Retry retrieval for the currently selected access format. | FR-04-20 |

## States drawn

| State | Image | What the user sees | Source / FR |
|---|---|---|---|
| Default | [s_f03_01.png](../img/s_f03_01/s_f03_01.png) | The three access-format choices are visible. No option is selected on first entry; matching results appear after the reader chooses a format. | UC-03 · FR-03-12; D19 |
| Empty | [s_f03_01_empty.png](../img/s_f03_01/s_f03_01_empty.png) | No matching books are found. Show the empty-state sentence once and keep the selector available for another choice. | AD-UC-03 d1 [No], s3 · FR-03-23 |
| Loading | [s_f03_01_loading.png](../img/s_f03_01/s_f03_01_loading.png) | Skeleton placeholders while the system retrieves books for the selected access format. No loading text. | System step s1 · FR-03-12; MSG-05 |
| Error | [s_f03_01_error.png](../img/s_f03_01/s_f03_01_error.png) | Shared MSG-04 banner and “Thử lại” action. Retain the selected format and any data already shown. | FR-04-20 |
| Results | [s_f03_01_success.png](../img/s_f03_01/s_f03_01_success.png) | Matching books appear on S-F03-01 with format labels. The example shows one physical book and one online book. The result list stays on this screen while the reader changes the format or finishes filtering. | AD-UC-03 d1 [Yes], s2 · FR-03-12 |

## Actions and where they go

| Element / event | User action / system event | Result / destination |
|---|---|---|
| Back button | Reader taps Back | Existing OPAC catalogue / search results (exit destination), or `S-F03-06` when opened from the chatbot (D35). |
| Access-format selector | Reader chooses “Trực tuyến”, “Bản giấy” or “Cả hai” | System retrieves matching books from the whole synced catalogue; results update on S-F03-01. |
| Choose another format | Reader changes the selected format after an empty state or results | Stay on S-F03-01; retrieve and display the new matching results from page 1 (D14). |
| Physical book row | Reader opens a physical book result | Existing OPAC Book Detail (exit destination); the current project does not create another book-detail screen here. |
| Online book row | Reader opens an online book result | Current OPAC online-book page (existing destination; no new viewer or download function is built here). |
| Online book opened | System records the book and time without reader identity | Background action s4 · FR-03-13. |
| Library-card sign-in check | System checks whether the reader is signed in with a library card | If Yes, add the book to reading history (s5 · FR-03-02); if No, do not add a history entry. These are background actions, not visible UI elements. |
| Retry | Reader taps “Thử lại” | Retry loading results for the currently selected format; stay on S-F03-01. |

## Open questions

None. Decisions: see [decision_index.md](../../../project/decision_index.md#s-f03-01).
