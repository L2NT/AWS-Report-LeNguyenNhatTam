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

- **Anh Long** – Security Solutions Architect, showcased **AWS Security Agent**, an actual AWS service, and talked about why security posture matters so much right now
- **Anh Huy** – AWS Certified Solutions Architect, shared exam-taking tips from his own certification journey

### Key Highlights

#### AWS Security Agent showcase (Anh Long)
- AWS Security Agent scans an account for common misconfigurations (loose IAM policies, publicly exposed resources, etc.) and surfaces findings the team can act on.
- The real point of the talk: in the "vibe coding" era, where a lot of code is AI-generated or pasted in without a full read-through, insecure defaults slip in more easily — so having something actively watching for that matters more than ever.

#### AWS Certification tips (Anh Huy)
- The exam is fully scenario-based multiple choice — no coding, but you need to reason through which AWS service actually fits the situation described.
- Practical (and slightly random) tip: exam rooms are almost always freezing, so bring a jacket if you don't want to be distracted halfway through.
- He also touched on time management during the exam — flagging uncertain questions and coming back at the end instead of getting stuck.

#### Quick networking round
- After the two talks, there was some open floor time where people who'd just gotten certified or were mid-prep swapped study resources and war stories — a nice, low-pressure way to end the morning.

### Key Takeaways

- Security can't be an afterthought when so much code today is "vibe coded" instead of reviewed line by line.
- A dedicated service like AWS Security Agent is genuinely useful for catching what nobody's manually checking.
- Exam prep is as much about strategy (time, question format) as it is about knowing the services, and smaller meetups make it easier to ask questions than a big seminar does.

### Applying to Work

- Added KMS encryption for DynamoDB (it had no customer-managed key before) and turned the key into a deployment variable so it's easy to swap per environment.
- Added a pytest step in CodePipeline's `pre_build` phase, so tests now gate every build before it can reach production — a check that simply didn't exist before.

### Event Experience

This was a small, low-key morning meetup rather than a big conference, which made it easier to actually talk to people — I got to ask Anh Long how much "vibe coding" has changed his day-to-day security reviews. Anh Huy's certification tips were the practical kind you don't really get from official docs. I left with concrete things to check in our own setup.

#### Some event photos
*Add your event photos here*
