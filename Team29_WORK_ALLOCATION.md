# Work Allocation Report — [Team ID]

## 1. Team Members

| Full Name | Student ID | GitHub Username | Email |
|-----------|------------|-----------------|-------|
| 林昀希 | 113403534 | Ivy714 | [待補] |
| 李盈萱 | 113403504 | Shiuan129 | [待補] |
| 陳思宇 | 113403501 | ssuyuchen | chenssuyu941007@gmail.com |

---

## 2. Task Ownership

For each task, the primary owner is the person most responsible for delivering that part. Supporting members assisted through review, testing, integration, or documentation.

### Code Repository

| Task | Primary Owner | Supporting Member(s) | Notes |
|------|---------------|----------------------|-------|
| **Task 1** — Relational schema design (`schema.sql`) | 林昀希 | 陳思宇 | 林昀希主要負責 PostgreSQL schema 設計與 ER Diagram 草稿。陳思宇協助閱讀 mock JSON data，檢查資料欄位、entity relationships、transaction data 與 policy data 是否有被 schema 正確支援。 |
| **Task 2a** — Core availability & fare queries (`query_national_rail_availability`, `query_metro_schedules`, `query_national_rail_fare`, `query_metro_fare`) | 林昀希 | 李盈萱、陳思宇 | 林昀希主要實作核心 PostgreSQL 查詢功能，包括 national rail availability、metro schedules、national rail fare 與 metro fare。李盈萱協助 review 查詢邏輯，陳思宇協助透過 pgAdmin、UI 與 AI agent 測試查詢結果。 |
| **Task 2b** — Seat & user queries (`query_available_seats`, `query_user_profile`, `query_user_bookings`, `query_payment_info`) | 林昀希 | 李盈萱、陳思宇 | 林昀希主要實作座位、使用者、訂票紀錄與付款資訊相關查詢。李盈萱協助 review，陳思宇協助測試 available seats、user profile、show my bookings 與 payment information 的查詢結果是否正確。 |
| **Task 2c** — Write operations (`execute_booking`, `execute_cancellation`) | 林昀希 | 陳思宇 | 林昀希主要實作訂票與取消訂票邏輯。陳思宇協助測試 booking、cancellation、show my bookings、seat reuse / seat availability，以及取消訂票後 UI 與資料庫狀態是否一致。 |
| **Task 2d** — Authentication queries (`login_user`, `register_user`, `get_user_secret_question`, `verify_secret_answer`, `update_password`) | 林昀希 | 陳思宇 | 林昀希主要實作登入、註冊、密碼重設與安全問題相關 PostgreSQL functions。陳思宇協助測試 registration、login、secret question verification 與 password update flow。 |
| **Task 3** — PostgreSQL seeding (`seed_postgres.py`) | 林昀希 | 陳思宇 | 林昀希主要實作 PostgreSQL seed 程式。陳思宇協助重新 seed、使用 pgAdmin 驗證資料是否正確寫入，並檢查 seeded data 是否與 mock JSON data 一致。 |
| **Task 4** — Neo4j graph design & seeding (`seed_neo4j.py`, `seed.cypher`) | 李盈萱 | 林昀希、陳思宇 | 李盈萱主要負責 Neo4j 路網設計與 graph seeding。林昀希在 Neo4j 階段協助補強 graph edges，陳思宇協助確認 JSON station data、schedule data 與路網資料的一致性。 |
| **Task 5** — Neo4j query functions (`graph/queries.py`) | 李盈萱 | 林昀希、陳思宇 | 李盈萱主要實作 Neo4j graph query functions，並確認 Dijkstra / shortest path 查詢結果。林昀希協助 query 與 agent tool 整合，陳思宇負責透過 UI 與 AI agent 測試 route query 是否能正確回應。 |
| **Task 6** *(if attempted)* — Optional extension | 未嘗試 | N/A | 最終提交未包含 optional extension。 |

---

### Design Document

