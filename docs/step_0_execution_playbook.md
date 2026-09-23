# Local AI Lab — Steps 0 Execution Playbook

**Purpose:** Turn the Local AI Lab thesis into a validated startup with disciplined execution.

**Current stage:** Pre-validation

**Rule:** Do not start full product development until the validation gates in this document are passed.

---

# 1. The Next 30 Days

## Outcome

At the end of 30 days we should know:

1. Who the first customer is.
2. What their highest-value workflow is.
3. Why existing tools are insufficient.
4. What minimum product solves that workflow.
5. Whether people will pay for it.
6. What technical architecture is actually required.

---

# 2. Week 1 — Customer Discovery

## Objective

Find the first narrow ICP and recurring workflows.

### Day 1 — Build interview database

Create a spreadsheet/database with:

- Name
- Role
- Company type
- AI tools used
- Local AI experience
- Hardware
- Top AI workflows
- Frequency
- Current solution
- Pain level
- Privacy sensitivity
- Cost sensitivity
- Automation interest
- Willingness to try
- Willingness to pay

Target:

**30 interviews**

Do not pitch the product initially.

---

## Day 2–3 — Recruit users

Recruit from:

- local LLM communities
- AI developer communities
- GitHub
- Reddit
- Discord
- LinkedIn
- personal engineering network
- startup communities

Target:

**10 interviews by end of week 1**

---

## Day 3–5 — Conduct interviews

Ask:

### Current behavior

- What do you use AI for every week?
- Which tasks do you repeat?
- Which AI tools do you currently use?
- Which tasks use local models?
- Which tasks use cloud models?

### Pain

- What is frustrating?
- What takes too much setup?
- What costs too much?
- What do you avoid because of privacy?
- What do you wish AI could do automatically?

### Local AI

- Why did you try local AI?
- What made you continue/stop?
- Which models?
- Which runtime?
- How much time did setup take?

### Automation

- What task would you delegate if AI could reliably do it?

### Money

Do not ask:

> "Would you pay for this?"

Instead ask:

> "What do you currently pay for AI tools?"

> "What would need to improve for you to replace one of them?"

---

# 3. Week 1 Deliverable

Create:

## Customer Workflow Map

Example:

| Workflow | Frequency | Current tool | Pain | Privacy | Automation | Potential |
|---|---:|---|---:|---:|---:|---:|
| Codebase analysis | Daily | Cursor | 4/5 | 4/5 | 5/5 | High |
| Private PDF analysis | Weekly | ChatGPT | 5/5 | 5/5 | 4/5 | High |
| Research | Daily | Perplexity | 3/5 | 2/5 | 4/5 | Medium |
| Personal knowledge | Weekly | Notes | 5/5 | 5/5 | 5/5 | High |

The actual values must come from interviews.

---

# 4. Week 2 — Competitive Teardown

## Objective

Understand exactly what existing products already solve.

Study at minimum:

- Ollama
- LM Studio
- Open WebUI
- AnythingLLM
- Jan
- GPT4All
- Cursor
- Claude
- ChatGPT
- Gemini
- Perplexity
- relevant agent/MCP products

For each capture:

- target user
- onboarding
- model management
- local inference
- cloud integration
- RAG
- memory
- agents
- MCP
- privacy
- routing
- pricing
- UX
- major limitations

Do not simply create a feature checklist.

Answer:

> **What job does each product own?**

---

# 5. Week 2 — Build the Opportunity Matrix

Score candidate workflows using:

```text
Opportunity =
Pain
× Frequency
× Willingness to Pay
× Differentiation
× Technical Feasibility
```

Candidate examples:

1. Private coding agent
2. Personal knowledge assistant
3. Hybrid research agent
4. Private document analyst
5. Local/cloud AI router
6. AI desktop assistant
7. Local AI developer environment

Do not choose based on intuition.

Choose based on evidence.

---

# 6. Week 2 Deliverable

Create:

## Product Opportunity Brief

It must contain:

### ICP

One specific customer.

### Problem

