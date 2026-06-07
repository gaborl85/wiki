---
title: "Documentation Taxonomies"
type: topic
created: 2026-06-07
last_updated: 2026-06-07
tags: [documentation, framework, taxonomy, categorization]
sources: ["What is technical documentation_ Examples, templates and how to write it – GitBook Blog.md", "Start here - Diátaxis in five minutes - Diátaxis.md"]
related: ["[[Technical Documentation]]", "[[Diátaxis Framework]]", "[[Documentation Best Practices]]"]
---

# Documentation Taxonomies

## Definition

Two complementary systems for categorizing documentation that serve different organizational purposes. Understanding both systems and how they relate prevents confusion and enables better documentation strategy.

## System 1: Audience-Based Taxonomy (GitBook)

**Question it answers:** "Who is this documentation for?"

### The Three Types

**Product Documentation**
- Serves: Customers/end users
- Purpose: Helps people use the product
- Focus: Tasks, workflows, troubleshooting, feature education
- Examples: User guides, manuals, knowledge bases, FAQs, release notes, troubleshooting docs
- Audience: Often less technical, focuses on outcomes

**Developer Documentation**
- Serves: Technical developers/engineers building on top of systems
- Purpose: Helps people build with or integrate with the product
- Focus: APIs, SDKs, integrations, architecture, technical specifications
- Examples: API docs, SDK guides, integration guides, architecture documentation, code samples
- Audience: Highly technical, assumes programming knowledge

**Process Documentation**
- Serves: Internal teams
- Purpose: Explains how the organization works
- Focus: Decision-making, planning, building, reviewing, maintaining
- Examples: PRDs, RFCs, runbooks, design system rules, project plans, technical briefs
- Audience: Mix of technical and non-technical internal stakeholders

### Characteristics

- **Audience-centric** — Starts with "who will read this?"
- **Organizational** — Reflects how the company structures knowledge
- **Output-focused** — Different types serve different user outcomes
- **Scalable** — Works for small teams and large organizations
- **Practical** — Helps teams decide "which folder does this go in?"

---

## System 2: Task-Based Taxonomy (Diátaxis)

**Question it answers:** "What task is the reader trying to accomplish?"

### The Four Types

**Tutorials**
- Reader's goal: Learn by doing
- Reader's mindset: "Teach me"
- Axis: Action + Study (act to build skill)
- Characteristics: Guided, hands-on, confidence-building
- Examples: "Let's build a game in Python", "Your first API call"

**How-to Guides**
- Reader's goal: Solve a specific problem
- Reader's mindset: "Help me do this"
- Axis: Action + Work (act to get work done)
- Characteristics: Task-focused, assumes competence, outcome-oriented
- Examples: "How to deploy to production", "Configure SSL certificates"

**Reference**
- Reader's goal: Look up facts
- Reader's mindset: "Tell me the specifics"
- Axis: Cognition + Work (understand to get work done)
- Characteristics: Accurate, complete, neutral, mirror the structure of what's described
- Examples: API reference, command line options, configuration parameters

**Explanation**
- Reader's goal: Understand why something works
- Reader's mindset: "Help me understand"
- Axis: Cognition + Study (understand to build knowledge)
- Characteristics: Explores in depth, explores context, explains reasoning
- Examples: "How the CAP theorem applies to our system", "Why we chose microservices"

### Characteristics

- **Reader-journey-centric** — Starts with "what is the reader trying to do right now?"
- **Universal** — Works the same way for any documentation domain
- **Pragmatic** — Implementation is iterative, not top-down
- **Psychological** — Based on how readers actually use documentation
- **Flexible** — Can be applied at any scale

---

## Comparison: System 1 vs. System 2

| Aspect | Audience-Based (GitBook) | Task-Based (Diátaxis) |
|--------|--------------------------|----------------------|
| **Organizing principle** | Who reads it? | What task are they doing? |
| **Number of categories** | 3 (Product, Developer, Process) | 4 (Tutorials, How-to, Reference, Explanation) |
| **Scope** | Organizational structure | Reader's moment-to-moment needs |
| **When to use** | Organizing documentation infrastructure | Organizing individual pages |
| **Scale** | Macro (entire docs system) | Micro to macro (pages and systems) |
| **Primary question** | "Which team uses this?" | "What is the reader's current goal?" |

---

## How They Work Together

### They Operate at Different Levels

**GitBook's taxonomy is macro-level:**
- It describes entire documentation areas or systems
- "We have product docs (for customers), developer docs (for integrators), and process docs (for teams)"
- Answers: How should we organize our documentation across teams and audiences?

