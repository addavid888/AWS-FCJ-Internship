---
title: "Week 6 Worklog"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

## Week 6 Objectives

- Understand **core database concepts**: tables, schemas, primary keys, foreign keys, indexes, partitioning, query execution plans, database logs, and buffer/cache behavior.
- Learn the differences between **relational** and **non-relational** databases, and where each fits.
- Distinguish between **OLTP** and **OLAP** workloads and how design choices impact performance.
- Explore AWS database services: **Amazon RDS**, **Amazon Aurora**, **Amazon ElastiCache**, and **Amazon Redshift**, including their ideal use cases and architectural differences.

---

## Tasks to be carried out this week

| Day | Task                                                                                                                                                                                                                                                                                                          | On-site? | Date       |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ---------- |
| 1   | - Study **database fundamentals** <br> - Understand tables, rows, and schema design <br> - Learn **primary key** vs **foreign key** and why normalization exists                                                                                                                                              |          | 10/13/2025 |
| 2   | - Explore **indexes**, how they work, and why they speed up queries <br> - Study **partitioning**, query planners, and **execution plans** <br> - Learn about transaction logs, WAL, and buffer/cache behavior                                                                                                |          | 10/14/2025 |
| 3   | - Compare **relational** vs **non-relational** databases <br> - Understand CAP considerations and consistency trade-offs <br> - Learn where document, key-value, graph, and wide-column stores fit                                                                                                            |          | 10/15/2025 |
| 4   | - Study **OLTP** (transactional) vs **OLAP** (analytical) systems <br> - Understand how data modeling differs for each <br> - Learn why analytical systems require columnar storage                                                                                                                           |          | 10/16/2025 |
| 5   | - Introduction to **Amazon RDS** and managed relational engines <br> - Explore snapshots, Multi-AZ, backups, storage autoscaling                                                                                                                                                                              |          | 10/17/2025 |
| 6   | - Deep dive into **Amazon Aurora**, its distributed storage layer <br> - Learn high-performance read scaling and failover design - Explore **Amazon ElastiCache** (Redis/Memcached) for caching, sessions, and low-latency workloads <br> - Study **Amazon Redshift** for OLAP and analytics queries at scale |          | 10/18/2025 |

---

## Week 6 Achievements

- **Mastered foundational database concepts**:

  - Understood how primary/foreign keys enforce relationships.
  - Learned how indexes affect performance and why poorly designed ones make databases cry.
  - Analyzed query execution plans and saw how optimizers decide access paths.
  - Understood logs, WAL, and buffer management as part of durability and performance.

- **Differentiated database types and use cases**:

  - Evaluated relational models for strong consistency and structured data.
  - Explored non-relational models for flexible schemas and distributed scaling.
  - Understood when to choose OLTP vs OLAP systems and why mixing them is usually a disaster.

- **Learned AWS managed database offerings**:

  - Used **Amazon RDS** for simplified relational engine management with backups and Multi-AZ.
  - Understood why **Aurora** achieves higher throughput using a shared storage layer.
  - Explored **ElastiCache** as an in-memory system for acceleration and state management.
  - Used **Amazon Redshift** as a columnar OLAP warehouse designed for complex analytical queries.