One specific painful problem.

### Existing alternatives

What they use today.

### Failure of alternatives

Specific limitations.

### Proposed solution

One workflow.

### Differentiator

Why we can solve it materially better.

### Business model

Who pays and why.

### Validation evidence

Interview references and observed behavior.

---

# 7. Week 3 — Prototype

Do not build the platform.

Build a **thin vertical slice**.

Example:

```text
User
 ↓
Desktop App
 ↓
Task
 ↓
Privacy Classifier
 ↓
Local/Cloud Router
 ↓
Model
 ↓
Tools/RAG
 ↓
Result
```

The prototype should prove:

> **The user can describe a task and the system intelligently decides how to execute it.**

---

# 8. Prototype Scope

## Screen 1 — Home

```text
What would you like to accomplish?

[ Ask anything... ]

Recent tasks
Knowledge
Agents
Models
```

## Screen 2 — Hardware

```text
Your machine

CPU
RAM
GPU
VRAM

Recommended local models
```

## Screen 3 — Models

```text
Installed
Available
Recommended
Cloud
```

## Screen 4 — Task execution

```text
Task

Privacy: High
Execution: Hybrid

Local:
- document indexing
- sensitive-data extraction

Cloud:
- advanced reasoning

Tools:
- filesystem
```

## Screen 5 — Result

Show:

- answer
- sources
- model
- local/cloud execution
- cost
- duration

---

# 9. Week 3 Technical Spike

Build experiments for:

### Local inference

Test:

- Ollama
- llama.cpp or another appropriate runtime
- model loading
- streaming
- structured output
- tool calling

### Cloud abstraction

Create one internal interface:

```ts
interface ModelProvider {
  generate(request: GenerateRequest): Promise<GenerateResponse>;
  stream(request: GenerateRequest): AsyncIterable<Chunk>;
  capabilities(): ModelCapabilities;
}
```

Providers should include:

```text
LocalProvider
OpenAIProvider
AnthropicProvider
GeminiProvider
```

The rest of the system should not care which provider is used.

---

# 10. Week 3 — Routing Engine

Create the first routing policy.

Inputs:

```text
Task
Privacy level
Context size
Hardware
Latency target
Cost target
Required capabilities
```

Output:

```text
ExecutionPlan
```

Example:

```json
{
  "execution": "hybrid",
  "localSteps": [
    "ingest_document",
    "extract_sensitive_information"
  ],
  "cloudSteps": [
    "reasoning"
  ],
  "model": "selected-provider-model",
  "requiresConfirmation": true
}
```

Do not attempt machine-learning-based routing initially.

Use deterministic rules.

---

# 11. Week 4 — Private Beta

Recruit:

**5–10 serious users**

Give them the prototype.

Ask them to perform real work.

Do not give them scripted demo tasks only.

Observe:

- onboarding
- model setup
- task completion
- errors
- routing decisions
- latency
- trust
- privacy understanding
- repeated use

---

# 12. The Critical Beta Question

Do not ask:

> "Do you like the product?"

Ask:

> **"What did you actually use it for?"**

And:

> **"Would you use it again tomorrow?"**

The second question is more important than compliments.

---

# 13. Validation Metrics

Minimum signal before building the larger platform:

### Activation

At least 60% of beta users successfully complete a meaningful task.

### Repeat usage

At least 40% return and use it again within the first week.

### Workflow concentration

At least 3 users independently repeat the same core workflow.

### Strong pain

At least 5 users describe the problem as significant enough to seek a solution.

### Payment signal

At least 3 users indicate concrete willingness to pay or replace an existing paid tool.

These are internal decision thresholds, not market facts.

---

# 14. Decision Gate

After beta, choose one:

## A — Strong signal

Build the vertical product.

## B — Mixed signal

Narrow the ICP/workflow.

## C — Weak signal

Return to interviews.

Do not automatically expand features.

---

# 15. Product Development Phase

Only after validation.

## Milestone 1 — Foundation

