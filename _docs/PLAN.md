# AI-Assisted Portfolio Tracker — Project Plan

## 1. Project Vision

Build an investment portfolio tracking application where AI coding agents are central to the software delivery process.

The experiment is not simply to add AI features to a portfolio tracker. The primary objective is to explore whether a small team of coding agents can take a software idea through:

> Product definition → Planning → Architecture → Implementation → QA → Iteration → Release

The human acts primarily as the **Product Owner / Experiment Lead**, while AI agents take the roles of:

- **PM Agent** — product discovery, requirements, user stories, acceptance criteria and backlog
- **Engineer Agent** — architecture, implementation, tests, documentation and bug fixes
- **QA Agent** — independent verification, test design, defect discovery and regression testing

A secondary objective is to build an AI-assisted portfolio analysis capability on top of a deterministic portfolio calculation engine.

---

## 2. Guiding Principles

### 2.1 Agents are first-class participants

Agents should perform meaningful software-development work rather than merely autocomplete code.

### 2.2 Separate responsibilities

The agent that implements a feature should not be the only agent responsible for deciding whether it works.

### 2.3 Deterministic calculations over LLM calculations

Financial calculations must be performed by application code.

The LLM may explain results, but should not be the authoritative calculator.

### 2.4 Human remains accountable

The human Product Owner makes final decisions about:

- product scope
- requirements
- architectural constraints where necessary
- release approval
- whether AI-generated insights are acceptable

### 2.5 Preserve the development trail

Important agent outputs, decisions, defects and iterations should be retained so the project can later be evaluated as an experiment.

---

# 3. Initial Product Brief

The initial brief given to the PM Agent should intentionally be short:

> Build a portfolio tracking application that allows an investor to record investments, monitor portfolio value and returns, and view portfolio allocation.

Do not initially provide a detailed implementation specification.

The purpose is to observe how effectively the PM Agent expands a vague product idea into a usable specification.

---

# 4. Product Scope

## Phase 1 — Portfolio Tracking MVP

The MVP should eventually support:

### Users

- user registration
- authentication
- basic profile

### Assets

- asset name
- ticker/symbol
- asset type
- currency
- market
- optional sector/category

Initial asset types may include:

- Nigerian equities
- US equities
- ETFs
- bonds
- treasury bills
- commercial paper
- mutual funds
- infrastructure funds
- cash

### Transactions

- buy
- sell
- dividend
- interest
- fees
- deposit
- withdrawal

### Portfolio

- holdings
- quantity
- average/cost basis
- current price
- current value
- unrealized gain/loss
- realized gain/loss
- income received
- portfolio return
- asset allocation

### Dashboard

The dashboard should provide a concise view of:

- total portfolio value
- total invested amount
- gain/loss
- return percentage
- income received
- allocation by asset type
- allocation by individual holding
- recent transactions

---

# 5. AI Portfolio Analyst

The AI layer should be introduced only after the deterministic portfolio tracker is functional.

Users should be able to ask questions such as:

- "How did my portfolio perform this month?"
- "Which holdings contributed most to my gains?"
- "What percentage of my portfolio is in equities?"
- "How much dividend income have I received?"
- "What are my largest holdings?"
- "How has my portfolio changed over time?"

The architecture should follow:

User question
→ AI Analyst
→ determine required data
→ Portfolio/API layer
→ deterministic calculations
→ AI interpretation
→ answer

The AI should not invent portfolio figures.

The system should provide the AI with verified portfolio data and calculations.

---

# 6. Agent Roles

## 6.1 PM Agent

### Responsibilities

- understand the initial product brief
- identify users and use cases
- produce product requirements
- identify ambiguities
- make explicit assumptions
- create user stories
- create acceptance criteria
- prioritize the backlog
- maintain requirements as the product evolves

### Required outputs

```text
docs/product/PRD.md
docs/product/requirements.md
docs/product/user-stories.md
docs/product/acceptance-criteria.md
docs/product/backlog.md
```

### Important rule

The PM Agent should explicitly record assumptions instead of silently inventing requirements.

---

## 6.2 Engineer Agent

### Responsibilities

- inspect existing repository
- translate approved requirements into implementation tasks
- propose architecture
- document technical decisions
- implement features
- write automated tests
- run builds and tests
- fix defects
- update documentation

### Required outputs

```text
docs/architecture/
docs/decisions/
source code
tests
```

The Engineer Agent should not modify requirements simply because an implementation is inconvenient.

If a requirement appears ambiguous or contradictory, it should flag the issue for the PM Agent/human.

---

## 6.3 QA Agent

### Responsibilities

- independently interpret requirements
- create test plans
- create automated tests where appropriate
- execute functional tests
- test edge cases
- test financial calculations
- test authorization
- test API behavior
- perform regression testing
- identify security issues
- challenge assumptions
- report defects clearly

### QA principle

> The QA Agent's job is to discover how the implementation could be wrong, not merely confirm that existing tests pass.

