# Wireframe notes: S-F01-02 Interactive digital library map

Actor: Reader · Frame: 360px · UI conventions: v0.8 · Author: Nhi

## Elements

| # | Element | Component | Content / data source | FR |
|---|---|---|---|---|
| 1 | Back button | Screen header | Accessible name: “Quay lại”. Return destination depends on entry point: S-F01-01 when opened from a book; existing OPAC main menu when opened from the menu. | — |
| 2 | Screen title | Screen header | “Bản đồ thư viện”. | — |
| 3 | Floor selector | Segmented control | Available floors, e.g. “Tầng 1”, “Tầng 2”, “Tầng 3”. When opened from the OPAC menu, select the lowest floor number by default. When opened from a book, select the book’s floor. | FR-01-02 |
| 4 | Floor plan | Floor plan | Simple block plan for one floor, with one tile per room. Use synced floor and room data; do not draw a real library floor plan. | FR-01-02 |
| 5 | Room tile | Room tile | Room code on each tile. Default: white with border. Selected room: brand-red fill and white text. Book’s room: highlight fill + 3px highlight border + “Sách của bạn ở đây” label. | FR-01-03, FR-01-11 |
| 6 | Shelf location details | Shelf location line | Shown only when opened from S-F01-01. Retain the book’s location above the floor selector: “Tầng <n> · Phòng <code> · Kệ <code>”. | FR-01-03, FR-01-10 |
| 7 | Map unavailable message | Banner | MSG-07: “Bản đồ tạm thời không hiển thị được. Thông tin vị trí kệ vẫn ở phía trên.” Shown when a floor plan cannot be read after entry from a book. | FR-01-10 |
| 8 | Room not found message | Banner | MSG-08: “Không tìm thấy phòng này trên bản đồ. Thông tin vị trí kệ vẫn ở phía trên.” Shown when the book’s room code is not found on the retrieved floor plan. | FR-01-09 |
| 9 | Selected-room details | Banner | “<room name> (<room code>), Tầng <n>”. Example: “Phòng đọc A (R-204), Tầng 2”. Shown after the reader selects a room. | FR-01-11 |

## States drawn

| State | Image | What the user sees | FR |
|---|---|---|---|
| Default | img/S-F01-02-numbered.png | Opened from the OPAC menu. Lowest floor number is selected by default; floor selector and room tiles are shown; no room is highlighted and no shelf-location details are shown. | FR-01-02 |
| Empty | Not applicable: this is a map view, not a list. A missing or unreadable floor plan is an Error state, not an empty map. | — | — |
| Loading | img/S-F01-02-states.png | Skeleton placeholders while synced floor/room data and the floor plan are retrieved. | FR-01-02 |
| Error — map unavailable | img/S-F01-02-states.png | MSG-07. When opened from a book, keep shelf-location details visible above the map. | FR-01-10 |
| Error — room cannot be identified | img/S-F01-02-states.png | MSG-08 when room R-299 is not found on the plan. Show the plain map and keep shelf-location details visible. R-299 is the sample missing room code; R-204 remains the confirmed room sample. | FR-01-09 |
| Error — selected floor unavailable | img/S-F01-02-states.png | Show MSG-07 above the previous floor’s map. Keep the previous map visible so the reader can choose another floor. | FR-01-10 |
| Success — book room highlighted | img/S-F01-02-states.png | Opened from S-F01-01: show the book’s floor, keep shelf details visible and highlight its room using fill, a 3px border and the text “Sách của bạn ở đây”. | FR-01-03 |
| Success — selected room | img/S-F01-02-states.png | After selecting a room from the map, highlight the selected tile and show its room name, room code and floor. Example: “Phòng đọc A (R-204), Tầng 2”. No shelf-location details are shown when entered from the menu. | FR-01-11 |

## Actions and where they go

| Element | User action / system event | Goes to |
|---|---|---|
| Back — opened from S-F01-01 | Tap | S-F01-01 |
| Back — opened from OPAC main menu | Tap | Existing OPAC main menu (exit) |
| Floor selector | Select another floor | Stays on S-F01-02; display that floor’s plan and rooms when available. |
| Floor selector — selected floor unavailable | System cannot read the selected floor plan | Stays on S-F01-02; show MSG-07 above the previous floor’s map. |
| Room tile | Select a reading room | Stays on S-F01-02; highlight the selected room and show its name, room code and floor. |

## Open questions

| # | Question | Default drawn |
|---|---|---|
| 1 | [NEEDS CLARIFICATION: MSG-07 says that shelf-location details remain “above”, but a reader who opens the map from the OPAC menu has no shelf-location details.] | In this wireframe, MSG-07 is used for map failures after entry from a book. Ask Linh/group to approve a menu-entry variant that does not refer to shelf details before using MSG-07 for that entry path. |
| 2 | [NEEDS CLARIFICATION: confirm the complete synced floor inventory and room-code inventory.] | Show Tầng 1–3 and illustrative room codes R-201–R-204. These are placeholders except the confirmed sample R-204 / “Phòng đọc A” on Tầng 2. Confirm the sample codes with the group before handoff. |

