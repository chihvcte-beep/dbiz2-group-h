# Wireframe notes: S-F01-02 Interactive digital library map

Actor: Reader · Frame: 360px · UI conventions: v0.7 · Use case: UC-02 · Activity diagram: AD-UC-02

## Elements

| # | Element | Component | Content / data source | FR |
|---|---|---|---|---|
| 1 | Back button and screen title | Screen header | Title: “Bản đồ thư viện”. Back destination depends on entry point: S-F01-01 when opened from a book; OPAC main menu when opened from the menu. | — |
| 2 | Screen title | Screen header | “Bản đồ thư viện”. [NUMBERING CHECK: title is part of element 1 / Screen header in the supplied numbered image; it does not currently have a separate visible marker.] | — |
| 3 | Floor selector | Segmented control | Available floors, e.g. “Tầng 1”, “Tầng 2”, “Tầng 3”. When opened from the OPAC menu, select the lowest floor number by default. | FR-01-02 |
| 4 | Floor plan | Floor plan | Simple block plan for one floor, with one tile per room. Use synced floor and room data; do not draw a real library floor plan. | FR-01-02 |
| 5 | Reading room | Room tile | Room code on each tile. Default: white with border. Selected: brand-red fill and white text. Book room highlighted: highlight fill + 3px highlight border + “Your book is here” label. | FR-01-03, FR-01-11 |
| 6 | Shelf location details | Shelf location line | When opened from S-F01-01, retain the shelf details already shown above the map: “Tầng <n> · Phòng <code> · Kệ <code>”. | FR-01-03, FR-01-10 |
| 7 | Map unavailable message | Banner | MSG-07: “Bản đồ tạm thời không hiển thị được. Thông tin vị trí kệ vẫn ở phía trên.” | FR-01-10 |
| 8 | Room not found message | Banner | MSG-08: “Không tìm thấy phòng này trên bản đồ. Thông tin vị trí kệ vẫn ở phía trên.” | FR-01-09 |
| 9 | Selected-room details | Banner / room details area | “<room name> (<room code>), Tầng <n>”. Example: “Phòng đọc A (R-204), Tầng 2”. | FR-01-11 |

## States drawn

| State | Image | What the user sees | FR |
|---|---|---|---|
| Default | img/S-F01-02-default.png, img/S-F01-02-numbered.png | Map opened from the OPAC menu. The lowest floor number (Tầng 1) is selected by default; available floors and reading rooms are shown with no room highlighted. | FR-01-02 |
| Empty | Not applicable: this is a map view, not a list. A missing or unreadable floor plan is an Error state, never an empty map. | — | FR-01-10 |
| Loading | img/S-F01-02-loading.png | Skeleton placeholders while the system retrieves synced floor/room data and the floor plan. | FR-01-02 |
| Error — map unavailable | img/S-F01-02-error.png | MSG-07. If the map was opened from a book, keep its shelf-location details visible. Do not draw an empty map when the floor plan cannot be read. | FR-01-10 |
| Error — room cannot be identified | img/S-F01-02-error-2.png, img/S-F01-02-error-2-numbered.png | MSG-08 when the book’s room code is not found on the retrieved floor plan; then show the plain map with available floors and rooms. Example missing room code: R-299. Keep shelf details visible. | FR-01-09 |
| Error — selected floor unavailable | img/S-F01-02-error-3.png, img/S-F01-02-error-3-numbered.png | When the reader switches to a floor whose plan cannot be read, show the map-unavailable message above the previous floor’s map. The previous map remains on screen so the reader can choose again. | FR-01-10 |
| Success — book room highlighted | img/S-F01-02-success.png, img/S-F01-02-success-numbered.png | Opened from S-F01-01: display the book’s floor plan with its room highlighted. Keep the shelf-location details visible. Highlight uses fill + thick border + “Your book is here” label, not colour alone. | FR-01-03 |
| Success — selected room | img/S-F01-02-selected-room.png, img/S-F01-02-selected-room-numbered.png | After the reader selects a reading room, highlight it and display its room name, room code and floor. Example: “Phòng đọc A (R-204), Tầng 2”. | FR-01-11 |

## Actions and where they go

| Element | User action / system event | Goes to |
|---|---|---|
| Entry from OPAC main menu | Reader chooses “Library map” | S-F01-02; show the lowest floor number by default |
| Entry from S-F01-01 | Reader chooses “Xem trên bản đồ” | S-F01-02; show the book’s floor and highlight its room if the room code exists on the plan |
| Floor selector | Reader chooses another floor | Stays on S-F01-02; display that floor’s plan and reading rooms if available |
| Floor selector — selected floor plan unavailable | System cannot read the selected floor’s plan | Stays on S-F01-02; show map-unavailable message above the previous floor’s map |
| Room tile | Reader selects a reading room | Stays on S-F01-02; highlight the room and show its name, room code and floor |
| Back | Tap when opened from S-F01-01 | S-F01-01 |
| Back | Tap when opened from OPAC main menu | Existing OPAC main menu (exit) |
| Finish | Reader has explored the desired floor or room | Activity ends; nothing is saved |

## Open questions

| # | Question | Default applied / note |
|---|---|---|
| 1 | [NUMBERING CHECK] The supplied S-F01-02-numbered.png shows markers 1, 3, 4 and 5; the screen title has no separate marker 2. | Element 1 is documented as the complete Screen header. If the team wants a separate title marker 2, update the numbered PNG and keep the notes in sync. |
| 2 | Exact floor inventory and complete room-code inventory are not supplied in the current screen inputs. | Use generic room-code placeholders in the wireframe. R-204 / “Phòng đọc A” is the confirmed sample from AD-UC-02. Do not present placeholder room codes as confirmed library data. |
| 3 | The floor-plan geometry is not supplied. | Use a simple block plan: one tile per room. Do not invent a real library layout. |

## Notes and scope limits

- The map is read-only. Floors and rooms come from synced data; there is no screen for editing floor plans or room data.
- Floor switching and room selection are loops within UC-02 and stay on S-F01-02.
- When opened from the OPAC menu, show the lowest floor number first and do not highlight a room.
- When opened from a book’s shelf location, show that book’s floor and highlight its room if its room code exists on the floor plan.
- If the room code is not found, show MSG-08 and then the plain map.
- If a floor plan cannot be read, show MSG-07; never show an empty map. For a failed floor switch, retain the previous floor’s map.
- The highlighted book room must differ by fill, a 3px border and the text label “Your book is here”; never use colour alone.
- Do not draw a list of books in a room or a staff screen for editing floor plans (Won’t).
- Room tiles and other interactive targets on Reader screens must meet the 44×44px target-size convention.