Required output:

```text
docs/qa/
    test-plan.md
    test-results.md
    defect-reports/
```

---

# 7. Development Workflow

Every feature should follow this loop:

```text
Product Requirement
        ↓
PM Agent
        ↓
User Story
        ↓
Acceptance Criteria
        ↓
Engineering Task
        ↓
Engineer Agent
        ↓
Implementation
        ↓
Automated Tests
        ↓
QA Agent
        ↓
Independent Verification
        ↓
   ┌────┴────┐
   │         │
 FAIL       PASS
   │         │
   ↓         ↓
Engineer   Release
   │
   ↓
Fix
   │
   └──→ QA
```

The loop should continue until the feature satisfies its acceptance criteria.

---

# 8. Development Phases

## Phase 0 — Experiment Setup

### Goals

Create the repository and establish the agent workflow.

### Tasks

- create Git repository
- define project structure
- create agent instructions
- define artifact conventions
- define branch/commit conventions
- establish experiment log
- define human approval gates
- decide initial technology constraints, if any

### Deliverables

```text
README.md
PLAN.md
AGENTS.md
docs/experiment/
```

---

# Phase 1 — Product Discovery

### Goal

Allow the PM Agent to transform the short product brief into a concrete MVP specification.

### Tasks

- run PM Agent
- review generated personas
- review requirements
- review assumptions
- review user stories
- review acceptance criteria
- approve MVP scope

### Human gate

The human decides:

> Is this actually the product I want to build?

---

# Phase 2 — Architecture

### Goal

Allow the Engineer Agent to propose the technical solution.

### Tasks

- repository/application structure
- database design
- domain model
- API design
- authentication approach
- frontend architecture
- testing strategy
- deployment approach
- logging/error handling

### Deliverable

An architecture decision record documenting:

- chosen architecture
- alternatives considered
- trade-offs
- assumptions
- unresolved risks

### Human gate

Review and approve the architecture before major implementation begins.

---

# Phase 3 — Core Implementation

Implement the MVP incrementally.

Suggested feature sequence:

1. authentication
2. asset management
3. transaction recording
4. holdings calculation
5. portfolio valuation
6. gain/loss calculation
7. portfolio allocation
8. dashboard
9. transaction history
10. basic reporting

Each feature goes through the complete PM → Engineer → QA loop.

---

# Phase 4 — Financial Correctness

This phase is particularly important.

Create a deterministic test suite covering:

### Simple purchase

```text
100 shares × ₦500
= ₦50,000 cost
```

### Multiple purchases

```text
100 @ ₦500
50  @ ₦600
```

Verify quantity, cost basis and average cost.

### Partial sale

```text
Buy 100 @ ₦500
Sell 40 @ ₦700
```

Verify:

- remaining quantity
- realized gain
- remaining cost basis
- unrealized gain

### Multiple buys and sells

Test more complicated transaction histories.

### Fees

Verify treatment of:

- transaction fees
- commissions
- other costs

### Dividends

Verify that dividend income is recorded separately from capital appreciation.

### Currency

Where supported, verify conversion and currency-specific calculations.

The portfolio calculation engine must have deterministic expected results.

---

# Phase 5 — QA Hardening

The QA Agent should perform:

- functional testing
- boundary testing
- invalid-input testing
- authorization testing
- authentication testing
- API testing
- database integrity testing
- concurrency testing where relevant
- regression testing
- financial calculation testing
- basic security testing

QA should have access to the original requirements, not only the Engineer Agent's implementation notes.

---

# Phase 6 — AI Portfolio Analyst

### Goal

Introduce AI only after the underlying portfolio data and calculations are trustworthy.

### Tasks

- define AI analyst requirements
- create safe data-access layer
- expose portfolio metrics to the AI
- implement question/answer workflow
- prevent unsupported financial claims
- provide source data/metrics used for responses
- test hallucination and calculation errors

### Example

Instead of asking the LLM to calculate:

> "What is my portfolio return?"

The application should calculate:

```text
portfolio_return = 12.43%
```

and provide that result to the LLM.

The LLM then explains:

> "Your portfolio is up 12.43% based on the current valuation..."

---

# Phase 7 — Agent-Driven Feature Expansion

After the MVP, deliberately add features using only the agent workflow.

Possible features:

- dividend calendar
- portfolio performance charts
- recurring investments
- watchlist
- benchmark comparison
- asset allocation targets
- portfolio history
- CSV import
- transaction import
- alerts
- tax-related reporting
- investment income reporting

Do not manually implement these features unless necessary.

The objective is to observe the agents operating an evolving codebase.

---

# 9. Experimentation Framework

The project should record how well the AI team performs.

For each feature record:

