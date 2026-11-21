# Việc còn lại: ảnh trạng thái và Screen Spec

| Mục | Nội dung |
|---|---|
| Cập nhật | 21/11/2026 |
| Đọc kèm | `huong-dan/screen-spec-chung.md` (luật chung), tệp `<Tên>-screen-spec.md` của bạn |
| Hạn | Ảnh tách: **càng sớm càng tốt** (hạn cũ 21/11) · Spec nháp: **24/11** · Soát chéo: **25/11** · Linh soát cuối, gộp: **26/11** |

## 1. Đã làm ngày 21/11

- Gộp nhánh `plinh` và `pnhi` vào `main`.
- Bản wireframe mới của **Hoa** (6 màn/modal) và **Nhi** (4 màn) đã thay bản cũ trong
  `screens/notes/` và `screens/img/`. Các tệp trùng ở thư mục gốc (`F02-01 notes.md`,
  `S-F01-01-notes (1).md`…) đã xoá.
- 9 spec đã có được đổi tên và chuyển vào `EXTERNAL DESIGN/screens/screen-spec-<ID>.md`.
- `ui-conventions.md` đã lên **v0.8** (bản của Linh).

**Trước khi làm tiếp, lấy bản mới nhất của `main`** (tải lại trang GitHub, hoặc `git pull`). Đừng
dùng bản tải về máy từ trước 21/11.

## 2. Tình trạng 15 màn

| Màn | Người vẽ | Ảnh đánh số đúng khổ | Ảnh tách trạng thái | Spec | Người viết spec |
|---|---|---|---|---|---|
| S-F00-01 (+ M-F00-01) | Ha | ❌ 773px | ❌ | ❌ chưa có | Ha |
| S-F00-02 | Ha | ❌ 773px | ❌ | ❌ chưa có | Ha |
| S-F00-03 | Ha | ❌ 1693px | ❌ | ✅ có | Linh |
| S-F02-03 (+ M-F02-03-01) | Ha | ❌ 1693px | ❌ | ❌ chưa có | Ha |
| S-F04-01 | Ha | ❌ 1693px | ❌ | ✅ có | Linh |
| S-F02-01 (+ M-F02-01-01, M-F02-01-02) | Hoa | ✅ | ❌ | ✅ có | Hoa |
| S-F02-02 | Hoa | ✅ | ❌ | ✅ có | Hoa |
| S-F02-04 (+ M-F02-04-01) | Hoa | ✅ | ❌ | ✅ có | Hoa |
| S-F01-01 | Nhi | ✅ | ❌ | ✅ có | Nhi |
| S-F01-02 | Nhi | ✅ | ❌ | ✅ có | Nhi |
| S-F03-01 | Nhi | ✅ | ❌ | ✅ có | Linh |
| S-F03-03 | Nhi | ✅ | ❌ | ✅ có | Nhi |
| S-F03-02 | Trieu | ❌ 1740px | ❌ | ❌ chưa có | Trieu |
| S-F03-06 | Trieu | ❌ 1740px | ❌ | ❌ chưa có | Trieu |
| S-F03-07 | Trieu | ❌ 1740px | ❌ | ❌ chưa có | Trieu |

Khổ đúng: màn **Reader rộng 1080px** (khung 360px × DPR 3), màn **Staff rộng 1280px** (DPR 1).
Xem khổ ảnh trên Windows: chuột phải vào ảnh › Properties › Details › Width.

## 3. Việc của từng người

Tất cả ảnh để trong `[DBIZ 2] GROUP H/EXTERNAL DESIGN/screens/img/`. Tên ảnh phải **đúng từng ký tự**
như dưới đây (spec đã trỏ sẵn tới các tên này).

### Ha

1. **Sửa màu theo token** (Linh soát: draw.io đang dùng màu ngoài `tokens.css`, nút chính màu tối, lỗi
   màu xám) trong `screens/src/Ha-wireframe-1.drawio`.
2. **Xuất lại ảnh đánh số đúng khổ** cho cả 7 wireframe: S-F00-01, S-F00-02, M-F00-01 rộng 1080px;
   S-F00-03, S-F02-03, S-F04-01, M-F02-03-01 rộng 1280px. Xuất từ draw.io (File › Export as › PNG,
   đặt chiều rộng), không chỉnh ảnh bằng tay. Tải lên với **cùng tên cũ** để thay bản cũ.
