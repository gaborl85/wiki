# LLM Wiki Schema & Rules

**This is the constitution of the wiki.** Every operation — ingest, query, lint, update — follows these rules. The wiki is a persistent, compounding artifact maintained by the LLM. Users guide sourcing and questions; the LLM maintains structure and consistency.

---

## Core Principles

1. **Persistent & Compounding** — The wiki is not a chat. Every ingest, query, and update leaves the wiki richer. Knowledge compounds over time.
2. **Sources are Immutable** — Everything in `/sources/` is read-only. The LLM reads from sources but never modifies them.
3. **Research is Living** — Everything in `/research/` is mutable. Pages are updated as new sources arrive, contradictions are flagged, and syntheses are revised.
4. **User Guides, LLM Executes** — User sources documents, asks questions, and guides emphasis. The LLM maintains the wiki structure and consistency.
5. **Consistency > Brilliance** — Predictable structure matters more than perfect prose. Follow conventions religiously.
6. **Each Ingest Touches 10-15 Pages** — A single source update cascades through entity pages, topic pages, and the index. This is intentional and necessary.

---

## Structural Conventions

### Directory Structure

```
/home/wiki/
├── CLAUDE.md                      # This file (schema & rules)
├── sources/                       # Immutable raw sources (by type)
│   ├── books/
│   ├── papers/
│   ├── articles/
│   ├── transcripts/
│   ├── videos/
│   ├── presentations/
│   ├── notes/
│   ├── tools/
│   └── datasets/
├── research/                      # Living knowledge synthesis
│   ├── index.md                  # Catalog of all research pages
│   ├── log.md                    # Chronological activity log
│   ├── entities/                 # People, companies, concepts, tools
│   ├── topics/                   # Emerging themes
│   └── syntheses/                # Keeper pages from queries
├── docs/                          # Curated technical documentation
│   ├── index.md                  # Diátaxis overview
│   ├── tutorials/
│   ├── how-to-guides/
│   ├── explanations/
│   └── reference/
└── docs/superpowers/specs/       # Design documents
```

### Naming Conventions

- **Files:** kebab-case, descriptive (`distributed-systems-taxonomy.md`, not `page-1.md`)
- **Folders:** kebab-case, plural (`entities/`, `topics/`)
- **Source files:** preserve original name if recognizable, else kebab-case with date prefix
- **Cross-references:** `[[page-name]]` (Obsidian-compatible wiki links)

### Front Matter (All Wiki Pages Except index.md and log.md)

Every page starts with YAML front matter:

```yaml
---
title: "Page Title"
created: 2026-06-07
last_updated: 2026-06-07
type: entity|topic|synthesis|guide|explanation|tutorial|how-to|reference
tags: [tag1, tag2]
sources: ["file1.pdf", "file2.md"]
related: ["[[other-page]]", "[[another-page]]"]
---

# Page Title

Content here...
```

**Rationale:** Metadata enables indexing, cross-referencing, source attribution, and update tracking.

---

## Research Area Pages

### Entities (`/research/entities/`)

**Purpose:** A page per distinct entity (Kubernetes, Prometheus, a person, a company, a concept).

**Template:**

```yaml
---
title: "Entity Name"
type: entity
tags: [category]
sources: ["file1.pdf", "file2.md"]
related: ["[[entity2]]", "[[topic1]]"]
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

**When to create:** Whenever an entity appears across multiple sources or is central to understanding a topic.

### Topics (`/research/topics/`)

**Purpose:** A page per emerging theme that connects multiple sources and entities.

**Template:**

```yaml
---
title: "Topic Name"
type: topic
tags: [category]
sources: ["file1.pdf", "file2.md"]
related: ["[[entity1]]", "[[topic2]]"]
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

**When to create:** When multiple sources converge on a theme, or when a query reveals a topic needing its own page.

### Syntheses (`/research/syntheses/`)

**Purpose:** Keeper pages created from queries. A query becomes a synthesis when the analysis is valuable enough to preserve and reference later.

