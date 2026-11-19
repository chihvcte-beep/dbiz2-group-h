# Screen Spec — phần việc của Linh

| Mục | Nội dung |
|---|---|
| Người thực hiện | **Linh** |
| Đọc kèm | `huong-dan/screen-spec-chung.md` (luật chung, cách điền, lời nhắc AI, checklist) |
| Phiên bản | v1.0 · 19/11/2026 |
| Vai trò | Viết 3 spec + **cổng soát cuối** cho cả 15 spec |
| Soát chéo | Spec của bạn do người vẽ wireframe gốc soát: **Ha** (S-F00-03, S-F04-01), **Nhi** (S-F03-01) |

## 1. Spec bạn viết

Bạn viết spec cho 3 màn **người khác vẽ wireframe**. Đầu vào là tệp ghi chú và ảnh của họ; chỗ nào
chưa rõ thì hỏi thẳng người vẽ, không tự đổi wireframe.

| # | Tệp | Màn hình | Actor · khổ | Priority | AD | Người vẽ |
|---|---|---|---|---|---|---|
| 1 | `screen-spec-S-F00-03.md` | Staff sign in | On-site Staff · 1280px | Must | AD-UC-10, AD-UC-13 | Ha |
| 2 | `screen-spec-S-F04-01.md` | Staff page | On-site Staff · 1280px | Must | AD-UC-10, AD-UC-13 | Ha |
| 3 | `screen-spec-S-F03-01.md` | Access-format filter and results | Reader · 360px | Should | AD-UC-03 | Nhi |

Ảnh riêng của 3 màn này do Ha và Nhi xuất (hạn 21/11).

### S-F00-03
- Một thông báo lỗi chung cho sai tài khoản hoặc không có quyền nhân viên, cho thử lại (FR-04-18,
  L8-03). Thành công → S-F04-01 (FR-04-07).
- Không có "Quên mật khẩu", "Ghi nhớ đăng nhập", đăng ký (không có FR).

### S-F04-01
- Chỉ 2 lựa chọn: "Print QR labels" → S-F02-03, "Reported reviews" → S-F02-04 (L8-04); ô thứ hai là
  phần Could.
- Không có phiên nhân viên → S-F00-03 mở thay: là **điều hướng**, ghi ở mục 6, không phải trạng thái
  lỗi (FR-04-08). Empty và các trạng thái không áp dụng: ghi lý do.
- Còn mở: có nút đăng xuất không.

### S-F03-01
- Câu hỏi **Q5** của tệp chung (lựa chọn sẵn khi mới mở) cần chốt với Nhi và nhóm.
- Lọc trên **toàn bộ danh mục đã đồng bộ** (L8-12); sách online mở trên OPAC hiện có → `(exit)`.
- Không có kết quả → "chọn định dạng khác" (FR-03-23). Tệp ghi chú của Nhi nói trạng thái lỗi trên
  ảnh chỉ là chỗ giữ chỗ: nếu dùng thì gắn **FR-04-20 / MSG-04**, nếu không thì ghi Not applicable.
- Tệp ghi chú chưa ghi Frame, phiên bản UI conventions và Author ở dòng đầu — nhắc Nhi bổ sung.

## 2. Việc của cổng soát (bắt đầu ngay)

### 2.1 Trước khi cả nhóm viết spec (hạn 21/11)

Điền bảng **"Consistency review"** ở `ui-conventions.md` §7 cho 20 wireframe (đang trống). Các điểm
đã thấy khi gộp bài, cần ghi vào bảng:

| Điểm | Màn |
|---|---|
| Ảnh đánh số sai khổ: 773px (cần 1080px) và 1693px (cần 1280px) | Toàn bộ wireframe của Ha |
| Ảnh đánh số sai khổ: 1740px (cần 1080px) | S-F01-01, S-F03-01, S-F03-03 (Nhi); S-F03-02, S-F03-06, S-F03-07 (Trieu) |
| Chưa có ảnh riêng từng trạng thái, chỉ có ảnh ghép `-states.png` | Toàn bộ 20 wireframe |
| HTML không liên kết `tokens.css`, tự khai báo màu trong tệp (30–40 mã màu mỗi tệp) — cần đối chiếu với token | S-F03-02, S-F03-06, S-F03-07 |
| Chưa có mã nguồn wireframe trong `screens/src/` | Wireframe của Nhi và Hoa |
| Ghi chú chưa theo dòng đầu chuẩn (Frame · UI conventions · Author) | S-F01-02, S-F03-01 |

Thêm một dòng Change log khi bảng điền xong, và ghi kết luận Q1–Q5 sau buổi họp chốt.

### 2.2 Soát cuối 15 spec (hạn 26/11)

Với mỗi spec, ngoài checklist mục 9 của tệp chung, soát **tính nhất quán giữa các spec**:

- Cùng một thành phần → cùng tên ở mọi spec (Review item, Screen header, Banner…).
- Cùng một thông báo → cùng câu chữ tiếng Việt, cùng mã MSG-xx.
- M-F00-01 chỉ được viết ở `screen-spec-S-F00-01.md`; spec khác chỉ trỏ tới.
- Khung đánh giá ở S-F02-01 và S-F02-02 dùng cùng tên thành phần.
- Mọi đích điều hướng khớp `screen-transition.md`; không màn nào cụt đường.
- Cùng tên trường dữ liệu `<Nhóm W0 Table 4> › <trường>` ở mọi spec.

Spec đạt → đổi Status thành `Reviewed`. Ghi kết quả soát vào bảng Consistency review (thêm cột hoặc
dòng "Screen Spec").
