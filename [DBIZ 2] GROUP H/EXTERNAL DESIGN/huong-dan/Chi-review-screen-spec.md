# Review Screen Spec — danh sách việc cần sửa

| Mục | Nội dung |
|---|---|
| Người review | Chi |
| Ngày | 22/11/2026 |
| Chuẩn đối chiếu | Template của thầy (`templates/screen-spec-template.md`) · Problem-Based SRS: truy vết hai chiều FR ↔ màn hình, không có tính năng "bịa", yêu cầu rõ ràng và kiểm được (ISO 29148) · `huong-dan/screen-spec-chung.md` · `ui-conventions.md` v0.8 · Function List (GROUP-H_UC_FR_COST.xlsx) · AD-UC-xx |
| Kết quả | 0/15 spec sẵn sàng chuyển `Reviewed`. Tổng: 47 mục **Phải sửa**. |

## 1. Tổng quan theo người

| Người | Spec | Phải sửa | Nên sửa | Gợi ý | Mức sẵn sàng |
|---|---|---|---|---|---|
| Ha | S-F00-01 (+M-F00-01) | 1 | 4 | 7 | Gần xong |
| Ha | S-F00-02 | 1 | 8 | 4 | Gần xong |
| Ha | S-F02-03 (+M-F02-03-01) | 3 | 7 | 4 | Còn nhiều |
| Linh | S-F00-03 | 0 | 7 | 6 | Gần xong |
| Linh | S-F04-01 | 2 | 9 | 1 | Còn nhiều |
| Linh | S-F03-01 | 4 | 4 | 3 | Còn nhiều |
| Hoa | S-F02-01 (+M-F02-01-01, M-F02-01-02) | 2 | 10 | 4 | Còn nhiều |
| Hoa | S-F02-02 | 5 | 4 | 2 | Còn nhiều |
| Hoa | S-F02-04 (+M-F02-04-01) | 2 | 4 | 3 | Trung bình |
| Nhi | S-F01-01 | 3 | 6 | 3 | Trung bình |
| Nhi | S-F01-02 | 5 | 5 | 2 | Còn nhiều |
| Nhi | S-F03-03 | 3 | 6 | 4 | Trung bình |
| Trieu | S-F03-02 | 6 | 7 | 4 | Còn nhiều |
| Trieu | S-F03-06 | 5 | 7 | 3 | Còn nhiều |
| Trieu | S-F03-07 | 5 | 7 | 3 | Còn nhiều |

## 2. Lỗi lặp lại ở nhiều spec (nhắc cả nhóm)

1. **Số thứ tự thành phần ở §3 không khớp ảnh đánh số** — S-F01-01, S-F01-02, S-F03-01, S-F03-02, S-F03-06, S-F03-07. Đánh lại §3 theo đúng số trên `<ID>-numbered.png`.
2. **Tự viết câu thông báo thay vì dùng đúng MSG trong ui-conventions** — S-F00-02, S-F02-01, S-F02-02, S-F02-04, S-F03-02, S-F03-06. Đặc biệt lỗi mạng phải là MSG-04 nguyên văn «Không tải được trang. Bạn kiểm tra kết nối mạng rồi thử lại.» + nút «Thử lại».
3. **Thiếu trạng thái lỗi mạng / FR-04-20** dù screen-list đã giao cho màn — S-F01-02, S-F03-01, S-F03-06 (và S-F03-03 đang ghi "provisional").
4. **Ghi kết luận tạm như thể đã chốt** trong khi câu hỏi ở §9 còn mở (hoặc tự đóng câu hỏi cần cả nhóm chốt) — S-F00-01, S-F00-02, S-F02-03 (Q3, Q4), S-F03-02 (Q4), S-F03-07 (SR-006).
5. **Rác do công cụ AI để lại** — S-F02-02 và S-F02-04 còn khoảng 50 dấu `[cite: n]`; S-F03-02, S-F03-06, S-F03-07 có link tới máy cá nhân `file:///C:/Users/admin/.gemini/…`.
6. **Lệch template của thầy** — đổi tên cột, mã quy tắc kiểu `SR-F03-0x-00x` thay vì `SR-001`, checklist cuối bị viết lại, câu hỏi mở thiếu nhãn `[NEEDS CLARIFICATION]`, có thêm mục ngoài template.
7. **Chi tiết kỹ thuật lẫn vào spec** (tên class CSS, aria, "database", "backend") — S-F03-02, S-F03-06, S-F03-07. Spec chỉ ghi CÁI GÌ, không ghi LÀM THẾ NÀO.
8. **Modal M-F00-01 dẫn sai chỗ / thiếu nhánh "Để sau" và quay lại sau đăng nhập** — S-F01-01, S-F03-03.

## 3. Câu hỏi của cả nhóm — ĐÃ CHỐT ngày 22/11/2026

Các spec và tài liệu chung ghi nguồn là "Group decision 22/11/2026 (Chi)".

| # | Câu hỏi | Đã chốt | Spec / tài liệu kéo theo |
|---|---|---|---|
| 1 | Bấm «Huỷ» hoặc đăng nhập giữa chừng: giữ hay bỏ thao tác đang chờ? | **Giữ.** Sau khi nhập đúng mã, bạn đọc về lại màn xuất phát và thao tác (lưu sách, đăng/báo cáo đánh giá…) tự làm tiếp | S-F00-01, S-F00-02, AD-UC-04, screen-transition |
| 2 | Che bớt email trên màn nhập mã OTP? | **Không che** | S-F00-02 |
| 3 | S-F02-03 hiện những sách nào? | **Sách bản giấy chưa từng được in nhãn** (sách mới từ lần đồng bộ gần nhất sẽ nằm đây đến khi in). Hệ thống ghi nhận sách đã in. Giữ dấu tick khi sang trang + dòng «Đã chọn n sách»; 20 dòng/trang; sắp theo tầng → phòng → kệ | S-F02-03, AD-UC-10, FR-02-23 (mới), FR-02-08 (sửa) |
| 4 | Nội dung nhãn QR | **Đã chốt nội dung:** QR bên trái; tên sách (≤ 2 dòng), «Tầng · Phòng · Kệ», dòng «Quét để xem thông tin và đánh giá»; **1 nhãn cho mỗi đầu sách**. **Khổ giấy: A4 dọc, decal 3 cột × 8 hàng = 24 nhãn 70×37 mm** | S-F02-03, M-F02-03-01, ui-conventions |
| 5 | Nút Back trên S-F02-02 | **Không có Back.** Chỉ mở được bằng camera quét QR trên sách; lối ra là «Xem sách này trên OPAC» | S-F02-02, ui-conventions §3, screen-transition |
| 6 | «Xem thêm đánh giá» trên S-F02-02 | **Có**, 10 đánh giá/lần như S-F02-01 | S-F02-02, AD-UC-06 |
| 7 | Đăng xuất cho nhân viên; phiên nhân viên | **Có nút «Đăng xuất»** trên các màn Staff → S-F00-03. Phiên **không tự hết hạn**, chỉ kết thúc khi bấm đăng xuất | S-F04-01, S-F02-03, S-F02-04, S-F00-03, FR-04-21 (mới) |
| 8 | Màn hình hẹp hơn khổ thiết kế | **Bổ sung mục responsive vào ui-conventions.** Reader: thiết kế 360px, dùng được từ 320px, màn rộng thì 1 cột tối đa 640px căn giữa. Staff: thiết kế 1280px, hỗ trợ từ 1024px; dưới 1024px hai cột xếp chồng; không hỗ trợ điện thoại | ui-conventions, S-F00-03, S-F04-01 |
| 9 | S-F03-01: sách có cả hai hình thức; phân trang | **Hiện cả 2 nhãn; có phân trang** (20/trang) | S-F03-01 |
| 10a | Nhãn «Xu hướng» trên sách bổ sung ở S-F03-07 | **Có gắn** (thành phần mới "Trend tag") | S-F03-07, ui-conventions §3 |
| 10b | Nút «Sở thích» trên S-F03-07 | **Luôn hiện** ở mọi trạng thái đã đăng nhập | S-F03-07, screen-transition |
| 11 | Hiện lý do gợi ý từng sách | **Không** ở bản 1 | S-F03-07 |
| 12 | Khi nào sách được ghi nhận là đã in nhãn? | **Chỉ khi nhân viên bấm «Đã in xong»** trong khung xem trước M-F02-03-01 (nút chính mới, cạnh «In» / «Đóng»). Bấm «Đóng» hoặc in bị lỗi thì không ghi nhận gì, sách vẫn nằm trong danh sách S-F02-03. Ha cần vẽ thêm nút «Đã in xong» | S-F02-03, M-F02-03-01, AD-UC-10, FR-02-08 (sửa câu chữ), ui-conventions |
| 13 | Một đầu sách có bản nằm ở nhiều kệ | Nhãn và thứ tự sắp xếp dùng **vị trí kệ chính do lần đồng bộ trả về** — cùng vị trí hiện ở S-F01-01 | S-F02-03, M-F02-03-01, AD-UC-10, FR-02-23, ui-conventions |
| 14 | S-F03-01: đổi hình thức truy cập thì đang ở trang nào? | **Về lại trang 1** của kết quả | S-F03-01 |
| 15 | Câu chữ nhóm tài liệu đề xuất | **Duyệt:** trạng thái trống S-F02-03 «Tất cả sách bản giấy đã được in nhãn. Sách mới sẽ hiện ở đây sau lần đồng bộ danh mục tiếp theo.» · dòng email S-F00-02 «Mã đã được gửi tới <email>.» Bỏ chữ "đề xuất / cần xác nhận"; đưa vào câu chữ dùng chung | S-F02-03, S-F00-02, ui-conventions §4 (MSG-10, MSG-11) |
| 16 | Dòng «Đã chọn <n> sách» là thành phần gì? | Thành phần mới **"Selection counter"** (chữ hiển thị cạnh nút thao tác hàng loạt, đếm dấu tick ở mọi trang) | S-F02-03, ui-conventions §3 |

**Đã có câu trả lời trong tài liệu, đóng được ngay:** S-F04-01 Q2 (UC-13 trong phạm vi, mức Could — screen-list dòng 18, 32) · câu hỏi "có cần xuất HTML" ở S-F00-03/S-F04-01 (screen-spec-chung §4.1 chấp nhận .drawio) · S-F02-04 Q2 (AD-UC-14 Q1: không có ô lý do) · S-F02-04 Q3 (Hoa-screen-spec §3) · S-F02-01 Q6 (ui-conventions §1) · S-F03-03 câu chữ danh sách trống (ui-conventions §4) · S-F03-02 Q5 (v0.8 dùng Multi-select chips).

## 4. Phần ảnh và wireframe đã làm thay (22/11) — người phụ trách cần xem lại

| Người | Đã làm | Cần người đó làm |
|---|---|---|
| Hoa | Dựng lại wireframe HTML `src/S-F02-01.html`, `S-F02-02.html`, `S-F02-04.html` theo đúng bản vẽ, dùng `tokens.css`; xuất đủ 26 ảnh trạng thái + 3 ảnh modal; notes lên v0.8 | So ảnh mới với bản vẽ của mình. Ảnh cao hơn bản cũ vì chữ theo token 16px; màu đổi sang token. Chọn câu lỗi mạng: bản vẽ ghi «Không thể tải dữ liệu do lỗi kết nối.», spec ghi MSG-04 — sửa một bên cho khớp |
| Nhi | Cắt 11 ảnh trạng thái S-F03-01, S-F03-03 từ ảnh ghép; mục Mockup + bảng State → Image cho S-F01-01, S-F01-02, S-F03-01, S-F03-03 | Đưa mã nguồn wireframe vào `src/`. Sửa các lệch ở mục 5 |
| Trieu | Chuyển 24 ảnh từ `src/` sang `img/`; notes lên v0.8 | — |

## 5. Lệch giữa bản vẽ và spec (phát hiện khi làm ảnh)

**Hoa**
- S-F02-01 Error-3 và S-F02-02 Error-3: chưa vẽ trường hợp "không phải người viết". S-F02-02 Error-3 hiện lỗi hai lần (banner + dưới ô), trái ui-conventions §4 (lỗi ô chỉ hiện ngay dưới ô).
- Toast vẽ nằm trong danh sách, kèm dòng ghi chú «(Cũng dùng: …)»; ui-conventions: giữa đáy màn, tự ẩn sau 4 giây. Trạng thái trống thiếu icon.
- Notes S-F02-01 dòng Success nhắc «#91» (giống mã đánh giá, trái quy tắc không hiện ID). §9 Q6 còn trích tên tệp cũ `M02-01-01 notes.md`.
- S-F02-04: câu lỗi, bố cục lỗi (bản vẽ giữ danh sách, spec chỉ còn banner), kích thước ở §8 (32px/24px/44px) khác bản vẽ (24px/18px/34px), vị trí Toast; notes ghi FR-02-10 + FR-04-12 nhưng ảnh chỉ ghi FR-02-10. Ngày của đánh giá #91 là 15/11 ở S-F02-04 nhưng 12/11 ở S-F02-01.

**Nhi**
- `S-F01-02-states.png` bị lỗi: tiêu đề các ô bị khung che, ô "Map unavailable" thực ra là trạng thái chọn phòng. Trạng thái "Default — opened from a book" ở §4 không có ảnh.
- Ảnh riêng S-F01-01/02 là bản vẽ khác ảnh ghép (Kệ B-01 vs S-08; S-F01-02 -error không có bản đồ; -error-2 banner đỏ bị co lại).
- S-F03-03: ảnh "vị trí kệ không có" giống hệt Default; ảnh Success cho sách Digital Marketing Basics vị trí của sách khác. Cùng sách này là «Trực tuyến» ở S-F03-01 nhưng «Bản giấy» ở S-F03-03.
- S-F03-01-numbered.png có số trùng (1–4 xuất hiện hai lần); §3 thiếu banner lỗi và nút «Thử lại» (số 8, 9). Icon trạng thái trống và icon ghim vị trí hiện thành ô vuông.

**Chung**
- `tokens.css` còn ghi v0.7 và cỡ chữ tác giả 14px, trong khi ui-conventions v0.8 ghi 16px.

---

# Chi tiết từng spec

Mỗi bảng: **Mức** (Phải sửa / Nên sửa / Gợi ý) · **Bằng chứng** là số dòng trong spec và tài liệu đối chiếu · **Cách sửa đề xuất**.

## Phần của Ha

### Review S-F00-01 Sign in: library card number (kèm modal M-F00-01) — người viết: Ha

Tóm tắt: Gần sẵn sàng. Đủ 9 mục, đủ 5 trạng thái, và M-F00-01 được viết đầy đủ bên trong với 3 biến thể câu chữ (MSG-01/02/03) đúng nguyên văn. Còn một mâu thuẫn phải sửa: việc bấm «Huỷ» có giữ lại thao tác đang chờ hay không. Ngoài ra cần ghi thêm nhãn ô nhập và làm sạch mục 8.

| # | Mức | Mục | Vấn đề | Bằng chứng | Cách sửa đề xuất |
|---|---|---|---|---|---|
| 1 | **Phải sửa** | §5, §6, §9 | Spec đã chọn sẵn đáp án "giữ lại thao tác đang chờ" khi bấm «Huỷ», trong khi chính câu hỏi này vẫn đang mở ở §9. Một kết luận tạm đang được viết như thể nhóm đã chốt. | Dòng 109 "Preserve the pending context"; SR-004 dòng 121 "Preserve the sign-in origin and requested action through OTP and Cancel"; dòng 147 Q-Cancel "should the origin retain or discard the pending action?" còn Open. screen-spec-chung §5 (hàng mục 9) coi "ghi kết luận tạm như thể đã chốt" là lỗi. | Ở §5 dòng 3 và SR-004 chỉ giữ phần chắc chắn: "«Huỷ» đưa bạn đọc về màn xuất phát (L8-01)". Việc giữ hay bỏ thao tác đang chờ để ở Q-Cancel, kèm phương án đang vẽ, cho đến khi nhóm chốt. |
| 2 | Nên sửa | §7 | FR-04-16 (không gửi được mã) được liệt kê, nhưng màn này không hiển thị gì cho FR đó. Lỗi gửi mã là trạng thái của S-F00-02. | Dòng 133; screen-list.md dòng 53 ("Error state of S-F00-02 (FR-04-16)"); AD-UC-11 §5. | Bỏ FR-04-16 khỏi §7, hoặc ghi rõ "chỉ chuyển sang S-F00-02, không hiển thị ở màn này". |
| 3 | Nên sửa | §3 #2 | Nhãn ô nhập «Số thẻ thư viện» có trên ảnh nhưng không được ghi ở §3. | Dòng 53; ảnh S-F00-01-numbered.png (nhãn phía trên ô #2); screen-spec-chung §5: cột Content ghi đúng nguyên văn chữ tiếng Việt; ui-conventions §5 "Every input has a visible label". | Thêm vào cột Content: Nhãn «Số thẻ thư viện». |
| 4 | Nên sửa | §3 #2 (Validation) | Quy tắc chưa đủ để kiểm đạt/không đạt: không nói kiểm tra lúc nào (khi bấm «Gửi mã» hay khi rời ô), và trỏ tới "the inline message in the image" thay vì ghi câu thông báo. Cũng không nhắc bàn phím số trên điện thoại. | Dòng 53; ui-conventions §2 dòng 97 và §3 dòng 130 (Text input: 7 chữ số, bàn phím số). | Viết lại: "Kiểm tra khi bấm «Gửi mã». Không đủ 7 chữ số thì hiện #5 «Số thẻ thư viện gồm 7 chữ số. Bạn kiểm tra lại nhé.» và không tra thẻ. Trên điện thoại mở bàn phím số." |
| 5 | Nên sửa | §8 | Có câu chép nhầm từ màn in nhãn ("Print is a browser-controlled exit"), dù màn này không có chức năng in. Bốn gạch đầu dòng không dùng 4 nhãn của mẫu, và có thuật ngữ kỹ thuật "DOM order". | Dòng 140–141; mẫu thầy §8 (Smallest supported width / What collapses or stacks / Information never carried by colour alone / Text contrast and minimum size). | Viết lại theo đúng 4 nhãn của mẫu. Bỏ câu về in. Thay "DOM order" bằng "thứ tự đọc và thứ tự di chuyển bằng bàn phím theo cột #". |
| 6 | Gợi ý | §3 #1 | Ở ui-conventions, "Screen header" gồm nút Quay lại và tiêu đề. Ảnh màn này lại không có nút Quay lại (việc trở về do «Huỷ» đảm nhận). Spec chưa nói rõ điều này, nên người lập trình có thể tự thêm nút Quay lại. | Dòng 52; ui-conventions §3 dòng 125; ảnh S-F00-01-numbered.png. | Ghi ở #1: "Không có nút Quay lại; «Huỷ» (#4) đảm nhận việc trở về." |
| 7 | Gợi ý | §3 cột Required | #8 «Thử lại» ghi Required = Yes, dù nút này chỉ xuất hiện ở trạng thái lỗi mạng. Các thành phần cũng chỉ xuất hiện theo trạng thái (#5–#7) đều ghi No. | Dòng 56–59. | Thống nhất: các thành phần chỉ xuất hiện theo trạng thái ghi No (hoặc "Theo trạng thái"). |
| 8 | Gợi ý | §4 Loading | Ảnh trạng thái đang tải cho thấy «Huỷ» vẫn bấm được, nhưng spec không nói bấm «Huỷ» lúc đang tra thẻ thì điều gì xảy ra. | Dòng 86; ảnh S-F00-01-loading-numbered.png. | Thêm một câu: «Huỷ» vẫn dùng được và đưa về màn xuất phát (hoặc bị khoá, tuỳ nhóm chọn). |
| 9 | Gợi ý | §1 | "Shown when" viết "requests a protected action". Thực ra màn này mở khi bạn đọc bấm «Đăng nhập» trong M-F00-01, hoặc bấm link "Sign in" trên trang OPAC. | Dòng 20; screen-list.md dòng 10 (Entry points). | Sửa câu theo đúng hai điểm vào trong screen-list. |
| 10 | Gợi ý | Bảng đầu tệp (Feature) | "F-00 shared sign-in" là tên tự đặt. F-00 chỉ là nhóm màn của screen-list và không có trong W0 Table 2. Các FR của màn này thuộc F-04. | Dòng 9; function-list W0 Table 2. | Ghi: "F-00 (Screen List grouping; FRs belong to F-04 Platform, Access & Operations)". |
| 11 | Gợi ý | M-F00-01 so với ui-conventions | ui-conventions viết "A modal never navigates", nhưng nút «Đăng nhập» của M-F00-01 lại mở S-F00-01 (đúng theo screen-list và L8-01). Lỗi này không nằm ở spec mà ở hai tài liệu chung đang vênh nhau. | ui-conventions §3 Rules dòng 165; screen-list.md dòng 40. | Nhắn Linh thêm ngoại lệ cho M-F00-01 vào ui-conventions §3. |
| 12 | Gợi ý | Câu chữ dùng chung | Câu từ chối «Không thể đăng nhập. Bạn kiểm tra thông tin rồi thử lại.» gần giống câu của S-F00-03 («…thông tin tài khoản…») nhưng chưa có mã MSG. | Dòng 87; screen-spec-S-F00-03.md dòng 63. | Đề nghị Linh đưa hai câu này vào bảng "Shared wording" của ui-conventions §4, để hai màn đăng nhập dùng thống nhất. |

