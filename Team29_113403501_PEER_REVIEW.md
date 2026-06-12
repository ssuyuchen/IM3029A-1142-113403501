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
| Date submitted | 2026/06/12 |

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

* **Reviewed and verified the JSON mock data**  
  I reviewed the JSON mock data used in the project, including users, stations, schedules, bookings, payments, feedback, refund policies, booking rules, travel policies, and ticket types. This helped ensure that the database design, seed workflow, RAG retrieval, and UI testing were based on consistent data.

* **Organized policy-related data for RAG retrieval**  
  I reviewed and organized `refund_policy.json`, `booking_rules.json`, `travel_policies.json`, and `ticket_types.json`. I checked that policy content about refunds, booking rules, ticket changes, day passes, bicycles, pets, luggage, and passenger rules could support realistic user questions.

* **Created and reviewed `policy_chunks.json`**  
  I helped convert the original policy JSON files into retrieval-friendly policy chunks. I checked whether each chunk had clear content, appropriate metadata, and enough semantic context for natural language retrieval.

* **Verified the `seed_vectors.py` and pgvector workflow**  
  I checked how `seed_vectors.py` reads policy chunks, generates embeddings, and inserts them into the `policy_documents` table. I also helped confirm that the policy chunks could be imported into pgvector correctly.

* **Assisted with PostgreSQL testing and pgAdmin verification**  
  I used pgAdmin to inspect seeded tables, imported records, and query results. This included checking users, bookings, payments, schedules, feedback, policy documents, and related relational records.

* **Assisted in reviewing `schema.sql`**  
  I helped review whether the schema met the project requirements, including primary keys, foreign keys, constraints, indexes, and `ON DELETE` behavior. I also checked whether the delete behavior matched the business logic of users, bookings, payments, feedback, stations, and schedules.

* **Assisted in reviewing and testing `queries.py` functions**  
  I helped test relational functions for schedule queries, national rail availability, user booking retrieval, booking creation, payment handling, cancellation logic, refund calculation, and seat availability.

* **Debugged login and reseeding issues**  
  I helped check whether the UI login input matched the authentication logic and PostgreSQL user credential data. I also helped confirm that reseeding should update existing credential records so that test accounts remained usable.

* **Tested booking display, cancellation, and seat availability behavior**  
  I tested the `show my booking` and cancellation workflows. I helped confirm that cancelled bookings should not appear in the active booking list and should not continue occupying seats.

* **Performed end-to-end UI and agent testing**  
  I tested whether the UI and agent could correctly call PostgreSQL, Neo4j, or RAG policy search based on user questions. I also checked whether the final answers were reasonable and consistent with the database or policy results.

* **Used the debug panel to verify the agent workflow**  
  I used the debug panel to inspect tool calls, raw database results, and final responses. This helped identify whether an issue came from the UI, agent intent detection, database query, RAG retrieval, or the data itself.

* **Completed and revised the design document**  
  I helped complete `Team29_DESIGN_DOC.md`, including sections related to project structure, database design, RAG workflow, testing results, Task 6 extension, and final integration. I also revised the document to make the explanation more consistent with the actual implementation.

* **Assisted with final functional verification and submission preparation**  
  In the final stage, I helped verify login, booking, show bookings, cancellation, refund handling, policy retrieval, reseeding, git synchronization, and demo flow. This helped confirm that the main functions could be demonstrated smoothly.

---

### A2. What challenges did you face?

> *Your answer:*

* **Understanding the full RAG and pgvector workflow**  
  At first, I needed time to clarify the relationship between policy JSON files, policy chunks, embeddings, pgvector, and semantic search. I handled this by breaking the workflow into smaller parts and checking each step separately.

* **Designing policy chunks suitable for natural language questions**  
  The policy chunks could not simply copy the original JSON structure. They needed enough semantic context to match realistic user questions about refunds, ticket changes, day passes, bicycles, pets, luggage, and travel rules.

* **Verifying database setup and reseeding behavior**  
  During testing, I needed to confirm whether PostgreSQL and pgvector could be rebuilt reliably. One issue was that existing credential records could affect login testing if they were not updated correctly during reseeding.

* **Determining appropriate schema constraints and delete behavior**  
  When reviewing `schema.sql`, it was not appropriate to apply the same `ON DELETE` rule to every relationship. I needed to consider the business meaning of each relationship and decide whether related records should be restricted, preserved, or removed.