**Diátaxis's taxonomy is micro-to-macro level:**
- It describes the structure of individual pages and can scale to entire systems
- "This page is a tutorial. This page is a how-to guide. This section is reference material."
- Answers: What type of content best serves the reader right now?

### Common Scenarios

**Product Documentation (GitBook) consists of:**
- Tutorials for customers learning features
- How-to guides for solving common customer problems
- Reference documentation (FAQs, commands, options)
- Explanations (why a feature works a certain way)

→ **All four Diátaxis types can exist within "Product Documentation"**

**Developer Documentation (GitBook) consists of:**
- Tutorials (getting started, learning the API)
- How-to guides (integrating with a specific framework, troubleshooting)
- Reference (API endpoints, error codes)
- Explanations (architectural decisions, design rationale)

→ **All four Diátaxis types can exist within "Developer Documentation"**

**Process Documentation (GitBook) consists of:**
- Tutorials (onboarding new team members)
- How-to guides (how to run a meeting, deploy a release)
- Reference (decision records, approved vendors)
- Explanations (why we make decisions this way, company values)

→ **All four Diátaxis types can exist within "Process Documentation"**

### Practical Example: Error Budgets

**Using GitBook's taxonomy (audience-based):**
- **Product Doc:** "Understanding Error Budgets" (for customers managing uptime expectations)
- **Developer Doc:** "Error Budget API" (for engineers building on top of the platform)
- **Process Doc:** "Our Error Budget Policy" (for internal teams deciding on SLOs)

**Using Diátaxis's taxonomy (task-based):**
- **Tutorial:** "Understanding Error Budgets: A Hands-On Introduction" (learn the concept by calculating one)
- **How-to:** "Set Your Service's Error Budget" (solve the problem: I need to decide my SLO)
- **Reference:** "Error Budget Formula and Calculation" (look up the math and parameters)
- **Explanation:** "Why Error Budgets Matter" (understand the philosophy and reasoning)

**Combined approach:**
- Product docs use Diátaxis structure internally (tutorials for onboarding, reference for quick lookup, etc.)
- Developer docs use Diátaxis structure internally
- Process docs use Diátaxis structure internally

---

## When to Use Which System

### Use GitBook's Audience-Based Taxonomy When:

- You're organizing documentation across multiple teams or audiences
- You need to decide how to split documentation infrastructure
- You're explaining "what documentation does our organization have?"
- You're staffing documentation work ("who owns customer docs vs. process docs?")

**Question to ask:** "Who is the primary audience for this documentation area?"

### Use Diátaxis's Task-Based Taxonomy When:

- You're writing or organizing a single page or page group
- You need to decide what type of content serves a specific reader need
- You're explaining "what is this page trying to help the reader do?"
- You're auditing documentation for clarity and completeness

**Question to ask:** "What is the reader trying to accomplish right now?"

---

## Key Insight: They're Orthogonal

These taxonomies are **orthogonal** — they describe different dimensions of documentation and don't contradict each other. A single page can be:

- **Audience:** Product documentation (for customers)
- **Task:** Tutorial (teaching by doing)

Or:

- **Audience:** Developer documentation (for engineers)
- **Task:** Reference (lookup material)

Both descriptions are true and useful. The audience-based taxonomy tells you who it's for; the task-based taxonomy tells you how it works.

---

## Synthesis: A Complete Documentation Strategy

**Complete documentation strategy uses both:**

1. **GitBook's audience taxonomy** to structure your documentation infrastructure and teams
2. **Diátaxis's task taxonomy** to structure pages and content within each audience area
3. **Best practices** to execute each page type well

**Structure:**
```
Documentation System (GitBook)
├── Product Documentation
│   ├── Tutorials (Diátaxis)
│   ├── How-to Guides (Diátaxis)
│   ├── Reference (Diátaxis)
│   └── Explanations (Diátaxis)
├── Developer Documentation
│   ├── Tutorials (Diátaxis)
│   ├── How-to Guides (Diátaxis)
│   ├── Reference (Diátaxis)
│   └── Explanations (Diátaxis)
└── Process Documentation
    ├── Tutorials (Diátaxis)
    ├── How-to Guides (Diátaxis)
    ├── Reference (Diátaxis)
    └── Explanations (Diátaxis)
```

All pages within each section follow best practices (clear headings, examples, consistent terminology, etc.)

---

## Open Questions

- How much can one page serve multiple audiences? (e.g., a tutorial for both customers and developers)
- Should a documentation system be organized primarily by GitBook's audience taxonomy or Diátaxis's task taxonomy?
- When do you nest Diátaxis types? (e.g., a how-to guide that contains mini-tutorials within it)
- How do these taxonomies apply to non-textual documentation (videos, diagrams, interactive tools)?
