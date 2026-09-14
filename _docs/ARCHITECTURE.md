# AI-Assisted Portfolio Tracker — Architecture

## 1. Architecture Vision

The system is designed around three distinct concerns:

1. **AI software-delivery agents**
   - PM Agent
   - Engineer Agent
   - QA Agent
   - Agent Orchestrator

2. **Application runtime**
   - Portfolio management
   - Financial calculations
   - Market data
   - Analytics
   - AI Portfolio Analyst

3. **Human control**
   - Product decisions
   - Architecture decisions
   - Approval gates
   - Release decisions

The central architectural principle is:

> **AI should orchestrate, interpret and assist. The application core should calculate, validate and enforce.**

### High-Level Architecture

```text
                         HUMAN
                   Product Owner
                         │
                         ▼
              ┌─────────────────────┐
              │  AGENT ORCHESTRATOR │
              └──────────┬──────────┘
                         │
          ┌──────────────┼──────────────┐
          │              │              │
          ▼              ▼              ▼
     ┌─────────┐    ┌───────────┐   ┌─────────┐
     │ PM      │    │ Engineer  │   │ QA      │
     │ Agent   │    │ Agent     │   │ Agent   │
     └────┬────┘    └─────┬─────┘   └────┬────┘
          │               │              │
          └───────────────┼──────────────┘
                          │
                          ▼
                  ┌───────────────┐
                  │ Git Repository │
                  └───────┬───────┘
                          │
                          ▼
                 ┌─────────────────┐
                 │ CI / Test / CD  │
                 └────────┬────────┘
                          │
                          ▼
              ┌────────────────────────┐
              │ Portfolio Application  │
              └────────────────────────┘