| Metric | Description |
|---|---|
| Feature | Feature name |
| PM iterations | Number of PM revisions |
| Engineering iterations | Number of implementation cycles |
| QA iterations | Number of QA cycles |
| Bugs found | Defects discovered |
| Requirements changed | Requirement modifications |
| Human interventions | Times human had to intervene |
| Tests generated | Automated tests created |
| Tests failed | Failed tests |
| Time | End-to-end development time |
| Cost | AI/API cost where measurable |
| Final status | Passed/Failed |

---

# 10. Key Research Questions

The experiment should gradually investigate:

### RQ1 — Requirements

How well can an AI PM transform a vague product idea into complete and consistent requirements?

### RQ2 — Implementation

How effectively can an AI coding agent implement those requirements without detailed human instructions?

### RQ3 — Verification

Can an independent QA agent reliably detect defects introduced by another coding agent?

### RQ4 — Financial correctness

Can agent-generated software correctly implement non-trivial financial calculations?

### RQ5 — Requirement drift

How much semantic drift occurs between:

```text
Original idea
→ PM specification
→ Engineering implementation
→ final product
```

### RQ6 — Technical debt

Does repeated agent-driven development cause increasing architectural or code-quality problems?

### RQ7 — Human intervention

How much human intervention is required as the project becomes larger and more complex?

### RQ8 — AI analyst reliability

Can an LLM provide useful portfolio explanations while remaining grounded in deterministic application data?

---

# 11. Evaluation Metrics

## Software quality

- test coverage
- defect density
- regression rate
- build failures
- static-analysis issues
- complexity
- duplication
- security findings

## Agent performance

- task completion rate
- number of iterations
- failed attempts
- requirement omissions
- incorrect assumptions
- human intervention rate
- time per feature
- cost per feature

## QA performance

- defects detected
- defects missed
- false positives
- regression detection
- edge cases discovered

## AI analyst performance

- factual accuracy
- calculation accuracy
- groundedness
- hallucination rate
- unsupported recommendations
- consistency

---

# 12. Human Approval Gates

The human should intervene at deliberate checkpoints rather than continuously directing the agents.

### Gate 1 — Product

Approve:

- PRD
- MVP scope
- assumptions

### Gate 2 — Architecture

Approve:

- architecture
- technology choices
- data model
- security approach

### Gate 3 — Feature

Approve feature requirements before implementation when necessary.

### Gate 4 — Release

Approve production/release candidate after QA.

This keeps the human in control without turning the experiment back into traditional manual development.

---

# 13. Important Constraints

## Financial disclaimer

This is a portfolio tracking and analysis application, not an autonomous investment adviser.

The AI should not independently execute trades.

Avoid language that presents generated opinions as guaranteed investment advice.

## Data integrity

User portfolio data must be treated as authoritative application data.

AI-generated text must never silently modify financial records.

## Security

Never expose:

- passwords
- API keys
- secrets
- access tokens
- sensitive production credentials

to agents unnecessarily.

---

# 14. Suggested Repository Structure

```text
ai-assisted-portfolio-tracker/
│
├── agents/
│   ├── pm/
│   ├── engineer/
│   └── qa/
│
├── backend/
│
├── frontend/
│
├── tests/
│
├── docs/
│   ├── product/
│   ├── architecture/
│   ├── decisions/
│   ├── qa/
│   └── experiment/
│
├── data/
│
├── experiments/
│
├── AGENTS.md
├── README.md
└── PLAN.md
```

---

# 15. First Milestone

The first milestone should NOT be writing application code.

### Milestone 1

Give the PM Agent only:

> Build a portfolio tracking application that allows an investor to record investments, monitor portfolio value and returns, and view portfolio allocation.

Then evaluate what it produces.

The immediate objective is to obtain:

```text
PRD
Requirements
User Stories
Acceptance Criteria
Backlog
Assumptions
Open Questions
```

Only after the human reviews those artifacts should the Engineer Agent begin.

---

# 16. Definition of Success

The project succeeds if it demonstrates a repeatable workflow where:

1. a human provides high-level product intent
2. the PM Agent converts intent into requirements
3. the Engineer Agent implements those requirements
4. the QA Agent independently verifies them
5. defects trigger another engineering cycle
6. the human approves major gates
7. the system can evolve through additional features
8. the process and outcomes are measurable

The ultimate goal is not:

> "AI wrote my portfolio tracker."

The stronger goal is:

> **"I created and evaluated an AI-centered software delivery team capable of taking a product from idea to tested software."**

---

# 17. Long-Term Direction

If the experiment works, the project can evolve from a portfolio tracker into a broader study of **Agentic Software Engineering**.

Potential future experiments:

- multiple competing Engineer Agents
- multiple independent QA Agents
- adversarial QA
- automated code review
- agent-generated pull requests
- agent-generated CI/CD
- autonomous bug fixing
- technical-debt monitoring
- requirements-to-test traceability
- long-running autonomous development
- comparison of different coding models
- human-vs-agent development efficiency

The portfolio tracker is therefore the **experimental environment**, not necessarily the final research product.
