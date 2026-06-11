# Peer Review Report

> **Instructions:** Complete this form **individually and independently**.  
> Do not discuss your ratings with teammates before submitting.  
> Submit via EEClass as a **separate, confidential submission** — not in the shared team repo.  
> Your teammates will not see this report.
>
> Reference the team's `WORK_ALLOCATION_TEMPLATE.md` when completing this form.

---

## Your Details

| Field | Your answer |
|-------|------------|
| Full Name | 陳思宇 |
| Student ID | 113403501 |
| Team ID | 29 |
| Date submitted | 2026/06/11 |

---

## Rating Scale

| Rating | Meaning |
|--------|---------|
| **5** | Exceeded expectations — delivered more than agreed; helped teammates; consistently high quality |
| **4** | Met expectations fully — delivered exactly what was agreed; on time; good quality |
| **3** | Mostly met expectations — minor shortfalls; one or two items completed late or with help |
| **2** | Partially met expectations — noticeable gaps; teammates had to cover some tasks |
| **1** | Did not meet expectations — significant tasks left incomplete; very limited contribution |

---

## Section A — Self-Assessment

### A1. What did you personally implement?

> *Your answer:*

- **閱讀與確認 JSON mock data**  
  閱讀專案提供的 JSON 資料，確認使用者、車站、班次、訂票、付款、feedback 和 policy 相關資料的欄位與關係，作為後續資料庫設計與測試的基礎。

- **整理 policy 相關資料**  
  分析 `refund_policy.json`、`booking_rules.json`、`travel_policies.json`、`ticket_types.json`，確認這些檔案如何對應退款、訂票、票種、行李、腳踏車、寵物與乘車規範等問題。

- **新增與調整 policy JSON 內容**  
  協助補充 policy 內容，讓系統能回答更多實際使用情境，例如 metro 和 national rail 在退款、改票、day pass、腳踏車、寵物與行李規範上的差異。

- **設計 policy chunk strategy**  
  規劃 policy 文件如何切成適合 RAG 檢索的 chunks，包含 chunk 範圍、命名方式與 metadata，讓使用者用自然語言提問時能找到正確規則。

- **建立與修改 `policy_chunks.json`**  
  協助將 policy JSON 整理成可匯入 pgvector 的 `policy_chunks.json`，並檢查每個 chunk 的內容與 metadata 是否清楚、可檢索。

- **確認 `seed_vectors.py` 執行流程**  
  確認 `seed_vectors.py` 如何讀取 policy chunks、產生 embedding，並將資料寫入 pgvector，確保 policy 資料能進入 RAG 流程。

- **確認 embedding model 可正常使用**  
  協助確認 `nomic-embed-text` 已正確 pull，並確認它能用於 policy chunks 的向量化。

- **確認 pgvector 寫入正常**  
  協助檢查 policy chunks 轉成 embedding 後是否成功寫入 pgvector，讓後續 policy search 可以正常取得資料。

- **協助 PostgreSQL 測試與 pgAdmin 驗證**  
  使用 pgAdmin 協助檢查資料表、資料匯入狀態與查詢結果，確認 PostgreSQL 部分能支援訂票、付款、班次與使用者紀錄等功能。

- **協助 review `schema.sql`**  
  協助檢查 schema 是否符合專案需求，包含 primary key、foreign key、constraints，以及每個 foreign key 的 `ON DELETE` 行為是否合理。

- **協助 review `queries.py` / relational queries**  
  協助檢查 relational query functions 是否符合 task requirements，例如查詢班次、訂票紀錄、建立 booking、付款、取消與退款等功能。

- **協助確認 Task 4 查詢功能**  
  協助測試 Task 4 相關查詢，確認 relational database 查詢與 agent tool 回傳的結果是否符合 mock data 與使用者問題。

- **協助端到端整合測試**  
  測試使用者從 UI 輸入問題後，系統是否能透過 agent 正確呼叫 PostgreSQL、Neo4j 或 RAG policy search，並回傳合理答案。

- **協助檢查 UI.py 與回報問題**  
  在 UI 測試時協助確認問題是否能觸發正確流程，並回報可能來自 UI、agent、database query 或 RAG retrieval 的錯誤。

- **使用 debug panel 驗證 agent 流程**  
  透過 debug panel 檢查 agent 呼叫的 tool、資料庫回傳結果與最後回答，協助定位整合問題。

- **協助整體需求符合度檢查**  
  在後期協助對照 project requirements，確認 schema、queries、agent、policy chunks、seed vectors、UI 測試與文件內容沒有明顯遺漏。

- **全組共同完成 git sync 與 reseed 確認**  
  收尾階段全組一起確認 git 版本同步、資料庫 reseed 結果，以及 PostgreSQL、Neo4j、pgvector 是否能正常重建。

