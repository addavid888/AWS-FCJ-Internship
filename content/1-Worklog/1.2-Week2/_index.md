---
title: "Week 2 Worklog"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2 Objectives:

- Deepen understanding of AWS **networking fundamentals** (VPC, Subnets, Route Tables, IGW).
- Learn how to design and configure a **custom VPC** with both public and private subnets.
- Practice managing connectivity: set up **route entries**, attach an **Internet Gateway**, and associate **Elastic IPs**.
- Explore **Elastic Network Interfaces (ENI)** and **VPC Endpoints** to connect securely to AWS services.
- Strengthen skills in combining **AWS Management Console** and **AWS CLI** for parallel resource management.

### Tasks to be carried out this week:

| Day | Task                                                                                                                                                                                                  | On-site? | Date       |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ---------- |
| 1   | - Review internship rules & AWS account setup basics <br> - Learn about **AWS global infrastructure** (Regions, Availability Zones, Edge Locations)                                                   | ✅       | 09/15/2025 |
| 2   | - Introduction to **Amazon VPC** and why networking is essential in AWS <br> - Understand CIDR blocks and IPv4 vs IPv6 <br> - Create a simple VPC with a default subnet                               |          | 09/16/2025 |
| 3   | - Learn about **Subnets** (Public vs Private) <br> - Reserved IPs in subnets <br> - Practice creating multiple subnets in different Availability Zones                                                |          | 09/17/2025 |
| 4   | - Study **Route Tables**: default vs custom <br> - Configure routes for intra-VPC communication <br> - Add route entry to allow internet access (0.0.0.0/0 → IGW)                                     |          | 09/18/2025 |
| 5   | - Learn about **Internet Gateway (IGW)** and how it connects VPCs to the internet <br> - Explore **Elastic IPs (EIP)** and billing considerations <br> - Practice attaching an EIP to an EC2 instance |          | 09/19/2025 |
| 6   | - Understand **Elastic Network Interfaces (ENI)** and their portability <br> - Learn about **VPC Endpoints** (Interface vs Gateway) <br> - Explore real-world use cases for private vs public traffic |          | 09/20/2025 |

### Week 2 Achievements

- Understood AWS Networking Services and their role in cloud infrastructure:

  - Amazon VPC (Virtual Private Cloud)
  - Subnets (Public & Private)
  - Route Tables
  - Internet Gateway (IGW)
  - Elastic Network Interface (ENI)
  - Elastic IP (EIP)
  - VPC Endpoints (Interface & Gateway)

- Learned how to create and configure a VPC:

  - Defined CIDR ranges (`10.10.0.0/16` as VPC, `10.10.x.0/24` as subnets).
  - Distinguished between _public subnets_ (with IGW routes) and _private subnets_.
  - Understood subnet IP reservation (network, broadcast, router, DNS, future use).

- Practiced working with Route Tables:

  - Identified the default route table and its role in intra-VPC communication.
  - Created and modified custom route tables.
  - Added route entries (e.g., `0.0.0.0/0 → IGW`) to allow public subnet internet access.

- Explored Elastic Network Interface (ENI) and Elastic IP (EIP):

  - Understood that ENI can be moved across EC2 instances while retaining IP and MAC.
  - Associated static Elastic IP with ENI for internet reachability.
  - Learned about AWS charging for unused EIPs to avoid waste.

- Gained knowledge about Internet Gateway (IGW):

  - Role as a horizontally scalable AWS-managed gateway to the internet.
  - Steps: Create IGW → Attach to VPC → Add route in Route Table → Associate with Public Subnet.
  - Understood the simplified approach compared to traditional network appliances.

- Analyzed VPC Topology using diagrams:

  - Identified relationship between VPCs, Availability Zones, and subnets.
  - Traced EC2 connectivity through ENI, Route Table, and IGW.
  - Differentiated how private vs. public subnets interact with external traffic.

- Acquired a clear mental model of how AWS networking components fit together to support real-world scenarios (public web servers, private databases, hybrid connectivity, etc.).
