# Research Index

**Last updated:** 2026-06-12 (4 sources ingested, 11 pages created)

A catalog of all research pages, organized by type. The LLM reads this first when answering queries to find relevant pages.

---

## Entities

- [[Technical Documentation]] — written content explaining products, systems, APIs, processes. Serves developers, customers, and internal teams. (1 source, created 2026-06-07)
- [[Diátaxis Framework]] — pragmatic documentation framework organizing content into four types (Tutorials, How-to Guides, Reference, Explanation) along two axes (Action/Cognition, Study/Work). (1 source, created 2026-06-07)
- [[Site Reliability Engineering]] — engineering discipline for achieving appropriate, sustainable reliability. Origins at Google. Core practices: SLI/SLO/Error Budgets, blameless postmortems, toil elimination. (1 source, created 2026-06-11)
- [[fwupd]] — Linux firmware update tool/daemon for staging firmware capsules to EFI System Partition. Requires write access to ESP; fails with permission denied on read-only partitions. (1 source, created 2026-06-12)
- [[EFI System Partition]] — Special-purpose FAT32 partition on UEFI systems for storing boot loaders and firmware updates. Critical for firmware update staging; often mounted read-only for safety. (1 source, created 2026-06-12)
- [[Ubuntu Snapd Architecture]] — Immutable system architecture using read-only seed partition for transactional updates. Design constraint affecting firmware updates and direct system modifications. (1 source, created 2026-06-12)

---

## Topics

- [[Documentation Best Practices]] — 10 core practices for creating useful, accurate, maintainable documentation. Applies to product docs, developer docs, process docs, and personal knowledge bases. (1 source, created 2026-06-07)
- [[Technical Documentation Writing Process]] — 8-step iterative process from audience definition through maintenance. Covers research, structure, writing, review, measurement, and updates. (1 source, created 2026-06-07)
- [[Diátaxis and Best Practices]] — How the Diátaxis framework (structure) and best practices (execution) work together. Shows how each best practice applies to each documentation type. (2 sources, created 2026-06-07)
- [[Documentation Taxonomies]] — Two complementary systems: GitBook's audience-based (Product/Developer/Process) and Diátaxis's task-based (Tutorials/How-to/Reference/Explanation). How they work together. (2 sources, created 2026-06-07)
- [[Systematic Linux Troubleshooting Methodology]] — Structured approach to diagnosing Linux failures: distinguish symptom from root cause, verify assumptions layer by layer, use tools to expose actual state. Key principle: trace through system layers to find root cause, not just the symptom. (1 source, created 2026-06-12)

---

## Syntheses (Keeper Pages)

- [[fwupd permission denied case study|fwupd-permission-denied-case-study]] — Firmware update failure on Ubuntu Snapd system: fwupd fails to stage firmware to read-only EFI partition. Full investigation demonstrates systematic troubleshooting methodology, from symptom to root cause (read-only ESP mount by design). Includes diagnosis steps, root cause analysis, and remediation trade-offs. (1 source, created 2026-06-12)

---

## By Source Type

- **Books:** 0 sources
- **Papers:** 0 sources
- **Articles:** 3 sources (GitBook: Technical Documentation guide, Diátaxis: Start here, Microsoft Learn: Intro to SRE)
- **Transcripts:** 0 sources
- **Videos:** 0 sources
- **Presentations:** 0 sources
- **Personal notes:** 1 source (fwupd troubleshooting case study)
- **Tools:** 0 sources
- **Datasets:** 0 sources

**Total:** 4 sources

---

## Recent Updates

- 2026-06-12: Supervised ingest of fwupd troubleshooting case study → 1 synthesis, 3 entities, 1 topic
  - [[fwupd-permission-denied-case-study]] (synthesis) — demonstrates systematic troubleshooting methodology
  - [[fwupd]], [[EFI System Partition]], [[Ubuntu Snapd Architecture]] (entities)
  - [[Systematic Linux Troubleshooting Methodology]] (topic)

- 2026-06-11: Supervised ingest of Microsoft Learn SRE Introduction → 1 entity
  - [[Site Reliability Engineering]] (entity) — definition, core principles, virtuous cycles, toil elimination, implementation strategy

- 2026-06-07: Created [[Documentation Taxonomies]] topic (synthesis)
  - Clarified the two type systems: audience-based (GitBook) vs. task-based (Diátaxis)
  - Showed how they work together and are orthogonal, not contradictory
  
- 2026-06-07: Added missing cross-references
  - documentation-best-practices.md now links to Diátaxis pages
  - technical-documentation-writing-process.md now links to Diátaxis pages

- 2026-06-07: Supervised ingest of Diátaxis "Start here" article → 1 entity, 1 topic
  - [[Diátaxis Framework]] (entity)
  - [[Diátaxis and Best Practices]] (topic)

- 2026-06-07: Supervised ingest of GitBook "Technical Documentation" article → 1 entity, 2 topics
  - [[Technical Documentation]] (entity)
  - [[Documentation Best Practices]] (topic)
  - [[Technical Documentation Writing Process]] (topic)
