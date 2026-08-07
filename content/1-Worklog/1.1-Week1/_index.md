---
title: "Week 1 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---
### Week 1 Objectives:

* Get connected with First Cloud AI Journey (FCAJ) members and get comfortable with the internship rules and workflow.
* Build a solid foundation in AWS Cloud fundamentals, global infrastructure, and core management tools.
* Practice account security (MFA), IAM, and networking (VPC) hands-on.
* Discuss as a team and lock in the Smart Docs AI project topic, then kick off the initial frontend.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| Mon | - Get acquainted with FCAJ members, read internship rules <br>&emsp;+ Introduce myself in the group chat, note the weekly online/offline schedule <br>&emsp;+ Read the rules carefully: reporting hours, leave request process, weekly Worklog submission deadline <br> - Watch "First Cloud Journey Kick off 2024", the Draw.io AWS architecture guide, and the Workshop guide (Hugo setup, folder structure, Markdown syntax) <br>&emsp;+ Install Hugo Extended + the hugo-theme-learn theme following the guide, test-run `hugo server` locally <br>&emsp;+ Learn the `content/` folder structure (each section has a bilingual `_index.md`/`_index.vi.md` pair) and the theme's own shortcode syntax <br> - Set up the Workshop report skeleton, update personal intro info <br>&emsp;+ Clone the sample repo, rename sections to match my personal structure, update `config.toml` (name, logo, contact info) <br>&emsp;+ Successfully build locally before pushing the first commit | 22/06/2026 | 22/06/2026 | [Kick off](https://www.youtube.com/watch?v=AQlsd0nWdZk&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=1) <br> [Draw.io Guide](https://www.youtube.com/watch?v=l8isyDe-GwY&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=2) <br> [Workshop Guide](https://www.youtube.com/watch?v=mXRqgMr_97U&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=3) |
| Tue | - Study cloud computing concepts, what sets AWS apart, AWS Global Infrastructure (Regions/AZs/Edge Locations), AWS management tools (Console/CLI/SDK) <br>&emsp;+ Distinguish Region/Availability Zone/Edge Location, understand why AWS uses multi-AZ to ensure high availability <br>&emsp;+ Compare Console, CLI, and SDK — decided to learn CLI alongside Console from the start <br> - Overview of AWS service groups: Compute/Storage/Networking/Database, note the flagship service of each group as a basis for choosing the architecture later <br> - Practice: create AWS Free Tier account, enable MFA to protect the root account, set up an AWS Budget alert at $5/month | 23/06/2026 | 23/06/2026 | [Cloud Concepts](https://www.youtube.com/watch?v=HxYZAK1coOI&list=PLahN4TLWtox2a3vElknwzU_urND8hLn1i&index=4) <br> [AWS Free Tier](https://000001.awsstudygroup.com/vi/) <br> [AWS Budgets](https://000007.awsstudygroup.com/vi/) |
| Wed | - Study IAM (Group/User/Policy/Role), learn the least-privilege principle — attach Policies to Groups/Roles rather than directly to Users <br> - Practice: create IAM Group/User/Role with a restricted Policy, use a personal User instead of the root account, try switching a Role to understand how temporary permissions work | 24/06/2026 | 24/06/2026 | [AWS IAM](https://000002.awsstudygroup.com/vi/) |
| Thu | - Team discussion: locked in the Smart Docs AI project topic and tech stack (ReactJS, Python, AWS) <br>&emsp;+ Weighed a few early ideas — chose a document RAG chatbot since it follows the GenAI trend and lets us leverage Bedrock <br>&emsp;+ Settled on ReactJS + Python/FastAPI + serverless AWS architecture to keep demo costs low | 25/06/2026 | 25/06/2026 | |
| Fri | - Build the initial frontend components for Smart Docs AI <br>&emsp;+ Scaffold the project with Vite + React, create the skeleton components (Layout, Sidebar, ChatWindow) following the agreed wireframe <br> - Push the source code to the team's GitHub repository <br>&emsp;+ Create the shared repo, agree on a branching convention (one branch per person, open a PR for review before merging into main) | 26/06/2026 | 26/06/2026 | Project Team GitHub Repository |
| Sat | - Study Amazon EC2 basics (instance types, AMI, EBS), distinguishing burstable T-family instances (cheap) from M/C instances (higher performance), prioritize free-tier for practice <br> - Overview of AWS Cloud9: test-drove the environment, then discussed with the team and decided to code locally and sync via GitHub instead | 27/06/2026 | 27/06/2026 | [AWS Cloud9](https://000049.awsstudygroup.com/vi/) |


### Week 1 Achievements:

* Got to know the FCAJ team and understood the internship rules/workflow.
* Built a solid grasp of AWS Cloud fundamentals: global infrastructure (Regions, AZs), core service groups, and management tools (Console/CLI).
* Successfully created an AWS Free Tier account, enabled MFA, and set up AWS Budgets to keep costs in check.
* Understood IAM's authorization model (User/Group/Role/Policy) and practiced creating the key resources.
* Finalized the Smart Docs AI project topic and tech stack (ReactJS, Python, AWS) as a team.
* Completed the initial frontend skeleton and pushed it to the team's GitHub repository.
* Got a first look at Amazon EC2 (instance types, AMI, EBS) ahead of next week.
