---
title: "Blog 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# AMAZON BEDROCK LANDING ZONE ARCHITECTURE

> *The post below was written by teammate Phong, and counts toward the group's shared blog quota (3 posts) as required by the FCAJ program.*

![Amazon Bedrock Baseline Architecture Diagram in an AWS Landing Zone](https://d2908q01vomqb2.cloudfront.net/fc074d501302eb2b93e2554793fcaf50b3bf7291/2025/06/18/ARCHBLOG-1133-image-1-960x630.png)

### 1. Baseline Architecture Overview
When deploying enterprise Generative AI (GenAI) applications with Amazon Bedrock, establishing a robust baseline architecture within an AWS Landing Zone (managed via AWS Control Tower) is a prerequisite for security, high availability, and compliance governance.

The Landing Zone architecture organizes enterprise cloud infrastructure into specialized AWS accounts (Multi-Account Strategy):
* **Core Network Account:** Manages centralized network routing and VPC Endpoints.
* **Security & Governance Account:** Manages CloudTrail audit trails and compliance monitoring.
* **Workload/AI Application Account:** Houses core application services and Amazon Bedrock models.

---

### 2. Defense-in-Depth Network Security with AWS PrivateLink & VPC Lattice
The architecture eliminates public internet transit for GenAI data through private connectivity endpoints:
* **Amazon Bedrock VPC Endpoints (AWS PrivateLink):** Enables internal VPC services to invoke Foundation Models and Knowledge Bases directly over private AWS networks.
* **Amazon VPC Lattice Auth Policies:** Enforces IAM authentication and authorization at the network service level, restricting Bedrock API access to authorized microservices.

---

### 3. Centralized Identity Management & Least-Privilege Access
* **AWS IAM Identity Center (SSO):** Integrates with enterprise directory services (Active Directory/Okta) to provide secure SSO access for developers and application consumers.
* **IAM Resource Policies & KMS Encryption:** All Bedrock assets (Knowledge Bases, Custom Models, Fine-tuning datasets) are encrypted using Customer Managed KMS Keys (KMS CMK) and enforced via strict IAM Resource Policies.

---

### 4. Governance with Service Control Policies (SCPs) & Audit Logging
* **Service Control Policies (SCPs):** Prevents unauthorized creation of Bedrock resources in non-approved AWS Regions and blocks disabling required audit logging settings.
* **Comprehensive Audit Trail:** All Bedrock model invocations, Knowledge Base updates, and data access events are logged into AWS CloudTrail and CloudWatch Logs for continuous compliance audits.

---

### Reference Documentation
* **Link blog:** [https://www.facebook.com/groups/awsstudygroupfcj/permalink/2207763766655250](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2207763766655250)
* **Original Article on AWS Architecture Blog:** [Amazon Bedrock baseline architecture in an AWS landing zone](https://aws.amazon.com/vi/blogs/architecture/amazon-bedrock-baseline-architecture-in-an-aws-landing-zone/)