3. **Xuất ảnh tách trạng thái** (theo phần "States drawn" trong tệp ghi chú của bạn):

   | Màn | Ảnh cần có |
   |---|---|
   | S-F00-01 | `S-F00-01.png`, `-loading.png`, `-loading-numbered.png`, `-error.png`, `-error-numbered.png`, `-error-2.png`, `-error-2-numbered.png`, `-error-3.png`, `-error-3-numbered.png` |
   | S-F00-02 | `S-F00-02.png`, `-loading.png`, `-loading-numbered.png`, `-error.png` … `-error-5.png` (5 ảnh) và `-error-numbered.png` … `-error-5-numbered.png` (5 ảnh), `-success.png`, `-success-numbered.png` |
   | S-F00-03 | `S-F00-03.png`, `-loading.png`, `-loading-numbered.png`, `-error.png`, `-error-numbered.png`, `-error-2.png`, `-error-2-numbered.png` |
   | S-F02-03 | `S-F02-03.png`, `-empty.png`, `-empty-numbered.png`, `-loading.png`, `-loading-numbered.png`, `-error.png`, `-error-numbered.png`, `-error-2.png`, `-error-2-numbered.png`, `-error-3.png`, `-error-3-numbered.png`, `-warning.png`, `-warning-numbered.png`, `-success.png`, `-page-2.png` |
   | S-F04-01 | `S-F04-01.png`, `-loading.png`, `-loading-numbered.png`, `-error.png`, `-error-numbered.png` |
   | M-F00-01 | `M-F00-01.png` (modal trên nền màn hình cha mờ) |
   | M-F02-03-01 | `M-F02-03-01.png` (modal trên nền màn hình cha mờ) |

   (`-loading.png` nghĩa là `S-F00-01-loading.png`, v.v.)
4. **Viết 3 spec**: `screens/screen-spec-S-F00-01.md` (gồm modal M-F00-01 ở §3.1, các màn khác
   đang trỏ tới mục này), `screen-spec-S-F00-02.md`, `screen-spec-S-F02-03.md` (gồm M-F02-03-01).
   Lưu ý riêng: xem `huong-dan/Ha-screen-spec.md` §3.
5. Báo nhóm chốt **Q3 (Blocking)** và **Q4** trước khi spec S-F02-03 lên `Reviewed`.

### Hoa

1. **Xuất ảnh tách trạng thái** (tên đã có sẵn trong 3 spec của bạn):

   | Màn | Ảnh cần có |
   |---|---|
   | S-F02-01 | `S-F02-01.png`, `-empty.png`, `-loading.png`, `-success.png`, `-error.png`, `-error-numbered.png`, `-error-2.png`, `-error-2-numbered.png`, `-error-3.png`, `-error-3-numbered.png` |
   | S-F02-02 | `S-F02-02.png`, `-empty.png`, `-loading.png`, `-success.png`, `-error.png`, `-error-2.png`, `-error-3.png` |
   | S-F02-04 | `S-F02-04.png`, `-empty.png`, `-loading.png`, `-error.png`, `-success.png`, `-success-2.png` |
   | Modal | `M-F02-01-01.png`, `M-F02-01-02.png`, `M-F02-04-01.png` (trên nền màn hình cha mờ) |

2. **Đưa mã nguồn wireframe** vào `screens/src/` (tệp HTML, `.drawio`, hoặc ghi đường dẫn Figma vào
   tệp ghi chú). Hiện chưa có nguồn nên Linh chưa soát được màu.
3. Sửa dòng đầu 6 tệp ghi chú: `UI conventions: v0.7` → `v0.8`.
4. Sau khi có ảnh: mở 3 spec trên GitHub, kiểm tra mọi ảnh đều hiện.

### Nhi

