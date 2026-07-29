---
title: "Event 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---

# Agentic AI Build Week powered by GenAI Fund

### Event Objectives

- Wrap up a large-scale hackathon (FCAJ x Agentic AI Build Week) with multiple competing teams (2K, Six Piller, One Team, Long & Co, and others)
- Give teams a stage to demo and pitch their Agentic AI products built on AWS
- Share hard-earned lessons from a 24-hour hackathon sprint — teamwork, pitching, and technical war stories
- Help participants walk away with portfolio-worthy projects and connections in the AWS Study Group community

### Speakers

- **One Team** – built a Zalo-style chatbot for food ordering, focused on a non-tech-friendly conversational UI
- **Long & Co** – built an AI assistant for Solution Architects that turns natural-language requirements into architecture diagrams, cost estimates, and deployable IaC
- **Nhóm 2K** – built a real-time crowd-monitoring system using computer vision and an agentic AI copilot
- **Six Piller** – built an Adaptive Workflow Engine for anti-money-laundering (AML) case triage

### Key Highlights

#### One Team – conversational food-ordering chatbot
- Skipped a full app in favor of a minimal, Zalo-like chat interface so non-tech users don't have to learn new navigation.
- Used natural-language prompts instead of menu buttons, letting the AI infer intent directly from what the user types — no account registration needed.
- Demoed against a simulated enterprise dataset (an FPT-style scenario) to show the agent could query structured business data (tax codes, quarterly revenue) and surface suggestions.
- Team's biggest takeaway: no matter how advanced the tech, it has to stay bounded by the actual business requirement — and shipping an MVP to production beats polishing a theory.

#### Long & Co – AI assistant for Solution Architects
- Tackles a real pain point for SAs: designing architecture, estimating cost, and deploying — sometimes in a single evening — while hand-drawn Draw.io diagrams and manually written IaC eat up all the time.
- Workflow: natural-language request + internal docs → AI drafts an architecture diagram → estimates AWS pricing → generates Terraform/CloudFormation → a human reviews and approves → the system deploys.
- The hard part, per the team, wasn't the diagram generation — it was managing the AI's context/memory so the architecture stayed consistent with internal rules (e.g., "Lambda must sit inside a VPC") and validating output against an allowed-services list on every run.
- Kept scope to a provable proof-of-concept with a step-by-step UI so judges could watch the agent's reasoning in real time.

#### Nhóm 2K – real-time crowd monitoring
- Pipeline: camera feeds into Amazon Kinesis Video Streams → AWS Fargate containers run YOLO for people detection and ByteTrack for tracking (so people aren't double-counted or missed) → density data lands in DynamoDB and S3.
- An agentic layer (Bedrock + OpenAI) lets operators query the system in plain language for a summary of an area or staffing suggestions.
- Standout feature: operators can draw custom "zones" on the camera feed (e.g., boarding gates, checkout lines), and the system flags color-coded alerts once a zone's density crosses a threshold.
- Biggest technical headaches were network stability for real-time video processing and needing a fixed, elevated camera angle for accurate zone counting.

#### Six Piller – AML Adaptive Workflow Engine
- Aims to replace a manual review process that costs roughly $20–$25 and about 3 hours per case, and that burns out analysts.
- Three-layer pipeline: Layer 1 does fast risk scoring (0–1) on live transactions via Kinesis Data Streams + XGBoost on Amazon Bedrock; Layer 2 uses AWS Step Functions to orchestrate specialized agents (KYC, transaction analysis, evidence-building) that compile an evidence file; Layer 3 buckets the case as Hold, Dismiss, or Escalate to a human.
- Design philosophy: AI is a "right hand," not a replacement, given how sensitive financial decisions are — every step of the agent's reasoning and evidence is logged for auditability, and the system lets one analyst handle far more cases than before.

#### Lessons from the 24-hour hackathon sprint
- Teamwork mattered more than any single line of code — teams that split roles clearly (backend, frontend, research, presenter) and dropped individual ego moved faster.
- Judges asking a lot of questions during pitching is actually a good sign — it means they're engaged; framing the pitch around a real pain point (not just cool tech) helped teams stand out.
- War stories included infra hiccups, accidentally pushing a `.env` file to GitHub, running on little sleep, and scrambling when the network died mid live-demo.
- The organizers' closing message: don't over-index on winning — the real value is the experience (networking, learning new tools, testing your own limits), and these projects double as solid portfolio pieces for future job applications.

### Key Takeaways

- Across very different domains (food ordering, cloud architecture, computer vision, AML), the common thread was starting from a real pain point instead of leading with the technology.
- Agentic AI patterns kept showing up: an orchestration layer (Step Functions or similar) coordinating specialized agents, human-in-the-loop checkpoints before anything risky happens, and context/memory management to keep AI output consistent.
- A hackathon is as much a lesson in teamwork and time pressure as it is a coding exercise — some of the sharpest advice came from the "what went wrong" retrospectives, not the demos themselves.

### Applying to Work

- Consider adding a human-in-the-loop approval step before any AI-driven action that changes infrastructure or makes a financial/security decision, similar to Long & Co's and Six Piller's designs.
- Look into an orchestration pattern (like Step Functions) for coordinating multiple specialized agents instead of building one large, do-everything agent.

### Event Experience

This was the closing/demo day of a hackathon rather than a talk-style event, so most of the day was four teams pitching back-to-back, followed by an open retrospective on what the 24 hours were actually like. I mostly sat and watched the demos and Q&A — the AML workflow engine and the SA architecture assistant were the two that stuck with me most, since both leaned heavily on human-in-the-loop design instead of trying to automate everything end to end.

#### Some event photos
*Photos go in `static/images/4-EventParticipated/4.2-Event2/` — once added, reference them here like `![](/images/4-EventParticipated/4.2-Event2/your-photo.jpg)`.*