- **全組共同完成 demo 排練**  
  Demo 前全組一起確認展示流程，測試各自負責的 database、query、agent、RAG 和 UI 功能是否能順利展示。

---

### A2. What challenges did you face?

> *Your answer:*

- **理解 RAG、embedding、pgvector 和 policy JSON 的關係**  
  一開始需要花時間釐清原始 policy JSON、policy chunks、embedding model、pgvector 和 semantic search 之間的資料流。後來透過整理流程，確認資料會從 policy JSON 轉成 chunks，再產生 embedding 並寫入 pgvector，最後提供 agent 查詢使用。

- **設計適合自然語言查詢的 policy chunks**  
  Policy chunks 不能只照 JSON 結構切分，還需要考慮使用者實際會怎麼問問題。因此在整理 chunks 時，特別注意退款、改票、票種、腳踏車、寵物、行李、day pass 等常見情境，讓檢索結果更準確。

- **確認 pgvector 寫入與 embedding model 正常**  
  在處理 `seed_vectors.py` 時，需要確認 `nomic-embed-text` 是否已經 pull，embedding 是否能產生，以及資料是否成功寫入 pgvector。透過重新執行 seed 流程與檢查資料庫內容來確認結果。

- **判斷 schema 中 foreign key 的 `ON DELETE` 行為**  
  檢查 `schema.sql` 時，不能只把所有 foreign key 都套用同一種刪除規則，而是需要依照 users、bookings、payments、feedback、stations、schedules 等資料關係判斷合理行為。透過逐一檢查 foreign key 與 business logic 來修正或確認。

- **端到端測試時需要定位錯誤來源**  
  UI 回答錯誤時，問題可能來自 UI、agent intent、database query、RAG retrieval 或資料本身。透過 debug panel 檢查 tool calling、資料庫回傳結果與最後回答，逐步定位問題。

- **Git 與版本同步需要反覆確認**  
  專案後期需要多次 pull、commit、push 和確認 branch 狀態。透過檢查目前修改檔案、commit 狀態與 push 結果，降低漏推或覆蓋他人修改的風險。

---

### A3. Self-rating

| Criterion | Rating (1–5) | Justification (1–2 sentences) |
|-----------|-------------|-------------------------------|
| I delivered the tasks assigned to me in the work allocation | 4 | 完成了 policy JSON、policy chunk strategy、`policy_chunks.json`、`seed_vectors.py` 流程確認、pgvector 寫入確認、PostgreSQL 測試、UI 整合測試與 demo 前確認等工作。 |
| The quality of my work was satisfactory | 4 | 工作過程中有反覆檢查資料格式、RAG 檢索流程、pgvector 寫入結果、schema 設計、query functions 與 agent 回答是否符合專案需求。 |
| I communicated well and kept the team informed | 4 | 有整理修改內容、測試結果、commit / push 狀態與發現的問題，讓隊友能了解目前進度與需要確認的部分。 |
| I met deadlines agreed within the team | 4 | 按照團隊進度完成 policy 整理、RAG 準備、資料庫測試、整合測試與 demo 前確認，並配合收尾階段的同步與檢查。 |
| **Overall self-rating** | 4 | 完成分配到的整合與測試相關工作，也額外協助 schema、queries、agent、RAG 與需求符合度檢查。 |

---

### A4. Estimated contribution percentage

> My estimated contribution: **33.333333%**

---

## Section B — Peer Assessments

### B1. Assessment of Teammate 1

| Field | Your answer |
|-------|------------|
| Teammate's full name | 林昀希 |
| Teammate's student ID | 113403534 |

#### What did this teammate deliver?

> *Your answer:*

- **主要負責 PostgreSQL relational database 相關工作**  
  負責或主要參與 `schema.sql`、PostgreSQL seed scripts、relational query functions，以及資料表設計與資料匯入流程。

- **設計 relational schema**  
  建立 users、bookings、payments、feedback、stations、schedules、ticket types、seat layouts 等資料表關係，並處理 primary key、foreign key、constraints 與 indexes。

- **實作 relational query functions**  
  實作或協助實作查詢班次、查詢使用者訂票紀錄、查詢 national rail availability、建立 booking、付款、取消與退款等功能。

- **協助資料庫整合與測試**  
  在整合階段協助確認 PostgreSQL query results 是否能被 agent 正確呼叫與使用。

#### Did their actual contribution match the agreed work allocation?

> *Your answer (Yes / Mostly / Partially / No — with explanation):*

是。林昀希完成了 work allocation 中 PostgreSQL 相關的主要工作，包含 schema、seed workflow 和 relational query implementation，也有參與後續整合與修正。整體貢獻符合原本的分工。

#### Peer rating for this teammate