- desktop shell
- local runtime
- provider abstraction
- model registry
- hardware detection
- secure local storage
- basic workspace

## Milestone 2 — Intelligence

- routing engine
- privacy classification
- model recommendation
- RAG
- memory

## Milestone 3 — Execution

- MCP gateway
- tool permissions
- agent runtime
- workflow engine

## Milestone 4 — Productization

- onboarding
- analytics
- error recovery
- model management
- cost dashboard
- update system

## Milestone 5 — Monetization

- account system
- billing
- cloud gateway
- usage limits
- Pro features

---

# 16. Engineering Principles

## Start modular, not distributed.

V1 should preferably be a modular monolith.

```text
Desktop
 ├── UI
 ├── Application Core
 ├── Model Manager
 ├── Router
 ├── Knowledge
 ├── Memory
 ├── Agent Runtime
 ├── MCP Gateway
 ├── Privacy Engine
 └── Local Storage
```

Split services only when operational evidence justifies it.

---

# 17. Security-by-Design Checklist

Before agents can perform real actions:

- [ ] filesystem permission scopes
- [ ] network permission scopes
- [ ] command execution sandbox
- [ ] secret isolation
- [ ] tool allowlist
- [ ] confirmation policy
- [ ] audit log
- [ ] prompt injection defenses
- [ ] untrusted content isolation
- [ ] cloud data policy
- [ ] user-visible execution trace

Default:

> **Read-only before write access.**

Default:

> **No unrestricted shell access.**

---

# 18. First Agent Policy

Agents should have:

```text
Identity
Permissions
Budget
Time limit
Tool allowlist
Network policy
Data policy
Human confirmation policy
```

Example:

```text
Coding Agent

Filesystem:
  project/       read/write
  home/          deny

Network:
  package registry allow
  arbitrary network deny

Shell:
  npm test       allow
  npm install    confirm
  rm -rf         deny
```

This becomes an important enterprise-grade foundation later.

---

# 19. Analytics Architecture

Capture product telemetry without violating the privacy promise.

Separate:

### Local telemetry

Detailed task/model data stays local unless user opts in.

### Anonymous product telemetry

Potentially collect:

- app version
- crash reports
- coarse performance metrics
- feature usage

Never make "private by default" claims that contradict actual telemetry behavior.

---

# 20. Business Validation

Before significant infrastructure spend, test:

### Free

Does local-only adoption grow?

### Pro

Will users pay for:

- hybrid routing
- cloud access
- agents
- advanced knowledge
- automation?

### Team

Will teams pay for:

- shared knowledge
- governance
- RBAC
- audit?

---

# 21. Go-To-Market Experiment #1

Create a simple landing page with one promise:

> **Your AI, running where it makes sense. Local when possible. Cloud when needed.**

CTA:

**Join the private beta**

Do not market 30 features.

Test 3 positioning variants:

1. Privacy
2. Cost/control
3. AI automation

Measure:

- visitor → signup
- signup → interview
- interview → beta
- beta → repeat use

---

# 22. Go-To-Market Experiment #2

Publish practical technical content:

- "What can a 12GB GPU actually run locally?"
- "Local vs cloud AI: what should run where?"
- "How much can local AI reduce API costs?"
- "Building a private coding agent"
- "Local AI hardware guide"
- "MCP + local AI"
- "Building a personal knowledge base"

Use these to attract the exact ICP.

---

# 23. Company Formation

Do not over-engineer the legal structure before product validation.

Once there is validated demand, establish:

- company entity
- founder agreements
- IP ownership
- trademark/domain strategy
- privacy policy
- terms
- open-source license policy
- contributor agreements
- security policy

If external funding is pursued:

- cap table
- incorporation documents
- financial model
- investor deck
- data room

Use qualified legal/accounting professionals for jurisdiction-specific decisions.

---

# 24. Financial Model

Build a model with:

### Revenue

```text
Users
×
Conversion
×
ARPU
```

### Cloud cost

```text
Cloud tokens
×
provider cost
```

### Infrastructure

