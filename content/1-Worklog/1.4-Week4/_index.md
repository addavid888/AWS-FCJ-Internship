---
title: "Week 4 Worklog"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

# Week 4 Agenda: Core Storage Services and Concepts

## Week 4 Objectives

- Understand how **Amazon S3** works as a global-scale object storage service.
- Learn how to manage access to S3 using **Access Points**, **Bucket Policies**, **IAM**, and **CORS**.
- Explore **S3 Storage Classes**, including lifecycle transitions and cost optimization.
- Practice setting up **S3 Static Websites**, configuring CORS, and tuning for performance with **object key design**.
- Learn how to archive and retrieve long-term data using **S3 Glacier** and its retrieval tiers.
- Understand hybrid storage solutions: **Snow Family** for data transfer appliances and **Storage Gateway** for on-premise integration.
- Gain basic familiarity with AWS **Backup** for centralized, automated backup management across services.

---

## Tasks to be carried out this week

| Day | Task                                                                                                                                                                                                                                            | On-site? | Date       |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ---------- |
| 1   | - Introduction to **Amazon S3** fundamentals <br> - Understand objects, buckets, regions, data consistency <br>- Study **S3 Access Points**, bucket policies, and access control models                                                         |          | 09/29/2025 |
| 2   | - Learn **S3 Storage Classes** (Standard, IA, One Zone, Intelligent Tiering, Glacier tiers) <br> - Explore lifecycle rules and cost-optimized storage planning                                                                                  | ✅       | 09/30/2025 |
| 3   | - Set up an **S3 Static Website** <br> - Configure **CORS** for web applications <br> - Understand public access settings and security considerations                                                                                           |          | 10/01/2025 |
| 4   | - Learn **S3 object key naming strategies** and how they affect performance <br> - Explore **multipart upload**, versioning, and replication options                                                                                            |          | 10/02/2025 |
| 5   | - Dive into **S3 Glacier** and retrieval tiers <br> - Practice creating vaults, uploading archives, and requesting restores                                                                                                                     |          | 10/03/2025 |
| 6   | - Explore hybrid and edge storage: **Snow Family** devices for large-scale data transfer <br> - Learn **AWS Storage Gateway** use cases (File/Volume/Tape Gateway) <br> - Introduction to **AWS Backup** for multi-service backup orchestration |          | 10/04/2025 |

---

## Week 4 Achievements

- **Understood S3 Object Storage Architecture**:

  - Learned how buckets and objects are globally accessible via unique URLs.
  - Understood S3’s strong read-after-write consistency and distributed design.
  - Explored Access Points for simplified and controlled data access at scale.

- **Gained Insight into S3 Storage Classes**:

  - Compared the cost, durability, and retrieval times across classes (Standard, IA, One Zone, Intelligent Tiering, Glacier family).
  - Designed lifecycle rules for automatic transitions and deletion.
  - Understood scenarios for using archival storage.

- **Configured S3 Static Hosting and CORS**:

  - Set up website indexing, error pages, and public access settings.
  - Configured CORS for cross-origin requests from web applications.
  - Understood the security risks of misconfigured public access.

- **Learned about Key Naming, Performance, and Data Management**:

  - Studied S3’s request parallelism and the effect of key distribution.
  - Practiced multipart uploads for large files.
  - Configured object versioning and replication (CRR/SRR).

- **Explored Glacier and Long-Term Archival**:

  - Created archives and retrieval requests across different retrieval tiers.
  - Understood the use cases for cold, infrequent, and deep archive storage.

- **Understood Hybrid Storage Services**:

  - Learned about **Snowcone, Snowball, Snowmobile** and their roles in bulk data transfer.
  - Explored **Storage Gateway** for bridging on-prem systems with cloud storage using file, volume, or tape interfaces.
  - Gained basic knowledge of **AWS Backup** for automated policy-based backups across AWS services.

- Developed a solid understanding of **how object, archival, and hybrid storage fit together** in AWS, creating the foundation for scalable, cost-efficient, and secure data management.
