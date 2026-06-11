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

* **Reviewed and verified the JSON mock data**  
  I reviewed the JSON mock data used in the project, including users, stations, schedules, bookings, payments, feedback, refund policies, booking rules, travel policies, and ticket types. This helped ensure that the later database design, seed workflow, policy retrieval, and UI testing were based on consistent data.

* **Organized and supplemented policy-related data**  
  I analyzed `refund_policy.json`, `booking_rules.json`, `travel_policies.json`, and `ticket_types.json` to understand how the policies corresponded to realistic user questions. I also helped supplement policy content related to refunds, booking rules, ticket changes, day passes, bicycles, pets, luggage, and other travel regulations.

* **Designed the policy chunk strategy for RAG retrieval**  
  I planned how the policy documents should be divided into retrieval-friendly chunks, including chunk scope, naming rules, metadata, and content structure. The goal was to make the RAG system retrieve the most relevant policy rule when users asked natural language questions.

* **Created and modified `policy_chunks.json`**  
  I helped convert the original policy JSON data into `policy_chunks.json`, which could be imported into pgvector. I checked whether each chunk had clear content, appropriate metadata, and enough semantic context for retrieval.

* **Verified the `seed_vectors.py` and pgvector workflow**  
  I checked how `seed_vectors.py` reads policy chunks, generates embeddings, and writes them into the `policy_documents` table. I also helped confirm that the `nomic-embed-text` embedding model was available and that the policy chunks could be inserted into pgvector correctly.

* **Assisted with PostgreSQL testing and pgAdmin verification**  
  I used pgAdmin to inspect tables, imported data, query results, and relational records. This included checking whether PostgreSQL supported users, bookings, payments, schedules, feedback, policy documents, and related database operations correctly.

* **Assisted in reviewing `schema.sql`**  
  I helped review whether the schema met the project requirements, including primary keys, foreign keys, constraints, indexes, and `ON DELETE` behavior. I also checked whether the delete behavior matched the business logic of users, bookings, payments, feedback, stations, schedules, and related records.

* **Assisted in reviewing and testing `queries.py` relational functions**  
  I helped check whether the relational query functions supported the required tasks, including schedule queries, national rail availability, user booking retrieval, booking creation, payment records, cancellation handling, and refund-related logic.

* **Assisted in debugging login authentication issues**  
  I helped identify and verify login-related problems by checking whether the UI correctly passed user input to the authentication function and whether PostgreSQL user credential data matched the expected login workflow. I also helped confirm the need to handle password input consistently during login testing.

* **Assisted in improving PostgreSQL reseeding behavior for user credentials**  
  I helped check the PostgreSQL seed workflow and identified that existing user credential records should be updated during reseeding when password hashes need to match the mock user data. This improved the reliability of repeated database setup and login testing.

* **Assisted in improving booking display logic**  
  I helped test the `show my booking` workflow and identified that cancelled national rail bookings should not appear in the active booking list. I assisted in adjusting the query logic so that bookings with `cancelled` status are excluded from normal booking display results.

* **Assisted in testing booking cancellation and seat availability behavior**  
  I tested the booking cancellation flow and checked whether cancelled bookings were correctly treated as no longer occupying seats. This helped identify the difference between application-level booking status logic and database-level seat uniqueness constraints.

* **Assisted with end-to-end integration testing**  
  I tested whether the system could correctly call PostgreSQL, Neo4j, or RAG policy search through the agent after a user entered a question in the UI. I also checked whether the final natural language answers were reasonable and consistent with the database results.

* **Used the debug panel to verify the agent workflow**  
  I used the debug panel to inspect the tools called by the agent, the raw database results, and the final answer. This helped locate whether an issue came from the UI, agent intent detection, database query, RAG retrieval, or the underlying data.

* **Assisted in final functional verification after code changes**  
  After modifying login, booking display, and cancellation-related logic, I helped verify the expected user flow: login, create booking, show booking, cancel booking, and confirm that cancelled bookings no longer appeared in active booking results.

* **Assisted in checking overall requirement compliance**  
  In the later stage, I helped compare the implementation against the project requirements to confirm that the schema, queries, agent, policy chunks, seed vectors, UI testing, and related functions did not have obvious omissions.

* **Jointly completed git synchronization, reseed verification, and demo rehearsal**  
  In the final stage, the team jointly checked git synchronization, database reseeding results, PostgreSQL, Neo4j, pgvector rebuild workflows, and demo flow. I also helped confirm that the main database, query, agent, RAG, and UI functions could be demonstrated smoothly.