**Template:**

```yaml
---
title: "Question or Analysis Title"
type: synthesis
tags: [category]
sources: ["file1.pdf", "file2.md"]
related: ["[[entity]]", "[[topic]]"]
query_date: 2026-06-07
---

# Question or Analysis Title

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

### Index (`/research/index.md`)

**Purpose:** Content-oriented catalog of all research pages. The LLM reads this first when answering queries to find relevant pages. Updated after every ingest, query with keeper page, or lint pass.

### Log (`/research/log.md`)

**Purpose:** Chronological, append-only record of all wiki activity. Structured for parseability (`grep "^## \[" log.md | tail -5`).

Entry format:
```
## [YYYY-MM-DD] <type> | <title/description>
**Details:** Key metadata (source, mode, pages updated, etc.)
**Tags:** #tag1 #tag2
```

---

## Docs Area Pages

### Diátaxis Structure

- **Tutorials** (`/docs/tutorials/`) — hands-on, learn-by-doing. "How to [action]" with step-by-step instructions.
- **How-to Guides** (`/docs/how-to-guides/`) — solve a specific, real-world problem. "How to [problem]" with practical steps.
- **Explanations** (`/docs/explanations/`) — understand concepts deeply. "Why [concept] works this way" with background and reasoning.
- **Reference** (`/docs/reference/`) — lookup facts, APIs, commands, configurations. Minimal prose, maximum specificity.

### Relationship to Research

- `/docs/` is **fed by** `/research/` — when research reaches a stable synthesis, it can be promoted to `/docs/`.
- **Separate namespaces** — a topic can exist in both areas (exploratory in research, polished in docs) without duplication.
- **Cross-references work both ways** — docs cite research for deep background; research links to docs for practical application.
- **Manual curation** — docs are not automatically generated; user decides when research is ready to curate.

### Index (`/docs/index.md`)

Overview of all documentation, organized by Diátaxis type. Updated as new docs are added.

---

## Workflows

### Supervised Ingest (Hands-On)

1. User provides a source (file or link)
2. LLM reads it, summarizes key takeaways
3. LLM discusses with user: "What stands out? What contradicts existing knowledge? What should we emphasize?"
4. User guides emphasis and connections
5. LLM writes:
   - Source summary (brief notes) in `/sources/<type>/`
   - Updates `/research/index.md`
   - Creates or updates entity pages in `/research/entities/`
   - Creates or updates topic pages in `/research/topics/`
   - Appends entry to `/research/log.md`
6. User reviews updates, requests revisions if needed

**When to use:** Important sources, active exploration, or when guiding emphasis.

**Ingest Summary Template (Internal):**

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

### Batch Ingest (Hands-Off)

1. User accumulates 3-5 sources in `/sources/`
2. User tells LLM: "Batch ingest these"
3. LLM processes all at once:
   - Reads all sources
   - Writes summaries
   - Identifies cross-references and contradictions
   - Updates index and related pages
   - Single log entry capturing all ingests
4. User reviews results afterward, requests updates if needed

**When to use:** Multiple sources accumulated, less engagement desired.

### Query Workflow

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

### Lint Workflow

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

## Summary: How to Use This Wiki

**For Ingests:** Tell me "supervised ingest" or "batch ingest" with sources. I'll read them, discuss takeaways with you, and update the wiki.

**For Queries:** Ask questions about the wiki. I'll search the index, read relevant pages, and give you an answer with citations. If it's valuable, I'll propose a keeper page.

**For Maintenance:** Tell me "lint the research wiki" every 5-10 ingests. I'll check for orphans, contradictions, stale claims, and suggest new topics to explore.

**For Documentation:** As research stabilizes, you decide when to promote pages to `/docs/` using the Diátaxis framework.

**For Updates:** You stay engaged, guide emphasis, and review changes. I maintain structure and consistency.

---

**Version:** 2026-06-07  
**Last Updated:** 2026-06-07
