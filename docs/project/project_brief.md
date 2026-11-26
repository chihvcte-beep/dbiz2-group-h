# Project brief: Group H Library Core System

Lessons 1 and 2 (kick-off, project management, handover from the client). Every later document
refers back to the names fixed here.

| Field | Value |
|---|---|
| Product | Group H Library Core System, an add-on to the National Library of Vietnam's existing OPAC catalogue system ([opac.nlv.gov.vn](https://opac.nlv.gov.vn)) |
| Client | National Library of Vietnam (Thư viện Quốc gia Việt Nam / NLV), under the Ministry of Culture, Sports and Tourism |
| Client contact | Representative of the Automation and Cataloguing Divisions |
| Team | Group H (six members: Chi, Triệu, Linh, Hà, Hoa, Nhi) |
| Course | DBIZ2 Digital Business Project II, followed by DBIZ3 (build) |

## Problem

Readers arriving at the National Library of Vietnam face significant difficulties physically locating books within sprawling multi-floor reading rooms and dense shelf rows because the existing OPAC system only provides generic call numbers and room names without precise shelf coordinates or interactive floor maps. Furthermore, readers have no way to read or share peer book reviews or ratings on the current catalogue, leaving them without qualitative peer guidance when selecting physical or digital titles. Readers also lack smart personalized recommendations and intuitive natural-language book discovery; they must rely on rigid keyword searches and cannot easily track their reading history or maintain an organized saved-books list for physical library visits.

On-site library staff endure slow, manual workflows when identifying unlabelled books, lack an automated mechanism to generate and batch-print standardized QR code labels for physical book stacks, and have no dedicated tool to moderate policy-violating or abusive reader reviews.

## Goal of the project

Readers pinpoint the exact shelf coordinates of physical books and navigate via interactive digital floor maps before or during their visit. Readers browse and post community book reviews, scan physical QR codes directly on book covers/spines, maintain personal reading histories and saved reading lists, and obtain conversational book discovery via an AI chatbot alongside preference-based recommendations.

On-site Staff access a minimal operational interface to batch-print 24-up A4 QR code label sheets for newly synced physical books and moderate reported reader reviews according to clear library guidelines.

The system integrates as a lightweight add-on, performing automated one-way daily synchronization from the Library Internal System (catalogue, shelf placements, library card reader accounts, and loan records) without modifying internal master databases.

Measures and stakeholder requirements agreed with the client are documented in [the CVCA](../context/cvca.md) and [scope.md](../function-list/scope.md), with effort and financial estimates detailed in [cost.md](../function-list/cost.md).

## Team and roles

| Member | Role | Owns |
|---|---|---|
| Chi | Integrator and Project Manager | F-00 Platform and Access; repository integrity, merges, task assignments, decision log, cross-document integration |
| Triệu | Feature Owner | F-03 Discovery, Reading History and Recommendation (UC-07, UC-08, UC-09; screens S-F03-02, S-F03-06, S-F03-07) |
| Linh | System Architecture and Lead Reviewer | System architecture ([system-architecture.md](../architecture/system-architecture.md)), system requirements (SyR), cross-specification consistency review |
| Hà | Feature Owner | F-00 Platform & Access and F-04 Operations (UC-10, UC-11, UC-13 staff part; screens S-F00-01 to S-F00-03, S-F04-01; CVCA stakeholder requirements) |
| Hoa | Feature Owner | F-02 Book Reviews and QR Codes (UC-04, UC-05, UC-06, UC-13, UC-14; screens S-F02-01 to S-F02-04; Architecture Decision Records / ADRs) |
| Nhi | Feature Owner | F-01 Book Location & Library Map, plus F-03 format filter & saved list (UC-01, UC-02, UC-03, UC-12; screens S-F01-01, S-F01-02, S-F03-01, S-F03-03; Business Rules in [scope.md](../function-list/scope.md)) |

## Milestones in DBIZ2

| When | Milestone | What the client sees |
|---|---|---|
| After Lesson 4 | Senior Meeting 1: project scope confirmation | CVCA, Context Diagram, Use Case Diagram, Sequence Diagrams, System Architecture |
| After Lesson 6 | Midterm | Function List, cost and effort budgeting (W0 Scope, W1–W5 FR List, Cost and Cash Flow) |
| After Lesson 8 | Senior Meeting 2: Final Package Review | Activity diagrams, usage flow, screen list, screen transitions, UI conventions, Wireframes and Screen Specs |

The whole documentation package is handed over to DBIZ3, where the team builds the product with AI coding agents.
