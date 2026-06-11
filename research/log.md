# Research Activity Log

**Chronological record of all wiki activity.** Append-only. Structured for parseability: `grep "^## \[" log.md | tail -5` shows recent entries.

---

## [2026-06-11] ingest | Intro to Site Reliability Engineering (articles)

**Source:** articles/mslearn/sre/Develop_a_Site_Reliability_Engineering_strategy/intro_to_sre/ (5 training modules)  
**Author:** Orin Thomas (Microsoft Learn)

**Key takeaways:**
- SRE is an engineering discipline for achieving *appropriate* (not perfect), *sustainable* reliability
- Three pillars: Reliability focus, Appropriate/pragmatic levels, Sustainability for people
- Originated at Google in 2003 as "what a software engineer would design for operations"
- Two virtuous cycles: (1) SLI/SLO/Error Budgets, (2) Blameless Postmortems
- Toil elimination: target 50% reactive ops / 50% project work
- Incremental implementation: start with monitoring, then SLI/SLO conversations

**Pages created:**
- [[Site Reliability Engineering]] (entity) — comprehensive overview of definition, core principles, key practices, and implementation strategy

**Connections & insights:**
- Fresh area; no prior SRE coverage in wiki
- Foundational material suitable as reference for future SRE-related queries
- Complements existing [[Technical Documentation]] and [[Documentation Taxonomies]] work with operational/reliability focus

**Tags:** #sre #operations #reliability #virtuous-cycles #toil

---

## [2026-06-07] synthesis | Documentation Taxonomies

**Event:** Created synthesis topic clarifying the relationship between two documentation type systems  
**Trigger:** Lint pass identified potential contradiction between GitBook's 3 types and Diátaxis's 4 types

**Key insight:** The two systems are orthogonal, not contradictory:
- **GitBook's audience-based taxonomy** (Product/Developer/Process) answers "Who reads this?"
- **Diátaxis's task-based taxonomy** (Tutorials/How-to/Reference/Explanation) answers "What is the reader doing?"

**Synthesis shows:**
- Both systems operate at different organizational levels (macro vs. micro)
- They work together: each Diátaxis type can exist within each GitBook audience category
- Practical example: how "Error Budgets" becomes 3 audience-based docs + 4 task-based pages
- When to use each system (infrastructure vs. content design)
- Complete documentation strategy uses both + best practices

**Pages referenced:** 
- [[Technical Documentation]] — provides the GitBook 3-type framework
- [[Diátaxis Framework]] — provides the 4-type framework
- [[Documentation Best Practices]] — execution layer for both systems

**Status:** Resolved the apparent contradiction. Wiki is now coherent across three levels:
1. What documentation is (Technical Documentation entity)
2. How to structure it (Diátaxis Framework entity + taxonomies topic)
3. How to write it well (Best Practices + Writing Process topics)

**Tags:** #taxonomy #framework #synthesis #contradiction-resolved

---

## [2026-06-07] ingest | Start here - Diátaxis in five minutes (article)

**Source:** articles/Start here - Diátaxis in five minutes - Diátaxis.md  
**Key takeaways:**
- Diátaxis organizes documentation into four types: Tutorials, How-to Guides, Reference, Explanation
- Organized along two axes: Action/Cognition + Study/Work
- Pragmatic framework emphasizing iteration over theory
- Four-step implementation: examine → identify → select → execute

**Pages created:**
- [[Diátaxis Framework]] (entity) — the framework, four types, two axes, implementation approach
- [[Diátaxis and Best Practices]] (topic) — how Diátaxis structure and best practices work together

**Connections & insights:**
- Fills coverage gap from previous lint pass
- Complements [[Documentation Best Practices]] — Diátaxis answers "what type?" while best practices answer "how to write?"
- Four types naturally map to reader needs at different stages
- Framework aligns with the wiki's own `/docs/` structure (tutorials, how-to-guides, explanations, reference)
- Shows how [[Technical Documentation]] types map to Diátaxis

**Notes:**
- Source was partial (stub file); fetched full content from https://diataxis.fr/start-here/
- Added [[Daniele Procida]] as author in entity metadata

**Tags:** #diataxis #documentation #framework #structure

---

## [2026-06-07] ingest | What is technical documentation? (article)

**Source:** articles/What is technical documentation_ Examples, templates and how to write it – GitBook Blog.md  
**Key takeaways:**
- Technical documentation answers "What is this?", "How does it work?", "What do I do next?"
- Serves three audiences: developers, customers, internal teams
- Three main types: product docs, developer docs, process docs
- 10 best practices for all documentation contexts
- 8-step iterative writing process

**Pages created:**
- [[Technical Documentation]] (entity) — definition, audiences, types, key characteristics
- [[Documentation Best Practices]] (topic) — 10 practices and how they relate to Diátaxis framework
- [[Technical Documentation Writing Process]] (topic) — 8-step process from audience definition through maintenance

**Updated pages:**
- research/index.md — added entity, topics, updated source count and recent activity

**Connections:**
- Best practices are universal across product docs, developer docs, process docs, and personal knowledge bases
- Best practices align with Diátaxis framework (Tutorials, How-to Guides, Explanations, Reference)
- Writing process is iterative and collaborative

**Tags:** #documentation #writing #best-practices #process