#### Câu hỏi mở

| Câu hỏi | Tài liệu đã trả lời chưa? | Cần nhóm quyết? |
|---|---|---|
| Q-Cancel (dòng 147): khi bấm «Huỷ», giữ hay bỏ thao tác đang chờ? | **Mới trả lời một phần.** screen-transition.md dòng 102–106 và L8-01 (activity-index dòng 76) đã chốt việc «Huỷ» đưa bạn đọc về màn xuất phát. Theo AD-UC-04 dòng 73–76, sau bước "Sign in (UC-11)" luồng quay lại bước kiểm tra phiên (`m0` → `d0`). Nếu vẫn chưa đăng nhập, yêu cầu bị từ chối (`s1`) và bạn đọc lại được hỏi "Sign in now?" (`d1`), tức là M-F00-01 hiện lại. Không tài liệu nào nói rõ có muốn hỏi lại như vậy hay không. | **Có.** Nhóm cần chọn một trong hai: (a) về màn xuất phát và yêu cầu kết thúc, giống «Để sau»; hoặc (b) về màn xuất phát và hỏi lại M-F00-01 như AD vẽ. Không chặn. Câu này trùng với Q-Cancel của S-F00-02, nên trả lời một lần cho cả hai. |

### Review S-F00-02 Verify email OTP — người viết: Ha

Tóm tắt: Khá đầy đủ. Đủ 9 mục, đủ 5 biến thể lỗi (mỗi biến thể có FR), các FR của screen-list đều có ở §7 và đều được thực hiện trên màn. Trước khi duyệt cần sửa: loại thành phần của #3 bị ghi sai, thiếu nguyên văn câu thông báo, chưa có quy tắc khi nhập mã sai định dạng, và §8 có nội dung chép nhầm.

| # | Mức | Mục | Vấn đề | Bằng chứng | Cách sửa đề xuất |
|---|---|---|---|---|---|
| 1 | **Phải sửa** | §3 #3 | "Validity" ghi Type = "Code input" (ô nhập mã). Trên ảnh đây chỉ là dòng chữ hướng dẫn «Mã có hiệu lực trong 5 phút.» (MSG-09), không phải ô nhập. Đọc spec, người lập trình sẽ dựng thêm một ô nhập thứ hai. | Dòng 51; ảnh S-F00-02-numbered.png (#3 là dòng chữ); ui-conventions §3 dòng 131 ("Code input: One field"). | Đổi Type thành "Text" (mẫu thầy cho phép), Content = MSG-09 «Mã có hiệu lực trong 5 phút.» |
| 2 | Nên sửa | §3 #4 (Validation) | Câu "server verifies value…" là chi tiết cách xây dựng. Spec cũng chưa nói nhập thiếu hoặc thừa chữ số, hay nhập chữ cái, rồi bấm «Đăng nhập» thì sao. Hiện chưa có câu thông báo (MSG) nào cho trường hợp này. | Dòng 52; FR-04-04 (mã 6 chữ số); ui-conventions §2 dòng 98, §3 dòng 131 (bàn phím số). | Ghi quy tắc nghiệp vụ, ví dụ: "Chỉ nhận chữ số, tối đa 6. «Đăng nhập» chỉ bấm được khi đủ 6 chữ số." Nếu nhóm muốn có câu báo lỗi thì ghi [NEEDS CLARIFICATION] ở §9, không tự đặt câu mới. |
| 3 | Nên sửa | §3 #8, #9 | Cột Content ghi mô tả ("Attempts left (4 to 1)"; "Invalidated, expired / used, send failure, or MSG-04") chứ không ghi nguyên văn câu hiển thị. | Dòng 56–57; ui-conventions §2 dòng 100: «Mã chưa đúng. Bạn còn `<n>` lần thử.» (n = 4…1). | #8: ghi mẫu câu «Mã chưa đúng. Bạn còn `<n>` lần thử.», với n từ 4 đến 1. #9: liệt kê đủ 4 câu (Error-2, Error-3, Error-4, MSG-04) đúng như §4. |
| 4 | Nên sửa | §3 #11 so với ảnh | #11 ghi Type = "Toast". Theo ui-conventions, Toast nằm ở giữa đáy màn, nền tối chữ trắng, tự ẩn sau 4 giây. Nhưng ảnh lại đặt «Đã gửi mã mới.» ở đầu nội dung, trong khối nền xám giống Banner. Spec và ảnh đang mô tả hai thành phần khác nhau. | Dòng 59; ui-conventions §3 dòng 152; ảnh S-F00-02-success-numbered.png. | Chọn một: giữ Toast (thì Ha sửa wireframe), hoặc đổi Type thành Banner loại success (thì sửa spec). |
| 5 | Nên sửa | §3 #3–#6, §6 | "During recovery" chưa được định nghĩa: không rõ là những trạng thái nào. Ảnh Error-2 và Error-4 còn cho thấy nhiều thay đổi mà spec không ghi: ô mã bị khoá, dòng MSG-09 (#3) biến mất, «Đăng nhập» thành nút phụ bị khoá, «Gửi mã mới» thành nút chính. | Dòng 53–54; ảnh S-F00-02-error-2-numbered.png, S-F00-02-error-4-numbered.png. | Thêm một quy tắc ở §6, ví dụ: "Ở Error-2, Error-3, Error-4: ẩn MSG-09; khoá ô mã và «Đăng nhập»; «Gửi mã mới» là nút chính." (Kiểm lại ảnh Error-3 cho khớp.) |
| 6 | Nên sửa | §6 SR-006 | Một quy tắc gộp hai việc không liên quan (không hiện email che bớt; Back/Cancel). Nguồn ghi là tệp phân việc cá nhân, không phải FR, AD, L8 hay ui-conventions. Ngoài ra quy tắc đã chốt "không hiện email" trong khi Q-Email ở §9 vẫn Open. | Dòng 98, 124; Ha-screen-spec.md dòng 46 (yêu cầu *giữ câu hỏi mở*, không quyết); screen-spec-chung §5 (hàng mục 6: Source = FR / nhánh AD / L8 / ui-conventions). | Tách thành hai quy tắc. Phần email ghi "theo phương án đang vẽ, chờ Q-Email". Phần Back/Cancel ghi nguồn screen-transition.md và L8-01. |
| 7 | Nên sửa | §6 SR-007 | "offer the appropriate recovery" là câu mơ hồ, không kiểm được đạt hay không đạt. | Dòng 99. | Ghi cụ thể: "Không gửi được mã → banner Error-4 và nút «Gửi mã mới»; lỗi mạng → MSG-04 và nút «Thử lại»; mã đã nhập được giữ lại." |
| 8 | Nên sửa | §3 #4 | Nhãn ô nhập «Mã xác thực» có trên ảnh nhưng không được ghi ở §3. | Dòng 52; ảnh S-F00-02-numbered.png; ui-conventions §5 (input phải có nhãn). | Thêm vào cột Content: Nhãn «Mã xác thực». |
| 9 | Nên sửa | §8 | Gạch thứ 4 nói về hộp thoại và "Print is a browser-controlled exit", trong khi màn này không có hộp thoại và không có chức năng in (chép nhầm từ màn khác). §8 cũng không dùng 4 nhãn của mẫu, và có thuật ngữ "DOM order". | Dòng 117–118; mẫu thầy §8. | Viết lại theo 4 nhãn của mẫu. Bỏ câu về hộp thoại và in. |
| 10 | Gợi ý | §4 Loading | Mới nói trạng thái chờ khi kiểm mã. Khi bấm «Gửi mã mới», màn cũng phải chờ gửi mã. | Dòng 68. | Bổ sung "hoặc đang gửi mã mới" vào Trigger. |
| 11 | Gợi ý | §5 #4 | Sau khi gửi mã mới, ảnh cho thấy ô mã được xoá trống. Theo FR-04-17 (giới hạn 5 lần sai là tính cho từng mã), số lần thử cũng phải tính lại từ đầu. Spec chưa ghi cả hai điều này. | Dòng 86; ảnh S-F00-02-success-numbered.png; FR-04-17. | Thêm vào System response: "Xoá ô mã; số lần thử tính lại từ 5 cho mã mới." |
| 12 | Gợi ý | §7 FR-04-12 | Ghi nhật ký là việc chạy ngầm, không hiển thị trên màn. | Dòng 111; screen-list.md dòng 101. | Giữ cũng được, nhưng ghi rõ "(background, nothing shown)". |
| 13 | Gợi ý | §3 cột Required | #12 «Thử lại» ghi Yes dù chỉ hiện khi lỗi mạng; #8–#11 ghi No. | Dòng 60. | Thống nhất cách ghi cho các thành phần chỉ xuất hiện theo trạng thái. |

#### Câu hỏi mở

| Câu hỏi | Tài liệu đã trả lời chưa? | Cần nhóm quyết? |
|---|---|---|
| Q-Email (dòng 124): có hiện địa chỉ email đã che bớt không? | **Chưa.** FR-04-01 và FR-04-04 chỉ nói gửi mã tới email đăng ký trên thẻ, không nói có hiển thị email hay không. AD-UC-11 và ui-conventions cũng không nhắc. | **Có.** Không chặn. Phương án đang vẽ là không hiện. Nếu nhóm chọn hiện thì cần thêm thành phần trên wireframe và cách che (ví dụ «a***@gmail.com»). |
| Q-Cancel (dòng 125): khi «Huỷ» thì thao tác đang chờ xử lý thế nào? | **Mới trả lời một phần,** giống Q-Cancel của S-F00-01. screen-transition.md dòng 102–106 và L8-01 đã chốt việc quay về màn xuất phát. AD-UC-04 dòng 73–76 cho thấy sau bước đăng nhập luồng quay lại kiểm tra phiên, nên nếu chưa đăng nhập thì M-F00-01 sẽ hiện lại. | **Có.** Chốt một lần cho cả S-F00-01 và S-F00-02, rồi trỏ về một chỗ (S-F00-01 §9). |
| (Mới, nên thêm vào §9) Nhập mã không đủ 6 chữ số thì báo gì, hay khoá nút? | **Chưa.** ui-conventions §2 chỉ có câu báo cho số thẻ, không có câu báo cho mã. | **Có.** Không chặn. |

### Review S-F02-03 QR code label printing (kèm modal M-F02-03-01) — người viết: Ha

Tóm tắt: Cấu trúc đủ 9 mục, modal được viết bên trong đúng cách, các FR-02-08/17/18 đều có ở §7 và đều được thực hiện trên màn. Chưa nên duyệt vì: Q3/Q4 được đóng chỉ bằng xác nhận của một người trong khi ui-conventions vẫn để mở; các câu cảnh báo/lỗi của FR-02-18 chưa được ghi nguyên văn (và hai chỗ trên ảnh đang ghi khác nhau); một dòng tương tác chép nhầm; dữ liệu mẫu tự mâu thuẫn.