| Section | Primary Author | Supporting Member(s) | Notes |
|---------|----------------|----------------------|-------|
| Section 1 — ER Diagram | 林昀希 | 陳思宇 | 林昀希根據 PostgreSQL schema 製作 ER Diagram 草稿。陳思宇協助檢查 ER Diagram 是否符合 mock JSON data、transactions、payments、feedback 與 policy-related data 的需求。 |
| Section 2 — Normalisation Justification | 林昀希 | 李盈萱、陳思宇 | 林昀希主要撰寫 relational database design 與 normalization 說明。李盈萱協助 review，陳思宇協助確認資料拆分是否符合 JSON data 與系統功能需求。 |
| Section 3 — Graph Database Design Rationale | 李盈萱 | 林昀希、陳思宇 | 李盈萱主要撰寫 Neo4j graph database 設計理由。林昀希協助補充 graph edges 與 route representation 相關說明，陳思宇協助檢查設計是否能支援 UI / AI agent 路線查詢。 |
| Section 4 — Vector / RAG Design | 陳思宇 | 林昀希、李盈萱 | 陳思宇主要負責 RAG / vector database 相關內容，包括整理 policy chunks、確認 `refund_policy.json`、`booking_rules.json`、`travel_policies.json`、`ticket_types.json` 的 chunk strategy，處理 `seed_vectors.py` 流程、確認 `nomic-embed-text` embedding model，並驗證資料能寫入 pgvector。 |
| Section 5 — AI Tool Usage Evidence | 陳思宇 | 林昀希、李盈萱 | 陳思宇主要統整 AI tool usage evidence，包括記錄用 AI 協助 schema 檢查、query 檢查、RAG chunk strategy、UI / agent 測試與 final report 撰寫的過程。林昀希與李盈萱補充各自負責部分的 AI 使用紀錄。 |
| Section 6 — Reflection & Trade-offs | 陳思宇 | 林昀希、李盈萱 | 陳思宇根據整合、測試、debug 與 demo 準備過程撰寫 reflection 與 trade-offs，並補充 RAG、UI integration、database verification 的實作取捨。林昀希與李盈萱協助補充 PostgreSQL 與 Neo4j 設計上的取捨。 |
| Section 7 — Optional Extension *(if applicable)* | 不適用 | N/A | 本專案未包含 optional extension。 |

---

## 3. Estimated Contribution Percentages

| Member | Estimated % | Brief justification |
|--------|-------------|---------------------|
| 林昀希 | 33.333% | 主要負責 PostgreSQL 相關工作，包括 relational schema design、ER Diagram draft、PostgreSQL seeding、relational query functions、booking/cancellation logic 與 authentication queries。 |
| 李盈萱 | 33.333% | 主要負責 Neo4j graph database 相關工作，包括 route graph design、`seed.cypher` / `seed_neo4j.py`、graph query functions，以及 shortest-path / Dijkstra 查詢驗證。 |
| 陳思宇 | 33.333% | 主要負責整合、測試與 RAG/vector 相關工作。具體包含閱讀與確認 mock JSON data、協助檢查 schema 是否符合資料需求、準備與修改 policy chunks / policy JSON、處理 `seed_vectors.py` 與 pgvector 寫入流程、確認 `nomic-embed-text` embedding model、使用 pgAdmin 驗證 PostgreSQL seed 結果、測試 UI 與 AI agent 的自然語言查詢流程、檢查 booking / cancellation / seat availability 行為、協助 debug panel 驗證，並統整 demo 與 final report 相關內容。 |
| **Total** | **100%** | |

---

## 4. Mid-Project Changes

| Change | Original plan | Revised plan | Reason |
|--------|---------------|--------------|--------|
| 後期整合階段增加跨任務支援。 | 一開始每位成員主要負責各自技術區塊：PostgreSQL、Neo4j、整合/測試。 | 在後期整合階段，組員互相支援 query review、reseed、UI 測試、debug panel 驗證與 demo 準備。 | 為了確保 PostgreSQL、Neo4j、RAG/vector data 與 UI 能正確整合並通過 final submission 前的測試。 |

---

## 5. Team Declaration

We confirm that this work allocation accurately reflects how responsibilities were divided within our team.

| Name | Signature / Typed name | Date |
|------|------------------------|------|
| 林昀希 | 林昀希 | 2026-06-11 |
| 李盈萱 | 李盈萱 | 2026-06-11 |
| 陳思宇 | 陳思宇 | 2026-06-11 |