| Criterion | Rating (1–5) | Justification (1–2 sentences) |
|-----------|-------------|-------------------------------|
| Delivered the tasks assigned in the work allocation | 4 | 完成了分配到的 PostgreSQL 相關實作工作，符合團隊原本的分工。 |
| Quality of their work was satisfactory | 4 | 實作內容大致能支援最終資料庫與 agent 流程，經過 review 和測試後可正常整合。 |
| Communicated well and kept the team informed | 4 | 在 schema、query 或整合問題需要討論時，有與組員進行溝通。 |
| Met deadlines agreed within the team | 4 | 大致依照團隊時程完成負責的工作。 |
| **Overall rating for this teammate** | 4 | 對 relational database 部分有明確且重要的貢獻。 |

#### Estimated contribution percentage for this teammate

> My estimate of their contribution: **33.333333%**

---

### B2. Assessment of Teammate 2

| Field | Your answer |
|-------|------------|
| Teammate's full name | 李盈萱 |
| Teammate's student ID | 113403504 |

#### What did this teammate deliver?

> *Your answer:*

- **主要負責 Neo4j graph database 與 route 相關工作**  
  負責或主要參與 Neo4j graph model、graph seed scripts、station nodes、route relationships，以及 shortest path / route query logic。

- **建立 graph nodes 與 relationships**  
  將 metro stations、national rail stations、interchange stations 與相鄰站點關係整理成 graph database 結構，支援路線查詢與轉乘分析。

- **實作 graph query functions**  
  實作或協助實作 route search、shortest path、station adjacency、metro / national rail interchange 等查詢功能。

- **協助 agent integration 與測試**  
  協助確認 agent 能正確呼叫 graph query tools，並將 Neo4j 查詢結果轉成使用者能理解的路線回答。

#### Did their actual contribution match the agreed work allocation?

> *Your answer (Yes / Mostly / Partially / No — with explanation):*

是。李盈萱完成了 work allocation 中 Neo4j 與 route query 相關的主要工作，也有參與系統整合與測試。整體貢獻符合原本的分工。

#### Peer rating for this teammate

| Criterion | Rating (1–5) | Justification (1–2 sentences) |
|-----------|-------------|-------------------------------|
| Delivered the tasks assigned in the work allocation | 4 | 完成了分配到的 graph database 與 route query 相關工作。 |
| Quality of their work was satisfactory | 4 | 實作內容能支援 route search 和 shortest path 等功能，經過測試後能整合進最終系統。 |
| Communicated well and kept the team informed | 4 | 在 graph query 或整合問題需要確認時，有與組員進行溝通。 |
| Met deadlines agreed within the team | 4 | 大致依照團隊時程完成負責的工作。 |
| **Overall rating for this teammate** | 4 | 對 graph database 與 route search 部分有明確且重要的貢獻。 |

#### Estimated contribution percentage for this teammate

> My estimate of their contribution: **33.333333%**

---

## Section C — Contribution Percentage Summary

| Member | Your estimated % | Notes |
|--------|----------------|-------|
| 陳思宇 | 33.333333% | 負責 policy data、RAG chunks、pgvector / `seed_vectors.py` 流程確認、PostgreSQL 測試、UI 整合測試、debug 驗證與需求符合度檢查。整體分工平均。 |
| 林昀希 | 33.333333% | 主要負責 PostgreSQL schema、seed scripts、relational queries 與 relational database 相關功能。整體分工平均。 |
| 李盈萱 | 33.333333% | 主要負責 Neo4j graph database、route / shortest path query、interchange relationship 與 graph integration。整體分工平均。 |
| **Total** | **100%** | 三位成員分工平均。 |

---

## Section D — Overall Team Reflection

### D1. What went well in the team's collaboration?

> *Your answer (2–4 sentences):*

團隊有將 TransitFlow 專案分成清楚的工作區塊，包含 PostgreSQL relational database、Neo4j graph database、RAG policy data、AI agent integration、UI testing 等部分。每位成員都有完成自己負責的區域，並在需要時協助整合與測試。整體來說，三位成員的工作量平均，最後也有一起確認主要功能能否正常運作。

---

### D2. What would you do differently if you did this project again?

> *Your answer (2–4 sentences):*

如果重新做一次，會希望更早定義每個檔案的負責人，以及 branch、merge、commit 和 push 的規則，減少後期整合時的混亂。也會在專案初期建立更完整的 task checklist，包含 schema constraints、foreign keys、query functions、RAG chunks、seed scripts、agent tools 和 UI testing。這樣最後檢查時會更有系統，也能減少接近 deadline 時重複修改的情況。

---

### D3. Is there anything else the markers should know about team dynamics or individual contributions?

> *Your answer (or "Nothing to add"):*

Nothing to add.

---

## Declaration

I confirm that this peer review reflects my honest and independent assessment.  
I understand it will be kept confidential from my teammates.

**Signed:** 陳思宇 **Date:** 2026/06/11