- storage
- compute
- bandwidth
- observability
- authentication
- billing

### Gross margin

```text
Revenue - variable infrastructure cost
--------------------------------------
Revenue
```

Hybrid AI products need special attention to cloud inference margins.

---

# 25. Founder Dashboard

Maintain one weekly dashboard.

## Product

- active users
- tasks/user
- repeat users
- successful tasks
- failed tasks

## AI

- local %
- cloud %
- routing accuracy
- latency
- cost/task

## Business

- signups
- activation
- conversion
- revenue
- churn

## Customer

- interviews
- support requests
- top workflows
- top complaints

---

# 26. Weekly Founder Review

Every week answer:

1. What did users actually do?
2. What surprised us?
3. What failed?
4. What should we stop building?
5. What should we build next?
6. What assumption became stronger?
7. What assumption became weaker?
8. What is the single most important experiment next week?

---

# 27. First 90-Day Roadmap

## Days 1–30 — Validate

- 30 interviews
- workflow database
- competitive research
- opportunity matrix
- landing page
- prototype
- 5–10 beta users

**Gate:** identify one high-value workflow.

## Days 31–60 — Prove

- build vertical MVP
- local runtime
- cloud abstraction
- router
- RAG
- basic privacy engine
- 10–25 active beta users

**Gate:** repeated usage.

## Days 61–90 — Productize

- improve reliability
- agent execution
- MCP
- observability
- billing experiment
- first paid users

**Gate:** evidence of willingness to pay.

---

# 28. What We Should Not Do in the Next 30 Days

Do not:

- build a 50-person architecture
- build a custom LLM
- build custom inference
- build a complex Kubernetes platform
- build every agent
- build mobile apps
- build enterprise SSO
- build an AI marketplace
- spend heavily on cloud
- hire before the core workflow is validated
- assume Reddit sentiment equals market demand
- mistake downloads for product-market fit

---

# 29. Definition of Startup Readiness

We can consider moving from experiment to startup execution when:

- one ICP is clear
- one primary workflow is clear
- users repeatedly use the product
- the product materially improves the workflow
- users understand the local/cloud value
- at least some users pay
- retention is measurable
- security architecture is credible
- unit economics are understood
- acquisition channel has an early signal

---

# 30. Immediate Founder Checklist

### This week

- [ ] Create interview tracker
- [ ] Recruit first 10 users
- [ ] Conduct interviews
- [ ] Record workflows
- [ ] Create competitor matrix
- [ ] Identify recurring pain
- [ ] Select 3 candidate workflows

### Next week

- [ ] Complete 30 interviews
- [ ] Score workflows
- [ ] Select ICP
- [ ] Write product opportunity brief
- [ ] Create landing page
- [ ] Recruit prototype users

### Week 3

- [ ] Build hardware detector
- [ ] Integrate local runtime
- [ ] Build provider abstraction
- [ ] Build simple router
- [ ] Add basic document flow

### Week 4

- [ ] Give prototype to users
- [ ] Observe real workflows
- [ ] Measure activation
- [ ] Measure repeat usage
- [ ] Collect objections
- [ ] Decide whether to proceed

---

# 31. The One Thing We Are Solving First

Do not lose the product thesis in the platform ambition.

The first version should answer one question:

> **Can we make local + cloud AI dramatically easier and more useful by automatically deciding where a user's task should run?**

If the answer is yes, the rest of the platform can be built around that capability.

If the answer is no, we change the product before accumulating technical debt.

---

# 32. First Founder Sprint

### Objective

Find the first painful, repeatable, monetizable workflow.

### Deliverables

1. 30 interviews
2. workflow database
3. competitor teardown
4. opportunity matrix
5. one ICP
6. one primary workflow
7. prototype specification
8. landing page
9. 5–10 beta users
10. validation decision

### Success condition

We finish the sprint with evidence, not assumptions.

---

# Final Operating Principle

**Build the company around validated user behavior, not around the technology being exciting.**

The technology enables the product.

The workflow creates the product.

The customer creates the business.

