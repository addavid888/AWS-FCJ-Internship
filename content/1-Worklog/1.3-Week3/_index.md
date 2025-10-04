---
title: "Week 3 Worklog"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives

- Understand how **Amazon EC2** instances operate within AWS infrastructure.
- Learn how to configure and launch EC2 instances using **AMI**, **Instance Types**, and **Key Pairs**.
- Explore the relationship between **EC2**, **EBS volumes**, and **Instance Store**.
- Practice **snapshot creation**, **volume attachment**, and **backup strategies**.
- Learn how to automate EC2 setup using **User Data** and retrieve **Metadata** for instance configuration.
- Gain basic knowledge of **EFS** and **FSx** for scalable and shared file storage.

---

### Tasks to be carried out this week

| Day | Task                                                                                                                                                                                                                                                     | On-site? | Date       |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ---------- |
| 1   | - Introduction to **Amazon EC2** <br> - Understand how virtualization works: **Hardware Node**, **Hypervisor**, and **EC2 Instance** layers <br> - Explore **Instance Types** and their effects on CPU, Memory, and Network performance                  |          | 09/22/2025 |
| 2   | - Learn about **AMI (Amazon Machine Image)**: how to select and launch EC2 instances <br> - Understand **root volume mapping** and custom AMI creation <br> - Study EC2 **pricing models** (On-demand, Reserved, Spot, Savings Plan)                     | ✅       | 09/23/2025 |
| 3   | - Study **Instance Store**: NVMe-based high-performance ephemeral storage <br> - Compare with **EBS Volumes** and discuss persistence, durability, and replication <br> - Practice launching instances with Instance Store and EBS                       |          | 09/24/2025 |
| 4   | - Learn **EBS (Elastic Block Store)** architecture and how it connects to EC2 via EBS Network <br> - Explore **EBS Volume types** (SSD, HDD) and durability (99.999%) <br> - Perform EBS **snapshot** and **restore** operations                         |          | 09/25/2025 |
| 5   | - Understand **User Data** and **Metadata** <br> - Write simple user-data scripts for automatic package installation and setup <br> - Retrieve EC2 metadata (IP, hostname, security groups) using `http://169.254.169.254/latest/meta-data/`             |          | 09/26/2025 |
| 6   | - Explore advanced storage services: **EFS (Elastic File System)** and **FSx** <br> - Learn use cases for **shared file access** and **high-performance workloads** <br> - Introduction to **AWS Application Migration Service** for VM migration to AWS |          | 09/27/2025 |

---

### Week 3 Achievements

- **Understood the EC2 architecture**:

  - EC2 instances run on a **hypervisor layer** (Nitro/KVM) atop physical hardware nodes.
  - Each instance uses an **AMI template** to define its OS and configuration.
  - Gained insight into how instance types define compute, memory, and networking capacity:contentReference[oaicite:1]{index=1}.

- **Learned about Instance Store vs EBS**:

  - Instance Store provides **temporary, ultra-fast NVMe storage** tied to the hardware node.
  - EBS provides **persistent block storage** replicated across storage nodes within an AZ for reliability.
  - Understood use cases: instance store for high IOPS workloads, EBS for durability:contentReference[oaicite:2]{index=2}.

- **Explored EBS architecture and operations**:

  - Studied how EBS connects via a **dedicated EBS Network** within an Availability Zone.
  - Learned about **EBS volume types** (SSD, HDD), **EBS-optimized instances**, and **multi-attach** support.
  - Practiced creating, attaching, detaching, and taking **snapshots** for backup.

- **Configured EC2 instances and Key Pairs**:

  - Generated SSH key pairs for secure access.
  - Connected to EC2 via public subnet using SSH.
  - Understood key pair encryption and its link to private/public subnets.

- **Used User Data and Metadata for automation**:

  - Wrote bash scripts for boot-time installation of packages and environment setup.
  - Accessed metadata endpoints to retrieve configuration data (IP, hostname, SGs).
  - Learned to automate EC2 provisioning without manual SSH setup.

- **Gained familiarity with higher-level storage services**:

  - Overviewed **EFS** for shared POSIX file systems across instances.
  - Learned about **FSx** for Windows-based or high-performance workloads.
  - Explored **Application Migration Service** as a tool for moving workloads to AWS.

- Developed a clear understanding of **how compute and storage layers interact** inside an AWS Availability Zone, and how these form the foundation for higher-level services.
