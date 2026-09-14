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


## Logical Architecture
┌─────────────────────────────────────────────────────────────┐
│                        Presentation                          │
│                                                             │
│  Web UI                                                     │
│  Dashboard │ Holdings │ Transactions │ Analytics │ Settings │
└────────────────────────────┬────────────────────────────────┘
                             │ HTTPS / JSON
                             ▼
┌─────────────────────────────────────────────────────────────┐
│                         API Layer                            │
│                                                             │
│  Authentication                                             │
│  Portfolio API                                               │
│  Asset API                                                   │
│  Transaction API                                             │
│  Dashboard API                                               │
│  Analytics API                                               │
│  AI Analyst API                                              │
└────────────────────────────┬────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────┐
│                    Application Layer                         │
│                                                             │
│  Portfolio Service                                           │
│  Transaction Service                                         │
│  Valuation Service                                           │
│  Performance Service                                         │
│  Allocation Service                                          │
│  Income Service                                              │
│  AI Analysis Service                                         │
└────────────────────────────┬────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────┐
│                       Domain Layer                           │
│                                                             │
│  Portfolio │ Holding │ Asset │ Transaction │ Position       │
│  Valuation │ Performance │ Income                           │
│                                                             │
│  Financial calculation rules                                │
└────────────────────────────┬────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────┐
│                    Infrastructure                           │
│                                                             │
│  Database │ Market Data │ Cache │ Authentication │ Logging  │
│  External APIs │ File Storage │ LLM Provider                │
└─────────────────────────────────────────────────────────────┘