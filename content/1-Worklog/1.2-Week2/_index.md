---
title: "Week 2 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---
### Week 2 Objectives:

* Refine/refactor the Smart Docs AI frontend.
* Study Amazon S3 (bucket/object management, static website hosting, CloudFront).
* Study Amazon RDS and EC2 Auto Scaling for application scalability.
* Get familiar with KMS and Amazon Cognito ahead of building the backend authentication.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon-Tue | - Refactor the Smart Docs AI frontend <br>&emsp;+ Split the ChatWindow/Sidebar components more cleanly, standardized the color/spacing theme with Tailwind to make future UI expansion easier <br> - Study Amazon S3: buckets/objects, static website hosting, blocking/allowing public access <br>&emsp;+ Compared 2 ways to host the frontend: S3 static website hosting (simple, HTTP only) vs. S3 + CloudFront (HTTPS, global caching) — decided on the latter since HTTPS would be needed for Cognito's OAuth callback flow later <br> - **Practice:** enable CloudFront in front of the static site <br>&emsp;+ Created a CloudFront distribution pointing to the S3 bucket, configured Origin Access Control (OAC) to block direct S3 access, allowing traffic only through CloudFront | 29/06/2026 | 30/06/2026 | [Amazon S3 Guide](https://000057.awsstudygroup.com/vi/) |
| Wed | - Study Amazon RDS & Aurora concepts <br>&emsp;+ Compared RDS (traditional managed engines: MySQL/PostgreSQL...) with Aurora (MySQL/PostgreSQL-compatible but higher performance, auto storage scaling) <br>&emsp;+ Noticed Smart Docs AI leans toward storing document metadata as key-value rather than complex relational data — noted DynamoDB as a candidate over RDS when designing the real backend <br> - Read up on RDS deployment, backup, and restore <br>&emsp;+ Learned the automated backup + manual snapshot mechanism and the default retention period — a baseline for comparing against DynamoDB's on-demand backup later | 01/07/2026 | 01/07/2026 | [Amazon RDS Guide](https://000005.awsstudygroup.com/vi/) |
| Thu | - Study EC2 Auto Scaling: Auto Scaling Group, Launch Template, Elastic Load Balancer, Target Group <br>&emsp;+ Understood the scaling mechanism based on CloudWatch metrics (CPU crosses a threshold → automatically add an instance), with the ELB distributing traffic through the Target Group to healthy instances <br> - Overview of EFS/FSx/Lightsail <br>&emsp;+ Noted that EFS fits well when multiple EC2 instances/containers need to read-write a shared file system — relevant to Smart Docs AI's need for shared document storage (though S3 was ultimately chosen for being cheaper and already familiar) | 02/07/2026 | 02/07/2026 | [EC2 Auto Scaling](https://000006.awsstudygroup.com/vi/) |
| Fri | - Study AWS KMS (encryption keys) and Amazon Cognito (user pools, sign-up/sign-in flow) to prep for the project's backend auth work <br>&emsp;+ Learned the Customer Managed Key vs. AWS Managed Key concepts in KMS — noted this would be needed for DynamoDB encryption later <br>&emsp;+ Studied Cognito's basic User Pool flow (sign-up → confirm email → sign-in) — this would become the foundation for the project's entire auth flow | 03/07/2026 | 03/07/2026 | [Amazon Cognito](https://000081.awsstudygroup.com/vi/) |
| Sat | - Finalize and update the Worklog for Week 1 and Week 2 <br>&emsp;+ Reviewed the tasks done during the week, cross-checked dates against what actually happened <br> - Sync all source code and docs to GitHub <br>&emsp;+ Committed + pushed all frontend changes, making sure the personal repo and the team repo stayed in sync | 04/07/2026 | 04/07/2026 | Personal GitHub Repository |


### Week 2 Achievements:

* Refactored the Smart Docs AI frontend, improving layout and user experience.
* Understood how Amazon S3 works: creating/managing buckets, uploading objects, static website hosting, and integrating CloudFront.
* Built a solid foundation in Amazon RDS: operations, backup, and restore.
* Understood how to scale applications with EC2 Auto Scaling (Auto Scaling Groups, Launch Templates, ELB, Target Groups).
* Got familiar with KMS (key management) and Amazon Cognito (user pools, sign-up/sign-in flow) - the foundation for the project's authentication work in later weeks.
* Completed and synced the Week 1 and Week 2 Worklogs to GitHub.