* **Debugging booking cancellation and active booking display**  
  Cancelled bookings needed to remain in the database for history and refund records, but they should not appear as active bookings or continue occupying seats. This required checking both query logic and database constraints.

* **Locating errors across UI, agent, database, and RAG layers**  
  When the UI produced an incorrect answer, the issue could come from several layers, including UI input handling, agent intent detection, PostgreSQL queries, Neo4j queries, RAG retrieval, or mock data. I used the debug panel, pgAdmin, and repeated testing to narrow down the source.

* **Writing the design document based on the actual implementation**  
  While completing the design document, I needed to make sure the content matched the real project instead of adding unsupported descriptions. This required checking the schema, query functions, RAG workflow, Task 6 extension, and testing process carefully.

* **Managing git and version synchronization**  
  Near the end of the project, the team needed to pull, commit, push, and check branch status several times. I helped reduce the risk of testing an old version or missing changes by checking modified files, commit status, push results, and reseeding steps.

---

### A3. Self-rating

| Criterion | Rating (1–5) | Justification (1–2 sentences) |
|-----------|-------------|-------------------------------|
| I delivered the tasks assigned to me in the work allocation | 4 | I completed the policy data work, RAG chunks, `policy_chunks.json`, `seed_vectors.py` and pgvector workflow checking, PostgreSQL testing, UI testing, design document work, and final functional verification. |
| The quality of my work was satisfactory | 4 | I repeatedly checked the data format, RAG retrieval workflow, pgvector insertion, schema design, query functions, login flow, booking cancellation behavior, design document content, and agent responses against the project requirements. |
| I communicated well and kept the team informed | 4 | I reported testing results, modification details, reseeding steps, git status, document progress, and discovered issues so that teammates could understand the current progress. |
| I met deadlines agreed within the team | 4 | I completed my assigned policy, RAG, testing, debugging, documentation, and final verification work according to the team schedule. |
| **Overall self-rating** | 4 | I completed my assigned integration and testing-related work and also helped with schema checking, RAG workflow, login behavior, booking cancellation logic, design document writing, and final requirement verification. |

---

### A4. Estimated contribution percentage

> My estimated contribution: **35%**

---

## Section B — Peer Assessments

### B1. Assessment of Teammate 1

| Field | Your answer |
|-------|------------|
| Teammate's full name | 林昀希 |
| Teammate's student ID | 113403534 |

#### What did this teammate deliver?

> *Your answer:*

* **Mainly responsible for PostgreSQL relational database work**  
  This teammate was mainly responsible for `schema.sql`, PostgreSQL seed scripts, relational query functions, table design, and the data import workflow.

* **Designed and implemented the relational schema**  
  This teammate built the relationships among users, bookings, payments, feedback, stations, schedules, ticket types, and seat layouts. She also handled primary keys, foreign keys, constraints, indexes, and related schema logic.

* **Implemented relational query functions**  
  This teammate implemented or helped implement functions for schedule queries, user booking records, national rail availability, booking creation, payment processing, cancellation, and refund-related logic.

* **Handled PostgreSQL integration and testing**  
  During integration, this teammate helped confirm whether PostgreSQL query results could be correctly called by the agent and displayed through the UI.

* **Merged and integrated team members’ work**  
  This teammate also helped merge different parts completed by team members and handled version synchronization or integration issues when combining PostgreSQL, Neo4j, RAG, agent, and UI work.

#### Did their actual contribution match the agreed work allocation?

> *Your answer:*

Yes. 林昀希 completed the main PostgreSQL-related work in the work allocation, including schema design, seed workflow, and relational query implementation. She also helped merge and integrate different team members’ parts and participated in final testing. Overall, her contribution matched the original division of work and supported the final integration stage.

#### Peer rating for this teammate

| Criterion | Rating (1–5) | Justification (1–2 sentences) |
|-----------|-------------|-------------------------------|
| Delivered the tasks assigned in the work allocation | 4 | She completed the assigned PostgreSQL-related implementation work and also helped merge team members’ work. |
| Quality of their work was satisfactory | 4 | Her implementation supported the relational database, booking workflow, payment records, cancellation logic, and final integration. |
| Communicated well and kept the team informed | 4 | She communicated with the team when schema, query, merge, or integration issues needed discussion. |
| Met deadlines agreed within the team | 4 | She generally completed her assigned PostgreSQL and integration work according to the team schedule. |
| **Overall rating for this teammate** | 4 | She made a clear contribution to the relational database part and helped with final merge and integration. |