---

### A2. What challenges did you face?

> *Your answer:*

* **Understanding the full RAG and pgvector workflow**  
  At first, I needed time to clarify the relationship among policy JSON files, policy chunks, embeddings, pgvector, and semantic search. I resolved this by organizing the workflow step by step: policy JSON is converted into chunks, embeddings are generated, vectors are inserted into pgvector, and the agent later uses semantic search to retrieve relevant policy rules.

* **Designing policy chunks suitable for natural language questions**  
  The policy chunks could not simply copy the original JSON structure. They also needed to match how users would ask questions in realistic situations. Therefore, I focused on common user topics such as refunds, ticket changes, ticket types, bicycles, pets, luggage, and day passes to improve retrieval accuracy.

* **Verifying database setup and repeated seeding behavior**  
  During testing, I needed to confirm whether PostgreSQL, pgvector, and the seed scripts could be rerun reliably. One challenge was identifying when reseeding did not overwrite existing credential records, which could cause login testing to fail even when the mock JSON account information was correct.

* **Determining appropriate schema constraints and delete behavior**  
  When reviewing `schema.sql`, it was not appropriate to apply the same rule to every foreign key or constraint. I needed to check the business meaning of each relationship and consider whether records such as bookings, payments, feedback, schedules, and users should be restricted, preserved, or removed under different conditions.

* **Debugging booking cancellation and active booking display**  
  During end-to-end testing, I found that cancelled bookings could still affect later testing if the query logic or database constraint did not match the intended business rule. I had to distinguish between keeping cancelled booking records for history and excluding them from active booking display or seat occupancy logic.

* **Locating errors across UI, agent, database, and RAG layers**  
  When the UI produced an incorrect result, the source of the issue could be the UI input handling, agent intent detection, PostgreSQL query, Neo4j route query, RAG retrieval, or the mock data itself. I used the debug panel and database inspection to narrow down the source of problems step by step.

* **Managing git and version synchronization**  
  In the later stage of the project, the team needed to pull, commit, push, and check branch status multiple times. I reduced the risk of missing changes or overwriting teammates' work by checking modified files, commit status, and push results carefully.

---

### A3. Self-rating

| Criterion | Rating (1–5) | Justification (1–2 sentences) |
|-----------|-------------|-------------------------------|
| I delivered the tasks assigned to me in the work allocation | 4 | I completed the policy JSON work, policy chunk strategy, `policy_chunks.json`, `seed_vectors.py` workflow verification, pgvector insertion verification, PostgreSQL testing, UI integration testing, and final functional verification tasks. |
| The quality of my work was satisfactory | 4 | I repeatedly checked the data format, RAG retrieval workflow, pgvector insertion results, schema design, query functions, login flow, booking cancellation behavior, and agent responses against the project requirements. |
| I communicated well and kept the team informed | 4 | I organized and reported modification details, testing results, commit / push status, and discovered issues so that teammates could understand the current progress and items requiring confirmation. |
| I met deadlines agreed within the team | 4 | I completed policy organization, RAG preparation, database testing, integration testing, debugging, and demo preparation according to the team schedule, and cooperated with the final synchronization and checking process. |
| **Overall self-rating** | 4 | I completed my assigned integration and testing-related work and also helped check the schema, queries, agent, RAG workflow, login behavior, booking cancellation logic, and requirement compliance. |

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

- **Mainly responsible for PostgreSQL relational database work**  
  This teammate was mainly responsible for or participated in `schema.sql`, PostgreSQL seed scripts, relational query functions, table design, and the data import workflow.

- **Designed the relational schema**  
  This teammate built the relationships among users, bookings, payments, feedback, stations, schedules, ticket types, and seat layouts, and handled primary keys, foreign keys, constraints, and indexes.

- **Implemented relational query functions**  
  This teammate implemented or helped implement functions for querying schedules, retrieving user booking records, checking national rail availability, creating bookings, processing payments, cancellations, and refunds.

- **Assisted with database integration and testing**  
  During integration, this teammate helped confirm whether PostgreSQL query results could be correctly called and used by the agent.

#### Did their actual contribution match the agreed work allocation?

> *Your answer (Yes / Mostly / Partially / No — with explanation):*

Yes. 林昀希 completed the main PostgreSQL-related work in the work allocation, including the schema, seed workflow, and relational query implementation. They also participated in later integration and revision. Overall, their contribution matched the original division of work.

