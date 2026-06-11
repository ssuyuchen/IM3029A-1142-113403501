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
| **Task 1** — Relational schema design (`schema.sql`) | 林昀希 | 陳思宇 | 林昀希主要負責 PostgreSQL schema 設計與 ER Diagram 草稿。陳思宇協助閱讀 JSON 資料，確認需要納入的實體、欄位與關聯。 |
| **Task 2a** — Core availability & fare queries (`query_national_rail_availability`, `query_metro_schedules`, `query_national_rail_fare`, `query_metro_fare`) | 林昀希 | 李盈萱、陳思宇 | 林昀希主要實作核心 PostgreSQL 查詢功能，包括班次查詢與票價查詢。李盈萱協助 review 查詢邏輯，陳思宇協助透過 pgAdmin 與 UI 測試查詢結果。 |
| **Task 2b** — Seat & user queries (`query_available_seats`, `query_user_profile`, `query_user_bookings`, `query_payment_info`) | 林昀希 | 李盈萱、陳思宇 | 林昀希主要實作座位、使用者、訂票紀錄與付款資訊相關查詢。李盈萱協助 review，陳思宇協助在整合階段測試查詢結果是否正確。 |
| **Task 2c** — Write operations (`execute_booking`, `execute_cancellation`) | 林昀希 | 陳思宇 | 林昀希主要實作訂票與取消訂票邏輯。陳思宇協助測試訂票、取消訂票、座位釋放與 UI 顯示結果。 |
| **Task 2d** — Authentication queries (`login_user`, `register_user`, `get_user_secret_question`, `verify_secret_answer`, `update_password`) | 林昀希 | 陳思宇 | 林昀希主要實作登入、註冊、密碼重設與安全問題相關 PostgreSQL functions。陳思宇協助功能測試與驗證。 |
| **Task 3** — PostgreSQL seeding (`seed_postgres.py`) | 林昀希 | 陳思宇 | 林昀希主要實作 PostgreSQL seed 程式。陳思宇協助使用 pgAdmin 驗證 seed 結果，並確認資料與 JSON 來源一致。 |
| **Task 4** — Neo4j graph design & seeding (`seed_neo4j.py`, `seed.cypher`) | 李盈萱 | 林昀希、陳思宇 | 李盈萱主要負責 Neo4j 路網設計與 graph seeding。林昀希在 Neo4j 階段協助補強 graph edges，陳思宇協助確認 JSON 資料與路網資料的一致性。 |
| **Task 5** — Neo4j query functions (`graph/queries.py`) | 李盈萱 | 林昀希、陳思宇 | 李盈萱主要實作 Neo4j graph query functions，並確認 Dijkstra / shortest path 查詢結果。林昀希協助相關 query 與 agent tool 整合，陳思宇負責端到端整合測試。 |
| **Task 6** *(if attempted)* — Optional extension | 未嘗試 | N/A | 最終提交未包含 optional extension。 |

---

### Design Document

| Section | Primary Author | Supporting Member(s) | Notes |
|---------|----------------|----------------------|-------|
| Section 1 — ER Diagram | 林昀希 | 陳思宇 | 林昀希根據 PostgreSQL schema 製作 ER Diagram 草稿。陳思宇協助檢查設計是否符合 JSON 資料內容。 |
| Section 2 — Normalisation Justification | 林昀希 | 李盈萱 | 林昀希主要撰寫 relational database design 與 normalization 說明。李盈萱協助 review。 |
| Section 3 — Graph Database Design Rationale | 李盈萱 | 林昀希 | 李盈萱主要撰寫 Neo4j graph database 設計理由。林昀希協助補充 graph edges 與 route representation 相關說明。 |
| Section 4 — Vector / RAG Design | 陳思宇 | 林昀希、李盈萱 | 陳思宇主要負責 policy data preparation、`seed_vectors.py`、embedding setup 與 pgvector 寫入驗證。林昀希與李盈萱協助確認 RAG 層與資料庫功能的整合。 |
| Section 5 — AI Tool Usage Evidence | 陳思宇 | 林昀希、李盈萱 | 陳思宇主要統整 AI tool usage evidence 與整合測試紀錄。林昀希與李盈萱提供各自負責部分的 AI 使用紀錄。 |
| Section 6 — Reflection & Trade-offs | 陳思宇 | 林昀希、李盈萱 | 陳思宇根據整合與測試過程撰寫 reflection 與 trade-offs。其他成員協助補充各自 task 的設計取捨。 |
| Section 7 — Optional Extension *(if applicable)* | 不適用 | N/A | 本專案未包含 optional extension。 |

---

## 3. Estimated Contribution Percentages

| Member | Estimated % | Brief justification |
|--------|-------------|---------------------|
| 林昀希 | 38% | 主要負責 PostgreSQL 核心部分，包括 relational schema design、PostgreSQL seeding、relational query functions、booking/cancellation logic 與 authentication queries。這些內容構成系統主要交易資料庫功能，因此工作量比例最高。 |
| 李盈萱 | 32% | 主要負責 Neo4j graph database 部分，包括 route graph design、graph seeding、graph query functions，以及 shortest-path / Dijkstra 查詢驗證。同時也協助 review PostgreSQL query logic。 |
| 陳思宇 | 30% | 主要負責整合、測試、RAG/vector preparation、policy data verification、pgAdmin 檢查、UI 端到端測試、debug panel 驗證與 demo 流程統整。 |
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
