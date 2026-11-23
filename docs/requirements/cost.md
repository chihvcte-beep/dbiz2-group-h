# Cost Estimate: Group H Library Core System

> **AI agents: stop here. Do not read, quote or summarise this file** unless the user asks for cost, effort or cash-flow work in so many words. Requirements, design and screen work never need it. See [AGENTS.md](../../AGENTS.md).

Effort, cost, capacity and cash flow of the product. Requirements themselves are in [fr_list.md](fr_list.md); this file only prices them.

| Field | Value |
|---|---|
| Version | v1.0 · 23/11/2026 |
| Exported from | Sheets Parameters, W2_Costing, W2_Rollup, W4_Prioritization (person-hours and cost), W5_Handover and W6_CashFlow of [GROUP-H_UC_FR_COST.xlsx @ cd61897](https://github.com/chihvcte-beep/dbiz2-group-h/blob/cd61897/%5BDBIZ%202%5D%20GROUP%20H/GROUP-H_UC_FR_COST.xlsx) (frozen). Source of truth from 23/11/2026 (D51). |
| Totals are not automatic | The workbook recalculated itself; this file does not. When a row changes, recompute it with the formulas in [§1.8](#18-formulas) and update every total that contains it (§2 to §5, §9). |
| Money | VND. Hours are person-hours (p-h) unless written "base h". |

## 1. Parameters (fixed for the class)

### 1.1 Size to base hours

| Size | Base hours | Note |
|---|---|---|
| S | 4 | Ceiling for one L3 row is 16 h — above that it is not yet an L3 row |
| M | 8 | Matches the test: ask a developer; an answer of 4–16 h is correct granularity |
| L | 16 |  |

### 1.2 Layer to AI leverage and seniority

| Layer | AI leverage factor | Default band | Note |
|---|---|---|---|
| FE | 0.35 | Junior | Screens, forms, repeated patterns — AI generates these well |
| BE | 0.70 | Senior | Business logic, state, concurrency |
| INT | 1 | Senior | Third-party APIs, credentials, sandboxes — AI helps least here |

### 1.3 Hourly rate by band

| Band | VND per hour | Source |
|---|---|---|
| Junior | 200,000 | ITviec 2025-26 median 25.35m VND/month x 1.35 overhead / 176 h |
| Senior | 300,000 | ITviec 2025-26 median 39.9m VND/month x 1.35 / 176 h |
| Expert | 400,000 | ITviec 2025-26 median 54.9m VND/month x 1.35 / 176 h |

### 1.4 Verification factor

| EARS precise? | Factor | Note |
|---|---|---|
| Yes | 0.15 | Clear criteria — fast to verify, often automatable |
| No | 0.40 | Vague criteria — a person must reason the answer out from scratch |

### 1.5 Function point weights

| FP type | Weight | What it counts |
|---|---|---|
| EI | 4 | External Input — data crosses the boundary inward and changes stored data |
| EO | 5 | External Output — data leaves the boundary WITH derived values or calculation |
| EQ | 4 | External inQuiry — retrieval only, no derived data, nothing stored changes |
| ILF | 10 | Internal Logical File — a group of data the system itself maintains |
| EIF | 7 | External Interface File — data the system reads but never maintains |
| NC | 0 | Not countable — a business rule or non-functional item inside another transaction |
| Hours per unadjusted function point | 3 | Class parameter, PRE-AI gross hours. Published industry figures range very widely; calibrate this from your own delivered projects rather than importing a benchmark |

### 1.6 Team capacity for DBIZ3

| Item | Value | Note |
|---|---|---|
| Team members | 6 |  |
| Weeks | 12 |  |
| Productive hours per person per week | 5 | Hours actually spent building, not hours present |
| Total capacity (person-hours) | 360 | Hard ceiling for the whole scope: Must + Should + Could |

### 1.7 Thresholds

| Threshold | Value | Note |
|---|---|---|
| Must, maximum share of scope effort | 60.0% | DSDM: above 60% the project enters the risk zone |
| Could, target share of scope effort | 20.0% | The contingency pool, expressed as scope rather than money |
| Hidden technical work, minimum share | 10.0% | Real projects run 20–30%; below 10% something is missing |
| Maximum hours for one L3 row | 16 |  |
| Minimum number of features | 3 |  |
| Maximum number of features | 6 |  |
| Estimate variance that triggers a review | 30.0% | If bottom-up and function-point estimates differ by more than this, something is mis-sized |

### 1.8 Formulas

- Person-hours  =  base hours x AI leverage factor  +  base hours x verification factor
- Cost  =  person-hours x hourly rate for the seniority band
- Function-point cross-check  =  unadjusted function points x hours per FP  (compare against total base hours)
- Note: once a ~20% Could pool exists as scope contingency, do NOT add a further 20% money contingency on top — that counts the same buffer twice.

- Estimation basis: **Bottom-up**. Bottom-up: base hours come from the S / M / L label on each L3 row.<br>Function-point: the L2 total comes from its function-point count x hours per FP, then S / M / L acts only as the RELATIVE weight that distributes those hours across the L3 rows. NC rows have no function points, so they always fall back to bottom-up — that is the 0 function point problem, and it is why the two methods can never fully replace each other.


## 2. Headline figures

The three MoSCoW tiers are the three scenarios. Always say which one you mean.

| Scenario | Scope | Person-hours | Cost (VND) | Meaning |
|---|---|---|---|---|
| Committed | Must only | 252.4 | 68,920,000 | What the team guarantees to deliver — the Minimum Usable SubseT |
| Expected | Must + Should | 345.6 | 93,680,000 | The figure given to the client; the base cash flow for Session 8 |
| Ceiling | Must + Should + Could | 506.6 | 136,980,000 | If the Could contingency pool is never consumed |

Team capacity is 360 p-h and covers Must + Should; the Could pool is optional (D43).


## 3. Per feature (effective priority)

| Feature | Name | L2 | L3 | Base h | Must p-h | Should p-h | Could p-h | Won't p-h | In-scope p-h | In-scope cost | Must % |
|---|---|---|---|---|---|---|---|---|---|---|---|
| F-01 | Book Location & Library Map | 10 | 15 | 92 | 39.6 | 6.8 | 9.4 | 0 | 55.8 | 13,540,000 | 71.0% |
| F-02 | Reviews & QR | 25 | 43 | 192 | 68.8 | 10.8 | 48.6 | 0 | 128.2 | 33,460,000 | 53.7% |
| F-03 | Discovery, Reading History & Recommendation | 25 | 42 | 236 | 0 | 58 | 103 | 23.4 | 161 | 43,300,000 | 0.0% |
| F-04 | Platform, Access & Operations | 21 | 36 | 244 | 144 | 17.6 | 0 | 45.8 | 161.6 | 46,680,000 | 89.1% |
|  | PROJECT TOTAL | 81 | 136 | 764 | 252.4 | 93.2 | 161 | 69.2 | 506.6 | 136,980,000 | 49.8% |

## 4. Threshold check

| Indicator | As first written (W1) | After W4 | Threshold | Verdict |
|---|---|---|---|---|
| Must share of in-scope effort | 46.1% | 49.8% | 60.0% | PASS |
| Could share (contingency pool) | 31.3% | 31.8% | 20.0% | PASS |
| In-scope effort vs team capacity (p-h) | 575.8 | 506.6 | 360 | OVER CAPACITY |
| Hidden technical work, share of effort | 28.5% | 28.5% | 10.0% | PASS |
| L3 rows above the hour ceiling | 0 | 0 | 0 | PASS |
| Feature count | 4 | 4 | 3-6 | PASS |

In-scope effort (Must + Should + Could) is over the 360 p-h capacity; Must + Should (345.6 p-h) is within it, and that is the commitment (D43).


## 5. Cost per FR

| FR | Name | Priority | Person-hours | Cost (VND) |
|---|---|---|---|---|
| [FR-01-01](fr_list.md#fr-01-01) | View book shelf location | Must | 5.4 | 1,420,000 |
| [FR-01-02](fr_list.md#fr-01-02) | Browse the digital library map | Must | 11.4 | 2,620,000 |
| [FR-01-03](fr_list.md#fr-01-03) | Show a book's room on the map | Could | 7.4 | 1,820,000 |
| [FR-01-04](fr_list.md#fr-01-04) | Prepare the digital floor plan | Must | 8 | 1,600,000 |
| [FR-01-05](fr_list.md#fr-01-05) | Check room codes against the internal system | Should | 6.8 | 2,040,000 |
| [FR-01-06](fr_list.md#fr-01-06) | Show that an online-only book has no shelf location | Must | 2 | 400,000 |
| [FR-01-07](fr_list.md#fr-01-07) | Handle a missing or inconsistent shelf location | Must | 5.4 | 1,420,000 |
| [FR-01-09](fr_list.md#fr-01-09) | Handle a room not found on the floor plan | Could | 2 | 400,000 |
| [FR-01-10](fr_list.md#fr-01-10) | Handle an unavailable floor plan | Must | 2 | 400,000 |
| [FR-01-11](fr_list.md#fr-01-11) | Select a reading room on the map | Must | 5.4 | 1,420,000 |
| [FR-02-01](fr_list.md#fr-02-01) | Write a book review | Must | 5.4 | 1,420,000 |
| [FR-02-02](fr_list.md#fr-02-02) | View book reviews | Must | 7.4 | 1,820,000 |
| [FR-02-03](fr_list.md#fr-02-03) | Edit own review | Could | 5.4 | 1,420,000 |
| [FR-02-04](fr_list.md#fr-02-04) | Delete own review | Could | 5.4 | 1,420,000 |
| [FR-02-05](fr_list.md#fr-02-05) | Open book information and reviews via QR code | Must | 5.4 | 1,420,000 |
| [FR-02-06](fr_list.md#fr-02-06) | Count QR code scans | Could | 3.4 | 1,020,000 |
| [FR-02-07](fr_list.md#fr-02-07) | Generate QR codes for new physical books | Must | 6.8 | 2,040,000 |
| [FR-02-08](fr_list.md#fr-02-08) | Print QR code labels | Must | 10.8 | 2,840,000 |
| [FR-02-09](fr_list.md#fr-02-09) | Report a review that breaks the rules | Could | 5.4 | 1,420,000 |
| [FR-02-10](fr_list.md#fr-02-10) | Review and remove reported reviews | Could | 5.4 | 1,420,000 |
| [FR-02-11](fr_list.md#fr-02-11) | Reject invalid review actions | Must | 5.4 | 1,420,000 |
| [FR-02-12](fr_list.md#fr-02-12) | Confirm review changes | Must | 2 | 400,000 |
| [FR-02-13](fr_list.md#fr-02-13) | Hide removed reviews from the list | Must | 3.4 | 1,020,000 |
| [FR-02-14](fr_list.md#fr-02-14) | View the reported-reviews list | Could | 5.4 | 1,420,000 |
| [FR-02-15](fr_list.md#fr-02-15) | End a review request with nothing to show | Must | 2 | 400,000 |
| [FR-02-16](fr_list.md#fr-02-16) | Handle a QR code linked to no book | Must | 5.4 | 1,420,000 |
| [FR-02-17](fr_list.md#fr-02-17) | Require at least one book for label printing | Must | 2 | 400,000 |
| [FR-02-18](fr_list.md#fr-02-18) | Leave books without a QR code out of the label sheet | Must | 5.4 | 1,420,000 |
| [FR-02-19](fr_list.md#fr-02-19) | Show an empty reported-reviews list | Could | 2 | 400,000 |
| [FR-02-20](fr_list.md#fr-02-20) | Dismiss a report on a review that follows the rules | Could | 5.4 | 1,420,000 |
| [FR-02-21](fr_list.md#fr-02-21) | Reject a duplicate report | Could | 5.4 | 1,420,000 |
| [FR-02-22](fr_list.md#fr-02-22) | Post a review under the reader's name or anonymously | Should | 5.4 | 1,420,000 |
| [FR-02-23](fr_list.md#fr-02-23) | List physical books awaiting a QR label | Must | 7.4 | 1,820,000 |
| [FR-02-24](fr_list.md#fr-02-24) | Reject a report on the reader's own review | Could | 5.4 | 1,420,000 |
| [FR-02-25](fr_list.md#fr-02-25) | Reprint QR labels for labelled books | Should | 5.4 | 1,420,000 |
| [FR-03-01](fr_list.md#fr-03-01) | View reading history | Should | 7.4 | 1,820,000 |
| [FR-03-02](fr_list.md#fr-03-02) | Add a history entry when an online book is opened from this platform | Should | 3.4 | 1,020,000 |
| [FR-03-03](fr_list.md#fr-03-03) | Add history entries from borrowed physical books | Should | 6.8 | 2,040,000 |
| [FR-03-04](fr_list.md#fr-03-04) | Mark reading status and progress | Should | 7.4 | 1,820,000 |
| [FR-03-05](fr_list.md#fr-03-05) | Set reading preferences | Could | 7.4 | 1,820,000 |
| [FR-03-06](fr_list.md#fr-03-06) | Save a physical book to a personal list | Should | 5.4 | 1,420,000 |
| [FR-03-07](fr_list.md#fr-03-07) | View saved books with shelf locations | Should | 7.4 | 1,820,000 |
| [FR-03-08](fr_list.md#fr-03-08) | Remove a saved book | Could | 5.4 | 1,420,000 |
| [FR-03-09](fr_list.md#fr-03-09) | Search books by chatting with the AI chatbot | Could | 34.8 | 9,840,000 |
| [FR-03-10](fr_list.md#fr-03-10) | Save chatbot conversations per reader | Could | 3.4 | 1,020,000 |
| [FR-03-11](fr_list.md#fr-03-11) | Recommend books automatically | Could | 23.6 | 6,480,000 |
| [FR-03-12](fr_list.md#fr-03-12) | Filter books by access format | Should | 5.4 | 1,420,000 |
| [FR-03-13](fr_list.md#fr-03-13) | Log anonymous online-book reads | Could | 3.4 | 1,020,000 |
| [FR-03-14](fr_list.md#fr-03-14) | View access formats of a book | Won't | 5.4 | 1,420,000 |
| [FR-03-15](fr_list.md#fr-03-15) | Download the PDF of an online book | Won't | 18 | 5,200,000 |
| [FR-03-16](fr_list.md#fr-03-16) | Reply when the chatbot finds no books | Could | 3.4 | 1,020,000 |
| [FR-03-17](fr_list.md#fr-03-17) | Handle an unavailable AI service | Could | 5.4 | 1,420,000 |
| [FR-03-18](fr_list.md#fr-03-18) | Prompt sign-in before chatting | Could | 2 | 400,000 |
| [FR-03-19](fr_list.md#fr-03-19) | Recommend popular books when there is no reader data | Could | 8.8 | 2,440,000 |
| [FR-03-20](fr_list.md#fr-03-20) | Top up short recommendation lists | Could | 3.4 | 1,020,000 |
| [FR-03-21](fr_list.md#fr-03-21) | Prompt sign-in for recommendations | Could | 2 | 400,000 |
| [FR-03-22](fr_list.md#fr-03-22) | Reject invalid reading history or preference updates | Should | 5.4 | 1,420,000 |
| [FR-03-23](fr_list.md#fr-03-23) | Show no results for an access-format filter | Should | 2 | 400,000 |
| [FR-03-24](fr_list.md#fr-03-24) | Reject saving a book twice | Should | 5.4 | 1,420,000 |
| [FR-03-25](fr_list.md#fr-03-25) | Show an empty saved books list | Should | 2 | 400,000 |
| [FR-04-01](fr_list.md#fr-04-01) | Sign in with library card and email OTP | Must | 20 | 5,600,000 |
| [FR-04-02](fr_list.md#fr-04-02) | Register or sign in with email OTP | Won't | 8.8 | 2,440,000 |
| [FR-04-03](fr_list.md#fr-04-03) | Sign in with Google | Won't | 18 | 5,200,000 |
| [FR-04-04](fr_list.md#fr-04-04) | Send and verify email OTP | Must | 16 | 4,800,000 |
| [FR-04-05](fr_list.md#fr-04-05) | Link an online account to a library card | Won't | 8.8 | 2,440,000 |
| [FR-04-06](fr_list.md#fr-04-06) | Reject linking when both profiles hold data | Won't | 3.4 | 1,020,000 |
| [FR-04-07](fr_list.md#fr-04-07) | Sign in On-site Staff with internal library account | Must | 18 | 5,200,000 |
| [FR-04-08](fr_list.md#fr-04-08) | Enforce sign-in and staff access control | Must | 6.8 | 2,040,000 |
| [FR-04-09](fr_list.md#fr-04-09) | Sync catalogue, shelf placement and library layout | Must | 18.4 | 5,520,000 |
| [FR-04-10](fr_list.md#fr-04-10) | Sync loan records | Must | 9.2 | 2,760,000 |
| [FR-04-11](fr_list.md#fr-04-11) | Handle sync failures | Should | 6.8 | 2,040,000 |
| [FR-04-12](fr_list.md#fr-04-12) | Keep an audit log | Must | 6.8 | 2,040,000 |
| [FR-04-13](fr_list.md#fr-04-13) | Deploy automatically | Must | 13.6 | 4,080,000 |
| [FR-04-14](fr_list.md#fr-04-14) | Run automated tests on every change | Must | 13.6 | 4,080,000 |
| [FR-04-15](fr_list.md#fr-04-15) | Monitor errors and availability | Won't | 6.8 | 2,040,000 |
| [FR-04-16](fr_list.md#fr-04-16) | Handle a failed OTP email | Must | 5.4 | 1,420,000 |
| [FR-04-17](fr_list.md#fr-04-17) | Limit incorrect OTP attempts | Must | 5.4 | 1,420,000 |
| [FR-04-18](fr_list.md#fr-04-18) | Reject invalid staff sign-in | Must | 5.4 | 1,420,000 |
| [FR-04-19](fr_list.md#fr-04-19) | Show the remaining OTP attempts | Should | 5.4 | 1,420,000 |
| [FR-04-20](fr_list.md#fr-04-20) | Handle a network or loading error | Must | 5.4 | 1,420,000 |
| [FR-04-21](fr_list.md#fr-04-21) | Sign out of the staff page | Should | 5.4 | 1,420,000 |

## 6. Cost per work item (L3)

Person-hours = base h × AI leverage + base h × verification factor. Risk order (W5 §3): 1 = integration, build first; 2 = server; 3 = screen.

| L3 | Layer | Size | Base h | EARS precise? | AI-assisted h | Verification h | Person-hours | Band | Rate | Cost (VND) | Priority | Risk order |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| FR-01-01-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Must | 2 |
| FR-01-01-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Must | 3 |
| FR-01-02-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Must | 2 |
| FR-01-02-FE | FE | L | 16 | Yes | 5.6 | 2.4 | 8 | Junior | 200,000 | 1,600,000 | Must | 3 |
| FR-01-03-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Could | 2 |
| FR-01-03-FE | FE | M | 8 | Yes | 2.8 | 1.2 | 4 | Junior | 200,000 | 800,000 | Could | 3 |
| FR-01-04-FE | FE | L | 16 | Yes | 5.6 | 2.4 | 8 | Junior | 200,000 | 1,600,000 | Must | 3 |
| FR-01-05-BE | BE | M | 8 | Yes | 5.6 | 1.2 | 6.8 | Senior | 300,000 | 2,040,000 | Should | 2 |
| FR-01-06-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Must | 3 |
| FR-01-07-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Must | 2 |
| FR-01-07-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Must | 3 |
| FR-01-09-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Could | 3 |
| FR-01-10-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Must | 3 |
| FR-01-11-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Must | 2 |
| FR-01-11-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Must | 3 |
| FR-02-01-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Must | 2 |
| FR-02-01-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Must | 3 |
| FR-02-02-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Must | 2 |
| FR-02-02-FE | FE | M | 8 | Yes | 2.8 | 1.2 | 4 | Junior | 200,000 | 800,000 | Must | 3 |
| FR-02-03-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Could | 2 |
| FR-02-03-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Could | 3 |
| FR-02-04-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Could | 2 |
| FR-02-04-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Could | 3 |
| FR-02-05-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Must | 2 |
| FR-02-05-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Must | 3 |
| FR-02-06-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Could | 2 |
| FR-02-07-BE | BE | M | 8 | Yes | 5.6 | 1.2 | 6.8 | Senior | 300,000 | 2,040,000 | Must | 2 |
| FR-02-08-BE | BE | M | 8 | Yes | 5.6 | 1.2 | 6.8 | Senior | 300,000 | 2,040,000 | Must | 2 |
| FR-02-08-FE | FE | M | 8 | Yes | 2.8 | 1.2 | 4 | Junior | 200,000 | 800,000 | Must | 3 |
| FR-02-09-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Could | 2 |
| FR-02-09-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Could | 3 |
| FR-02-10-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Could | 2 |
| FR-02-10-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Could | 3 |
| FR-02-11-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Must | 2 |
| FR-02-11-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Must | 3 |
| FR-02-12-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Must | 3 |
| FR-02-13-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Must | 2 |
| FR-02-14-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Could | 2 |
| FR-02-14-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Could | 3 |
| FR-02-15-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Must | 3 |
| FR-02-16-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Must | 2 |
| FR-02-16-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Must | 3 |
| FR-02-17-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Must | 3 |
| FR-02-18-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Must | 2 |
| FR-02-18-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Must | 3 |
| FR-02-19-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Could | 3 |
| FR-02-20-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Could | 2 |
| FR-02-20-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Could | 3 |
| FR-02-21-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Could | 2 |
| FR-02-21-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Could | 3 |
| FR-02-22-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Should | 2 |
| FR-02-22-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Should | 3 |
| FR-02-23-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Must | 2 |
| FR-02-23-FE | FE | M | 8 | Yes | 2.8 | 1.2 | 4 | Junior | 200,000 | 800,000 | Must | 3 |
| FR-02-24-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Could | 2 |
| FR-02-24-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Could | 3 |
| FR-02-25-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Should | 2 |
| FR-02-25-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Should | 3 |
| FR-03-01-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Should | 2 |
| FR-03-01-FE | FE | M | 8 | Yes | 2.8 | 1.2 | 4 | Junior | 200,000 | 800,000 | Should | 3 |
| FR-03-02-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Should | 2 |
| FR-03-03-BE | BE | M | 8 | Yes | 5.6 | 1.2 | 6.8 | Senior | 300,000 | 2,040,000 | Should | 2 |
| FR-03-04-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Should | 2 |
| FR-03-04-FE | FE | M | 8 | Yes | 2.8 | 1.2 | 4 | Junior | 200,000 | 800,000 | Should | 3 |
| FR-03-05-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Could | 2 |
| FR-03-05-FE | FE | M | 8 | Yes | 2.8 | 1.2 | 4 | Junior | 200,000 | 800,000 | Could | 3 |
| FR-03-06-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Should | 2 |
| FR-03-06-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Should | 3 |
| FR-03-07-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Should | 2 |
| FR-03-07-FE | FE | M | 8 | Yes | 2.8 | 1.2 | 4 | Junior | 200,000 | 800,000 | Should | 3 |
| FR-03-08-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Could | 2 |
| FR-03-08-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Could | 3 |
| FR-03-09-BE | BE | L | 16 | No | 11.2 | 6.4 | 17.6 | Senior | 300,000 | 5,280,000 | Could | 2 |
| FR-03-09-FE | FE | M | 8 | No | 2.8 | 3.2 | 6 | Junior | 200,000 | 1,200,000 | Could | 3 |
| FR-03-09-INT | INT | M | 8 | No | 8 | 3.2 | 11.2 | Senior | 300,000 | 3,360,000 | Could | 1 |
| FR-03-10-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Could | 2 |
| FR-03-11-BE | BE | L | 16 | No | 11.2 | 6.4 | 17.6 | Senior | 300,000 | 5,280,000 | Could | 2 |
| FR-03-11-FE | FE | M | 8 | No | 2.8 | 3.2 | 6 | Junior | 200,000 | 1,200,000 | Could | 3 |
| FR-03-12-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Should | 2 |
| FR-03-12-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Should | 3 |
| FR-03-13-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Could | 2 |
| FR-03-14-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Won't | 2 |
| FR-03-14-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Won't | 3 |
| FR-03-15-BE | BE | M | 8 | Yes | 5.6 | 1.2 | 6.8 | Senior | 300,000 | 2,040,000 | Won't | 2 |
| FR-03-15-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Won't | 3 |
| FR-03-15-INT | INT | M | 8 | Yes | 8 | 1.2 | 9.2 | Senior | 300,000 | 2,760,000 | Won't | 1 |
| FR-03-16-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Could | 2 |
| FR-03-17-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Could | 2 |
| FR-03-17-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Could | 3 |
| FR-03-18-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Could | 3 |
| FR-03-19-BE | BE | M | 8 | Yes | 5.6 | 1.2 | 6.8 | Senior | 300,000 | 2,040,000 | Could | 2 |
| FR-03-19-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Could | 3 |
| FR-03-20-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Could | 2 |
| FR-03-21-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Could | 3 |
| FR-03-22-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Should | 2 |
| FR-03-22-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Should | 3 |
| FR-03-23-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Should | 3 |
| FR-03-24-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Should | 2 |
| FR-03-24-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Should | 3 |
| FR-03-25-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Should | 3 |
| FR-04-01-BE | BE | M | 8 | Yes | 5.6 | 1.2 | 6.8 | Senior | 300,000 | 2,040,000 | Must | 2 |
| FR-04-01-FE | FE | M | 8 | Yes | 2.8 | 1.2 | 4 | Junior | 200,000 | 800,000 | Must | 3 |
| FR-04-01-INT | INT | M | 8 | Yes | 8 | 1.2 | 9.2 | Senior | 300,000 | 2,760,000 | Must | 1 |
| FR-04-02-BE | BE | M | 8 | Yes | 5.6 | 1.2 | 6.8 | Senior | 300,000 | 2,040,000 | Won't | 2 |
| FR-04-02-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Won't | 3 |
| FR-04-03-BE | BE | M | 8 | Yes | 5.6 | 1.2 | 6.8 | Senior | 300,000 | 2,040,000 | Won't | 2 |
| FR-04-03-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Won't | 3 |
| FR-04-03-INT | INT | M | 8 | Yes | 8 | 1.2 | 9.2 | Senior | 300,000 | 2,760,000 | Won't | 1 |
| FR-04-04-BE | BE | M | 8 | Yes | 5.6 | 1.2 | 6.8 | Senior | 300,000 | 2,040,000 | Must | 2 |
| FR-04-04-INT | INT | M | 8 | Yes | 8 | 1.2 | 9.2 | Senior | 300,000 | 2,760,000 | Must | 1 |
| FR-04-05-BE | BE | M | 8 | Yes | 5.6 | 1.2 | 6.8 | Senior | 300,000 | 2,040,000 | Won't | 2 |
| FR-04-05-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Won't | 3 |
| FR-04-06-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Won't | 2 |
| FR-04-07-BE | BE | M | 8 | Yes | 5.6 | 1.2 | 6.8 | Senior | 300,000 | 2,040,000 | Must | 2 |
| FR-04-07-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Must | 3 |
| FR-04-07-INT | INT | M | 8 | Yes | 8 | 1.2 | 9.2 | Senior | 300,000 | 2,760,000 | Must | 1 |
| FR-04-08-BE | BE | M | 8 | Yes | 5.6 | 1.2 | 6.8 | Senior | 300,000 | 2,040,000 | Must | 2 |
| FR-04-09-INT | INT | L | 16 | Yes | 16 | 2.4 | 18.4 | Senior | 300,000 | 5,520,000 | Must | 1 |
| FR-04-10-INT | INT | M | 8 | Yes | 8 | 1.2 | 9.2 | Senior | 300,000 | 2,760,000 | Must | 1 |
| FR-04-11-BE | BE | M | 8 | Yes | 5.6 | 1.2 | 6.8 | Senior | 300,000 | 2,040,000 | Should | 2 |
| FR-04-12-BE | BE | M | 8 | Yes | 5.6 | 1.2 | 6.8 | Senior | 300,000 | 2,040,000 | Must | 2 |
| FR-04-13-BE | BE | L | 16 | Yes | 11.2 | 2.4 | 13.6 | Senior | 300,000 | 4,080,000 | Must | 2 |
| FR-04-14-BE | BE | L | 16 | Yes | 11.2 | 2.4 | 13.6 | Senior | 300,000 | 4,080,000 | Must | 2 |
| FR-04-15-BE | BE | M | 8 | Yes | 5.6 | 1.2 | 6.8 | Senior | 300,000 | 2,040,000 | Won't | 2 |
| FR-04-16-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Must | 2 |
| FR-04-16-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Must | 3 |
| FR-04-17-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Must | 2 |
| FR-04-17-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Must | 3 |
| FR-04-18-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Must | 2 |
| FR-04-18-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Must | 3 |
| FR-04-19-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Should | 2 |
| FR-04-19-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Should | 3 |
| FR-04-20-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Must | 2 |
| FR-04-20-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Must | 3 |
| FR-04-21-BE | BE | S | 4 | Yes | 2.8 | 0.6 | 3.4 | Senior | 300,000 | 1,020,000 | Should | 2 |
| FR-04-21-FE | FE | S | 4 | Yes | 1.4 | 0.6 | 2 | Junior | 200,000 | 400,000 | Should | 3 |

All rows, Won't included: base 764 h · person-hours 575.8 · cost 156,740,000 VND.


## 7. Function-point cross-check

A check on the bottom-up hours, never the estimate itself. NC rows (rules, non-functional items) score 0 FP.

| FR | FP type | FP |
|---|---|---|
| [FR-01-01](fr_list.md#fr-01-01) | EQ | 4 |
| [FR-01-02](fr_list.md#fr-01-02) | EQ | 4 |
| [FR-01-03](fr_list.md#fr-01-03) | EQ | 4 |
| [FR-01-04](fr_list.md#fr-01-04) | NC | 0 |
| [FR-01-05](fr_list.md#fr-01-05) | NC | 0 |
| [FR-01-06](fr_list.md#fr-01-06) | NC | 0 |
| [FR-01-07](fr_list.md#fr-01-07) | NC | 0 |
| [FR-01-09](fr_list.md#fr-01-09) | NC | 0 |
| [FR-01-10](fr_list.md#fr-01-10) | NC | 0 |
| [FR-01-11](fr_list.md#fr-01-11) | EQ | 4 |
| [FR-02-01](fr_list.md#fr-02-01) | EI | 4 |
| [FR-02-02](fr_list.md#fr-02-02) | EQ | 4 |
| [FR-02-03](fr_list.md#fr-02-03) | EI | 4 |
| [FR-02-04](fr_list.md#fr-02-04) | EI | 4 |
| [FR-02-05](fr_list.md#fr-02-05) | EQ | 4 |
| [FR-02-06](fr_list.md#fr-02-06) | NC | 0 |
| [FR-02-07](fr_list.md#fr-02-07) | NC | 0 |
| [FR-02-08](fr_list.md#fr-02-08) | EI | 4 |
| [FR-02-09](fr_list.md#fr-02-09) | EI | 4 |
| [FR-02-10](fr_list.md#fr-02-10) | EI | 4 |
| [FR-02-11](fr_list.md#fr-02-11) | NC | 0 |
| [FR-02-12](fr_list.md#fr-02-12) | NC | 0 |
| [FR-02-13](fr_list.md#fr-02-13) | NC | 0 |
| [FR-02-14](fr_list.md#fr-02-14) | EQ | 4 |
| [FR-02-15](fr_list.md#fr-02-15) | NC | 0 |
| [FR-02-16](fr_list.md#fr-02-16) | NC | 0 |
| [FR-02-17](fr_list.md#fr-02-17) | NC | 0 |
| [FR-02-18](fr_list.md#fr-02-18) | NC | 0 |
| [FR-02-19](fr_list.md#fr-02-19) | NC | 0 |
| [FR-02-20](fr_list.md#fr-02-20) | EI | 4 |
| [FR-02-21](fr_list.md#fr-02-21) | NC | 0 |
| [FR-02-22](fr_list.md#fr-02-22) | NC | 0 |
| [FR-02-23](fr_list.md#fr-02-23) | EQ | 4 |
| [FR-02-24](fr_list.md#fr-02-24) | NC | 0 |
| [FR-02-25](fr_list.md#fr-02-25) | EQ | 4 |
| [FR-03-01](fr_list.md#fr-03-01) | EQ | 4 |
| [FR-03-02](fr_list.md#fr-03-02) | NC | 0 |
| [FR-03-03](fr_list.md#fr-03-03) | NC | 0 |
| [FR-03-04](fr_list.md#fr-03-04) | EI | 4 |
| [FR-03-05](fr_list.md#fr-03-05) | EI | 4 |
| [FR-03-06](fr_list.md#fr-03-06) | EI | 4 |
| [FR-03-07](fr_list.md#fr-03-07) | EQ | 4 |
| [FR-03-08](fr_list.md#fr-03-08) | EI | 4 |
| [FR-03-09](fr_list.md#fr-03-09) | EO | 5 |
| [FR-03-10](fr_list.md#fr-03-10) | NC | 0 |
| [FR-03-11](fr_list.md#fr-03-11) | EO | 5 |
| [FR-03-12](fr_list.md#fr-03-12) | EQ | 4 |
| [FR-03-13](fr_list.md#fr-03-13) | NC | 0 |
| [FR-03-14](fr_list.md#fr-03-14) | EQ | 4 |
| [FR-03-15](fr_list.md#fr-03-15) | EQ | 4 |
| [FR-03-16](fr_list.md#fr-03-16) | NC | 0 |
| [FR-03-17](fr_list.md#fr-03-17) | NC | 0 |
| [FR-03-18](fr_list.md#fr-03-18) | NC | 0 |
| [FR-03-19](fr_list.md#fr-03-19) | NC | 0 |
| [FR-03-20](fr_list.md#fr-03-20) | NC | 0 |
| [FR-03-21](fr_list.md#fr-03-21) | NC | 0 |
| [FR-03-22](fr_list.md#fr-03-22) | NC | 0 |
| [FR-03-23](fr_list.md#fr-03-23) | NC | 0 |
| [FR-03-24](fr_list.md#fr-03-24) | NC | 0 |
| [FR-03-25](fr_list.md#fr-03-25) | NC | 0 |
| [FR-04-01](fr_list.md#fr-04-01) | EI | 4 |
| [FR-04-02](fr_list.md#fr-04-02) | EI | 4 |
| [FR-04-03](fr_list.md#fr-04-03) | EI | 4 |
| [FR-04-04](fr_list.md#fr-04-04) | NC | 0 |
| [FR-04-05](fr_list.md#fr-04-05) | EI | 4 |
| [FR-04-06](fr_list.md#fr-04-06) | NC | 0 |
| [FR-04-07](fr_list.md#fr-04-07) | EI | 4 |
| [FR-04-08](fr_list.md#fr-04-08) | NC | 0 |
| [FR-04-09](fr_list.md#fr-04-09) | NC | 0 |
| [FR-04-10](fr_list.md#fr-04-10) | NC | 0 |
| [FR-04-11](fr_list.md#fr-04-11) | NC | 0 |
| [FR-04-12](fr_list.md#fr-04-12) | NC | 0 |
| [FR-04-13](fr_list.md#fr-04-13) | NC | 0 |
| [FR-04-14](fr_list.md#fr-04-14) | NC | 0 |
| [FR-04-15](fr_list.md#fr-04-15) | NC | 0 |
| [FR-04-16](fr_list.md#fr-04-16) | NC | 0 |
| [FR-04-17](fr_list.md#fr-04-17) | NC | 0 |
| [FR-04-18](fr_list.md#fr-04-18) | NC | 0 |
| [FR-04-19](fr_list.md#fr-04-19) | NC | 0 |
| [FR-04-20](fr_list.md#fr-04-20) | NC | 0 |
| [FR-04-21](fr_list.md#fr-04-21) | NC | 0 |

Transactional FP: 130. Bottom-up hours per transactional FP by feature: F-01 5.75, F-02 4, F-03 5.13, F-04 12.20 (project 5.88).


Data functions (W0 Table 4, described in [scope.md](../project_brief/scope.md#table-4-data-functions)):

| Data group | ILF / EIF | FP |
|---|---|---|
| Book placement & library layout | EIF | 7 |
| Book review | ILF | 10 |
| Reading history & preferences | ILF | 10 |
| Book catalogue | EIF | 7 |
| Reader accounts | EIF | 7 |
| Book QR codes | ILF | 10 |
| Saved books list | ILF | 10 |
| Reader loan records | EIF | 7 |
| Chatbot conversations | ILF | 10 |
| Staff accounts | EIF | 7 |
| Online book read log | ILF | 10 |

Total data-function points: 95.


## 8. Assumptions (W5 §2)

| Assumption | Value | Source |
|---|---|---|
| Junior rate | 200,000 | ITviec 2025-26 salary report |
| Senior rate | 300,000 | ITviec 2025-26 salary report |
| Expert rate | 400,000 | ITviec 2025-26 salary report |
| AI leverage — FE / BE / INT | 0.35 / 0.7 / 1 | Class parameter, recalibrated each cohort |
| Verification factor — precise / vague | 0.15 / 0.4 | Class parameter |
| Hours per function point | 3 | Class parameter — used only for the cross-check |
| Team capacity (person-hours) | 360 | 6 people x 12 weeks x 5 h |
| Money contingency on the Must set | 0.10 | Covers estimation error only. Do NOT add 20% on top of the Could pool — same buffer twice. |

## 9. Cash flow (W6)

### 9.1 Assumptions

| Assumption | Value | Unit |
|---|---|---|
| Discount rate (WACC / hurdle rate) | 12.0% | % per year |
| Evaluation horizon | 5 | years (1 to 5) |
| Annual running cost as % of build cost | 15.0% | % of build / year |
| Contingency rate on the Must set | 10.0% | % of Must cost |
| Must-set cost (contingency base) | 68,920,000 | VND |

Steady-state annual benefit by tier (VND): Must 30,000,000, Should 15,000,000, Could 10,000,000.


Adoption ramp-up (share of steady-state benefit): year 0 0.0%, year 1 40.0%, year 2 70.0%, year 3 100.0%, year 4 100.0%, year 5 100.0%.


### 9.2 Scenarios and year-0 investment

| Scenario | Must | Should | Could | Build cost | Contingency | Year-0 investment | Benefit / year | Running cost / year |
|---|---|---|---|---|---|---|---|---|
| Pessimistic — Must only | 1 | 0 | 0 | 68,920,000 | 6,892,000 | 75,812,000 | 30,000,000 | 10,338,000 |
| Base — Must + Should | 1 | 1 | 0 | 93,680,000 | 6,892,000 | 100,572,000 | 45,000,000 | 14,052,000 |
| Optimistic — full scope | 1 | 1 | 1 | 136,980,000 | 6,892,000 | 143,872,000 | 55,000,000 | 20,547,000 |

### 9.3 Pessimistic — Must only — Year-0 investment 51,942,000 VND

| Line item | Year 0 | Year 1 | Year 2 | Year 3 | Year 4 | Year 5 |
|---|---|---|---|---|---|---|
| Benefits | 0 | 12,000,000 | 21,000,000 | 30,000,000 | 30,000,000 | 30,000,000 |
| Running cost | 0 | -10,338,000 | -10,338,000 | -10,338,000 | -10,338,000 | -10,338,000 |
| Investment (build + contingency) | -75,812,000 | 0 | 0 | 0 | 0 | 0 |
| Net cash flow | -75,812,000 | 1,662,000 | 10,662,000 | 19,662,000 | 19,662,000 | 19,662,000 |
| Cumulative net cash flow | -75,812,000 | -74,150,000 | -63,488,000 | -43,826,000 | -24,164,000 | -4,502,000 |
| Discount factor | 1 | 0.893 | 0.797 | 0.712 | 0.636 | 0.567 |
| PV of net cash flow | -75,812,000 | 1,483,929 | 8,499,681 | 13,995,023 | 12,495,556 | 11,156,747 |
| Cumulative PV | -75,812,000 | -74,328,071 | -65,828,390 | -51,833,367 | -39,337,811 | -28,181,064 |
| Payback(year in which cumulative turns >= 0) |  |  |  |  |  |  |

### 9.4 Base — Must + Should — Year-0 investment 71,462,000 VND

| Line item | Year 0 | Year 1 | Year 2 | Year 3 | Year 4 | Year 5 |
|---|---|---|---|---|---|---|
| Benefits | 0 | 18,000,000 | 31,500,000 | 45,000,000 | 45,000,000 | 45,000,000 |
| Running cost | 0 | -14,052,000 | -14,052,000 | -14,052,000 | -14,052,000 | -14,052,000 |
| Investment (build + contingency) | -100,572,000 | 0 | 0 | 0 | 0 | 0 |
| Net cash flow | -71,462,000 | 3,948,000 | 17,448,000 | 30,948,000 | 30,948,000 | 30,948,000 |
| Cumulative net cash flow | -71,462,000 | -67,514,000 | -50,066,000 | -19,118,000 | 11,830,000 | 42,778,000 |
| Discount factor | 1 | 0.893 | 0.797 | 0.712 | 0.636 | 0.567 |
| PV of net cash flow | -71,462,000 | 3,525,000 | 13,909,439 | 22,028,175 | 19,668,013 | 17,560,726 |
| Cumulative PV | -71,462,000 | -67,937,000 | -54,027,561 | -31,999,386 | -12,331,373 | 5,229,354 |
| Payback (year in which cumulative turns >= 0) |  |  |  |  | 4 |  |

### 9.5 Optimistic — full scope — Year-0 investment 103,002,000 VND

| Line item | Year 0 | Year 1 | Year 2 | Year 3 | Year 4 | Year 5 |
|---|---|---|---|---|---|---|
| Benefits | 0 | 22,000,000 | 38,500,000 | 55,000,000 | 55,000,000 | 55,000,000 |
| Running cost | 0 | -20,547,000 | -20,547,000 | -20,547,000 | -20,547,000 | -20,547,000 |
| Investment (build + contingency) | -143,872,000 | 0 | 0 | 0 | 0 | 0 |
| Net cash flow | -143,872,000 | 1,453,000 | 17,953,000 | 34,453,000 | 34,453,000 | 34,453,000 |
| Cumulative net cash flow | -143,872,000 | -142,419,000 | -124,466,000 | -90,013,000 | -55,560,000 | -21,107,000 |
| Discount factor | 1 | 0.893 | 0.797 | 0.712 | 0.636 | 0.567 |
| PV of net cash flow | -143,872,000 | 1,297,321 | 14,312,022 | 24,522,965 | 21,895,504 | 19,549,557 |
| Cumulative PV | -143,872,000 | -142,574,679 | -128,262,657 | -103,739,692 | -81,844,188 | -62,294,630 |
| Payback (year in which cumulative turns >= 0) |  |  |  |  |  |  |

### 9.6 Results

| Metric | Pessimistic: Must only | Base: Must + Should | Optimistic: full scope |
|---|---|---|---|
| Year-0 investment (VND) | 75,812,000 | 71,462,000 | 143,872,000 |
| Steady-state benefit per year (VND) | 30,000,000 | 45,000,000 | 55,000,000 |
| Total benefits over horizon (VND) | 123,000,000 | 184,500,000 | 225,500,000 |
| Total running cost over horizon (VND) | 51,690,000 | 70,260,000 | 102,735,000 |
| Net cash flow over horizon, undiscounted (VND) | -4,502,000 | 42,778,000 | -21,107,000 |
| NPV (VND) | -28,181,064 | 5,229,354 | -62,294,630 |
| IRR (% per year) | -1.7% | 14.3% | -4.2% |
| Payback, simple (years) | > horizon | 3.62 | > horizon |
| Profitability index (PV of inflows / investment) | 0.63 | 1.07 | 0.57 |
| Decision signal | ACCEPT | ACCEPT | REJECT / REVIEW |

## 10. Known inconsistencies to fix

Found when the workbook was exported on 23/11/2026. The figures above are copied as they were; fix them here, not in the archived workbook.

1. **Base scenario, year 0.** §9.2 gives a year-0 investment of 100,572,000 VND, but the net cash flow of year 0 in §9.4 is -71,462,000 VND, and §9.6 uses that smaller figure. With 100,572,000 VND the base NPV is about -23,880,646 VND instead of 5,229,354 VND, so the "ACCEPT" signal of the base scenario may not hold.
2. **Pessimistic scenario heading** says year-0 investment 51,942,000 VND, but the table uses 75,812,000 VND.
3. **Pessimistic decision signal** is "ACCEPT" although its NPV is negative (-28,181,064 VND) and its profitability index is 0.63.