1. **Đặt tên và xuất ảnh tách trạng thái.** Tệp ghi chú của bạn đang trỏ mọi trạng thái về ảnh ghép
   `-states.png`; cần một ảnh riêng cho mỗi trạng thái. Tên đề xuất:

   | Màn | Trạng thái → tên ảnh |
   |---|---|
   | S-F01-01 | Default `S-F01-01.png` · Loading `-loading.png` · Lỗi vị trí kệ `-error.png` · Lỗi mạng `-error-2.png` · Đã lưu `-success.png` · Đã có trong danh sách `-success-2.png` · Chỉ bản trực tuyến `-online-only.png` |
   | S-F01-02 | Default `S-F01-02.png` · Loading `-loading.png` · Bản đồ không dùng được `-error.png` · Không xác định được phòng `-error-2.png` · Tầng không dùng được `-error-3.png` · Tô phòng của sách `-success.png` · Phòng đã chọn `-success-2.png` |
   | S-F03-01 | Default `S-F03-01.png` · Empty `-empty.png` · Loading `-loading.png` · Error `-error.png` · Có kết quả `-success.png` |
   | S-F03-03 | Default `S-F03-03.png` · Empty `-empty.png` · Loading `-loading.png` · Error `-error.png` · Đã bỏ khỏi danh sách `-success.png` · Vị trí kệ không có `-error-2.png` |

   Có thành phần chỉ xuất hiện ở trạng thái lỗi thì xuất thêm `-error-numbered.png`.
2. **Sửa cột Image** trong phần "States drawn" của 4 tệp ghi chú cho khớp tên trên, và sửa **mục 2
   Mockup** của 3 spec (S-F01-01, S-F01-02, S-F03-03): ảnh chính là `img/<ID>.png`, kèm bảng
   "State → Image". Không dùng `-states.png` làm ảnh chính.
3. **Đưa mã nguồn wireframe** vào `screens/src/`; điền dòng `Wireframe source` trong spec (đang ghi
   `NEEDS CLARIFICATION`).
4. Báo Linh khi ảnh S-F03-01 xong (Linh viết spec màn này).

### Trieu

1. **Chuyển 3 tệp HTML sang dùng `screens/src/tokens.css`** (Linh soát: đang tự khai báo màu, tên
   thành phần ngoài `ui-conventions.md` §3), rồi xuất lại ảnh.
2. **Xuất lại ảnh đánh số rộng 1080px** (Chrome, khung 360, DPR 3: bước 5–6 trong
   `huong-dan/Trieu-wireframe-4.md`) cho S-F03-02, S-F03-06, S-F03-07. Tải lên với cùng tên cũ.
3. **Xuất ảnh tách trạng thái:**

   | Màn | Ảnh cần có |
   |---|---|
   | S-F03-02 | `S-F03-02.png`, `-empty.png`, `-loading.png`, `-error.png`, `-success.png` |
   | S-F03-06 | `S-F03-06.png`, `-loading.png`, `-error.png`, `-no-match.png`, `-success.png` |
   | S-F03-07 | `S-F03-07.png`, `-loading.png`, `-error.png`, `-cold-start.png`, `-topped-up.png` |

4. **Viết 3 spec**: `screens/screen-spec-S-F03-02.md`, `screen-spec-S-F03-06.md`,
   `screen-spec-S-F03-07.md`. Lưu ý riêng: `huong-dan/Trieu-screen-spec.md` §3.

### Linh

1. Spec **S-F03-01**: ảnh Default đang ghi `img/S-F03-01-default.png` → đổi thành `img/S-F03-01.png`;
   thêm ảnh `-error.png` nếu mục 4 có trạng thái Error. Đối chiếu lại tên ảnh với Nhi.
2. Spec **S-F00-03, S-F04-01**: khi Ha xuất ảnh xong, kiểm tra tên ảnh trong spec khớp tệp thật.
3. Bảng **Consistency review** (`ui-conventions.md` §7) đang dựa trên ảnh cũ ngày 19/11. Ảnh của Hoa và
   Nhi đã đúng khổ: soát lại khi mọi người tải ảnh mới lên.
4. Ngày 26/11: soát cuối 15 spec, đổi `Status` thành `Reviewed`.

## 4. Quy tắc chung khi tải tệp lên