#### Estimated contribution percentage for this teammate

> My estimate of their contribution: **35%**

---

### B2. Assessment of Teammate 2

| Field | Your answer |
|-------|------------|
| Teammate's full name | 李盈萱 |
| Teammate's student ID | 113403504 |

#### What did this teammate deliver?

> *Your answer:*

* **Mainly responsible for Neo4j graph database and route-related work**  
  This teammate was mainly responsible for the Neo4j graph model, graph seed scripts, station nodes, route relationships, interchange stations, and shortest path / route query logic.

* **Created graph nodes and relationships**  
  This teammate organized metro stations, national rail stations, interchange stations, and adjacent station relationships into a graph database structure to support route search and transfer analysis.

* **Implemented graph query functions**  
  This teammate implemented or helped implement route search, shortest path, station adjacency, and metro / national rail interchange query functions.

* **Completed Task 6 optional extension**  
  This teammate completed the Task 6 extension, including the seat occupancy query, trip history UI, Seat Capacity tab, My Bookings tab, and related integration testing.

* **Assisted with agent and UI integration testing**  
  This teammate helped confirm whether the agent could correctly call graph query tools and Task 6 seat occupancy functions, and whether the results could be shown clearly through the UI.

#### Did their actual contribution match the agreed work allocation?

> *Your answer:*

Yes. 李盈萱 completed the main Neo4j and route query-related work in the work allocation. She also completed the Task 6 optional extension, including seat occupancy lookup, trip history UI, Seat Capacity tab, My Bookings tab, and related integration testing. Overall, her contribution matched the original division of work and supported the final project extension.

#### Peer rating for this teammate

| Criterion | Rating (1–5) | Justification (1–2 sentences) |
|-----------|-------------|-------------------------------|
| Delivered the tasks assigned in the work allocation | 4 | She completed the assigned Neo4j route query work and the Task 6 optional extension, including seat occupancy and trip history UI features. |
| Quality of their work was satisfactory | 4 | Her work supported route search, seat capacity lookup, user booking display, and final UI integration after testing. |
| Communicated well and kept the team informed | 4 | She communicated with the team when graph query, Task 6, UI extension, or integration issues needed confirmation. |
| Met deadlines agreed within the team | 4 | She completed the assigned graph database work and Task 6 extension within the project schedule. |
| **Overall rating for this teammate** | 4 | She made a clear contribution to the graph database part and the optional Task 6 extension. |

#### Estimated contribution percentage for this teammate

> My estimate of their contribution: **30%**

---

## Section C — Contribution Percentage Summary

| Member | Your estimated % | Notes |
|--------|------------------|-------|
| 陳思宇 | 35% | Responsible for policy data, RAG chunks, pgvector / `seed_vectors.py` workflow verification, PostgreSQL testing, UI integration testing, debug verification, design document writing, and requirement compliance checking. |
| 林昀希 | 35% | Mainly responsible for PostgreSQL schema, seed scripts, relational queries, merge support, and relational database integration. |
| 李盈萱 | 30% | Mainly responsible for Neo4j graph database, route / shortest path queries, interchange relationships, Task 6 optional extension, and UI extension testing. |
| **Total** | **100%** | The contribution percentages were estimated based on each member’s actual completed work. |

---

## Section D — Overall Team Reflection

### D1. What went well in the team's collaboration?

> *Your answer:*

The team divided the TransitFlow project into clear work areas, including PostgreSQL relational database, Neo4j graph database, RAG policy data, UI testing, Task 6 extension, and final documentation. Each member completed their assigned area and helped with integration or testing when needed. Overall, the workload was balanced among the three members, and the team checked the main functions together before final submission.

---

### D2. What would you do differently if you did this project again?

> *Your answer:*

If we had more time, I would start integration testing earlier and keep more detailed testing notes during development. Although the main functions were completed successfully, testing more natural language questions, booking cases, route queries, cancellation cases, and policy-related questions could make the system more reliable. I would also organize the final documentation earlier so that the final checking process would be smoother.

---

### D3. Is there anything else the markers should know about team dynamics or individual contributions?

> *Your answer:*

Nothing to add.

---

## Declaration

I confirm that this peer review reflects my honest and independent assessment.  
I understand it will be kept confidential from my teammates.

**Signed:** 陳思宇 **Date:** 2026/06/12