#### Peer rating for this teammate

| Criterion | Rating (1–5) | Justification (1–2 sentences) |
|-----------|-------------|-------------------------------|
| Delivered the tasks assigned in the work allocation | 4 | They completed the assigned PostgreSQL-related implementation work according to the team’s original division of tasks. |
| Quality of their work was satisfactory | 4 | Their implementation generally supported the final database and agent workflow, and it could be integrated properly after review and testing. |
| Communicated well and kept the team informed | 4 | They communicated with the team when schema, query, or integration issues needed discussion. |
| Met deadlines agreed within the team | 4 | They generally completed their assigned work according to the team schedule. |
| **Overall rating for this teammate** | 4 | They made a clear and important contribution to the relational database part of the project. |

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

- **Mainly responsible for Neo4j graph database and route-related work**  
  This teammate was mainly responsible for or participated in the Neo4j graph model, graph seed scripts, station nodes, route relationships, and shortest path / route query logic.

- **Created graph nodes and relationships**  
  This teammate organized metro stations, national rail stations, interchange stations, and adjacent station relationships into a graph database structure to support route search and transfer analysis.

- **Implemented graph query functions**  
  This teammate implemented or helped implement route search, shortest path, station adjacency, and metro / national rail interchange query functions.

- **Assisted with agent integration and testing**  
  This teammate helped confirm whether the agent could correctly call graph query tools and convert Neo4j query results into route answers that users could understand.

#### Did their actual contribution match the agreed work allocation?

> *Your answer (Yes / Mostly / Partially / No — with explanation):*

Yes. 李盈萱 completed the main Neo4j and route query-related work in the work allocation, and also participated in system integration and testing. Overall, their contribution matched the original division of work.

#### Peer rating for this teammate

| Criterion | Rating (1–5) | Justification (1–2 sentences) |
|-----------|-------------|-------------------------------|
| Delivered the tasks assigned in the work allocation | 4 | They completed the assigned graph database and route query-related work. |
| Quality of their work was satisfactory | 4 | Their implementation supported route search and shortest path functions, and it could be integrated into the final system after testing. |
| Communicated well and kept the team informed | 4 | They communicated with the team when graph query or integration issues needed confirmation. |
| Met deadlines agreed within the team | 4 | They generally completed their assigned work according to the team schedule. |
| **Overall rating for this teammate** | 4 | They made a clear and important contribution to the graph database and route search part of the project. |

#### Estimated contribution percentage for this teammate

> My estimate of their contribution: **33.333333%**

---

## Section C — Contribution Percentage Summary

| Member | Your estimated % | Notes |
|--------|----------------|-------|
| 陳思宇 | 33.333333% | Responsible for policy data, RAG chunks, pgvector / `seed_vectors.py` workflow verification, PostgreSQL testing, UI integration testing, debug verification, and requirement compliance checking. The workload was evenly divided among the three members. |
| 林昀希 | 33.333333% | Mainly responsible for PostgreSQL schema, seed scripts, relational queries, and relational database-related functions. The workload was evenly divided among the three members. |
| 李盈萱 | 33.333333% | Mainly responsible for Neo4j graph database, route / shortest path queries, interchange relationships, and graph integration. The workload was evenly divided among the three members. |
| **Total** | **100%** | The three members contributed equally. |

---

## Section D — Overall Team Reflection

### D1. What went well in the team's collaboration?

> *Your answer (2–4 sentences):*

The team divided the TransitFlow project into clear work areas, including the PostgreSQL relational database, Neo4j graph database, RAG policy data, AI agent integration, and UI testing. Each member completed their own assigned area and assisted with integration and testing when needed. Overall, the workload was balanced among the three members, and the team checked the main functions together before the final submission.

---

### D2. What would you do differently if you did this project again?

> *Your answer (2–4 sentences):*

If we had more time, I would expand the testing coverage and try more user scenarios before the final submission. Although the main functions were completed successfully, testing more natural language questions, booking cases, route queries, and policy-related questions could make the system even more reliable. I would also keep more detailed testing notes so that the final verification process would be easier to review.

---

### D3. Is there anything else the markers should know about team dynamics or individual contributions?

> *Your answer (or "Nothing to add"):*

Nothing to add.

---

## Declaration

I confirm that this peer review reflects my honest and independent assessment.  
I understand it will be kept confidential from my teammates.

**Signed:** 陳思宇 **Date:** 2026/06/11
