# LLM Wiki Design Specification

**Date:** 2026-06-07  
**Author:** Brainstorming session with Claude Code  
**Status:** Approved design, ready for implementation

---

## Executive Summary

This document describes the architecture and workflows for a persistent, LLM-maintained personal knowledge base. The wiki is organized into two separate areas — `/research/` for exploratory knowledge (research deep-dives, reading notes, syntheses) and `/docs/` for curated technical documentation (Diátaxis framework). Knowledge is sourced from books, papers, articles, transcripts, videos, presentations, personal notes, tools, and datasets, all stored in version control. The LLM incrementally builds and maintains the wiki, updating entity pages, revising topics, and integrating new sources. Users stay engaged through guided ingest workflows, flexible query modes, and periodic health checks (linting). The wiki compounds over time — each source update touches 10-15 pages, cross-references are maintained, contradictions are flagged, and the wiki grows richer with every addition.

---

## 1. Directory Structure & Conventions

### 1.1 High-Level Layout

```
/home/wiki/
├── .git/
├── .gitignore
├── CLAUDE.md                  # Schema, rules, workflows
├── sources/                   # Immutable raw sources
│   ├── books/
│   ├── papers/
│   ├── articles/
│   ├── transcripts/
│   ├── videos/
│   ├── presentations/
│   ├── notes/
│   ├── tools/
│   └── datasets/
├── research/                  # Exploratory knowledge synthesis
│   ├── index.md              # Research index & catalog
│   ├── log.md                # Chronological activity log
│   ├── entities/             # People, companies, concepts, tools
│   ├── topics/               # Emerging topics from synthesis
│   └── syntheses/            # Keeper pages from queries
├── docs/                      # Curated technical documentation
│   ├── index.md              # Docs index (Diátaxis overview)
│   ├── tutorials/            # Hands-on, learn-by-doing
│   ├── how-to-guides/        # Solve a specific problem
│   ├── explanations/         # Understand concepts deeply
│   └── reference/            # Lookup facts, APIs, commands
└── docs/superpowers/specs/   # Design documents
```

### 1.2 Naming Conventions

- **Files:** kebab-case, descriptive (`distributed-systems-taxonomy.md`, not `page-1.md`)
- **Folders:** kebab-case, plural when collections (`topics/`, `entities/`)
- **Source files:** preserve original filename if recognizable (e.g., `2026_SRE_Workbook.pdf`), else kebab-case with date prefix
- **Cross-references:** `[[page-name]]` wiki links (Obsidian-compatible)

### 1.3 Immutability & Mutability

- **Immutable:** Everything in `/sources/` — raw documents, transcripts, PDFs, datasets. The LLM reads from these but never modifies them.
- **Mutable:** Everything in `/research/` and `/docs/` — the LLM maintains these, updating pages when new sources arrive, integrating contradictions, revising syntheses.

---

## 2. Front Matter & Metadata Standards

Every wiki page (except index.md and log.md) begins with YAML front matter:

```yaml
---
title: "Page Title"
created: 2026-06-07
last_updated: 2026-06-07
type: entity|topic|synthesis|guide|explanation  # page type
tags: [tag1, tag2, tag3]
sources: ["source-file-1.md", "source-file-2.pdf"]  # files from /sources/
related: ["[[other-page]]", "[[another-page]]"]  # internal wiki links
---

# Page Title

Content here...
```

**Rationale:** Front matter provides metadata for indexing, tracking updates, and maintaining citations back to sources.

---

## 3. Research Area (`/research/`)

### 3.1 Purpose

