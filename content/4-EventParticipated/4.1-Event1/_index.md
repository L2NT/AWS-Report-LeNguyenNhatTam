---
title: "Event 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Cloud Architect x Meet Up

### Event Objectives

- Create an informal space where cloud architects, engineers, and AWS learners can swap real-world experience
- Showcase AWS Security Agent and highlight why security matters more than ever in the age of "vibe coding"
- Share practical tips and mindset for tackling AWS certification exams
- Grow the local AWS Study Group / cloud community through casual networking

### Speakers

The meetup featured four speakers in total; the two sessions below are the ones covered in detail here:

- **Anh Long** – Security Solutions Architect, showcased **AWS Security Agent**, an actual AWS service, and talked about why security posture matters so much right now
- **Anh Huy** – AWS Certified Solutions Architect, shared exam-taking tips from his own certification journey

### Key Highlights

#### AWS Security Agent showcase (Anh Long)
- AWS Security Agent scans an entire project end-to-end for a much broader range of issues than typical account-level misconfigurations — hardcoded secrets and API keys left in code, outdated dependencies with known CVEs, exposed S3 buckets and overly open security groups, missing encryption at rest/in transit, and common code-level risks like injection flaws — then surfaces every finding through a visual dashboard instead of raw logs.
- It also auto-generates a full PDF report of everything it finds, so the team has something shareable to act on without manually compiling results.
- The real point of the talk: in the "vibe coding" era, where a lot of code is AI-generated or pasted in without a full read-through, insecure defaults slip in more easily — so having something actively watching for that matters more than ever.

#### AWS Certification tips (Anh Huy)
- The exam is fully scenario-based multiple choice — no coding, but you need to reason through which AWS service actually fits the situation described.
- Practical (and slightly random) tip: exam rooms are almost always freezing, so bring a jacket if you don't want to be distracted halfway through.
- He also touched on time management during the exam: if a question is taking too long, skip it and keep moving — later questions sometimes hint at, or even give away, the answer to one you were stuck on earlier. The exam interface has a flag feature for exactly this, letting you mark uncertain questions and jump straight back to all of them once you've gone through the whole exam.
- He also pointed out that not every question is a standard single-answer multiple choice — some are "multiple response" questions, where you have to pick two or more correct answers out of five or more options, so it's worth checking how many answers a question expects before submitting.

### Key Takeaways

- Security can't be an afterthought when so much code today is "vibe coded" instead of reviewed line by line — vulnerabilities can hide anywhere from hardcoded secrets to outdated dependencies, not just account misconfigurations.
- A dedicated service like AWS Security Agent is genuinely useful for catching what nobody's manually checking, and packaging results into a dashboard plus an auto-generated PDF report makes it much easier to actually act on.
- Exam prep is as much about strategy — skipping and flagging tough questions, watching out for multiple-response formats — as it is about knowing the services, and meetups like this make it easier to ask questions than a big seminar does.

### Applying to Work

- Added KMS encryption for DynamoDB (it had no customer-managed key before) and turned the key into a deployment variable so it's easy to swap per environment.
- Added a pytest step in CodePipeline's `pre_build` phase, so tests now gate every build before it can reach production — a check that simply didn't exist before.

### Event Experience

This meetup had four speaker sessions, but the ones that stuck with me most were Anh Long's and Anh Huy's. Anh Long helped me understand more clearly what AWS Security Agent actually does, and how useful its auto-generated report is; Anh Huy shared practical exam tips that official docs rarely cover. I left the session with a lot of questions about the security side of our own project's setup.

#### Some event photos
![Event 1 photo](/images/4-EventParticipated/4.1-Event1/Event-11-07-2026.jpeg)
