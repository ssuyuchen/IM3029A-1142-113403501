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

- **Reviewed and verified the JSON mock data**  
  I reviewed the JSON data provided in the project and checked the fields and relationships related to users, stations, schedules, bookings, payments, feedback, and policy data. This provided the foundation for later database design and testing.

- **Organized policy-related data**  
  I analyzed `refund_policy.json`, `booking_rules.json`, `travel_policies.json`, and `ticket_types.json` to understand how these files correspond to refund rules, booking rules, ticket types, luggage policies, bicycle policies, pet policies, and travel regulations.

- **Added and adjusted policy JSON content**  
  I helped supplement the policy content so that the system could answer more realistic user scenarios, such as differences between metro and national rail rules for refunds, ticket changes, day passes, bicycles, pets, and luggage.

- **Designed the policy chunk strategy**  
  I planned how the policy documents should be divided into chunks suitable for RAG retrieval, including chunk scope, naming rules, and metadata. This helped the system retrieve the correct rules when users asked questions in natural language.

- **Created and modified `policy_chunks.json`**  
  I helped convert the policy JSON data into `policy_chunks.json`, which could be imported into pgvector, and checked whether each chunk had clear content and useful metadata for retrieval.

- **Verified the `seed_vectors.py` workflow**  
  I checked how `seed_vectors.py` reads policy chunks, generates embeddings, and writes the data into pgvector to ensure that policy data could enter the RAG workflow correctly.

- **Verified that the embedding model worked properly**  
  I helped confirm that `nomic-embed-text` was correctly pulled and could be used to vectorize the policy chunks.

- **Verified that pgvector insertion worked properly**  
  I helped check whether policy chunks were successfully converted into embeddings and inserted into pgvector, so that later policy search could retrieve the correct data.

- **Assisted with PostgreSQL testing and pgAdmin verification**  
  I used pgAdmin to help inspect tables, imported data, and query results, confirming that the PostgreSQL part could support bookings, payments, schedules, and user records.

- **Assisted in reviewing `schema.sql`**  
  I helped check whether the schema met the project requirements, including primary keys, foreign keys, constraints, and whether each foreign key had an appropriate `ON DELETE` behavior.

- **Assisted in reviewing `queries.py` / relational queries**  
  I helped check whether the relational query functions met the task requirements, such as querying schedules, retrieving user booking records, creating bookings, processing payments, cancellations, and refunds.

- **Assisted in verifying Task 4 query functions**  
  I helped test Task 4 related queries and checked whether the relational database query results and agent tool outputs matched the mock data and user questions.

- **Assisted with end-to-end integration testing**  
  I tested whether the system could correctly call PostgreSQL, Neo4j, or RAG policy search through the agent after a user entered a question in the UI, and whether the final answer was reasonable.

- **Assisted in checking `UI.py` and reporting issues**  
  During UI testing, I helped check whether user questions triggered the correct workflow and reported issues that might come from the UI, agent, database queries, or RAG retrieval.

- **Used the debug panel to verify the agent workflow**  
  I used the debug panel to inspect the tools called by the agent, the raw database results, and the final answer, which helped identify integration problems.

- **Assisted in checking overall requirement compliance**  
  In the later stage, I helped compare the implementation against the project requirements to confirm that the schema, queries, agent, policy chunks, seed vectors, UI testing, and related functions did not have obvious omissions.

- **Jointly completed git sync and reseed verification**  
  In the final stage, the team jointly checked git synchronization, database reseeding results, and whether PostgreSQL, Neo4j, and pgvector could be rebuilt correctly.

- **Jointly completed demo rehearsal**  
  Before the demo, the team jointly confirmed the presentation flow and tested whether each database, query, agent, RAG, and UI function could be demonstrated smoothly.

---

### A2. What challenges did you face?

> *Your answer:*

- **Understanding the relationship between RAG, embeddings, pgvector, and policy JSON**  
  At first, I needed time to clarify the data flow among the original policy JSON files, policy chunks, the embedding model, pgvector, and semantic search. I resolved this by organizing the workflow: policy JSON is converted into chunks, embeddings are generated, the vectors are inserted into pgvector, and the agent later uses them for policy retrieval.

- **Designing policy chunks suitable for natural language queries**  
  Policy chunks could not simply follow the original JSON structure. They also needed to consider how users would ask questions in real scenarios. Therefore, I paid special attention to common topics such as refunds, ticket changes, ticket types, bicycles, pets, luggage, and day passes to improve retrieval accuracy.

- **Verifying pgvector insertion and the embedding model**  
  While working with `seed_vectors.py`, I needed to confirm whether `nomic-embed-text` had been pulled correctly, whether embeddings could be generated, and whether the data was inserted into pgvector successfully. I verified this by rerunning the seed process and checking the database content.

- **Determining appropriate `ON DELETE` behavior for foreign keys in the schema**  
  When reviewing `schema.sql`, it was not appropriate to apply the same delete rule to every foreign key. The behavior needed to match the business logic of users, bookings, payments, feedback, stations, and schedules. I checked the foreign keys one by one and evaluated them according to their relationships.

- **Locating errors during end-to-end testing**  
  When the UI produced an incorrect answer, the issue could come from the UI, agent intent detection, database query, RAG retrieval, or the underlying data. I used the debug panel to inspect tool calls, raw database results, and the final answer to locate problems step by step.

- **Managing git and version synchronization**  
  In the later stage of the project, the team needed to pull, commit, push, and check branch status multiple times. I reduced the risk of missing changes or overwriting teammates' work by checking modified files, commit status, and push results carefully.

---

### A3. Self-rating

| Criterion | Rating (1–5) | Justification (1–2 sentences) |
|-----------|-------------|-------------------------------|
| I delivered the tasks assigned to me in the work allocation | 4 | I completed the policy JSON work, policy chunk strategy, `policy_chunks.json`, `seed_vectors.py` workflow verification, pgvector insertion verification, PostgreSQL testing, UI integration testing, and demo preparation tasks. |
| The quality of my work was satisfactory | 4 | I repeatedly checked the data format, RAG retrieval workflow, pgvector insertion results, schema design, query functions, and agent responses against the project requirements. |
| I communicated well and kept the team informed | 4 | I organized and reported modification details, testing results, commit / push status, and discovered issues so that teammates could understand the current progress and items requiring confirmation. |
| I met deadlines agreed within the team | 4 | I completed policy organization, RAG preparation, database testing, integration testing, and demo preparation according to the team schedule, and cooperated with the final synchronization and checking process. |
| **Overall self-rating** | 4 | I completed my assigned integration and testing-related work and also helped check the schema, queries, agent, RAG workflow, and requirement compliance. |

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

If we had more time, I would expand the testing coverage and try more user scenarios before the final submission. Although the main functions were completed successfully, testing more natural language questions, booking cases, route queries, and policy-related questions could make the system even more reliable. I would also keep more detailed testing notes so that the final verification process would be easier to review.中文

---

### D3. Is there anything else the markers should know about team dynamics or individual contributions?

> *Your answer (or "Nothing to add"):*

Nothing to add.

---

## Declaration

I confirm that this peer review reflects my honest and independent assessment.  
I understand it will be kept confidential from my teammates.

**Signed:** 陳思宇 **Date:** 2026/06/11
