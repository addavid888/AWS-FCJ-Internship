---
title: "Week 5 Worklog"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---

## Week 5 Objectives

- Understand the **Shared Responsibility Model** and what security boundaries AWS handles vs what you must handle.
- Learn how to manage permissions and identities using **AWS IAM**, including policies, roles, and least-privilege principles.
- Explore **Amazon Cognito** for user authentication and how it integrates with modern applications.
- Study **AWS Organizations** and **AWS Identity Center (SSO)** for multi-account management and centralized governance.
- Learn how encryption works in AWS through **AWS Key Management Service (KMS)** and why proper key handling matters.

---

## Tasks to be carried out this week

| Day | Task                                                                                                                                                                                                                   | On-site? | Date       |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ---------- |
| 1   | - Study the **Shared Responsibility Model** in depth <br> - Understand security boundaries: AWS security **of** the cloud vs your security **in** the cloud <br> - Review real-world consequences of misconfigurations | ✅       | 10/06/2025 |
| 2   | - Learn core **IAM concepts**: Users, Groups, Roles, Policies <br> - Practice writing IAM policies using JSON <br> - Explore permission boundaries, least privilege, and policy evaluation logic                       |          | 10/07/2025 |
| 3   | - Introduction to **Amazon Cognito** <br> - Understand User Pools vs Identity Pools <br> - Implement basic app authentication workflow (signup, login, tokens)                                                         |          | 10/08/2025 |
| 4   | - Learn **AWS Organizations**: multi-account structure, OU design, SCPs <br> - Explore **AWS Identity Center** for centralized access and SSO                                                                          |          | 10/09/2025 |
| 5   | - Deep dive into **AWS KMS** <br> - Learn about CMKs, key policies, encryption context <br> - Practice encrypting/decrypting data and understanding envelope encryption                                                |          | 10/10/2025 |
| 6   | - Combine all concepts: build a secure, multi-account governance model <br> - Create IAM roles for app access, enforce SCPs, and encrypt resources with KMS                                                            |          | 10/11/2025 |

---

## Week 5 Achievements

- **Understood the Shared Responsibility Model**:

  - Analyzed the exact security boundaries between AWS and the customer.
  - Identified common failure points caused by misunderstanding these boundaries.
  - Learned why misconfigurations often matter more than infrastructure failure.

- **Mastered IAM foundations**:

  - Wrote IAM policies and debugged access denials using policy evaluation logic.
  - Learned when to use roles instead of long-lived credentials.
  - Applied least-privilege principles across test environments.

- **Implemented modern authentication with Cognito**:

  - Learned how Cognito handles user identities, OAuth flows, and token issuance.
  - Studied integration patterns for web and mobile applications.
  - Understood security pitfalls when rolling your own authentication.

- **Explored AWS Organizations & Identity Center**:

  - Designed Organization Units and applied Service Control Policies (SCPs).
  - Centralized identity management with SSO for multiple AWS accounts.
  - Understood governance patterns used by large enterprises.

- **Learned secure key management with KMS**:

  - Understood how AWS manages encryption keys and why envelope encryption is standard.
  - Practiced encrypting resources and controlling access with key policies.
  - Explored multi-region keys, automatic rotation, and auditing with CloudTrail.
