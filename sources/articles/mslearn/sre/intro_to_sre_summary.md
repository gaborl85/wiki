---
title: Intro to Site Reliability Engineering - Training Summary
source: Microsoft Learn
url: https://learn.microsoft.com/en-us/training/modules/intro-to-site-reliability-engineering/
author: Orin Thomas
date: 2026-06-11
---

# Summary

Five-part foundational training on SRE fundamentals covering definition, context, core practices, and implementation.

**Core Definition:**
Site Reliability Engineering is an engineering discipline devoted to helping an organization sustainably achieve the appropriate level of reliability in their systems, services, and products.

**Key Takeaways:**
- Reliability is the focus (not performance, efficiency, or cost)
- "Appropriate" reliability is pragmatic—based on business needs, not perfection
- Sustainability matters for people doing the work (preventing burnout, unsustainable on-call)
- SRE originated at Google in 2003; distinct from DevOps but shares automation + observability
- Implementation is incremental: start with monitoring, then SLI/SLO conversations

**Two Virtuous Cycles:**
1. SLI/SLO/Error Budgets: Define health indicators → set reliability targets → use error budget for managed risk-taking
2. Blameless Postmortems: Learn from incidents by blaming systems/processes, not people

**Toil Elimination:**
Target allocation: 50% reactive ops work, 50% project/improvement work. Automate repetitive, manual, low-value tasks.