- **Đúng thư mục:**

  | Loại tệp | Thư mục |
  |---|---|
  | Ảnh (`.png`) | `[DBIZ 2] GROUP H/EXTERNAL DESIGN/screens/img/` |
  | Tệp ghi chú (`<ID>-notes.md`) | `[DBIZ 2] GROUP H/EXTERNAL DESIGN/screens/notes/` |
  | Spec (`screen-spec-<ID>.md`) | `[DBIZ 2] GROUP H/EXTERNAL DESIGN/screens/` |
  | Nguồn wireframe (`.html`, `.drawio`) | `[DBIZ 2] GROUP H/EXTERNAL DESIGN/screens/src/` |

- **Không** tải lên thư mục gốc của kho.
- **Không** để tên có `(1)`, `copy`, dấu cách, hay viết tắt khác (`F02-01 notes.md`, `M02-01-01…` là sai).
  Máy tự thêm `(1)` khi tải trùng tên: đổi tên lại trước khi tải lên.
- Muốn **thay** một tệp: tải lên tệp **cùng tên** vào cùng thư mục, GitHub tự thay bản cũ.
- Chỉ sửa tệp của mình. Tệp dùng chung (`screen-list.md`, `ui-conventions.md`, `screen-transition.md`)
  muốn đổi thì báo người phụ trách.
- Không sửa ảnh bằng tay: đổi gì thì sửa nguồn rồi xuất lại.

## 5. Hướng dẫn đẩy lên `main`

### Cách A: trên trang web GitHub (không cần cài gì)

1. Mở kho `https://github.com/chihvcte-beep/dbiz2-group-h`, đăng nhập.
2. Nút chọn nhánh ở góc trái phải ghi **main**.
3. Bấm lần lượt vào thư mục cần tải: `[DBIZ 2] GROUP H` › `EXTERNAL DESIGN` › `screens` › `img`
   (hoặc `notes`, `src`, hoặc dừng ở `screens` nếu tải spec).
4. Bấm **Add file › Upload files**, kéo thả các tệp vào.
5. Ở ô **Commit changes**, ghi ngắn gọn bạn làm gì, ví dụ:
   `Ha: export state images S-F00-01, S-F00-02`.
6. Chọn **Commit directly to the main branch**, bấm **Commit changes**.
7. Lặp lại bước 3–6 cho từng thư mục (ảnh vào `img`, ghi chú vào `notes`…).
8. **Kiểm tra:** mở thư mục vừa tải, xem tệp đúng tên, đúng chỗ. Mở spec của bạn trên GitHub, cuộn tới
   mục 2: mọi ảnh phải hiện (ảnh không hiện = sai tên hoặc sai thư mục).

Sửa nhanh một tệp `.md` có sẵn: mở tệp › bấm biểu tượng bút chì › sửa › **Commit changes** ›
**Commit directly to the main branch**.

Lỡ tải sai chỗ hoặc sai tên: mở tệp sai › nút **…** › **Delete file** › commit, rồi tải lại đúng chỗ.

### Cách B: bằng Git trên máy (nếu đã quen)

```bash
git checkout main
git pull                      # luôn lấy bản mới nhất trước
# chép tệp vào đúng thư mục ở mục 4
git add "[DBIZ 2] GROUP H/EXTERNAL DESIGN/screens"
git commit -m "Ha: export state images S-F00-01, S-F00-02"
git push origin main
```

Nếu `git push` báo bị từ chối (rejected): chạy `git pull` rồi `git push origin main` lại.

### Sau khi đẩy lên

Nhắn nhóm: đã tải gì, màn nào. Hoàn thành spec nháp thì nhắn người soát chéo để soát trước 25/11:
**Ha ↔ Hoa**, **Nhi ↔ Trieu**; spec của Linh do Ha (S-F00-03, S-F04-01) và Nhi (S-F03-01) soát.
Linh soát cuối.

## 6. Checklist trước khi báo xong

- [ ] Ảnh đánh số đúng khổ (Reader 1080px / Staff 1280px).
- [ ] Đủ ảnh tách theo bảng mục 3 của bạn, đúng tên, nằm trong `screens/img/`.
- [ ] Modal có ảnh `<Modal ID>.png` trên nền màn hình cha mờ.
- [ ] Mã nguồn wireframe nằm trong `screens/src/`.
- [ ] Spec nằm ở `screens/screen-spec-<ID>.md`, đủ 9 mục, mọi ảnh trong spec hiện được trên GitHub.
- [ ] Thư mục gốc kho không có tệp nào của bạn.