| # | Mức | Mục | Vấn đề | Bằng chứng | Cách sửa đề xuất |
|---|---|---|---|---|---|
| 1 | **Phải sửa** | §9 Q3, Q4; §6 SR-006, SR-007 | Q3 (cách tìm sách, Blocking) và Q4 (nội dung nhãn, số nhãn mỗi trang) được ghi "Closed 21/11/2026: Confirmed by Ha". Theo hướng dẫn chung, hai câu này phải **cả nhóm** chốt. Trong khi đó ui-conventions v0.8 (cùng ngày 21/11) vẫn ghi Label sheet là [NEEDS CLARIFICATION] (2×5 hay 3 cột) và "Group decision required". Hai tài liệu đang mâu thuẫn nhau. | Dòng 121–122, 148–149; screen-spec-chung §6 bảng Q1–Q5 và §7 ("21/11 Họp chốt Q1–Q5, Cả nhóm"); Ha-screen-spec.md dòng 49–50 ("phải được nhóm chốt"); ui-conventions §3 dòng 155, §7 câu hỏi mở 2 (dòng 387). | Nếu nhóm đã họp: ghi "Closed <ngày>: nhóm chốt …" và nhắn Linh cập nhật ui-conventions §3 và §7. Nếu chưa: để Open, kèm "phương án đang vẽ". SR-006 và SR-007 khi đó ghi nguồn là "phương án đang vẽ, chờ Q3/Q4". |
| 2 | **Phải sửa** | §3 #9, §3.1 #5, §4 (Error — all lack QR, Warning) | Các câu hiển thị cho FR-02-18 không được ghi nguyên văn ở bất kỳ đâu; §4 chỉ mô tả bằng tên sách mẫu. Trên ảnh lại có hai cách viết khác nhau: trên màn là «Không in nhãn cho **các** sách chưa có mã QR:» kèm danh sách, trong modal là «Không in nhãn cho sách chưa có mã QR: Modern Business Ethics.». Trường hợp không sách nào có QR có thêm «Không tạo được trang nhãn.». Spec cũng không nói đây là Banner loại nào (cảnh báo hay lỗi). | Dòng 61, 74, 84, 86; ảnh S-F02-03-warning-numbered.png, S-F02-03-error-2-numbered.png, S-F02-03-success.png. | Ghi nguyên văn vào #9, #5 và §4. Thống nhất một câu cho cả hai chỗ (sửa ảnh theo). Ghi rõ loại: Banner warning khi chỉ một phần sách bị bỏ ra, Banner error khi tất cả bị bỏ ra. |
| 3 | **Phải sửa** | §5 dòng 5 | Dòng 5 «In nhãn» chép nguyên System response của dòng 4 (tạo trang nhãn, ghi nhật ký, mở M-F02-03-01), nhưng cột "Goes to" lại là S-F00-03. Cùng một dòng nói hai điều trái nhau. | Dòng 107 so với dòng 106. | User action: "Bấm «In nhãn» khi phiên nhân viên đã hết". System response: "Không tạo trang nhãn; mở S-F00-03 (FR-04-08)". |
| 4 | Nên sửa | Dữ liệu mẫu ở §4 và §3.1 | Ảnh mặc định của modal có nhãn cho "Modern Business Ethics", nhưng §4 Warning và Error-2 lại nói chính cuốn này chưa có mã QR nên bị bỏ ra. Người kiểm thử sẽ không biết bộ dữ liệu nào đúng. | Dòng 92 (M-F02-03-01 › Default "three labels"); ảnh M-F02-03-01-numbered.png; dòng 84, 86. | Dùng một cuốn khác cho ảnh mặc định của modal, hoặc ghi rõ đó là bộ dữ liệu khác (mọi sách đều có QR). |
| 5 | Nên sửa | §4 Warning so với Success | Không rõ danh sách sách bị bỏ ra hiện ở đâu: trên màn (#9, ảnh warning), trong modal (§3.1 #5), hay cả hai (ảnh success cho thấy cả hai cùng lúc). Cũng không rõ trạng thái Warning xảy ra trước hay sau khi modal mở. | Dòng 61, 74, 86–87, 96; ảnh S-F02-03-warning-numbered.png, S-F02-03-success.png. | Viết rõ trình tự ở §5 dòng 4, ví dụ: "Bấm «In nhãn» → banner #9 (warning) trên màn **và** modal mở với #5" hoặc chỉ một trong hai. Tránh để danh sách hiện trùng mà không có lý do. |
| 6 | Nên sửa | §6 SR-006 | "newly synced physical books, newest first, with pagination" chưa kiểm được đạt hay không đạt. Không nói "mới đồng bộ" là trong bao lâu (lần đồng bộ gần nhất, hay N ngày), mỗi trang bao nhiêu sách (ảnh có 4), và sách cũ cần in lại nhãn (nhãn rách, mất) có tìm được không. | Dòng 121; ảnh S-F02-03-numbered.png, S-F02-03-page-2.png. | Ghi các con số cụ thể. Phần nào chưa có đáp án thì đưa vào §9 (xem Câu hỏi mở). |
| 7 | Nên sửa | §3 #5 | Hai nút «Trang trước» / «Trang sau» bị gộp vào một dòng, và không nói khi nào nút bị khoá. Trên ảnh, nút «Trang trước» nhạt ở trang 1 và «Trang sau» nhạt ở trang cuối. | Dòng 58; ảnh S-F02-03-numbered.png, S-F02-03-page-2.png. | Tách thành hai dòng, hoặc thêm: "«Trang trước» khoá ở trang đầu; «Trang sau» khoá ở trang cuối." |
| 8 | Nên sửa | §5 dòng 8 | Nút «Đóng» được gắn với AD-UC-10 `a4` ("Receive the printable QR label sheet"). Thực ra `a4` là lúc modal mở, tức thuộc dòng 4. "Goes to" ghi S-F02-03, trong khi người dùng vẫn ở nguyên màn này. | Dòng 110; AD-UC-10 §2 (a4); screen-list.md dòng 178. | Gắn a4 vào dòng 4. Dòng 8 ghi "Goes to: stays". |
| 9 | Nên sửa | §8 | Dùng thông số của màn bạn đọc ("16px input text", "Reader targets are at least 44 × 44px") cho một màn nhân viên. Có thuật ngữ "DOM order". Không theo 4 nhãn của mẫu. | Dòng 139–141; ui-conventions §6 dòng 268, 272 (Staff: control 40px, nhãn/nút 14px, tiêu đề 24px). | Viết lại theo 4 nhãn với thông số Staff. |
| 10 | Nên sửa | §6 SR-004 | Đây là một ca kiểm thử (3 sách, 1 thiếu QR → 2 nhãn), không phải quy tắc màn hình luôn phải giữ. SR-003 đã nêu quy tắc này rồi. | Dòng 119; screen-spec-chung §5 (hàng mục 6). | Bỏ SR-004, hoặc chuyển thành ví dụ ở §4 Warning. |
| 11 | Gợi ý | §3 | Số # nhảy từ 6 sang 8 (không có #7). Số này khớp với tệp ghi chú, nhưng người đọc dễ nghĩ là thiếu một thành phần. | Dòng 59–60; S-F02-03-notes.md dòng 14–15. | Thêm một câu dưới bảng: "#7 không dùng (giữ số theo tệp ghi chú)". |
| 12 | Gợi ý | §3.1 #2 (nội dung nhãn) | Mỗi nhãn chỉ ghi một dòng vị trí kệ. Nhưng ui-conventions §2 quy định vị trí kệ là "one line per physical copy", còn FR-02-07 nói mã QR gắn với "physical book". Chưa rõ in một nhãn cho mỗi đầu sách hay cho mỗi bản sao, và nhãn ghi gì khi sách chưa có vị trí kệ (FR-01-07). | Dòng 71; ui-conventions §2 dòng 101; FR-02-07, FR-01-07. | Đưa vào §9 thành [NEEDS CLARIFICATION]. |
| 13 | Gợi ý | §5 dòng 7 | Không nói sau khi hộp thoại in của trình duyệt đóng thì nhân viên ở đâu: modal còn mở hay đã đóng. | Dòng 109. | Thêm một câu, ví dụ: "Sau khi hộp thoại in đóng, modal vẫn mở; nhân viên bấm «Đóng» để quay lại danh sách." |
| 14 | Gợi ý | §7 FR-04-12 | Ghi nhật ký in nhãn là việc chạy ngầm, không hiển thị trên màn. | Dòng 134; screen-list.md dòng 101. | Ghi rõ "(background, nothing shown)". |

#### Câu hỏi mở

| Câu hỏi | Tài liệu đã trả lời chưa? | Cần nhóm quyết? |
|---|---|---|
| Q3 (dòng 148): nhân viên tìm sách để in nhãn bằng cách nào? Đang ghi Closed, xác nhận bởi Ha. | **Chưa được nhóm chốt.** screen-spec-chung §6 ghi Q3 là Blocking và phải họp nhóm chốt. Không thấy biên bản nhóm. AD-UC-10 chỉ nói "Select physical books on the staff page". | **Có,** và **chặn** việc chuyển Status sang Reviewed (Ha-screen-spec.md dòng 49–50). Khi chốt cần thêm: khoảng thời gian tính là "mới đồng bộ", số sách mỗi trang, có cho tìm sách cũ để in lại không. |
| Q4 (dòng 149): nội dung nhãn và số nhãn mỗi trang A4? Đang ghi Closed, xác nhận bởi Ha. | **Mới trả lời một phần.** AD-UC-10 câu hỏi 3 đã chốt khổ A4, còn bố cục "set in Lesson 8". ui-conventions §3 dòng 155 và §7 câu hỏi mở 2 vẫn ghi "Group decision required" (2×5 hay 3 cột). | **Có.** Không chặn spec, nhưng phải được nhóm chốt và cập nhật ui-conventions cho khớp. |
| Q-Selection (dòng 150): sách đã tick có được giữ khi chuyển trang không? | **Chưa.** Không tài liệu nào nói. Câu này ảnh hưởng tới FR-02-17 (nếu mất lựa chọn khi chuyển trang thì có thể rơi vào lỗi "chưa chọn sách"). | **Có.** Không chặn. Phương án đang vẽ: chỉ tính các sách tick trên trang đang xem. |
| (Mới, nên thêm vào §9) In một nhãn cho mỗi đầu sách hay cho mỗi bản sao? Sách chưa có vị trí kệ thì nhãn ghi gì? | **Chưa.** FR-02-07 viết "physical book"; ui-conventions §2 ghi vị trí kệ theo từng bản sao. | **Có.** Không chặn spec, nhưng cần rõ trước khi làm DBIZ3. |

## Phần của Linh

### Review S-F00-03 Staff sign in — người viết: Linh (wireframe: Ha)

Tóm tắt: Nội dung nghiệp vụ đúng: một câu từ chối chung, cho thử lại, đăng nhập xong sang S-F04-01, đủ FR-04-07/08/18/20. Tuy vậy tệp vẫn còn nhiều phần "nháp làm việc" nằm ngoài mẫu: link ảnh GitHub, ghi chú bàn giao, Status tự đặt, checklist viết lại. Cột Validation ở §3 bị dùng để mô tả hành vi, và chưa có quy tắc khi để trống ô.

| # | Mức | Mục | Vấn đề | Bằng chứng | Cách sửa đề xuất |
|---|---|---|---|---|---|
| 1 | Nên sửa | §3 #2, #3 | Hai ô ghi "Required" nhưng không nói bỏ trống thì sao: hiện lỗi dưới ô (câu nào?) hay khoá nút «Đăng nhập». ui-conventions chưa có câu thông báo cho trường hợp này. Câu "no additional client-side format rule" còn dùng thuật ngữ kỹ thuật. | Dòng 59–60; ui-conventions §4 (không có MSG cho ô trống). | Ghi quy tắc nghiệp vụ cụ thể. Nếu cần câu thông báo mới thì ghi [NEEDS CLARIFICATION] ở §9 và hỏi Ha, không tự đặt. Thay "client-side" bằng "trên màn hình". |
| 2 | Nên sửa | §3 #2, #3 | Nhãn ô «Tài khoản thư viện» và «Mật khẩu» có trên ảnh nhưng không được ghi ở §3. | Dòng 59–60; ảnh S-F00-03-numbered.png; screen-spec-chung §5 (Content = chữ tiếng Việt nguyên văn). | Thêm nhãn vào cột Content. |
| 3 | Nên sửa | §3 #4–#8 (Validation) | Cột Validation đang chứa hành vi. Ví dụ #5 "Submits the internal staff account…", #6 "Show the generic rejection…", #7 "Display while…". Đây không phải quy tắc kiểm tra dữ liệu nhập. | Dòng 61–65; mẫu thầy §3; screen-spec-chung §5 (mọi ô nhập có quy tắc hoặc ghi `none`). | Thành phần không phải ô nhập thì ghi "none". Chuyển phần hành vi sang §5 hoặc §6. |
| 4 | Nên sửa | §4 Error, §5 #3 | Ảnh trạng thái lỗi cho thấy sau khi bị từ chối thì ô «Mật khẩu» bị xoá trống còn tài khoản được giữ lại. Spec không ghi điều này. Spec chỉ nói giữ tên tài khoản khi lỗi mạng. | Dòng 74, 83; ảnh S-F00-03-error-numbered.png. | Thêm vào §5 #3 hoặc một quy tắc ở §6: "Bị từ chối: giữ tài khoản, xoá mật khẩu." |
| 5 | Nên sửa | Bảng đầu tệp (Status) | "Draft — pending v0.8 mockup correction and review" không phải giá trị hợp lệ. Mẫu chỉ cho Draft hoặc Reviewed. | Dòng 12; mẫu thầy dòng 18; screen-spec-chung §5 (Status). | Ghi "Draft". |
| 6 | Nên sửa | §2 và cuối tệp | Tệp còn ảnh nhúng từ link GitHub bên ngoài thư mục, các ghi chú nháp và bàn giao (dòng 27–33, 48–50), và cả mục "Review handoff" sau checklist (dòng 145–150). Những phần này không có trong mẫu. Người đọc sau (và AI lập trình ở DBIZ3) sẽ không biết ảnh nào mới là chuẩn. | Dòng 27–50, 145–150; mẫu thầy §2 (`img/<Screen ID>.png`). | Giữ lại ảnh `img/S-F00-03.png`, ảnh đánh số và bảng State → Image. Chuyển các ghi chú quy trình sang pull request. |
| 7 | Nên sửa | §8 | Có 7 gạch đầu dòng, trong đó trùng nhau (dòng 111 và 112 cùng nói khổ 1280px), và không theo 4 nhãn của mẫu. | Dòng 111–117; mẫu thầy §8. | Viết lại theo 4 nhãn: khổ nhỏ nhất; phần nào xếp chồng khi hẹp (chờ câu hỏi 4); không dùng màu làm tín hiệu duy nhất; độ tương phản và cỡ chữ (Staff 14px nhãn/nút, 24px tiêu đề). |
| 8 | Gợi ý | §6 SR-003 | Nguồn ghi là FR-04-18 và L8-03, nhưng hai nguồn này chỉ yêu cầu "display an error message". Việc dùng *cùng một câu* và không cho biết lý do bị từ chối là quyết định trong ghi chú của Ha và trong tệp phân việc của Linh. | Dòng 94; S-F00-03-notes.md dòng 44; Linh-screen-spec.md dòng 25. | Thêm nguồn "S-F00-03-notes (default drawn)" để thấy đây là quyết định thiết kế, không phải câu chữ của FR. |
| 9 | Gợi ý | §6 SR-007 | Nguồn là hai tệp hướng dẫn cá nhân (Linh-screen-spec.md, Ha-wireframe-1.md). Theo screen-spec-chung, nguồn chỉ được là FR, nhánh AD, L8 hoặc ui-conventions. | Dòng 98; screen-spec-chung §5 (hàng mục 6). | Ghi lý do theo tài liệu chung: "No FR in W1; L8-02". |
| 10 | Gợi ý | §1 / §5 | Thiếu nhánh AD-UC-10 và AD-UC-13 `d1` [No]: nhân viên không thử lại nữa, rời đi và không vào được trang nhân viên. | AD-UC-10 §3 (dòng "d6 [No] → d1 [No]", ví dụ «lib.reader»). | Thêm một câu ở "leaves when": "Staff stop trying: no staff session, the staff page does not open." |
| 11 | Gợi ý | §3 #4 so với ghi chú | Spec đổi đúng #4 thành "Text button" (khớp ui-conventions §3 dòng 132, 158), nhưng tệp ghi chú của Ha vẫn ghi "Password input". | S-F00-03-notes.md dòng 12. | Nhắn Ha sửa tệp ghi chú cho khớp. |
| 12 | Gợi ý | §9 câu 1–3 | Ba câu này là việc nội bộ về ảnh và tệp xuất, không phải câu hỏi nghiệp vụ của màn hình. | Dòng 123–125. | Chuyển ra pull request hoặc danh sách việc của Ha. §9 chỉ giữ câu hỏi về hành vi màn hình. |
| 13 | Gợi ý | Completion checklist | Checklist 7 dòng của mẫu bị viết lại (thêm mục về ảnh, sửa câu chữ). | Dòng 132–140; mẫu thầy dòng 88–97. | Chép đúng checklist của mẫu và tick theo thực tế. |

#### Câu hỏi mở

| Câu hỏi | Tài liệu đã trả lời chưa? | Cần nhóm quyết? |
|---|---|---|
| 1. Có cần thêm bản xuất HTML không (dòng 123)? | **Đã trả lời.** screen-spec-chung §4 và §4.1 cho phép nguồn wireframe là HTML **hoặc** tệp `.drawio`. `src/Ha-wireframe-1.drawio` là đủ. | Không. Đóng câu hỏi. |
| 2. Ảnh Default/Loading/Error đã có chưa (dòng 124, NEEDS CLARIFICATION, Blocking)? | Đây là việc kiểm tra tệp ảnh, không phải câu hỏi nghiệp vụ. Hiện trong `img/` đã có S-F00-03.png, -loading, -error, -error-2 kèm bản đánh số. Chi soát ảnh riêng. | Không. Bỏ khỏi §9. |
| 3. Sửa màu draw.io và khổ 1280px (dòng 125, Blocking)? | Là việc của Ha, đã ghi ở ui-conventions §7 (bảng Consistency review). | Không. Bỏ khỏi §9. |
| 4. Bố cục màn nhân viên khi màn hình hẹp hơn 1280px (dòng 126)? | **Chưa rõ.** ui-conventions Q3 chốt khung Staff là 1280px, nhưng §5 lại ghi "Smallest supported width: 360px" áp cho mọi màn. Không tài liệu nào nói màn nhân viên co giãn ra sao. | **Có.** Không chặn. Linh (chủ ui-conventions) nên chốt chung cho cả 4 màn nhân viên. |
| (Mới, nên thêm) Để trống tài khoản hoặc mật khẩu rồi bấm «Đăng nhập» thì báo gì? | **Chưa.** FR-04-18 chỉ nói về thông tin bị hệ thống tài khoản từ chối. | **Có.** Không chặn. |

### Review S-F04-01 Staff page — người viết: Linh (wireframe: Ha)

Tóm tắt: Chưa sẵn sàng để duyệt. Phần chính đúng: 2 ô chức năng, đi đúng tới S-F02-03 và S-F02-04, MSG-04/MSG-05 đúng nguyên văn. Nhưng có hai điểm trái tài liệu chung: (1) "không có phiên nhân viên" bị xếp vào trạng thái Lỗi; (2) một câu hỏi được đánh là chặn trong khi tài liệu đã trả lời. Ngoài ra bảng §3, bảng đầu tệp và checklist lệch khỏi mẫu.

| # | Mức | Mục | Vấn đề | Bằng chứng | Cách sửa đề xuất |
|---|---|---|---|---|---|
| 1 | **Phải sửa** | §4 Error, §5 #4 | Trường hợp "không có phiên nhân viên → mở S-F00-03" đang được xếp vào trạng thái **Error** (Trigger: "…or invalid session"). Screen-list nói rõ đây không phải thông báo mà là chuyển màn, và tệp phân việc của chính Linh cũng ghi như vậy. | Dòng 69, 79; screen-list.md dòng 62 ("Not a message: the staff sign-in S-F00-03 opens instead"); Linh-screen-spec.md dòng 32–33 ("là điều hướng, ghi ở mục 6, không phải trạng thái lỗi"). | Bỏ phần phiên khỏi dòng Error (chỉ giữ MSG-04 và «Thử lại»). Việc chuyển sang S-F00-03 đã có ở SR-002, giữ nguyên. |
| 2 | **Phải sửa** | §3 #3, SR-004, §9 Q2, bảng đầu tệp | Spec coi ô «Đánh giá bị báo cáo» là chưa chắc có ("only if UC-13 is in the shipped scope") và đánh Q2 là **Blocking**. Thực ra tài liệu đã trả lời: UC-13 nằm trong phạm vi với ưu tiên Could, ô này là "phần Could trong màn Must" (bị cắt thì ô biến mất, màn vẫn giữ). | Dòng 57, 90, 119; screen-list.md dòng 18 (S-F02-04 Could) và dòng 32; W0 Table 1 có UC-13; FR-02-10/14/19/20 là Could trong W1 và **không** có trong danh sách cắt W0 Table 3; L8-04 (2 ô). | Đóng Q2 kèm trích dẫn. #3 ghi như thành phần bình thường (Required Yes, Priority Could). SR-004 viết lại: "Could part: if UC-13 is cut, the tile is removed and the screen stays (screen-list notes)". |
| 3 | Nên sửa | §3 #2, #3 | Dòng mô tả trong mỗi ô chức năng không được ghi: «Chọn sách bản giấy để in nhãn.» và «Xem và xử lý các đánh giá bị báo cáo.», cũng như biểu tượng. Theo ui-conventions, một Menu tile gồm biểu tượng, tiêu đề và một dòng mô tả. | Dòng 56–57; ảnh S-F04-01-numbered.png; ui-conventions §3 dòng 148. | Thêm dòng mô tả (nguyên văn) và biểu tượng vào cột Content. |
| 4 | Nên sửa | §3 tiêu đề cột, cột Required | Cột "Validation" của mẫu bị đổi tên thành "Validation / visibility". Cột Required ghi "Conditional" trong khi mẫu chỉ cho Yes/No. Nội dung cột thực chất là hành vi chuyển màn. | Dòng 53–60; mẫu thầy §3 (dòng 39–41). | Giữ đúng tên cột của mẫu. Required ghi Yes/No. Validation ghi "none" (màn này không có ô nhập). Chuyển phần chuyển màn sang §5. |
| 5 | Nên sửa | §6 SR-005, §7 FR-04-08 | Trạng thái đang tải (Loading) được gắn với FR-04-08, trong khi FR-04-08 là kiểm soát quyền truy cập. Một FR đang bị gán cho việc không liên quan. | Dòng 91, 100; FR-04-08 trong W1 ("deny the request… no valid session"). | Nguồn của Loading là ui-conventions §4 MSG-05. Ở §7, FR-04-08 chỉ ghi "chặn khi không có phiên nhân viên → S-F00-03". |
| 6 | Nên sửa | §6 SR-003, SR-004, SR-007 | SR-003 và SR-004 chỉ lặp lại các dòng chuyển màn đã có ở §5. SR-007 ("Keep component names… consistent with UI Conventions") là câu chung chung, không kiểm được đạt hay không đạt cho riêng màn này. | Dòng 89–93; screen-spec-chung §5 (hàng mục 6: quy tắc là điều màn hình luôn phải giữ, không chép lại). | Bỏ SR-003 và SR-007. Giữ SR-004 với nội dung mới (xem mục 2). |
| 7 | Nên sửa | §3 #4 | "replaces task tiles as appropriate" là câu mơ hồ. | Dòng 58. | Ghi cụ thể: "Skeleton thay chỗ 2 ô chức năng, cùng hình dạng (ui-conventions §3 Skeleton)." |
| 8 | Nên sửa | Bảng đầu tệp | (a) Status "**Draft — Pending Wireframe Alignment and Group Review**" không hợp lệ, phải là Draft hoặc Reviewed. (b) Ô Activity diagrams có câu nghi vấn "confirm diagram references…", trong khi AD-UC-10 §5 và AD-UC-13 §5 đều đã ghi S-F04-01. (c) Priority có thêm chú thích. (d) Feature thiếu tên tính năng. | Dòng 8–12; AD-UC-10 §5; AD-UC-13 §5. | Status: "Draft". Activity diagrams: "AD-UC-10, AD-UC-13". Priority: "Must" (chuyển chú thích Could sang §3 #3). Feature: "F-04 Platform, Access & Operations". |
| 9 | Nên sửa | §2 và cuối tệp | Tệp còn ảnh nhúng từ link GitHub bên ngoài, các ghi chú nháp (dòng 27–37, 47) và mục "Review handoff" (dòng 140–145). Những phần này không có trong mẫu. | Dòng 27–47, 140–145; mẫu thầy §2. | Giữ ảnh `img/S-F04-01.png`, ảnh đánh số và bảng State → Image. Chuyển ghi chú quy trình sang pull request. |
| 10 | Nên sửa | Completion checklist | Checklist của mẫu bị thay bằng danh sách tự đặt. Các mục bắt buộc của mẫu đều mất: mọi FR có trong Function List, mọi hành động trong AD có dòng ở §5, mọi thành phần hiển thị dữ liệu ghi rõ trường… | Dòng 126–135; mẫu thầy dòng 88–97; screen-spec-chung §5 (hàng Completion checklist). | Chép đúng checklist của mẫu và tick theo thực tế. |
| 11 | Nên sửa | §8 | Có 6 gạch, không theo 4 nhãn của mẫu. Không có dòng "What collapses or stacks on a narrow screen". | Dòng 107–112; mẫu thầy §8. | Viết lại theo 4 nhãn. Phần co giãn ghi "xem §9 câu hỏi 4". |
| 12 | Gợi ý | §5 #1 | "Staff page address / session gate" không phải một thành phần trong §3, nhưng lại được đặt như một dòng tương tác. | Dòng 76. | Chuyển nội dung này lên §1 (điểm vào) và SR-001/SR-002. Ở §5 chỉ giữ các thành phần bấm được. |

#### Câu hỏi mở

| Câu hỏi | Tài liệu đã trả lời chưa? | Cần nhóm quyết? |
|---|---|---|
| 1. Có nút đăng xuất cho nhân viên không (dòng 118)? | **Chưa.** W1 không có FR nào về đăng xuất. screen-spec-chung §6 quy tắc 2 và 4 cấm tự thêm thành phần hoặc FR. Thời hạn của phiên nhân viên cũng chưa tài liệu nào nói tới. | **Có.** Không chặn. Nếu nhóm muốn có nút đăng xuất thì phải thêm FR mới vào W1 trước, rồi mới sửa wireframe. |
| 2. UC-13 / «Đánh giá bị báo cáo» có trong bản giao không (dòng 119, Blocking)? | **Đã trả lời.** screen-list.md dòng 18 và 32; W0 Table 1 (UC-13); W1 (FR-02-10/14/19/20 = Could, không có trong W0 Table 3). Kết luận: có trong phạm vi, ưu tiên Could. | Không. Đóng câu hỏi và bỏ "Blocking". |
| 3. Ảnh Default/Loading/Error đã có, đúng khổ chưa (dòng 120, Blocking)? | Đây là việc của ảnh, không phải câu hỏi nghiệp vụ. Hiện trong `img/` đã có S-F04-01.png, -loading, -error kèm bản đánh số. Chi soát ảnh riêng. | Không. Bỏ khỏi §9. |
| 4. Bố cục khi màn hình hẹp hơn 1280px (dòng 121)? | **Chưa rõ,** giống câu hỏi 4 của S-F00-03 (ui-conventions Q3 chốt 1280px, nhưng §5 lại ghi 360px là khổ nhỏ nhất). | **Có.** Không chặn. Chốt chung cho 4 màn nhân viên. |
| 5. Có cần bản HTML minh hoạ không (dòng 122)? | **Đã trả lời.** screen-spec-chung §4 và §4.1 chấp nhận nguồn `.drawio`. | Không. Đóng câu hỏi. |

### Review S-F03-01 Access-format filter and results — người viết: Linh
Tóm tắt: Phần luật lọc (3 lựa chọn, lọc trên toàn bộ danh mục, nghĩa của "Cả hai", ghi nhận lượt đọc ẩn danh) đúng với AD-UC-03. Tuy vậy spec chưa viết từ tệp ghi chú mới nhất của Nhi: mục 3 lệch số và thiếu thành phần, trạng thái lỗi và FR-04-20 bị để ngỏ dù ghi chú đã có, và hai câu hỏi mở của ghi chú bị bỏ sót. Cần sửa trước khi soát chéo. (Đã bỏ qua mục 2 và tên ảnh theo yêu cầu.)

| # | Mức | Mục | Vấn đề | Bằng chứng | Cách sửa đề xuất |
|---|---|---|---|---|---|
| 1 | Phải sửa | §3 | Số `#` và danh sách thành phần lệch với tệp ghi chú và ảnh đánh số. Thiếu #3 nhãn hướng dẫn "Chọn hình thức truy cập". Bộ chọn phải là #4 (spec ghi #3). Danh sách kết quả là #5 (spec ghi #4). Nhãn hình thức (#6) bị gộp vào dòng kết quả. Thông báo không có kết quả là #7 (spec ghi #5). Thiếu #8 Banner MSG-04 và #9 nút "Thử lại". Ngoài ra spec tự thêm #6 "Online-book link" kiểu Text link, trong khi ghi chú nói cả dòng sách mở trang đích. | Spec dòng 53–64; `notes/S-F03-01-notes.md` dòng 9–17; `img/S-F03-01-numbered.png` (1 Back, 2 tiêu đề, 3 "Chọn hình thức truy cập", 4 bộ chọn) | Chép lại §3 đúng 9 dòng của ghi chú, giữ nguyên số. Bỏ dòng Text link riêng, ghi "whole Book row opens…" ở #5. |
| 2 | Phải sửa | §4 Error, §5, §7 | Dòng Error để `[NEEDS CLARIFICATION]`, §7 không có FR-04-20, §5 không có dòng "Thử lại". Thực ra tệp ghi chú đã định rõ lỗi là MSG-04 + "Thử lại" (FR-04-20), screen-list liệt kê S-F03-01 trong phạm vi FR-04-20, và tệp phân việc của Linh cũng dặn gắn FR-04-20/MSG-04. Bảng kiểm dòng 144 lại ghi Error "explicitly marked not applicable", mâu thuẫn với dòng 73. | Spec dòng 73, 105–112, 76–88, 144; `notes/S-F03-01-notes.md` dòng 16–17, 26, 40; `screen-list.md` dòng 30; `Linh-screen-spec.md` dòng 39–40 | Error = MSG-04 "Không tải được trang. Bạn kiểm tra kết nối mạng rồi thử lại." + "Thử lại", giữ hình thức đang chọn và dữ liệu đang hiện. Thêm FR-04-20 vào §7 và thêm dòng Retry vào §5. |
| 3 | Phải sửa | §9 | Hai câu hỏi mở của ghi chú không được chép sang: #2 (sách có cả hai hình thức hiện nhãn thế nào — đang vẽ: hiện cả "Bản giấy" và "Trực tuyến") và #3 (danh sách dài thì chia trang hay có nút "Xem thêm"). Câu #3 ảnh hưởng trực tiếp tới cách lập trình. | Spec dòng 125–135; `notes/S-F03-01-notes.md` dòng 47–48; `screen-spec-chung.md` §5 dòng "9 Open questions" | Thêm 2 câu vào §9, ghi kèm phương án đang vẽ. Câu chia trang nên để Blocking = Yes, vì không FR nào nói về chia trang ở màn này. |
| 4 | Phải sửa | Bảng kiểm cuối | Các mục đã đánh dấu không đúng sự thật: "Every element in Nhi's notes appears… retaining the original #" (sai, xem dòng 1), "Error… explicitly marked not applicable" (sai, xem dòng 2), "all listed user/system actions are represented" (thiếu Retry). | Spec dòng 141–147; mẫu dòng 88–97 | Kiểm lại và bỏ dấu ở các mục chưa đạt. |
| 5 | Nên sửa | §3 hàng "— (system)", §5 dòng 5–6 | Hai việc chạy ngầm (ghi nhận lượt đọc ẩn danh, thêm vào lịch sử đọc) được liệt kê như thành phần và như hành động của người dùng. screen-list ghi rõ đây là "Background steps… no user interface". | Spec dòng 63–64, 84–85; `screen-list.md` dòng 97 | Bỏ khỏi §3 và §5. Giữ ở §6 (SR-007, SR-008) và §7, như vậy đã đủ để truy vết. |
| 6 | Nên sửa | §3 #3, §4 Default, SR-009 | Spec ghi "do not assume a default", nhưng ghi chú và ảnh đã vẽ rõ: lúc mới mở **không có lựa chọn nào được chọn**, và chỉ hiện kết quả sau khi bạn đọc chọn. Câu Q5 trong hướng dẫn chung cũng ghi "Xem ảnh Default của Nhi". | Spec dòng 59, 70, 102; `notes/S-F03-01-notes.md` dòng 23, 46; `img/S-F03-01-numbered.png`; `screen-spec-chung.md` Q5 | Mô tả đúng trạng thái đang vẽ ("no option selected; no results until the reader chooses"), ghi là phương án tạm cho đến khi nhóm chốt Q5. |
| 7 | Nên sửa | §6 SR-006 | Nguồn ghi FR-03-13 là sai: FR-03-13 là ghi nhận lượt đọc ẩn danh. Quy tắc "không tự làm trình đọc hay tải PDF" đến từ việc cắt FR-03-14/FR-03-15. | Spec dòng 99; function list W0 Table 3 (dòng "Showing the access format… (FR-03-14) and downloading PDFs… (FR-03-15)"); AD-UC-03 §6 câu 1 | Đổi nguồn thành "W0 Table 3 (FR-03-14, FR-03-15 Won't); AD-UC-03 Q1". |
| 8 | Nên sửa | §4 Empty | Không ghi nguyên văn câu thông báo, chỉ mô tả bằng lời. | Spec dòng 71; `ui-conventions.md` §4 dòng "No results"; ghi chú dòng 15 | Ghi nguyên văn "Không tìm thấy sách. Hãy chọn hình thức khác." |
| 9 | Gợi ý | Bảng đầu tệp | Ghi AD-UC-03 là v1.2, trong khi tệp AD hiện là v1.3. Status không phải một giá trị Draft/Reviewed. | Spec dòng 10, 12; AD-UC-03 bảng đầu tệp ("v1.3 · Draft") | Ghi `AD-UC-03` (không ghi số phiên bản, hoặc ghi v1.3) và `Draft`. |
| 10 | Gợi ý | Cuối tệp | Phần "Review handoff" nằm ngoài cấu trúc của mẫu, và có dòng "Status: Draft until…" trùng với bảng đầu tệp. | Spec dòng 152–157 | Chuyển nội dung này sang mô tả pull request hoặc §9. |
| 11 | Gợi ý | §8 | Có nói giữ nguyên bố cục của Nhi, nhưng chưa nói cụ thể phần nào xếp chồng khi màn hẹp. | Spec dòng 118; mẫu dòng 76 | Ví dụ: "Book row: cover left, title/author/labels stacked right; two Format labels wrap to a second line". |

#### Câu hỏi mở

| # §9 | Câu hỏi | Tài liệu đã trả lời chưa? |
|---|---|---|
| 1 | Q5: lựa chọn nào được chọn sẵn khi mới mở | **Đã có phương án vẽ, nhưng nhóm chưa chốt chính thức.** Ghi chú dòng 23 và ảnh: không chọn sẵn lựa chọn nào. `screen-spec-chung.md` Q5 dẫn về "ảnh Default của Nhi". Cần ghi kết luận của buổi họp 21/11 (nếu đã họp) dưới dạng `Closed <ngày>: …`. |
| 2 | Câu thông báo không có kết quả | **Đã có câu trả lời:** ghi chú dòng 15 và ui-conventions §4 (No results) trùng nguyên văn "Không tìm thấy sách. Hãy chọn hình thức khác." Spec nói "Nhi's notes leave exact wording open" là không đúng. Có thể đóng. |
| 3 | Trạng thái lỗi là gì, có áp FR-04-20 không | **Đã có câu trả lời:** ghi chú dòng 16–17, 26 (MSG-04 + "Thử lại", FR-04-20); `screen-list.md` dòng 30. Có thể đóng. |
| 4 | Tên trường dữ liệu theo W0 Table 4 | **Trả lời được một phần:** W0 Table 4 có nhóm "Book catalogue" (titles, authors, access formats). Tài liệu không có tên ở mức trường, nên ghi `Book catalogue › title / author / access format` là đủ. Ô bìa sách chỉ là khối xám, không có dữ liệu (ui-conventions Q6). Đề xuất Blocking = No. |
| 5 | Ảnh success đã tải lên chưa | Thuộc phần ảnh, Chi soát riêng. |
| 6 | Dòng đầu của ghi chú đã có metadata chưa | **Đã có:** `notes/S-F03-01-notes.md` dòng 3 "Actor: Reader · Frame: 360px · UI conventions: v0.8 · Author: Nhi". Có thể đóng. |
| 7 | Đường dẫn mã nguồn wireframe | **Chưa giải quyết:** `screens/src/` không có tệp nào của S-F03-01. Đây là việc Nhi cần làm. |
| Ghi chú #2, #3 (bị bỏ sót) | Nhãn cho sách có cả hai hình thức; chia trang danh sách | **Thật sự cần nhóm quyết.** AD-UC-03 Q2 chỉ chốt nghĩa của "Cả hai", không nói cách gắn nhãn. Không FR nào nói về chia trang ở S-F03-01. |

## Phần của Hoa

### Review S-F02-01 Book reviews (kèm M-F02-01-01, M-F02-01-02) — người viết: Hoa

Tóm tắt: Gần sẵn sàng. Đủ 9 mục, hai hộp thoại viết đúng cách của nhóm, mọi FR của màn trong `screen-list.md` đều có ở mục 7 và có thành phần hoặc thao tác thực hiện (UC-04, UC-05, UC-14 đều đủ). Còn 2 lỗi phải sửa: quy tắc hiện nút "Xem thêm đánh giá" trái với FR-02-02, và trường hợp "không tìm thấy sách" vẫn cho viết đánh giá. Ngoài ra một số câu thông báo và hành vi chưa ghi đủ cụ thể để kiểm thử.

| # | Mức | Mục | Vấn đề | Bằng chứng | Cách sửa đề xuất |
|---|---|---|---|---|---|
| 1 | Phải sửa | §6 SR-004, §4 Default | Quy tắc hiện nút "Xem thêm đánh giá" bị sai. Spec ghi chỉ hiện khi "more than 10 published reviews remain". Ví dụ sách có 15 đánh giá: sau trang 1 chỉ còn 5 đánh giá, nút sẽ ẩn và bạn đọc không xem được đánh giá 11–15. Ở §4 có câu "if >10 published reviews exist", câu này chỉ đúng với trang đầu. | Dòng 133, 95. FR-02-02: "IF more reviews exist after the displayed page, THEN … allow the reader to request the next page". Bảng kiểm thử của AD-UC-05 d3: 7 đánh giá thì không có trang sau, 25 đánh giá thì có. | Viết lại: "Hiện khi sau trang đang xem còn ít nhất 1 đánh giá; ẩn khi đã hiện hết". Sửa câu ở §4 theo cùng ý. |
| 2 | Phải sửa | §3 #10, §4 Empty | Trường hợp sách không tồn tại chưa rõ. (a) Câu thông báo chỉ ghi "book-not-found variant", không có nguyên văn. (b) Ở §4, khung viết đánh giá #3–#6 vẫn hiện, nghĩa là bạn đọc viết được đánh giá cho một cuốn sách không tồn tại. Điều này trái điều kiện của AD-UC-04 (sách phải có trong danh mục). | Dòng 68, 96. FR-02-15. Mục "Preconditions" của AD-UC-04. AD-UC-05 nhánh d1 [No] (sách mã 99999). Hoa-nhan-xet-wireframe.md mục S-F02-01 #9. | Ghi nguyên văn câu cho trường hợp không tìm thấy sách. Ghi rõ là ẩn #2 và #3–#6. Nếu chưa vẽ thì đưa vào mục 9. |
| 3 | Nên sửa | §3 #12, §4 Error | Chỉ có câu lỗi khi để trống, mà lại ghi "e.g." (chỉ là ví dụ). Chưa có nguyên văn câu lỗi khi vượt 2.000 ký tự và khi không phải văn bản thuần, nên không kiểm được chữ trên màn. | Dòng 70, 98. ui-conventions §4 (mẫu "cái gì sai + sửa thế nào"). Kiểm thử của AD-UC-04 d3 [No] với 2.001 ký tự. | Liệt kê đủ nguyên văn từng câu lỗi và bỏ chữ "e.g.". |
| 4 | Nên sửa | §3 #3 Validation, SR-008 | Yêu cầu "plain text only, 1–2,000 characters" chưa kiểm được. Spec không nói khi dán chữ có định dạng hoặc mã thì hệ thống từ chối hay tự bỏ định dạng. Cũng không nói ô chỉ có khoảng trắng có tính là "trống" không, và khoảng trắng ở đầu, cuối có được đếm không. | Dòng 61, 137. FR-02-01. | Định nghĩa "văn bản thuần" và cách đếm ký tự, ví dụ: bỏ khoảng trắng ở đầu và cuối; chỉ có khoảng trắng thì coi là trống. |
| 5 | Nên sửa | §3 #3, §5 dòng 5 | Chế độ sửa đánh giá chưa đủ. Nút "cancel edit" không có nhãn, không có số trên ảnh, cũng không có dòng ở §5 nói bấm vào thì sao. Khi sửa, ô "Đăng ẩn danh" giữ lựa chọn cũ hay quay về mặc định thì chưa ghi, trong khi FR-02-22 áp dụng cả lúc sửa. | Dòng 61, 113. FR-02-22 ("submits or edits"). Hoa-nhan-xet-wireframe.md S-F02-01 #6. screen-spec-chung.md §6 quy tắc 2 (không thêm thành phần không có trên ảnh). | Vẽ chế độ sửa, hoặc ghi câu hỏi ở mục 9. Đặt nhãn cho nút huỷ sửa theo ui-conventions §1. Thêm dòng ở §5. Ghi trạng thái ban đầu của ô ẩn danh khi sửa. |
| 6 | Nên sửa | §4 Loading | Lần tải nào cũng thay toàn màn bằng Skeleton, kể cả khi bấm "Xem thêm", khi lưu, xoá hay báo cáo. Như vậy danh sách đang xem sẽ biến mất. Điều này trái ý FR-04-20 (giữ dữ liệu đang hiển thị) và ui-conventions §3 (Load more chỉ chuyển sang "disabled while loading"). | Dòng 97. ui-conventions §3 Load more button. FR-04-20. | Tách làm hai: mở màn lần đầu thì dùng Skeleton; tải trang sau hoặc lưu thì giữ nội dung, chỉ tắt nút đang bấm. |
| 7 | Nên sửa | §3.1 #1, §3.2 #1 | Câu trong hai hộp thoại chưa ghi nguyên văn. Trên ảnh là: "Bạn có chắc muốn xoá đánh giá này? Đánh giá sẽ không còn hiển thị công khai." và "Bạn muốn báo cáo đánh giá này với thư viện?". Spec lại viết "permanent removal" (xoá vĩnh viễn), sai nghĩa: theo AD-UC-04, xoá chỉ là ẩn khỏi hiển thị công khai, đánh giá vẫn được lưu ở trạng thái Removed. | Dòng 79, 87. Ảnh M-F02-01-01-numbered, M-F02-01-02-numbered. AD-UC-04 phần reading notes và câu hỏi 3. | Chép đúng câu trên ảnh và bỏ chữ "permanent". |
| 8 | Nên sửa | §5 dòng 3 | "attempt to write/submit" còn mơ hồ: hệ thống hỏi đăng nhập lúc bạn đọc chạm vào ô viết hay lúc bấm "Đăng đánh giá"? Nội dung đã gõ có còn sau khi đăng nhập xong quay lại không? | Dòng 111. AD-UC-04 (kiểm tra đăng nhập trước khi chọn hành động). screen-transition.md: hành động đã yêu cầu được tiếp tục sau khi đăng nhập. | Ghi một thời điểm cụ thể và quy tắc giữ nội dung đã gõ. S-F03-06 đã ghi "preserves entered text", có thể làm tương tự. |
| 9 | Nên sửa | §5 dòng 2, dòng 13 | Chỉ mô tả trường hợp thành công. Chưa có nhánh sửa hoặc xoá đánh giá không phải của mình (AD-UC-04 d4 [No], d7 [No]): khi đó đánh giá giữ nguyên và hiện Banner lỗi ở #11. | Dòng 110, 121. AD-UC-04 d4, d7 và các kiểm thử với đánh giá #91. | Thêm vào cột System response: "If not own review: no change, #11 error Banner '…' (FR-02-11)". |
| 10 | Nên sửa | §3 #11 | Một Banner dùng cho 3 thông báo khác loại nhưng không ghi loại Banner nào. ui-conventions có 4 loại: info, success, warning, error. "Đã báo cáo rồi" là thông báo, không phải lỗi (screen-list ghi "Message state"). Ngoài ra một thành phần đang gắn với 3 FR không liên quan nhau (FR-04-20, FR-02-21, FR-02-11). | Dòng 69, 98. screen-list.md dòng 74. ui-conventions §3 Banner. | Ghi loại Banner cho từng câu, ví dụ MSG-04 là error, "đã báo cáo" là info hoặc warning. |
| 11 | Nên sửa | §5 dòng 4 | Liên kết "Xem quy định…" ghi đích là "stays" (ở lại màn). Theo ui-conventions, Text link dùng để đi sang trang khác. Đích ở đây là trang quy định của thư viện (AD-UC-13 câu hỏi 1). | Dòng 112. ui-conventions §3 Text link. screen-spec-chung §5 cột "Goes to". | Ghi "Library review guideline page (exit), URL pending". |
| 12 | Nên sửa | §8 | Mục 8 ghi vùng chạm cho Back, ô ẩn danh, nút chính và Load more, nhưng bỏ sót các nút chữ "Sửa", "Xoá đánh giá", "Báo cáo đánh giá" và liên kết #5. Trên ảnh các nút này nhỏ, trong khi màn bạn đọc yêu cầu vùng chạm ít nhất 44×44px. | Dòng 164. ui-conventions §5. | Thêm yêu cầu vùng chạm 44×44px cho các nút chữ và liên kết. |
| 13 | Gợi ý | §3 #7, #8 | "Báo cáo đánh giá" đang dùng kiểu chữ đỏ (`.danger`). ui-conventions chỉ dùng kiểu này cho hành động xoá hoặc gỡ, mà báo cáo không xoá gì. Trên ảnh "Sửa" lại màu xanh, trông giống liên kết (Hoa-nhan-xet #7 cũng nêu). | Dòng 65–66. ui-conventions §3 Text button. | Hỏi Linh có giữ màu đỏ cho nút Báo cáo không. |
| 14 | Gợi ý | §6 SR-004 | Chỉ ghi "newest first (dd/MM/yyyy)". Khi nhiều đánh giá cùng ngày (ảnh có 2 đánh giá ngày 12/11/2026) thì thứ tự không xác định. | Dòng 133. | Sắp theo thời điểm đăng; trên màn vẫn chỉ hiện ngày. |
| 15 | Gợi ý | §3 #4 | Nguồn dữ liệu của ô "Đăng ẩn danh" đang ghi `Reader accounts › full registered name`. Thật ra ô này lưu lựa chọn ẩn danh của đánh giá (thuộc nhóm Book review); họ tên chỉ là phần hiển thị. | Dòng 62. W0 Table 4. | Ghi `Book review › anonymous choice`, họ tên lấy từ `Reader accounts › full name`. |
| 16 | Gợi ý | §9 Q6 | Tên tệp ghi sai: "M02-01-01 notes.md". Tệp thật là `notes/M-F02-01-01-notes.md`. | Dòng 175. | Sửa tên tệp. |

#### Câu hỏi mở

| Câu | Đánh giá |
|---|---|
| Q1 Báo cáo đánh giá của chính mình | Đã đóng đúng: nhóm chốt ngày 19/11/2026 (AD-UC-14 câu hỏi 2). |
| Q2 Địa chỉ trang quy định viết đánh giá | Tài liệu đã trả lời một phần: AD-UC-13 câu hỏi 1 (chốt 04/11/2026) quyết định đặt liên kết tới quy định của thư viện ở khung viết đánh giá. Chỉ còn thiếu địa chỉ cụ thể, cần xin thư viện, nhóm không phải họp. Không chặn. |
| Q3 "Xem thêm đánh giá" nối thêm hay thay trang | Chưa tài liệu nào trả lời. AD-UC-05 chỉ ghi "reviews 11 to 20 are shown"; tên "Load more" trong ui-conventions gợi ý là nối thêm. Cần Linh hoặc nhóm chốt. Đề xuất: nối thêm. |
| Q4 Dùng "Book row" cho khối thông tin sách | Cần nhóm quyết. ui-conventions §3 chưa ghi S-F02-01 trong cột "Used on", và Hoa-nhan-xet #11 cũng xếp vào "Cần nhóm chốt". Linh bổ sung cột "Used on" hoặc đặt tên thành phần mới. |
| Q5 Hộp thoại có trích nội dung đánh giá không | Chưa tài liệu nào trả lời. Nhóm quyết; không chặn. |
| Q6 Tiêu đề hộp thoại và nút "Huỷ" | Có thể đóng. ui-conventions §1 dặn "use the screen/modal notes as the source of truth", và tệp ghi chú của hộp thoại ghi "Xoá đánh giá?" và "Báo cáo đánh giá?". "Huỷ" đã có trong bảng nhãn chuẩn của ui-conventions §1 (Cancel in a modal). Linh chỉ cần điền vào bảng ở §1. |
| Còn thiếu ở mục 9 | (a) Chế độ sửa đánh giá chưa vẽ (dòng 5 ở bảng trên). (b) Trường hợp không tìm thấy sách hiển thị những gì (dòng 2). (c) Nội dung đã gõ có được giữ sau khi đăng nhập không (dòng 8). |

### Review S-F02-02 Book information and reviews (QR landing page) — người viết: Hoa

Tóm tắt: Chưa sẵn sàng nộp. Tệp còn 58 dấu "[cite: …]" do công cụ AI để lại. Màn trích FR-02-02 (xem theo từng trang) nhưng không có cách xem trang sau. Nút Back bấm vào không làm gì. Khung đánh giá dùng lại đúng tên thành phần của S-F02-01 (L8-07), không có nút Báo cáo; phần này tốt.

| # | Mức | Mục | Vấn đề | Bằng chứng | Cách sửa đề xuất |
|---|---|---|---|---|---|
| 1 | Phải sửa | Toàn tệp | Có 58 dấu "[cite: 3, 9, 14]"… ở cuối câu. Đây là rác do công cụ AI để lại, không trỏ tới tài liệu nào. Lập trình viên hoặc AI đọc spec ở DBIZ3 sẽ bị nhầm. | Dòng 19, 21, 27, 29, 45, 49–62, 68–72, 78–87, 93–99, 121–124, 130–134. | Xoá hết. Khi cần ghi nguồn thì dùng mã: FR, AD, L8, MSG. |
| 2 | Phải sửa | §7 FR-02-02, §3, §9 Q2 | Mục 7 trích FR-02-02 ("IF more reviews exist… allow the reader to request the next page") nhưng màn không có cách xem trang sau. Ảnh hiện đúng 10 đánh giá và không có nút, nên từ đánh giá thứ 11 trở đi không xem được. AD-UC-06 ghi rõ trang này theo luật của UC-05: "one page at a time". Câu hỏi Q2 đang chặn (Blocking) mà vẫn còn mở. | Dòng 106, 131. Ảnh S-F02-02-numbered. AD-UC-06 §1 reading notes. Hoa-nhan-xet-wireframe.md S-F02-02 #6. | Nhóm chốt Q2 trước khi nộp. Nếu theo AD thì thêm Load more button như S-F02-01 (#9) và vẽ lại ảnh. Nếu không có trang sau thì bỏ FR-02-02 khỏi §7 và ghi màn hiện tối đa bao nhiêu đánh giá. |
| 3 | Phải sửa | §5 dòng 1 | Nút Back có hiện trên màn nhưng đích là "stays", tức bấm vào không có gì xảy ra. `screen-transition.md` cũng không vẽ đường Back cho S-F02-02. | Dòng 78, 130. screen-transition.md (S-F02-02 chỉ có đường "View this book on the OPAC"). ui-conventions §3 Screen header. | Nhóm chốt Q1: bỏ nút Back, hoặc cho Back về trang chi tiết sách trên OPAC. Không để một nút không có hành vi. |
| 4 | Phải sửa | §3 #9 | Một số # gộp hai thành phần khác loại (Review item và Banner), lại gắn 5 FR không liên quan nhau. Lập trình viên không biết đặt tên thành phần theo dòng nào; trên ảnh đánh số, #9 chỉ chỉ vào các đánh giá. | Dòng 57. screen-spec-chung §5 (mỗi thành phần một dòng, giữ số #). | Tách Banner ra một dòng có số riêng (kèm ảnh `-error-numbered`), hoặc ghi "same as screen-spec-S-F02-01 #11". |
| 5 | Phải sửa | §4 Error, SR-004 | Trường hợp mã QR không gắn với sách nào còn thiếu. Câu thông báo chỉ có "Không tìm thấy sách." cộng "next-step guidance" mà không có nguyên văn phần sau. Spec không nói màn còn hiện gì (thông tin sách, khung viết, liên kết OPAC?), nên dễ thành ngõ cụt. Cũng chưa ghi quy tắc "không tăng lượt quét". | Dòng 71, 96. FR-02-16 ("SHALL not increase any scan count"). AD-UC-06 d1 [No] (mã QR-000777). ui-conventions §4 mẫu "No results". Hoa-nhan-xet S-F02-02 #3. | Ghi nguyên văn câu đầy đủ. Liệt kê phần nào còn hiện, phần nào ẩn. Thêm "không tăng lượt quét" vào SR-004. |
| 6 | Nên sửa | §3 #13, §4 Error-3 | Chưa có nguyên văn các câu lỗi: để trống, vượt 2.000 ký tự, sửa đánh giá không phải của mình. Ở Banner chỉ ghi "non-owner action rejection", không có câu. | Dòng 61, 71. | Ghi "same wording as screen-spec-S-F02-01 §3 #11, #12" sau khi S-F02-01 đã đủ câu. |
| 7 | Nên sửa | §3 #4, §5 dòng 3, 4, 6 | Các điểm chưa rõ của S-F02-01 cũng có ở đây: định nghĩa "văn bản thuần"; nút huỷ sửa chưa có nhãn và chưa có dòng ở §5; ô ẩn danh khi sửa giữ lựa chọn nào; hỏi đăng nhập lúc nào và có giữ nội dung đã gõ không. Thêm nữa, #4 (ô viết) gắn FR-02-04 (xoá đánh giá), không liên quan. | Dòng 52, 80–83. | Sửa cùng lúc với S-F02-01 để hai màn giống nhau như L8-07 yêu cầu. Bỏ FR-02-04 khỏi #4. |
| 8 | Nên sửa | §4 Loading | Giống S-F02-01: khi lưu, sửa hay xoá, toàn màn bị thay bằng Skeleton nên danh sách đang xem biến mất. | Dòng 70. FR-04-20. | Giữ nội dung, chỉ tắt nút trong lúc đang lưu. |
| 9 | Nên sửa | §6 SR-005 | Quy tắc dựa trên FR-02-06 (đếm lượt quét) nhưng FR-02-06 không có ở §7. screen-list xếp việc đếm lượt quét là việc chạy nền, không có giao diện. | Dòng 97. screen-list.md dòng 95. | Bỏ SR-005, hoặc ghi rõ đây là việc chạy nền (FR-02-06), không phải hành vi của màn. |
| 10 | Gợi ý | §7 | FR-02-02 và FR-02-15 không có trong cột "Use cases / FRs served" của screen-list cho S-F02-02 (cột này chỉ có "UC-05 rule · FR-02-13"). Dùng được vì AD-UC-06 nói theo luật của UC-05, nhưng hai tài liệu đang chưa khớp. | screen-list.md dòng 16. | Nhắn người giữ screen-list bổ sung, hoặc ghi vào mục 9. |
| 11 | Gợi ý | §8 | Chưa ghi vùng chạm 44×44px cho các liên kết #3, #6 và các nút chữ "Sửa", "Xoá đánh giá". | Dòng 124. ui-conventions §5. | Bổ sung. |

#### Câu hỏi mở

| Câu | Đánh giá |
|---|---|
| Q1 Back khi mở thẳng từ mã QR | Hai tài liệu chung đang mâu thuẫn. `screen-transition.md` không có đường Back từ S-F02-02, nghiêng về "không có Back". ui-conventions §3 lại nói mọi màn có Back. Cần nhóm (Linh) chốt. Nên đổi Blocking thành Yes, vì hiện nút đang không làm gì. |
| Q2 Có "Xem thêm đánh giá" không | Tài liệu trả lời một phần: AD-UC-06 reading notes ghi "one page at a time" theo UC-05, tức là phải có trang sau. Nhưng câu Q2 trong screen-spec-chung vẫn ghi "Phương án đang vẽ: Không có" và chưa chốt. Cần nhóm chốt; ghi Blocking là đúng. |
| Q3 Có nút Báo cáo không | Đóng đúng hướng (L8-07). Nhưng L8-07 trong activity-index đang ở trạng thái "Default applied 2026-11-08; team to confirm", nên ghi "Closed" là quá mức. Ghi lại cho đúng trạng thái. |
| Q4 Địa chỉ trang quy định | Giống S-F02-01 Q2: AD-UC-13 câu hỏi 1 đã chốt có liên kết, chỉ còn xin địa chỉ từ thư viện. |
| Q5 "Book row" có tóm tắt | Giống S-F02-01 Q4: cần Linh quyết. Ở đây thêm phần "Tóm tắt" mà Book row không có. |

### Review S-F02-04 Reported reviews (kèm M-F02-04-01) — người viết: Hoa

Tóm tắt: Truy vết tốt. Đủ 4 FR của màn trong screen-list (FR-02-14, FR-02-10, FR-02-19, FR-02-20), mọi thao tác của nhân viên trong AD-UC-13 đều có dòng ở §5, hộp thoại viết đúng cách của nhóm và khớp ảnh. Cần làm hai việc: xoá 54 dấu "[cite: …]", và sửa trạng thái Error vì hiện đang làm mất dữ liệu đang hiển thị.

| # | Mức | Mục | Vấn đề | Bằng chứng | Cách sửa đề xuất |
|---|---|---|---|---|---|
| 1 | Phải sửa | Toàn tệp | Có 54 dấu "[cite: n]" do công cụ AI để lại, không trỏ tới tài liệu nào. | Dòng 19, 21, 27, 40, 46, 52–61, 67–69, 75–80, 87–93, 99–103, 119–122, 128–130, 136–142. | Xoá hết. Khi cần ghi nguồn thì dùng mã. |
| 2 | Phải sửa | §4 Error | Trạng thái Error chỉ còn tiêu đề và Banner. Như vậy khi bấm Gỡ hoặc Bỏ qua mà bị lỗi, hàng chờ và đánh giá đang xem đều biến mất. Điều này trái FR-04-20 ("keep the data already shown") và screen-list ("data already shown is kept"). Spec cũng không nói sau thao tác lỗi thì báo cáo còn trong hàng chờ hay không. | Dòng 78. FR-04-20. screen-list.md dòng 58. | Tách làm hai trạng thái. (a) Mở màn lần đầu bị lỗi: chỉ có Banner MSG-04 và "Thử lại". (b) Lưu bị lỗi: giữ nguyên hàng chờ và chi tiết, đánh giá vẫn hiển thị công khai (Published), báo cáo vẫn mở (Open), kèm Banner MSG-04. |
| 3 | Nên sửa | §3 #2, #3 | Ngày trên thẻ được ghi là `Book review › posted date` (ngày đăng đánh giá). Nhưng trên ảnh, đánh giá #91 của Trần Minh Anh hiện ngày 15/11/2026, còn ở S-F02-01 cùng đánh giá này hiện 12/11/2026. Có vẻ ảnh đang hiện ngày báo cáo. | Dòng 53–54. Ảnh S-F02-04-numbered và S-F02-01-numbered. | Ghi rõ là ngày đăng hay ngày báo cáo (`Review report › reported date`), rồi sửa dữ liệu mẫu cho khớp. |
| 4 | Nên sửa | §4 Default, §6 | Còn thiếu quy tắc cho các trường hợp sau: (a) thứ tự trong hàng chờ, ví dụ báo cáo cũ nhất trước; (b) thẻ nào được chọn sẵn khi mở màn và sau khi xử lý xong một thẻ ("next open report" là thẻ nào); (c) một đánh giá bị nhiều bạn đọc báo cáo thì hiện một thẻ hay nhiều thẻ; (d) khi có nhiều báo cáo thì cuộn hay chia trang. | Dòng 75, 79. AD-UC-13 s4 và kiểm thử với #91, #95. | Thêm SR: thứ tự sắp xếp; mặc định chọn thẻ đầu tiên; gộp theo đánh giá; danh sách cuộn. |
| 5 | Nên sửa | §6 SR-001, §5 | Chưa nói khi phiên đăng nhập của nhân viên hết hạn giữa chừng (đang ở màn này rồi bấm Gỡ) thì sao. Theo FR-04-08, yêu cầu sẽ bị từ chối. | Dòng 99. FR-04-08. AD-UC-13 s1. | Thêm dòng ở §4 hoặc §5: phiên hết hạn thì mở S-F00-03; hoặc ghi vào mục 9. |
| 6 | Nên sửa | §8 | Thẻ đang chọn chỉ phân biệt bằng viền đỏ và nền nhạt, tức chỉ bằng màu. Nhãn "Đang chờ" hiện trên mọi thẻ, nhưng hàng chờ chỉ có báo cáo đang mở nên nhãn luôn giống nhau, không giúp phân biệt. | Dòng 121. ui-conventions §5 (không dùng màu làm tín hiệu duy nhất). | Thêm dấu hiệu "đang chọn" không dựa vào màu. Cân nhắc bỏ nhãn "Đang chờ". |
| 7 | Gợi ý | §7 FR-04-12, SR-006 | Có từ ngữ kỹ thuật: "backend audit entry logging", "reloads from the server". Spec nên nói màn làm gì, không nói làm bằng cách nào. | Dòng 114, 104. | Viết "an audit entry is written (FR-04-12)" và "the list is loaded again". |
| 8 | Gợi ý | §3 #2 | Mã đánh giá ("Đánh giá #91") hiện cho nhân viên thấy, nhưng không FR nào yêu cầu. Ở màn bạn đọc, mã này đã được bỏ. | Dòng 53. | Nếu giữ để nhân viên đối chiếu thì ghi lý do. |
| 9 | Gợi ý | §3 #7 | Banner MSG-04 được gắn thêm FR-02-10 và FR-02-20; một thành phần đang ghép với các FR không liên quan. | Dòng 58. | Chỉ giữ FR-04-20. |

#### Câu hỏi mở

| Câu | Đánh giá |
|---|---|
| Q1 Bố cục hai cột | Chưa tài liệu nào chốt. Hoa-screen-spec.md gọi đây là phương án tạm. Nhóm quyết; không chặn. |
| Q2 Hiện lý do báo cáo | Có thể đóng. AD-UC-14 câu hỏi 1 (chốt 04/11/2026): không có ô lý do, vì FR-02-09 không yêu cầu; L8-10 cũng vậy. Không có dữ liệu lý do thì không có gì để hiển thị. Ghi "Closed 04/11/2026 (AD-UC-14 Q1): No". |
| Q3 Hai câu Toast khác nhau, và hộp thoại có trích nội dung đánh giá không | Phần Toast có thể đóng: Hoa-screen-spec.md §3 yêu cầu "hai thông báo thành công khác nhau", và AD-UC-13 có hai kết quả khác nhau (s5 và s7). Phần trích nội dung đánh giá trong hộp thoại thì nhóm vẫn phải quyết. Nên tách thành hai câu hỏi. |

## Phần của Nhi

### Review S-F01-01 Shelf location (with Save to my list) — người viết: Nhi
Tóm tắt: Nội dung nghiệp vụ đúng hướng (đủ các trạng thái chỉ-bản-trực-tuyến, thiếu vị trí kệ, đã lưu, đã lưu từ trước, lỗi mạng), nhưng chưa nộp được: số thứ tự ở mục 3 lệch với tệp ghi chú và ảnh đánh số, phần đăng nhập thiếu nhánh "Để sau", và bảng kiểm cuối không theo mẫu của thầy. (Đã bỏ qua mục 2 và tên ảnh theo yêu cầu.)

| # | Mức | Mục | Vấn đề | Bằng chứng | Cách sửa đề xuất |
|---|---|---|---|---|---|
| 1 | Phải sửa | §3 | Số `#` không khớp tệp ghi chú và ảnh đánh số, dù dòng 55 ghi "Numbering follows S-F01-01 wireframe notes". Spec gộp tên sách và tác giả vào #2, đặt dòng vị trí kệ ở #3, MSG-06 ở #4, thông báo chỉ-bản-trực-tuyến ở #5, Toast ở #8, còn hai dòng cuối không có số ("State only"). Ghi chú và ảnh lại đánh: 2 tên sách, 3 tác giả, 4–5 hai dòng vị trí kệ (bản 1, bản 2), 6 Lưu, 7 Xem trên bản đồ, 8 MSG-06, 9 chỉ-bản-trực-tuyến, 10 Toast đã lưu, 11 Toast đã có, 12 MSG-04 + "Thử lại". | Spec dòng 55–68; `notes/S-F01-01-notes.md` dòng 9–20; `img/S-F01-01-numbered.png` (số 1–7); `screen-spec-chung.md` §3 và §5 dòng "3 Element inventory" ("giữ số #") | Đánh lại §3 theo đúng 12 dòng của tệp ghi chú: tách tên sách và tác giả, thêm dòng bản sách thứ 2, đánh số 10–12 cho hai Toast và lỗi mạng thay cho chữ "State only". |
| 2 | Phải sửa | Bảng kiểm cuối | Đây là bảng kiểm tự đặt, không phải 7 mục của mẫu thầy. Mục đã đánh dấu xong "All eight numbered elements in Nhi's v0.8 notes" là sai, vì tệp ghi chú có 12 thành phần. | Spec dòng 148–157; `templates/screen-spec-template.md` dòng 88–97; `screen-spec-chung.md` §5 dòng "Completion checklist" ("Chép checklist của mẫu… tick thật") | Chép nguyên 7 mục của mẫu và chỉ đánh dấu những mục đã kiểm thật. |
| 3 | Phải sửa | §5 | (a) Dòng 5 ghi đích là "`M-F00-01`; Sign in continues to `S-F00-01`", còn dòng 95 viết "specified in the shared screen documentation" — chưa trỏ đúng chỗ đặc tả hộp thoại. (b) Thiếu kết quả khi bạn đọc bấm "Để sau": theo AD-UC-12, nhánh d1 [No] từ chối và không lưu gì. (c) Thiếu đường quay lại sau khi nhập đúng mã: S-F00-02 → S-F01-01. | Spec dòng 91, 95; `screen-spec-chung.md` §4.2 (`Goes to: M-F00-01 (see screen-spec-S-F00-01.md §3.1)`); `screen-spec-S-F00-01.md` dòng 61 (§3.1 có thật); AD-UC-12 §3 nhánh "d0 [No] → d1 [No]"; `screen-transition.md` (S00_02 → S01_01 "[OTP accepted]") | Sửa đích thành `M-F00-01 (see screen-spec-S-F00-01.md §3.1)`. Thêm 2 dòng: "Để sau → hộp thoại đóng, không lưu, stays" và "Sau khi nhập đúng mã → quay lại S-F01-01 và tiếp tục Lưu". |
| 4 | Nên sửa | §3, §4 | Tên cột khác mẫu: "Validation / visibility" (mẫu là "Validation") và "Trigger / outcome" (mẫu là "Trigger"). | Spec dòng 57, 72; mẫu dòng 39, 47 | Dùng đúng tên cột của mẫu; điều kiện hiện/ẩn ghi vào cột Content hoặc §6. |
| 5 | Nên sửa | Bảng đầu tệp | Feature chỉ ghi `F-01`, thiếu tên tính năng. Status ghi "Draft — pending group review…" thay vì một giá trị Draft/Reviewed. | Spec dòng 9, 12; mẫu dòng 15, 18; W0 Table 2 (F-01 Book Location & Library Map) | Ghi `F-01 Book Location & Library Map` và `Draft`. |
| 6 | Nên sửa | §3 #7, SR-007 | Cụm "usable room location" mơ hồ, không kiểm tra được đúng/sai. Theo AD-UC-01, nút "Xem trên bản đồ" xuất hiện sau bước s4, tức là ngay khi tầng, phòng và kệ đều đủ và khớp (d2 [Yes]). Trường hợp phòng không có trên sơ đồ là trạng thái lỗi của S-F01-02 (FR-01-09, L8-11), không phải lý do để ẩn nút. | Spec dòng 65, 107; AD-UC-01 sơ đồ (s4 → d3) và §5; `activity-index.md` L8-11 | Viết lại: "Shown whenever a shelf location line is shown (floor, room and shelf codes complete — AD-UC-01 d2 [Yes]); hidden for online-only books and when MSG-06 is shown." |
| 7 | Nên sửa | §3 cột Type | "Informational Toast" không có trong danh sách thành phần ở ui-conventions §3; ở đó chỉ có "Toast", và Toast vốn đã có trạng thái informational. #2 gộp tên sách và tác giả vào một "Section title" (xem thêm dòng 1). | Spec dòng 60, 67; `ui-conventions.md` §3 (Toast: "states: success and informational"; Section title "including book sections… S-F01-01") | Type = "Toast". Tên sách = Section title; tác giả = Text (theo ghi chú #3). |
| 8 | Nên sửa | §8 | Thiếu 2 trong 4 gạch đầu dòng của mẫu: phần nào xếp chồng khi màn hẹp, và cỡ chữ tối thiểu. | Spec dòng 125–134; mẫu dòng 75–78; `ui-conventions.md` §5–§6 (chữ thân 16px, tiêu đề 20px) | Thêm: "Stacks: buttons full width, one per row; location lines wrap under the pin icon"; "Body 16px, title 20px". |
| 9 | Nên sửa | §9 | Hai câu hỏi còn mở trong tệp ghi chú chưa được chép sang: #1 (tên thành phần cho tên sách) và #3 (bản sách thứ 2 chỉ là dữ liệu minh hoạ). | `notes/S-F01-01-notes.md` dòng 49, 51; `screen-spec-chung.md` §5 dòng "9 Open questions" | Chép sang §9. Câu #1 đóng luôn vì ui-conventions v0.8 §3 đã có "Section title"; câu #3 ghi Blocking = No. |
| 10 | Gợi ý | §7 | Spec có liệt kê FR-04-08. Theo screen-list.md, FR-04-08 chỉ được trích ở các màn đăng nhập, trang nhân viên và hộp thoại M-F00-01. | Spec dòng 123; `screen-list.md` dòng 29 | Bỏ FR-04-08 khỏi §7, chỉ giữ làm nguồn của SR-005. |
| 11 | Gợi ý | §3 cột Content | Tên trường dữ liệu chưa viết theo dạng `<Nhóm W0 Table 4> › <trường>`. | Spec dòng 60–61; `screen-spec-chung.md` §5 dòng "3 Element inventory" | Viết `Book catalogue › title`, `Book catalogue › author`, `Book placement & library layout › floor / room code / shelf code`. |
| 12 | Gợi ý | §6 SR-010 | Nguồn ghi chung chung "W0 scope". | Spec dòng 110; W0 Table 3, dòng "Features not rebuilt (a)… copy availability" | Ghi rõ nguồn: "W0 Table 3 — Features not rebuilt (a)". |

#### Câu hỏi mở

| # §9 | Câu hỏi | Tài liệu đã trả lời chưa? |
|---|---|---|
| 1 | Câu Toast "Đã lưu sách vào danh sách của bạn." đã được duyệt chưa | **Chưa.** Bảng thông báo MSG không có câu này. Câu viết đúng mẫu "Success = what is done" ở ui-conventions §4, nên có thể giữ, nhưng Linh (người giữ ui-conventions) cần chốt. Không chặn việc nộp. |
| 2 | Báo "đã có trong danh sách" có giữ dạng Toast thông tin không | **Đã có câu trả lời.** ui-conventions §3 ghi Toast có "states: success and informational"; câu "Sách này đã có trong danh sách của bạn." trùng nguyên văn ví dụ "Already done" ở §4. Có thể đóng. |
| 3 | Nhiều bản sách: gộp hay mỗi bản một dòng | **Đã có câu trả lời.** AD-UC-01 §6 câu 1 (chốt 2026-11-04: mỗi bản một dòng); ui-conventions §2 "Shelf location… one line per physical copy". Có thể đóng. |
| 4 | Ảnh xuất 1080px | Thuộc phần ảnh, Chi soát riêng; không đánh giá ở đây. |
| 5 | Đường dẫn mã nguồn wireframe | **Chưa giải quyết.** Thư mục `screens/src/` hiện không có tệp nào của S-F01-01 (chỉ có `Ha-wireframe-1.drawio`, `S-F03-02/06/07.html`, `_template.html`, `components.html`, `tokens.css`). Đây là việc Nhi cần làm, không cần nhóm quyết. |
| Ghi chú #1 (chưa chép) | Tên thành phần cho tên sách | **Đã có câu trả lời:** ui-conventions v0.8 §3 "Section title… including book sections" (có liệt kê S-F01-01). |
| Ghi chú #3 (chưa chép) | Dữ liệu minh hoạ của bản sách thứ 2 | Chỉ cần ghi rõ là dữ liệu mẫu (ui-conventions Q6: mức trung bình, chữ thật). Không cần nhóm quyết. |

### Review S-F01-02 Interactive digital library map — người viết: Nhi
Tóm tắt: Tách hai điểm vào (từ menu OPAC và từ một cuốn sách) rõ ràng, khớp AD-UC-02. Tuy vậy còn lỗi phải sửa: nhãn phòng bằng tiếng Anh, thiếu trạng thái lỗi mạng (FR-04-20), bỏ sót câu hỏi về MSG-07 khi mở từ menu, và mục 3 lệch với ảnh đánh số hiện tại. (Đã bỏ qua mục 2 và tên ảnh theo yêu cầu.)

| # | Mức | Mục | Vấn đề | Bằng chứng | Cách sửa đề xuất |
|---|---|---|---|---|---|
| 1 | Phải sửa | §3 #5, §4, SR-008 | Nhãn phòng chứa sách ghi tiếng Anh `Your book is here`. ui-conventions và tệp ghi chú quy định chữ trên giao diện là "Sách của bạn ở đây". Riêng ảnh đánh số hiện tại lại có chú giải "Phòng chứa sách" — cần thống nhất với wireframe. | Spec dòng 67, 84, 111; `ui-conventions.md` §3 Room tile và §5 ("Sách của bạn ở đây"); `notes/S-F01-02-notes.md` dòng 13; `img/S-F01-02-numbered.png` (chú giải "Phòng chứa sách") | Đổi thành "Sách của bạn ở đây" ở cả 3 chỗ. Nhờ Nhi xem lại chú giải "Phòng chứa sách" trên wireframe: hoặc đưa vào §3, hoặc bỏ khỏi ảnh. |
| 2 | Phải sửa | §4, §7 | Thiếu trạng thái lỗi mạng/tải (MSG-04 + "Thử lại") và thiếu FR-04-20 ở §7. screen-list.md nêu rõ FR-04-20 áp dụng cho S-F01-02. MSG-07 chỉ dùng khi sơ đồ tầng hỏng (FR-01-10), không thay được lỗi mạng. | Spec dòng 73–85, 116–124; `screen-list.md` dòng 30; `screen-spec-chung.md` §5 dòng "4 States" ("Lỗi mạng/tải dùng MSG-04 (FR-04-20)") | Thêm dòng "Error — network/load failure" dùng MSG-04 + "Thử lại", giữ lại dữ liệu đang hiện. Thêm FR-04-20 vào §7. Nếu wireframe chưa vẽ trạng thái này, ghi ở §9 và báo Nhi vẽ bổ sung. |
| 3 | Phải sửa | §4, SR-006, §9 | Tệp ghi chú có câu hỏi mở #1: MSG-07 ghi "Thông tin vị trí kệ vẫn ở phía trên", nhưng khi mở bản đồ từ menu OPAC thì không có thông tin kệ nào. Spec bỏ câu hỏi này và áp "exact MSG-07" cho mọi lối vào. Theo AD-UC-02, nhánh d1 [No] mở từ menu là "no map is drawn" và không có thông tin kệ, nên câu chữ sẽ sai. | Spec dòng 81, 109, 137–145; `notes/S-F01-02-notes.md` dòng 46; AD-UC-02 §3 nhánh d1 [No]; `ui-conventions.md` §4 MSG-07 | Chép câu hỏi sang §9 dưới dạng `[NEEDS CLARIFICATION]`, Blocking = Yes. Trong lúc chờ, chỉ dùng MSG-07 khi mở từ một cuốn sách. Nhờ Linh thêm một biến thể câu chữ cho lối vào từ menu. |
| 4 | Phải sửa | §3, §9 #1 | Dòng #1 và #2 cùng mô tả tiêu đề màn hình, và §9 #1 nói ảnh không có số 2. Ảnh đánh số hiện tại **đã có** số 2 trên tiêu đề. Ảnh còn có hai chữ không nằm trong §3: nhãn "Chọn tầng" phía trên bộ chọn tầng và chú giải "Phòng chứa sách". | Spec dòng 59, 63–64, 141; `img/S-F01-02-numbered.png`; `notes/S-F01-02-notes.md` dòng 9–10 (1 = Back, 2 = Title) | #1 chỉ là nút Quay lại, #2 là tiêu đề "Bản đồ thư viện". Thêm "Chọn tầng" và chú giải vào §3, hoặc nhờ Nhi bỏ khỏi wireframe. Đóng §9 #1. |
| 5 | Phải sửa | Bảng kiểm cuối | Bảng kiểm tự đặt, không phải 7 mục của mẫu. Mục "All numbered elements… documented" đã đánh dấu là sai (xem dòng 4). | Spec dòng 149–160; mẫu dòng 88–97 | Chép nguyên 7 mục của mẫu và chỉ đánh dấu những mục đã kiểm thật. |
| 6 | Nên sửa | §5 #8 | Đích "Activity ends" không phải Screen ID, `stays` hay trang OPAC `(exit)`. | Spec dòng 98; `screen-spec-chung.md` §5 dòng "5 Interactions"; AD-UC-02 d4 [Finish] | Ghi `stays`, hoặc bỏ dòng này vì việc rời màn đã có ở dòng 6–7 (nút Quay lại). |
| 7 | Nên sửa | §3 #9 | Type ghi "Banner / room details area" — không phải một tên trong ui-conventions §3. | Spec dòng 71; `notes/S-F01-02-notes.md` dòng 17 (Banner); `ui-conventions.md` §3 | Chọn đúng một tên: "Banner" (loại info), theo tệp ghi chú. |
| 8 | Nên sửa | Bảng đầu tệp, §3/§4/§5 | Feature thiếu tên; Status không phải một giá trị Draft/Reviewed; tên cột khác mẫu ("Validation / visibility", "Trigger / outcome", "User action / system event"). | Spec dòng 9, 12, 61, 75, 89; mẫu dòng 15, 18, 39, 47, 57 | Ghi `F-01 Book Location & Library Map`, `Draft`, và dùng đúng tên cột của mẫu. |
| 9 | Nên sửa | §8 | Thiếu gạch đầu dòng "phần nào xếp chồng khi màn hẹp" và cỡ chữ tối thiểu. | Spec dòng 126–135; mẫu dòng 75–78; `ui-conventions.md` §6 font/size | Thêm ví dụ: "Floor plan tiles 2 per row at 360px; floor selector stays one row; body 16px, title 20px". |
| 10 | Nên sửa | §6 SR-010 | SR-010 là lời dặn người vẽ ("đừng bịa sơ đồ"), không phải điều màn hình luôn phải giữ, và nguồn chỉ là ghi chú wireframe (không có FR/AD). | Spec dòng 113; `screen-spec-chung.md` §5 dòng "6 Screen-level rules" | Chuyển sang §8 hoặc §9. Nếu giữ, ghi nguồn là FR-01-04 / W0 Table 4 (sơ đồ do nhóm dự án vẽ một lần). |
| 11 | Gợi ý | §3 cột Content | Tên dữ liệu chưa viết theo dạng `<Nhóm W0 Table 4> › <trường>`. | Spec dòng 65–68, 71 | Viết ví dụ `Book placement & library layout › floor`, `› room code`, `› room name`. |
| 12 | Gợi ý | §6 SR-002, SR-007 | Nguồn chưa trỏ tới quyết định đã chốt. | Spec dòng 105, 110; AD-UC-02 §6 câu 1 (tầng thấp nhất, chốt 2026-11-04) và câu 2 (giữ bản đồ tầng trước) | Ghi nguồn `AD-UC-02 Q1`, `AD-UC-02 Q2`. |

#### Câu hỏi mở

| # §9 | Câu hỏi | Tài liệu đã trả lời chưa? |
|---|---|---|
| 1 | Ảnh thiếu số 2 cho tiêu đề | **Đã có câu trả lời:** ảnh `img/S-F01-02-numbered.png` hiện tại đã có số 2 trên tiêu đề. Đánh lại §3 rồi đóng câu này. |
| 2 | Danh sách đủ các tầng và mã phòng từ dữ liệu đồng bộ | **Thật sự cần thư viện cung cấp** (dữ liệu đồng bộ FR-04-09). Không nên để Blocking cho spec: ui-conventions Q6 cho phép dữ liệu mẫu, chỉ R-204 / "Phòng đọc A" là mẫu đã xác nhận. Đề xuất đổi Blocking = No. |
| 3 | Nguồn hình dạng sơ đồ tầng | **Đã có câu trả lời:** W0 Table 4 ("The floor-plan drawing is a fixed asset built once by the project team… room codes must match the internal system") và FR-01-04; ui-conventions §3 Floor plan ("block plan… no real library drawing"). Có thể đóng. |
| 4 | Ảnh xuất 1080px | Thuộc phần ảnh, Chi soát riêng. |
| 5 | Đường dẫn mã nguồn wireframe | **Chưa giải quyết:** `screens/src/` không có tệp nào của S-F01-02. Đây là việc Nhi cần làm. |
| Ghi chú #1 (bị bỏ sót) | Câu chữ MSG-07 khi mở bản đồ từ menu | **Thật sự cần nhóm quyết:** ui-conventions §4 chỉ có một câu MSG-07, chưa có biến thể. Cần Linh bổ sung (xem dòng 3). |

### Review S-F03-03 Saved books list — người viết: Nhi
Tóm tắt: Mục 3 khớp tệp ghi chú và ảnh đánh số (#1–#10). Quy tắc "thiếu vị trí kệ là trạng thái của từng dòng" viết đúng. Phải sửa Priority (đang ghi Must, trái với screen-list là Should), bảng kiểm cuối và phần trỏ tới hộp thoại đăng nhập. Vài câu hỏi ở §9 thực ra tài liệu đã trả lời. (Đã bỏ qua mục 2 và tên ảnh theo yêu cầu.)

| # | Mức | Mục | Vấn đề | Bằng chứng | Cách sửa đề xuất |
|---|---|---|---|---|---|
| 1 | Phải sửa | Bảng đầu tệp, §9 #5 | Priority ghi "Must" và viện dẫn một tệp `screen-list-UC12(3).md` không có trong kho. screen-list.md ghi Should; L8-14 chốt S-F03-03 là Should; W4 xếp FR-03-07 và FR-03-25 Should, FR-03-08 Could. | Spec dòng 8, 146; `screen-list.md` dòng 21; `activity-index.md` L8-14; function list W4 (FR-03-07, FR-03-08, FR-03-25) | Ghi `Should`, đóng §9 #5 với nguồn là screen-list.md và L8-14. |
| 2 | Phải sửa | Bảng kiểm cuối | Bảng kiểm tự đặt, không phải 7 mục của mẫu. | Spec dòng 152–163; mẫu dòng 88–97 | Chép nguyên 7 mục của mẫu và chỉ đánh dấu những mục đã kiểm thật. |
| 3 | Phải sửa | §5 dòng 1, dòng 96 | Đích ghi "`M-F00-01` → `S-F00-01`", và dòng 96 nói hộp thoại được đặc tả trong "shared screen documentation" — chưa trỏ đúng chỗ. Thiếu kết quả khi bấm "Để sau" (AD-UC-12 d1 [No]: từ chối, không hiện danh sách). Thiếu đường quay lại S-F03-03 sau khi nhập đúng mã. | Spec dòng 87, 96; `screen-spec-chung.md` §4.2; `screen-spec-S-F00-01.md` §3.1 (dòng 61); AD-UC-12 §3; `screen-transition.md` (S00_02 → S03_03 "[OTP accepted]") | Ghi `M-F00-01 (see screen-spec-S-F00-01.md §3.1)`. Thêm dòng "Để sau → request ends, list not shown" và "OTP accepted → back to S-F03-03, list loads". |
| 4 | Nên sửa | §5 dòng 8, §6 SR-010, §7 FR-03-06 | "Lưu một cuốn sách" không phải hành động trên màn này, và đích "Existing OPAC book display / `S-F01-01` (outside this screen)" không phải đích hợp lệ; screen-transition không có mũi tên S-F03-03 → S-F01-01. screen-list cũng không giao FR-03-06 cho S-F03-03 (FR-03-06 thuộc S-F01-01). | Spec dòng 94, 111, 118; `screen-list.md` dòng 21 (FR-03-07, FR-03-08, FR-03-25, FR-01-07); `screen-transition.md` dòng S03_03 | Bỏ §5 dòng 8 và bỏ FR-03-06 khỏi §7. Nếu muốn giữ ý này, viết một câu trong §1. |
| 5 | Nên sửa | §6 SR-009, §7, §9 #3 | FR-04-20 bị ghi là "provisional mapping", trong khi screen-list.md nêu rõ S-F03-03 nằm trong phạm vi FR-04-20. | Spec dòng 110, 124, 144; `screen-list.md` dòng 30; `screen-spec-chung.md` §5 dòng "4 States" | Bỏ chữ "provisional" và đóng §9 #3. |
| 6 | Nên sửa | §3 | Ảnh đánh số có dòng phụ đề "Danh sách sách bản giấy bạn đã lưu" dưới tiêu đề, nhưng §3 và tệp ghi chú đều không có. | `img/S-F03-03-numbered.png`; spec dòng 59–70 | Thêm vào ghi chú và §3 (Text, chữ cố định), hoặc nhờ Nhi bỏ khỏi wireframe. |
| 7 | Nên sửa | §5 dòng 3, 4, 6 | Ba dòng này là việc hệ thống hiển thị, không phải hành động của bạn đọc. | Spec dòng 89, 90, 92; mẫu §5 "User action" | Chuyển nội dung sang §4 (trạng thái) và §6; §5 chỉ giữ Back, Bỏ khỏi danh sách, Thử lại và phần đăng nhập. |
| 8 | Nên sửa | Bảng đầu tệp, §3/§4/§5 | Tên màn hình viết "Saved Books List" khác screen-list ("Saved books list", ui-conventions yêu cầu viết hoa kiểu câu). Status không phải một giá trị Draft/Reviewed. Tên cột khác mẫu ("Validation / visibility", "Trigger / outcome", "Element / event"). | Spec dòng 1, 6, 12, 59, 74, 85; `screen-list.md` dòng 21; `ui-conventions.md` §1 (sentence case) | Sửa cho khớp screen-list, ghi `Draft`, dùng đúng tên cột của mẫu. |
| 9 | Nên sửa | §8 | Thiếu gạch đầu dòng "phần nào xếp chồng khi màn hẹp" và cỡ chữ tối thiểu. | Spec dòng 127–136; mẫu dòng 75–78 | Ví dụ: "Book row: cover left, text right; shelf line and Remove button stack below; body 16px, title 20px". |
| 10 | Gợi ý | §3 #5 | Thông báo MSG-06 nằm trong từng dòng sách nhưng ghi kiểu "Banner". Theo ui-conventions, Banner là thông báo cho cả màn và đặt ở đầu nội dung. | Spec dòng 65; `ui-conventions.md` §3 Banner ("Top of the content") và §4 "Where messages go" | Ghi §9 hỏi Linh tên thành phần cho thông báo trong một dòng, hoặc ghi rõ đây là ngoại lệ đã thống nhất. |
| 11 | Gợi ý | §4 / §6 | Chưa nói tới trường hợp đã chốt ở AD-UC-12 câu 2: sách bị lần đồng bộ xoá khỏi danh mục vẫn nằm trong danh sách và hiện "chưa có vị trí kệ". | AD-UC-12 §6 câu 2 (chốt 2026-11-04) | Thêm vào SR-005. |
| 12 | Gợi ý | §3 cột Content | Tên dữ liệu chưa viết theo dạng `<Nhóm W0 Table 4> › <trường>`. | Spec dòng 62, 64 | Ví dụ `Saved books list › book`, `Book catalogue › title / author`, `Book placement & library layout › floor / room code / shelf code`. |
| 13 | Gợi ý | §7 FR-04-08 | screen-list nói FR-04-08 chỉ trích ở các màn đăng nhập, trang nhân viên và hộp thoại M-F00-01. | Spec dòng 123; `screen-list.md` dòng 29 | Chỉ giữ làm nguồn của SR-001 và SR-002. |

#### Câu hỏi mở

| # §9 | Câu hỏi | Tài liệu đã trả lời chưa? |
|---|---|---|
| 1 | Dữ liệu sách mẫu so với danh mục | Không cần nhóm quyết: ui-conventions Q6 cho phép wireframe dùng chữ thật làm mẫu. Đề xuất Blocking = No, chỉ ghi "sample data". |
| 2 | Câu Toast "Đã bỏ sách khỏi danh sách." | **Chưa có trong bảng thông báo MSG.** Câu viết đúng mẫu "Success" ở ui-conventions §4. Cần Linh chốt; không chặn việc nộp. |
| 3 | MSG-04 / FR-04-20 có áp cho màn này không | **Đã có câu trả lời:** `screen-list.md` dòng 30 liệt kê S-F03-03. Có thể đóng. |
| 4 | Câu thông báo danh sách trống | **Đã có câu trả lời:** ui-conventions §4, dòng ví dụ "Empty state", trùng nguyên văn "Bạn chưa lưu sách nào. Bấm Lưu vào danh sách ở trang vị trí kệ sách." (FR-03-25). Có thể đóng. |
| 5 | Priority Must hay Should | **Đã có câu trả lời:** `screen-list.md` dòng 21 = Should; `activity-index.md` L8-14. Có thể đóng (xem dòng 1). |
| 6 | Ảnh xuất 1080px | Thuộc phần ảnh, Chi soát riêng. |
| 7 | Đường dẫn mã nguồn wireframe | **Chưa giải quyết:** `screens/src/` không có tệp nào của S-F03-03. Đây là việc Nhi cần làm. |

## Phần của Trieu

### Review S-F03-02 Reading history and preferences — người viết: Trieu
Tóm tắt: Spec theo mẫu đầy đủ nhất trong nhóm (đủ 9 mục, đủ 5 trạng thái, đủ FR của screen-list). Tuy vậy còn một số chỗ mâu thuẫn với ui-conventions (câu MSG-01 tự đặt, Toast 3 giây, khung focus 3px, dùng Checkbox thay cho Multi-select chips), số thứ tự #7–#11 lệch ảnh đánh số, và có nhiều chi tiết kỹ thuật lẫn vào. Cần một lượt sửa trước khi duyệt.

| # | Mức | Mục | Vấn đề | Bằng chứng | Cách sửa đề xuất |
|---|---|---|---|---|---|
| 1 | Phải sửa | §3 #7–#11 | Số thứ tự lệch ảnh đánh số. Trên ảnh: 7 = ô chọn "Trạng thái đọc", 8 = ô tiến độ, 9 = "Lưu thay đổi", 10 = "Huỷ", 11 = "Cập nhật tiến độ". Spec (và tệp ghi chú) lại đánh: 7 = "Cập nhật tiến độ", 8 = ô chọn trạng thái, 9 = ô tiến độ, 10 = "Lưu thay đổi", 11 = "Huỷ". Bảng kiểm dòng 169 lại ghi là đã khớp. | Spec dòng 63–67, 169; `img/S-F03-02-numbered.png`; `notes/S-F03-02-notes.md` dòng 15–19 | Chọn một bên làm chuẩn: sửa ảnh (sửa nguồn `src/S-F03-02.html` rồi xuất lại) hoặc đánh lại số trong ghi chú và spec. §3, §4 dòng 86 (#9, #16) và §5 (#7–#11) phải dùng cùng một bộ số. |
| 2 | Phải sửa | §5 dòng 1, SR-F03-02-001 | Spec tự đặt câu chữ cho MSG-01: "Bạn cần đăng nhập bằng thẻ thư viện để xem và quản lý lịch sử đọc." Câu chuẩn của MSG-01 là "Bạn cần đăng nhập bằng thẻ thư viện để làm việc này." Hộp thoại M-F00-01 chỉ có 3 biến thể (MSG-01/02/03). | Spec dòng 96, 112; `ui-conventions.md` §4 MSG-01; `screen-spec-S-F00-01.md` dòng 94–96; `screen-spec-chung.md` §6 luật 4 ("Không tạo… MSG mới") | Dùng nguyên văn MSG-01. Nếu muốn câu riêng cho lịch sử đọc, ghi ở §9 và đề xuất với Linh. |
| 3 | Phải sửa | §4 Success | Toast "appears for 3 seconds", trong khi ui-conventions quy định Toast "disappears after 4 seconds". | Spec dòng 88; `ui-conventions.md` §3 Toast | Ghi 4 giây, hoặc chỉ dẫn tới ui-conventions §3. |
| 4 | Phải sửa | §8 | Ghi "3px focus ring", trong khi ui-conventions quy định khung focus 2px. | Spec dòng 150; `ui-conventions.md` §5 ("colour/focus, 2px, 2px offset") | Sửa thành 2px. |
| 5 | Phải sửa | §3 #13, §9 #5 | Chọn chủ đề sở thích đang dùng "Checkbox". ui-conventions v0.8 §3 đã có thành phần riêng "Multi-select chips — choose multiple reading interests (FR-03-05), S-F03-02". Như vậy câu hỏi §9 #5 đã có câu trả lời. | Spec dòng 69, 162; `ui-conventions.md` §3 Multi-select chips | Đổi Type thành Multi-select chips, đóng §9 #5 (nguồn ui-conventions v0.8). Nhờ Trieu sửa wireframe và xuất lại ảnh trước. |
| 6 | Phải sửa | §9 #4 | Câu này ghi "Closed 19/11/2026: Approved provisional text", nhưng tệp ghi chú vẫn ghi "Awaiting final copy sign-off". Đây đúng là lỗi "ghi kết luận tạm như thể đã chốt" mà hướng dẫn chung cảnh báo. | Spec dòng 161; `notes/S-F03-02-notes.md` dòng 61; `screen-spec-chung.md` §5 dòng "9 Open questions" | Nếu đã chốt thật thì ghi ai chốt, ở đâu. Nếu chưa thì để Open. |
| 7 | Nên sửa | §3 cột Type | Một số tên không có trong ui-conventions §3. "Headings" phải là Section title. "Book card" chỉ dùng trong tin trả lời của chatbot (S-F03-06), một dòng sách trong danh sách là Book row. "Progress bar" phải là "Progress bar & label". "Text input" cho ô tiến độ phải là "Number input" (ui-conventions ghi rõ cho S-F03-02). | Spec dòng 59, 60, 62, 65, 68; `ui-conventions.md` §3 (Section title, Book row, Book card, Number input, Progress bar & label) | Đổi đúng tên theo ui-conventions §3. |
| 8 | Nên sửa | §4, §5, §6, §8 | Lẫn chi tiết kỹ thuật (cách làm) vào spec, trong khi spec chỉ nên nói màn hình làm gì: `aria-busy="true"`, `banner.error`, `.toast.is-floating`, "database", "backend", "SVG icons", `--font-heading`, `--size-control`, `:focus-visible`. | Spec dòng 85, 87, 88, 100, 104, 119, 147–150; pbsrs "Content Restrictions"; brief mục C | Viết bằng lời nghiệp vụ, ví dụ "error Banner", "Toast", "saved data stays unchanged", "visible focus ring", và dẫn tới token trong ui-conventions §6. |
| 9 | Nên sửa | §4 Error (Inline) | Câu "Also handles invalid subject preferences" không kiểm tra được: không có câu báo lỗi, không có thành phần hiển thị, không nói lỗi hiện ở đâu. AD-UC-07 d4 [No] → s10 yêu cầu từ chối và hiện thông báo lỗi. | Spec dòng 86; AD-UC-07 §3 nhánh d4 [No]; FR-03-22 | Thêm câu thông báo (Banner hoặc Inline error dưới nhóm chủ đề), hoặc ghi lý do trường hợp này không xảy ra được (chỉ liệt kê chủ đề đã đồng bộ) và chuyển thành câu hỏi ở §9. |
| 10 | Nên sửa | SR-F03-02-002, §3 #9 | "integer constrained strictly between 0 and 100 inclusive" tự mâu thuẫn ("strictly between" nghĩa là không gồm 0 và 100). Chưa nói khi ô để trống hoặc nhập số lẻ (ví dụ 45,5) thì sao, trong khi câu lỗi chỉ nói về khoảng 0–100. | Spec dòng 65, 72, 113; FR-03-04 ("between 0 and 100 percent"); `ui-conventions.md` §2 Reading progress ("whole number 0–100") | Viết "whole number from 0 to 100 inclusive". Thêm quy tắc và câu báo lỗi cho trường hợp ô trống hoặc không phải số nguyên. |
| 11 | Nên sửa | §5 | Thiếu nhánh "Để sau" của hộp thoại đăng nhập (AD-UC-07 d1 [No]: từ chối, không hiện gì). Chỉ có nhánh đăng nhập. | Spec dòng 96, 112; AD-UC-07 §3 nhánh "d0 [No] → d1 [No]" | Thêm dòng: "Để sau → modal closes, history not shown". |
| 12 | Nên sửa | §6 | Chưa ghi phần sở thích là phần Could (FR-03-05), tức là có thể cắt bỏ mà vẫn giữ màn hình. | Spec dòng 108–119; `screen-list.md` dòng 32; `Trieu-screen-spec.md` dòng 41; W4 FR-03-05 Could | Thêm quy tắc: "Preferences section (#12–#14) is Could scope (FR-03-05); removable without removing the screen." |
| 13 | Nên sửa | §2 | Đường dẫn tới ui-conventions trỏ vào một thư mục trên máy cá nhân (`file:///C:/Users/admin/.gemini/...`), người khác mở không được. | Spec dòng 49 | Dùng đường dẫn tương đối `../ui-conventions.md#6-design-tokens`. |
| 14 | Gợi ý | §6 | Mã quy tắc viết "SR-F03-02-001", khác mẫu "SR-001". | Spec dòng 112–119; mẫu dòng 65 | Dùng SR-001…SR-008. |
| 15 | Gợi ý | §3 cột Required | Các thành phần chỉ hiện theo điều kiện (#15 Empty, #16 lỗi, #17 Banner, #18 Toast, #19 Skeleton) lại ghi Required = "Yes". | Spec dòng 71–75 | Ghi "Conditional" hoặc "No". |
| 16 | Gợi ý | §4, §5 | "FR-03-01*" có dấu sao nhưng không giải thích. Đích "Existing OPAC personal area" thiếu chữ `(exit)`. | Spec dòng 84, 97; `screen-spec-chung.md` §5 dòng "5 Interactions" | Bỏ dấu sao (hoặc giải thích), thêm `(exit)`. |
| 17 | Gợi ý | §7 FR-04-08 | screen-list nói FR-04-08 chỉ trích ở các màn đăng nhập, trang nhân viên và hộp thoại M-F00-01. | Spec dòng 133; `screen-list.md` dòng 29 | Chỉ giữ làm nguồn của SR-001. |

#### Câu hỏi mở

Spec không có `[NEEDS CLARIFICATION]` nào.

| # §9 | Câu hỏi | Tài liệu đã trả lời chưa? |
|---|---|---|
| 1–3 | Trạng thái ban đầu; mượn lại cùng sách; "Đã đọc xong" khi chưa đủ 100% | **Đã đóng đúng:** AD-UC-07 §6 câu 1, 2, 4 (chốt 2026-11-04). Không cần làm gì thêm. |
| 4 | Câu thông báo lịch sử trống | **Chưa có nguồn chốt:** ui-conventions §4 không có câu này; tệp ghi chú vẫn ghi đang chờ. Cần Linh chốt, hoặc ghi rõ ai đã chốt ngày 19/11 (xem dòng 6). |
| 5 | Dùng Checkbox hay chip cho sở thích | **Đã có câu trả lời:** ui-conventions v0.8 §3 "Multi-select chips… (FR-03-05) S-F03-02". Đóng câu này, sửa wireframe và §3 (xem dòng 5). |
| Mới | Câu MSG-01 riêng cho lịch sử đọc (dòng 2) | Nếu nhóm muốn có câu riêng thì **cần Linh quyết** (thêm biến thể vào ui-conventions §4 và S-F00-01 §3.1). Còn không thì dùng MSG-01 chuẩn. |
| Mới | Câu báo lỗi khi chọn sở thích không hợp lệ (dòng 9) | **Cần nhóm quyết:** chưa có câu nào trong tài liệu. AD-UC-07 Q3 chỉ định nghĩa điều kiện "hợp lệ". |

### Review S-F03-06 AI chatbot book search — người viết: Trieu

Tóm tắt: Chưa sẵn sàng nộp. Spec chưa khớp ảnh ở 4 chỗ: số trên ảnh đánh số, chữ gợi ý trong ô nhập, chữ của liên kết trong thông báo lỗi, và câu "không tìm thấy sách". Lỗi mạng đang bị gộp vào thông báo lỗi AI, nên FR-04-20 và MSG-04 không được thực hiện. Quy tắc SR-009 ghi sai nguồn. Phần tốt: hỏi đăng nhập sau khi gửi tin đầu tiên (L8-05), dùng đúng MSG-02, các câu đã chốt ngày 04/11 ghi đúng là đã đóng.

| # | Mức | Mục | Vấn đề | Bằng chứng | Cách sửa đề xuất |
|---|---|---|---|---|---|
| 1 | Phải sửa | §3 so với ảnh đánh số | Số trên ảnh không khớp spec. Ảnh S-F03-06-numbered có các số 1, 2, 3, 8, 9: số 3 chỉ khung hội thoại trống, số 8 là ô nhập, số 9 là "Gửi". Trong spec, #3 là bong bóng của bạn đọc, #7 là ô nhập, #8 là "Gửi". Khối chào "Hỏi trợ lý tìm sách / Nhập câu hỏi bằng ngôn ngữ tự nhiên…" có trên ảnh nhưng không có ở §3. Các số #4–#6 và #9–#11 không có trên ảnh đánh số nào. | §3 dòng 57–67. Ảnh img/S-F03-06-numbered.png. screen-spec-chung.md §5 (số # phải khớp ảnh). Trieu-nhan-xet-wireframe.md C3. | Đánh lại số cho khớp. Thêm khối chào vào §3, hoặc bỏ khỏi ảnh (Trieu-nhan-xet S-F03-06 #10 đã đề nghị bỏ hoặc hỏi nhóm). Chụp thêm ảnh đánh số cho trạng thái có kết quả và trạng thái lỗi. |
| 2 | Phải sửa | §1, §3 #7, #10, §5 dòng 6 | Chữ trong spec khác chữ trên ảnh. (a) Chữ gợi ý ô nhập: spec ghi "Nhập câu hỏi tìm sách…"; ảnh ghi "Nhập câu hỏi của bạn..." (Default), "Nhập câu hỏi tiếp theo..." (có kết quả), "Nhập câu hỏi khác..." (không có kết quả), "Tìm kiếm AI tạm thời gián đoạn" (lỗi). (b) Câu ở #10: spec "Rất tiếc, thư viện chưa có…"; ảnh "Không tìm thấy sách nào phù hợp với yêu cầu trên. Bạn hãy thử tìm với các chủ đề liên quan như Thủ công mỹ nghệ, Kỹ năng dã ngoại hoặc chọn từ khóa khác nhé." (c) Liên kết trong thông báo lỗi: spec ghi "dùng bộ lọc hình thức" / "Dùng bộ lọc hình thức"; ảnh ghi "Lọc theo hình thức". | Dòng 29, 63, 66, 93. Ảnh S-F03-06.png, -success, -no-match, -error. screen-spec-chung §6 quy tắc 2 (spec phải khớp wireframe). | Chọn một cách viết cho mỗi chữ, rồi sửa cả ảnh và spec cho trùng từng chữ. |
| 3 | Phải sửa | §4 Error, §7 FR-04-20 | Lỗi mạng hoặc lỗi tải đang dùng chung thông báo lỗi AI (FR-03-17). Không có Banner MSG-04 "Không tải được trang. Bạn kiểm tra kết nối mạng rồi thử lại." kèm nút "Thử lại" như FR-04-20 và ui-conventions §4 quy định. Mục 7 ghi "MSG-04 / FR-03-17 error banner", nhưng ở §3 không có thành phần MSG-04 nào. Mất mạng mà lại khuyên bạn đọc "dùng bộ lọc hình thức" là không hợp lý, vì bộ lọc cũng cần mạng. | Dòng 80, 123. FR-04-20. ui-conventions MSG-04. screen-list.md dòng 30 và 58. | Thêm thành phần Banner MSG-04 và nút "Thử lại", cùng trạng thái lỗi riêng. Thông báo FR-03-17 chỉ dùng khi dịch vụ AI lỗi hoặc quá 10 giây. |
| 4 | Phải sửa | §6 SR-F03-06-009 | Quy tắc ghi nguồn là W0 Table 3 cho các mục "voice input, file/image attachments, thumbs up/down rating, conversation management dashboards". W0 Table 3 không có các mục này; bảng đó chỉ có like/dislike cho sách và báo cáo đánh giá cho nhân viên. Đây là phạm vi tự đặt, không có nguồn. | Dòng 109. function-list.md W0 Table 3. screen-list.md dòng 106 ("Floating chatbot widget"). | Bỏ SR-009, vì spec chỉ ghi những gì màn làm. Nếu muốn giữ thì chỉ giữ ý "không có widget nổi", nguồn là screen-list / L8-13. |
| 5 | Phải sửa | §3 | Các thành phần hiển thị dữ liệu chưa ghi trường dữ liệu: #3 và #4 (nên ghi `Chatbot conversations › reader message / reply`), #5 (nên ghi `Book catalogue › title, author, access format`). Ở checklist, dòng 161 đã đánh dấu đạt mục này dù chưa đạt. | Dòng 59–61, 161. Checklist của mẫu. screen-spec-chung §5 cột Content. | Ghi theo dạng `<Nhóm W0 Table 4> › <trường>`; chỉ đánh dấu checklist sau khi đã kiểm. |
| 6 | Nên sửa | §4 Default, Empty | Default ghi "Previous session history loaded if authenticated" (hiện lại hội thoại cũ khi đã đăng nhập). Không FR nào yêu cầu hiển thị lại: FR-03-10 chỉ yêu cầu lưu, AD-UC-08 câu hỏi 3 nói giữ lại chứ không nói hiện lên. Ảnh Default lại là khung trống. Empty ghi "identical to Default (§2.3)", nhưng spec không có mục §2.3 nào. | Dòng 75–76. | Bỏ câu hiển thị lịch sử, hoặc đưa vào mục 9. Ghi rõ §2.3 là của tài liệu nào, hoặc bỏ. |
| 7 | Nên sửa | §3 #7, #8, §5 dòng 2–3 | Ô nhập còn mâu thuẫn. (a) Loại ghi "Text input" (theo ui-conventions là ô một dòng) nhưng mô tả "Multi-line". (b) Không có giới hạn độ dài. (c) #7 ghi "Non-empty string", còn §5 ghi "non-whitespace text", hai quy tắc khác nhau. (d) Nếu ô nhiều dòng thì phím Enter là gửi hay xuống dòng? (e) Trên ảnh Default, nút "Gửi" đang bật dù ô trống, trái với #8 ("disabled when input is empty"). | Dòng 63–64, 89–90. Ảnh S-F03-06.png. | Thống nhất một dòng hay nhiều dòng. Ghi quy tắc: "ít nhất 1 ký tự không phải khoảng trắng, tối đa N ký tự". Vẽ lại nút Gửi ở trạng thái tắt. |
| 8 | Nên sửa | §4 Error | Ảnh lỗi khoá ô nhập (chữ "Tìm kiếm AI tạm thời gián đoạn", nút Gửi màu xám) nhưng spec không nhắc tới. Nếu ô bị khoá thì bạn đọc không gửi tin khác được (AD-UC-08 d4 [Send another message]), và spec không nói khi nào ô mở lại. | Ảnh -error. Dòng 80. | Ghi rõ ô nhập có bị khoá không và khi nào mở lại. |
| 9 | Nên sửa | §3 #5, #10, §4 Success | (a) Không ghi một câu trả lời có tối đa bao nhiêu thẻ sách (số 4 chỉ là dữ liệu mẫu). (b) Không nói thẻ sách trực tuyến mở ra đâu; AD-UC-08 c2 chỉ nói về sách giấy (đi tiếp UC-01). (c) Câu #10 là câu cố định hay do trợ lý soạn? Ảnh có gợi ý chủ đề cụ thể, và FR-03-16 yêu cầu "suggest alternative search terms or subjects". | Dòng 61, 66, 78. FR-03-16. AD-UC-08 c2. | Ghi số thẻ tối đa. Ghi rõ #10 do trợ lý soạn và phải có ít nhất 1 từ khoá hoặc chủ đề gợi ý; câu trong spec chỉ là ví dụ. |
| 10 | Nên sửa | §6, §9 | Mã quy tắc viết "SR-F03-06-001…", khác mẫu ("SR-001…"). Câu hỏi mở số 4 chưa viết theo dạng `[NEEDS CLARIFICATION: …]`. | Dòng 101–109, 150. Template §6, §9. screen-spec-chung §5. | Đổi mã thành SR-001…; viết lại câu hỏi 4 theo mẫu. |
| 11 | Nên sửa | §2 | Liên kết trỏ tới một tệp trên máy cá nhân ("file:///C:/Users/admin/.gemini/antigravity/…"), người khác mở không được. | Dòng 49. | Dùng đường dẫn tương đối: `../ui-conventions.md#6-design-tokens`. |
| 12 | Nên sửa | §8 | Trên ảnh lỗi, liên kết màu xanh nằm trên nền đỏ nhạt. Trieu-nhan-xet S-F03-06 #3 đã đo độ tương phản 4,26:1, dưới mức 4,5:1. Mục 8 không nhắc. Vùng chạm cho liên kết "Xem chi tiết sách" cũng chưa ghi. | Ảnh -error. ui-conventions §6 (màu liên kết chỉ dùng trên nền trắng hoặc nền trang). | Ghi màu liên kết trong Banner lỗi đạt 4,5:1. Ghi vùng chạm 44px. |
| 13 | Gợi ý | §6 SR-004 | Ghi "permanently retained" (lưu vĩnh viễn), trong khi AD-UC-08 câu hỏi 3 chỉ nói "kept for the whole release" (giữ suốt bản phát hành). | Dòng 104. | Sửa theo đúng câu của AD. |
| 14 | Gợi ý | §6 SR-007, §8 | Có chi tiết kỹ thuật: "SVG icons", ".message-composer", "--font-heading", "--size-control". | Dòng 107, 130, 136, 139. | Dùng tên thành phần và tên token trong ui-conventions; bỏ tên lớp và biến CSS. |
| 15 | Gợi ý | §5 dòng 4 | Bạn đọc chọn "Để sau" trong M-F00-01 thì nội dung đã gõ có còn trong ô không? (Kiểm thử của AD-UC-08: "the message is not sent".) | Dòng 91. | Ghi rõ nội dung vẫn giữ trong ô nhập. |

#### Câu hỏi mở

| Câu | Đánh giá |
|---|---|
| Q1–Q3 (10 giây, không lưu thông báo lỗi, không xoá hội thoại) | Đóng đúng theo AD-UC-08 câu hỏi 1–3 (chốt 04/11/2026). |
| Q4 Nhãn liên kết trên thẻ sách ("Xem chi tiết sách" hay "Xem sách") | Chưa tài liệu nào trả lời: ui-conventions §3 (Book card) chỉ ghi "Text link to the book", còn bảng nhãn chuẩn ở §1 chưa có. Linh chốt; không chặn. Trieu-nhan-xet #8 đề xuất "Xem sách". |
| Còn thiếu ở mục 9 | (a) Khối chào trên màn trống: giữ hay bỏ (Trieu-nhan-xet #10). (b) Có hiển thị lại hội thoại cũ không (dòng 6 ở bảng trên). |

### Review S-F03-07 Book recommendations — người viết: Trieu

Tóm tắt: Khung đủ. Các quy tắc 10 sách, "xu hướng" trong 30 ngày, sách phổ biến và MSG-03 lấy đúng từ AD-UC-09; mọi FR của màn trong screen-list có ở §7. Nhưng số trên ảnh đánh số và câu phụ đề không khớp spec, điều kiện "chưa có dữ liệu" và "bổ sung xu hướng" lệch với FR-03-19 và FR-03-20, và quyết định "không gắn nhãn Xu hướng" đang ghi như đã chốt dù nhóm chưa chốt.

| # | Mức | Mục | Vấn đề | Bằng chứng | Cách sửa đề xuất |
|---|---|---|---|---|---|
| 1 | Phải sửa | §3 so với ảnh đánh số | Số trên ảnh không khớp spec. Ảnh S-F03-07-numbered: số 3 là phụ đề, số 4 là nút "Sở thích", số 6/7/8 là tên sách, tác giả, nhãn hình thức. Trong spec: #3 là "Sở thích", #4 là phụ đề, #6–#8 là thông báo khi chưa có dữ liệu, liên kết và tiêu đề "Sách phổ biến". Các số #6–#12 của spec không có trên ảnh nào. | Dòng 57–68. Ảnh img/S-F03-07-numbered.png. Trieu-nhan-xet-wireframe.md C3. | Đánh lại số cho khớp. Chụp thêm ảnh đánh số cho trạng thái chưa có dữ liệu và trạng thái lỗi. |
| 2 | Phải sửa | §3 #4 | Câu phụ đề khác ảnh. Spec: "…dựa trên lịch sử đọc và chủ đề bạn quan tâm." Ảnh Default: "…dựa trên lịch sử đọc và sở thích của bạn (hiển thị 4 trong 10 sách)." Phần trong ngoặc là ghi chú của bản vẽ bị lẫn vào chữ trên màn. Ảnh trạng thái bổ sung xu hướng có câu khác: "Gợi ý được cá nhân hoá kết hợp sách mượn nhiều trong 30 ngày qua."; câu này không có trong spec. | Dòng 60. Ảnh -numbered, -topped-up. | Ghi nguyên văn câu cho từng trạng thái. Bỏ "(hiển thị 4 trong 10 sách)" khỏi chữ trên màn. |
| 3 | Phải sửa | §4 Cold-start, SR-004 | Điều kiện "chưa có dữ liệu" thiếu hội thoại chatbot. FR-03-19 và AD-UC-09 d2 đều nói: không có lịch sử đọc, không có sở thích VÀ không có hội thoại chatbot. Spec chỉ ghi "zero reading history and zero subject preferences" / "no loans, online reads, or preferences". Một bạn đọc đã trò chuyện với chatbot nhưng chưa đọc sách sẽ bị xếp vào trạng thái sai. | Dòng 77, 106. FR-03-19. AD-UC-09 d2. | Thêm điều kiện "và không có hội thoại chatbot". |
| 4 | Phải sửa | §4 Topped-up, SR-003 | Điều kiện "greater than 0 but strictly fewer than 3" bỏ sót trường hợp bạn đọc có dữ liệu nhưng không có sách nào khớp. Theo AD-UC-09 d3 [No], "fewer than three" gồm cả 0, nên trường hợp này cũng phải bổ sung sách xu hướng. Hiện không trạng thái nào xử lý trường hợp đó. SR-003 ghi "until at least 3 … (up to 10 total)": chưa rõ thêm bao nhiêu sách xu hướng. | Dòng 78, 105. FR-03-20. AD-UC-09 d3. | Sửa điều kiện thành "fewer than 3 (including 0)". Ghi số sách xu hướng được thêm, ví dụ thêm cho đủ 10, hoặc cho đủ 3. |
| 5 | Phải sửa | §6 SR-006, §9 | Quyết định "sách xu hướng không gắn nhãn" lấy nguồn là tệp nhận xét Trieu-nhan-xet-wireframe.md, không phải FR, AD, L8 hay quyết định của nhóm. Trieu-screen-spec.md dặn: "Nhãn 'Xu hướng' … giữ ở mục 9 cho đến khi nhóm chốt", nhưng §9 không có câu hỏi này. | Dòng 108. Trieu-screen-spec.md §3 (S-F03-07). screen-spec-chung §5 (nguồn hợp lệ cho cột Source). | Chuyển thành câu hỏi `[NEEDS CLARIFICATION: …]` với phương án đang vẽ là "không gắn nhãn". Bỏ SR-006, hoặc ghi nguồn là câu hỏi đó. |
| 6 | Nên sửa | §3 #3, §9 Q5 | "Sở thích" ghi là Text link nhưng trên ảnh là nút có viền (Secondary button). Ảnh trạng thái chưa có dữ liệu không có nút này, trong khi Q5 ghi "kept in header in all states". | Dòng 59, 149. Ảnh -cold-start, -numbered. | Thống nhất loại thành phần, và ghi rõ trạng thái nào có nút. |
| 7 | Nên sửa | §5 dòng 1, §4 | Với bạn đọc chưa đăng nhập: spec không nói phía sau hộp thoại màn hiện gì, và sau khi chọn "Để sau" thì màn hiện gì. AD-UC-09 d1 [No]: "no list is shown"; screen-transition: chọn Not now thì ở lại màn. Như vậy đang thiếu một trạng thái. | Dòng 90. Kiểm thử AD-UC-09 d0 [No] → d1 [No]. | Thêm trạng thái "Signed out", ví dụ chỉ có tiêu đề và lời mời đăng nhập, không có danh sách. Nếu chưa vẽ thì ghi vào mục 9. |
| 8 | Nên sửa | §3 #4, #8 | Loại thành phần "Paragraph text" và "Headings" không có trong ui-conventions §3 (ở đó có "Section title"). | Dòng 60, 64. ui-conventions §3. | Dùng "Section title". Với phụ đề, hỏi Linh nên dùng tên thành phần nào. |
| 9 | Nên sửa | §3 #5, #9, #10 | Còn thiếu tên trường dữ liệu: nhãn hình thức (`Book catalogue › access format`); #9 và #10 không ghi trường nào. "Ranked by loan/QR scan count" không rõ tiêu chí nào xếp trước. | Dòng 61, 65, 66. | Ghi tên trường. Ghi rõ: xếp theo lượt quét QR (FR-03-19); chỉ dùng lượt mượn khi việc đếm lượt quét (FR-02-06) bị cắt (AD-UC-09 câu hỏi 1). |
| 10 | Nên sửa | §9 Q1, SR-004, #6 | Q1 ghi như thể luôn dùng lượt mượn ("Use highest loan counts"), nhưng AD-UC-09 câu hỏi 1 chỉ áp dụng khi việc đếm lượt quét bị cắt. Câu thông báo #6 lại nói "quan tâm nhiều nhất qua mã QR"; nếu chuyển sang lượt mượn thì câu này sai. | Dòng 145, 106, 62. AD-UC-09 câu hỏi 1. | Ghi kèm điều kiện. Chuẩn bị câu thông báo không phụ thuộc vào cách xếp hạng. |
| 11 | Nên sửa | §8 | Ghi tác giả cỡ chữ 14px, nhưng ui-conventions §6 quy định tác giả 16px trên màn bạn đọc. Giãn dòng tên sách ghi 1.4, khác token (1.3). | Dòng 135–136. ui-conventions §6 (font/size, font/line-height). | Sửa theo token. |
| 12 | Nên sửa | §2, §4, §6, §9 | Các lỗi về hình thức giống S-F03-06: (a) mã quy tắc "SR-F03-07-00x" khác mẫu SR-001; (b) câu hỏi 4 và 5 chưa viết theo dạng `[NEEDS CLARIFICATION]`; (c) liên kết trỏ tới tệp trên máy cá nhân (file:///…); (d) lý do "Not applicable" ở §4 viết bằng tiếng Việt, trong khi spec phải viết tiếng Anh. | Dòng 49, 81–82, 103–109, 148–149. screen-spec-chung §5. | Sửa theo mẫu. |
| 13 | Gợi ý | §4, §6 SR-007, §8 | Có chi tiết kỹ thuật: "aria-busy", "banner.error", "SVG icon", "--size-control". | Dòng 79, 80, 109, 137. | Dùng tên thành phần và tên token trong ui-conventions. |
| 14 | Gợi ý | §4 Empty | Spec ghi "không bao giờ trống", nhưng chưa nói nếu danh sách sách phổ biến cũng trống (chưa có lượt quét hay lượt mượn nào) thì sao. | Dòng 81. | Thêm một câu dự phòng, hoặc giải thích vì sao trường hợp này không xảy ra. |
| 15 | Gợi ý | §3 cột Required | Mọi dòng đều ghi "Yes", kể cả thành phần chỉ hiện ở một trạng thái (#6, #9–#12). | Dòng 62–68. | Ghi "No" cho các thành phần chỉ hiện theo trạng thái. |

#### Câu hỏi mở

| Câu | Đánh giá |
|---|---|
| Q1 Xếp hạng sách phổ biến | Đóng nhưng ghi sai điều kiện (xem dòng 10 ở bảng trên). AD-UC-09 câu hỏi 1 có câu trả lời, nhưng chỉ áp dụng khi việc đếm lượt quét bị cắt. |
| Q2 Định nghĩa "xu hướng", Q3 10 sách | Đóng đúng theo AD-UC-09 câu hỏi 2 và 3 (chốt 04/11/2026). |
| Q4 Nhãn giải thích lý do gợi ý | Không FR nào yêu cầu. Theo luật của nhóm "không thêm tính năng không có FR", có thể đóng là "No in release 1" (Trieu-nhan-xet #2 cũng đề xuất phương án tạm là "không"). Muốn có thì phải thêm FR mới, nhóm quyết. |
| Q5 Nút "Sở thích" hiện ở mọi trạng thái | Hai tài liệu chung lệch nhau. `screen-transition.md` chỉ cho S-F03-07 → S-F03-02 khi "[no reading data yet]". AD-UC-09 d4 "[Set reading preferences]" (reading notes: "or the reader's own wish") và bảng của screen-list (AD-UC-09 c3) lại cho phép lúc nào cũng được. Cần nhóm chốt rồi sửa screen-transition cho khớp (Trieu-nhan-xet #13). |
| Còn thiếu ở mục 9 | (a) Nhãn "Xu hướng" (dòng 5 ở bảng trên). (b) Màn hiện gì khi bạn đọc chưa đăng nhập chọn "Để sau" (dòng 7). |
