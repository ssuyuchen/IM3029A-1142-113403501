# Work Allocation Report — [Team ID]

## 1. Team Members

| Full Name | Student ID | GitHub Username | Email |
|-----------|------------|-----------------|-------|
| 林昀希 | 113403534 | Ivy714 | [待補] |
| 李盈萱 | 113403504 | Shiuan129 | [待補] |
| 陳思宇 | 113403501 | ssuyuchen | chenssuyu941007@gmail.com |

---

## 2. Task Ownership

### Code Repository

| Task | Primary Owner | Supporting Member(s) | Notes |
|------|---------------|----------------------|-------|
| **Task 1** — Relational schema design (`schema.sql`) | 林昀希 | 陳思宇 | 林昀希負責 PostgreSQL schema 設計與 ER diagram 草稿。陳思宇協助對照 mock JSON data，確認資料表、欄位與關聯能涵蓋專案資料需求。 |
| **Task 2a** — Core availability & fare queries (`query_national_rail_availability`, `query_metro_schedules`, `query_national_rail_fare`, `query_metro_fare`) | 林昀希 | 李盈萱、陳思宇 | 林昀希實作班次查詢與票價查詢。李盈萱協助檢查查詢邏輯，陳思宇透過 pgAdmin、UI 與 agent 測試查詢結果。 |
| **Task 2b** — Seat & user queries (`query_available_seats`, `query_user_profile`, `query_user_bookings`, `query_payment_info`) | 林昀希 | 李盈萱、陳思宇 | 林昀希實作座位、使用者、訂票紀錄與付款資訊查詢。陳思宇協助測試 available seats、user profile、show my bookings 與 payment information 的結果。 |
| **Task 2c** — Write operations (`execute_booking`, `execute_cancellation`) | 林昀希 | 陳思宇 | 林昀希實作訂票與取消訂票功能。陳思宇協助測試 booking、cancellation、seat availability、seat reuse，以及取消後 UI 與資料庫狀態是否一致。 |
| **Task 2d** — Authentication queries (`login_user`, `register_user`, `get_user_secret_question`, `verify_secret_answer`, `update_password`) | 林昀希 | 陳思宇 | 林昀希實作登入、註冊、密碼更新與安全問題相關功能。陳思宇協助測試 authentication flow。 |
| **Task 3** — PostgreSQL seeding (`seed_postgres.py`) | 林昀希 | 陳思宇 | 林昀希實作 PostgreSQL seeding。陳思宇協助重新 seed，並使用 pgAdmin 檢查資料是否正確寫入。 |
| **Task 4** — Neo4j graph design & seeding (`seed_neo4j.py`, `seed.cypher`) | 李盈萱 | 林昀希、陳思宇 | 李盈萱負責 Neo4j 路網設計與 graph seeding。林昀希協助補充 graph edges，陳思宇協助檢查 station 與 schedule data 是否和路網一致。 |
| **Task 5** — Neo4j query functions (`graph/queries.py`) | 李盈萱 | 林昀希、陳思宇 | 李盈萱實作 Neo4j graph queries 與 shortest-path 查詢。林昀希協助 query 與 agent tool 整合，陳思宇透過 UI 與 agent 測試 route query。 |
| **Task 6** *(if attempted)* — Optional extension | 未嘗試 | N/A | Final submission did not include an optional extension. |

---

### Design Document

| Section | Primary Author | Supporting Member(s) | Notes |
|---------|----------------|----------------------|-------|
| Section 1 — ER Diagram | 林昀希 | 陳思宇 | 林昀希負責 ER diagram。陳思宇協助對照 mock JSON data，確認圖中的 entities 與 relationships 合理。 |
| Section 2 — Normalisation Justification | 林昀希 | 李盈萱、陳思宇 | 林昀希撰寫 normalization justification。李盈萱協助 review，陳思宇協助檢查資料拆分是否符合 JSON data 與系統功能。 |
| Section 3 — Graph Database Design Rationale | 李盈萱 | 林昀希、陳思宇 | 李盈萱撰寫 Neo4j graph design rationale。林昀希協助補充 graph edges 說明，陳思宇協助確認該設計能支援 route query。 |
| Section 4 — Vector / RAG Design | 陳思宇 | 林昀希、李盈萱 | 陳思宇負責 RAG / vector database 設計說明，包括 policy chunks、policy JSON、`seed_vectors.py`、`nomic-embed-text` embedding model，以及 pgvector 寫入驗證。 |
| Section 5 — AI Tool Usage Evidence | 陳思宇 | 林昀希、李盈萱 | 陳思宇整理 AI tool usage evidence，內容包含 schema 檢查、query 檢查、RAG chunk strategy、UI / agent 測試與 report 撰寫紀錄。 |
| Section 6 — Reflection & Trade-offs | 陳思宇 | 林昀希、李盈萱 | 陳思宇整理 reflection 與 trade-offs，涵蓋整合測試、debug、RAG、UI testing 與 database verification。林昀希與李盈萱補充 PostgreSQL 與 Neo4j 部分。 |
| Section 7 — Optional Extension *(if applicable)* | 不適用 | N/A | The project did not include an optional extension. |

---

## 3. Estimated Contribution Percentages

| Member | Estimated % | Brief justification |
|--------|-------------|---------------------|
| 林昀希 | 33.3% | 負責 PostgreSQL 相關工作，包括 schema、ER diagram、seeding、relational queries、booking/cancellation，以及 authentication functions。 |
| 李盈萱 | 33.3% | 負責 Neo4j 相關工作，包括 route graph design、`seed.cypher`、`seed_neo4j.py`、graph queries，以及 shortest-path testing。 |
| 陳思宇 | 33.3% | 負責 integration testing、RAG/vector preparation 與 final verification，包括 mock JSON data 檢查、policy chunks、`seed_vectors.py`、embedding model setup、pgvector verification、pgAdmin 檢查、UI / agent 測試，以及 booking / cancellation / seat availability 測試。 |
| **Total** | **100%** | |

---

## 4. Mid-Project Changes

| Change | Original plan | Revised plan | Reason |
|--------|---------------|--------------|--------|
| 後期整合階段增加跨任務支援。 | 原先三位成員分別負責 PostgreSQL、Neo4j、RAG / integration testing。 | 後期整合時，成員互相支援 query review、reseed、UI testing、debug panel verification 與 demo preparation。 | 需要確認 PostgreSQL、Neo4j、RAG/vector data 與 UI 可以在 final submission 前正常整合。 |

---

## 5. Team Declaration

We confirm that this work allocation accurately reflects how responsibilities were divided within our team.

| Name | Signature / Typed name | Date |
|------|------------------------|------|
| 林昀希 | 林昀希 | 2026-06-11 |
| 李盈萱 | 李盈萱 | 2026-06-11 |
| 陳思宇 | 陳思宇 | 2026-06-11 |
