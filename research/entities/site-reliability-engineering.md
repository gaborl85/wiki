---
title: Site Reliability Engineering
type: entity
created: 2026-06-11
last_updated: 2026-06-11
tags: [operations, discipline, reliability]
sources: ["intro_to_sre_summary.md"]
related: []
---

# Site Reliability Engineering

**What is it?**
An engineering discipline devoted to helping organizations sustainably achieve the appropriate level of reliability in their systems, services, and products. Originated at Google in 2003 when Ben Treynor (now Treynor Sloss) asked: "What happens when you ask a software engineer to design an operations function?"

**Core Principles:**

- **Reliability as the focus** — Reliability is the primary property, not performance, efficiency, or cost
- **Appropriate levels** — Pragmatic reliability targets based on business needs. Chasing unnecessary reliability wastes time and resources
- **Sustainability for people** — Operations practices must be sustainable for the humans doing the work. Unsustainable on-call, constant firefighting, and burnout undermine reliability

**Key Practices:**

**Virtuous Cycle #1: SLI/SLO/Error Budgets**
- Service Level Indicator (SLI): How you measure if the service is healthy (e.g., success rate, latency, throughput)
- Service Level Objective (SLO): The target reliability level agreed upon with service owners and stakeholders
- Error Budget: The allowance for unreliability (100% - SLO). If SLO is 99% uptime, you have 1% error budget to spend on risky deployments, experiments, or handling incidents

**Virtuous Cycle #2: Blameless Postmortems**
- Postmortem analysis focuses on process and system failures, not individual blame
- Goal: Learn from incidents and improve systems to prevent recurrence
- Underlying belief: "You can't fire your way to reliability"

**Toil Elimination**
- Toil: Repetitive, manual, low-value operational work (resets, provisioning, restarts) with no long-term benefit
- SRE target: 50% reactive ops / 50% project and improvement work
- Strategy: Automate toil to free capacity for meaningful reliability work

**Implementation:**
Adopt incrementally. Start with reliable monitoring, then have SLI/SLO conversations with service owners. Don't simply rename job titles; real adoption requires mindset and practice changes.