The research area is **exploratory and living**. It contains:
- **Summaries** of ingested sources (what we learned)
- **Entity pages** (people, companies, tools, concepts — what are they, what do they do, roles)
- **Topic pages** (emerging themes — what connects sources, where do they contradict, what's unclear)
- **Synthesis pages** (keeper pages from queries — valuable analyses, comparisons, implications)

### 3.2 Entities (`/research/entities/`)

**Purpose:** A page per distinct entity (Kubernetes, Prometheus, a person, a company, a concept).

**Format:**

```yaml
---
title: "Entity Name"
type: entity
tags: [category-tag]
sources: ["file1.pdf", "file2.md"]
related: [[[entity2]], [[topic1]]]
---

# Entity Name

**What is it?** 1-2 sentence definition.

**Key characteristics:**
- Characteristic 1
- Characteristic 2

**Role in [topic1]:** How it relates to broader topics.

**Mentions in sources:** Which sources mention it and in what context.

**Contradictions/gaps:** Any conflicting claims or missing information.
```

**When to create:** Whenever a distinct entity (person, tool, concept) appears across multiple sources or is central to understanding a topic. One entity = one page.

### 3.3 Topics (`/research/topics/`)

**Purpose:** A page per emerging theme that connects multiple sources and entities.

**Format:**

```yaml
---
title: "Topic Name"
type: topic
tags: [category]
sources: ["file1.pdf", "file2.md", "file3.md"]
related: [[[entity1]], [[entity2]], [[topic2]]]
---

# Topic Name

**Definition:** What is this topic? Why does it matter?

**Key concepts:**
- Concept A: definition
- Concept B: definition

**Entities & their roles:**
- [[Entity1]]: role in this topic
- [[Entity2]]: role in this topic

**Synthesis:** What do the sources say collectively? What's the current understanding?

**Contradictions:** Where do sources disagree? What's unresolved?

**Open questions:** What's unclear? What would we need to know more about?

**Related topics:** [[other-topic]], [[another-topic]]
```

**When to create:** When multiple sources converge on a theme, or when you query about a topic that doesn't yet have a page.

### 3.4 Syntheses (`/research/syntheses/`)

**Purpose:** Keeper pages created from queries. A query becomes a synthesis when the analysis is valuable enough to preserve and reference later.

**Format:**

```yaml
---
title: "Question or Analysis Title"
type: synthesis
tags: [category]
sources: [list of sourced files]
related: [list of related pages]
query_date: 2026-06-07
---

# [Question/Analysis Title]

**Question:** What was asked?

**Answer:** [detailed synthesis with citations]

**Key findings:**
- Finding 1: [[source-entity]]
- Finding 2: [[source-topic]]

**Implications:** What does this mean? How does it apply?

**Related pages:** [[entity]], [[topic]]

**Open questions:** What wasn't answered? What follow-ups exist?
```

**When to create:** On user request during a query, or when the LLM recognizes a synthesis valuable enough to keep.

### 3.5 Index (`/research/index.md`)

**Purpose:** Content-oriented catalog of all research pages. The LLM reads this first when answering queries to find relevant pages.

**Format:**

```markdown
# Research Index

## Entities
- [[Kubernetes]] — container orchestration platform (12 sources, last updated 2026-06-07)
- [[Prometheus]] — metrics monitoring tool (5 sources, updated 2026-06-05)
- [[SRE]] — concept: reliability engineering practices (8 sources, updated 2026-06-07)
- ...

## Topics
- [[SRE Principles]] — error budgets, incident response, reliability goals (12 sources)
- [[Distributed Systems]] — challenges, consensus, consistency models (8 sources)
- [[Observability]] — metrics, logs, traces, and their relationships (6 sources)
- ...

## Syntheses (Keeper Pages)
- [[Chaos Engineering and Resilience]] — relationship to error budgets (2026-06-05)
- [[Observability in SRE]] — how they connect (2026-06-01)
- ...

## By Source Type
- **Books:** 7 sources
- **Papers:** 12 sources
- **Articles:** 23 sources
- **Transcripts:** 4 sources
- **Videos:** 3 sources
- **Presentations:** 2 sources
- **Personal notes:** 5 sources
- **Tools:** 1 source
- **Datasets:** 0 sources

## Recent Updates
- 2026-06-07: Ingested "The Site Reliability Workbook" (book)
- 2026-06-05: Queried "How do chaos engineering and error budgets relate?" → synthesis page created
- 2026-06-01: Linted research area → 2 orphans found and fixed
```

**Update frequency:** After every ingest, query with keeper page, or lint pass.

### 3.6 Log (`/research/log.md`)

**Purpose:** Chronological, append-only record of all wiki activity. Structured for parseability (`grep "^## \[" log.md | tail -5`).

**Format:**

```markdown
# Research Activity Log

## [2026-06-07] ingest | The Site Reliability Workbook (book)
**Source:** books/2026-SRE-Workbook.pdf  
**Key sections:** Incident response, error budgets, SLOs, monitoring strategy  
**Updated pages:** SRE (entity), SRE Principles (topic)  
**New connections:** Error budgets framework added to [[SRE Principles]]  
**Tags:** #sre #reliability

## [2026-06-05] query | How do chaos engineering and error budgets relate?
**Mode:** Supervised  
**Keeper page:** [[Chaos Engineering and Resilience]]  
**Sources cited:** Papers on chaos engineering, [[SRE Principles]] page  
**Tags:** #chaos-engineering #sre

## [2026-06-01] lint | Research health check
**Orphans found:** 2 (fixed by adding cross-references)  
**Contradictions flagged:** 1 (distributed systems consistency — needs resolution)  
**Stale claims:** 0  
**Missing coverage:** Suggested new topic "Observability deep-dive"  
**Tags:** #maintenance
```

**Entry format:**
```
## [YYYY-MM-DD] <type> | <title/description>
**Details:** Key metadata (source, mode, pages updated, etc.)
**Tags:** #tag1 #tag2
```

**Update frequency:** After every ingest, query with keeper page, or lint pass.

---

## 4. Docs Area (`/docs/`)

### 4.1 Purpose

Curated, public-facing technical documentation following the Diátaxis framework. Separate from research but fed by it. Starts empty, filled as research stabilizes.

### 4.2 Structure

- **Tutorials** (`/docs/tutorials/`) — hands-on, learn-by-doing. "How to [action]" with step-by-step instructions.
- **How-to Guides** (`/docs/how-to-guides/`) — solve a specific, real-world problem. "How to [problem]" with practical steps.
- **Explanations** (`/docs/explanations/`) — understand concepts deeply. "Why [concept] works this way" with background and reasoning.
- **Reference** (`/docs/reference/`) — lookup facts, APIs, commands, configurations. Minimal prose, maximum specificity.

### 4.3 Relationship to Research

- `/docs/` is **fed by** `/research/` — stable research syntheses can be promoted to docs.
- **Separate namespaces** — a topic can exist in both (exploratory in research, polished in docs) without duplication.
- **Cross-references work both ways** — docs cite research for deep background; research links to docs for practical application.
- **Manual curation** — docs are not automatically generated; user decides when research is ready to curate.

### 4.4 Index (`/docs/index.md`)

Overview of all documentation, organized by Diátaxis type. Updated as new docs are added.

---

## 5. CLAUDE.md Schema

The CLAUDE.md file contains:

### 5.1 Core Principles
- The wiki is a persistent, compounding artifact
- Sources are immutable; research synthesis is living
- LLM maintains the wiki; user guides sourcing and questions
- Consistency over brilliance — predictable structure matters
- Knowledge compounds — each ingest touches 10-15 pages

### 5.2 Structural Rules
- Immutable sources (`/sources/`) organized by type
- Research entities/topics/syntheses are living, updated as new sources arrive
- Front matter standards for all wiki pages
- Naming conventions (kebab-case, descriptive)
- Cross-referencing conventions (`[[page-name]]`)
- When to create entities vs. topics vs. syntheses

### 5.3 Ingest Workflows

#### 5.3.1 Supervised Ingest (Hands-On)
1. User provides a source (file or link)
2. LLM reads it, summarizes key takeaways
3. LLM discusses with user: "What stands out? What contradicts existing knowledge? What should we emphasize?"
4. User guides emphasis and connections
5. LLM writes:
   - Source summary in `/sources/<type>/`
   - Updates `/research/index.md`
   - Creates or updates entity pages in `/research/entities/`
   - Creates or updates topic pages in `/research/topics/`
   - Appends entry to `/research/log.md`
6. User reviews updates (in Obsidian or editor), requests revisions if needed

**Guidance:** Use for important sources, when you want to guide emphasis, or when you're actively exploring a topic.

#### 5.3.2 Batch Ingest (Hands-Off)
1. User accumulates 3-5 sources in `/sources/`
2. User tells LLM: "Batch ingest these" (with minimal guidance)
3. LLM processes all at once:
   - Reads all sources
   - Writes summaries
   - Identifies cross-references and contradictions
   - Updates index and related pages
   - Single log entry capturing all ingests
4. User reviews results afterward, requests updates if needed

**Guidance:** Use when you want to accumulate sources without engagement, then process together.

#### 5.3.3 Template: Supervised Ingest Summary

LLM produces this internally before writing pages:

```
Source: [filename, source type, date]
Title: [source title]

Key takeaways:
- [takeaway 1]
- [takeaway 2]
- [takeaway 3]

Entities mentioned: [list]
Topics relevant to: [list]

Contradictions with existing knowledge: [list or "none"]

New cross-references to add: [list]

Pages to create/update:
- [page 1 reason]
- [page 2 reason]
```

### 5.4 Query Workflow

1. User asks a question (e.g., "What's the relationship between observability and error budgets?")
2. LLM searches `/research/index.md` to identify relevant pages
3. LLM reads them, synthesizes an answer with citations
4. LLM proposes: keeper page (valuable synthesis) or conversation-only (exploratory)
5. User decides
6. If keeper: LLM files page in `/research/syntheses/`, updates index, logs entry
7. If conversation-only: log entry notes it was a query, not a keeper page

**Keeper page criteria:**
- Synthesis is valuable and reusable (not a one-off answer)
- Connects multiple sources or entities in a new way
- Likely to be referenced in future queries

### 5.5 Lint Workflow

Run every 5-10 ingests to keep the wiki healthy.

1. User asks: "Lint the research wiki"
2. LLM scans all pages for:
   - **Orphans:** Pages with no inbound links (suggest connections or deletion)
   - **Contradictions:** Conflicting claims across pages (flag for user to resolve)
   - **Stale claims:** Old information superseded by newer sources (update or remove)
   - **Missing cross-references:** Related pages not linked (add links)
   - **Coverage gaps:** Topics mentioned but lacking their own page (suggest creation)
3. LLM reports findings and suggests new pages to research or questions to explore
4. User reviews, decides what to investigate next
5. Log entry documents the lint pass

---

## 6. Knowledge Domains

The wiki will accumulate knowledge in three primary domains:

1. **Research deep-dives** — topics like SRE, Cloud Engineering, and other specialized areas explored over weeks or months
2. **Reading notes** — syntheses from books, papers, articles, transcripts, videos, presentations
3. **Technical documentation** — curated Diátaxis-style guides and references

Sources come from:
- Books
- Papers
- Articles & blog posts
- Transcripts (podcasts, interviews, talks)
- Videos
- Presentations & slides
- Personal notes & observations
- Tools & projects studied
- Datasets & reports

---

## 7. Workflows Summary

| Workflow | When to Use | Output | Result |
|----------|------------|--------|--------|
| **Supervised Ingest** | Important sources, active exploration | Source summary, updated entity/topic pages | User guided, high engagement |
| **Batch Ingest** | Multiple sources accumulated | Source summaries, batch updates | Fast, less engagement |
| **Query** | Ask a question about the wiki | Answer with citations, optionally keeper page | Exploratory or compounding |
| **Lint** | Every 5-10 ingests | Health report, suggested improvements | Maintains consistency, finds gaps |
| **Docs Promotion** | When research is stable and curated | New Diátaxis-format page in `/docs/` | Polished, public-facing knowledge |

---

## 8. Scope & Assumptions

**In scope:**
- Personal knowledge base for research, reading notes, and technical documentation
- LLM-driven maintenance and synthesis
- Git-based version control
- Obsidian-compatible markdown and wiki links

**Out of scope:**
- Collaborative editing (single user)
- Real-time sync or cloud storage
- Full-text search beyond grep and index.md navigation
- Automatic embedding-based retrieval (index.md is sufficient for moderate scale ~100 sources)

**Assumptions:**
- User will actively source documents and guide ingests
- User will periodically review and lint the wiki
- LLM will follow CLAUDE.md rules consistently
- Obsidian is the primary IDE for browsing and editing

---

## 9. Implementation Plan Next Steps

1. **Setup:** Create folder structure, initialize CLAUDE.md, write index.md and log.md templates
2. **First ingest:** Walk through a supervised ingest workflow end-to-end to validate approach
3. **Establish patterns:** Refine templates and rules based on first ingest
4. **Scale:** Batch ingest additional sources, run lint passes periodically

---

## 10. Success Criteria

- [ ] Directory structure created and documented
- [ ] CLAUDE.md written with clear rules and workflows
- [ ] index.md and log.md initialized
- [ ] First supervised ingest completed successfully
- [ ] Cross-references and updates working as expected
- [ ] User can navigate and query the wiki effectively
- [ ] Lint workflow identifies and fixes issues

---

**Design approved:** 2026-06-07  
**Ready for:** Implementation planning and first ingest
