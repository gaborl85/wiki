---
title: "Diátaxis Framework"
type: entity
created: 2026-06-07
last_updated: 2026-06-07
tags: [documentation, framework, structure]
sources: ["Start here - Diátaxis in five minutes - Diátaxis.md"]
related: ["[[Technical Documentation]]", "[[Documentation Best Practices]]", "[[Diátaxis and Best Practices]]"]
---

# Diátaxis Framework

## What is it?

Diátaxis is a pragmatic approach to documentation that organizes content into four distinct types, each serving a different reader need at a different stage of their journey. Rather than treating documentation as a monolithic body of text, Diátaxis recognizes that readers have different goals — sometimes they're learning, sometimes they're working; sometimes they need to understand concepts, sometimes they need to accomplish tasks.

**Core principle:** "The user will learn through what they do—not because someone has tried to teach them." Documentation should be structured around reader goals, not around the product.

## The Four Documentation Types

### 1. Tutorials

**Purpose:** Skill-building through guided, structured learning experiences.

**Characteristics:**
- Instructor guides the learner through practical tasks
- Focus is on confidence-building and skill acquisition, not task completion
- Reader is a beginner with no prior knowledge assumed
- The experience itself teaches, not explanation

**When to use:** "Let me teach you how to do this."

**Example:** "Let's create a simple game in Python"

**Reader mindset:** Learning mode. "Show me how."

### 2. How-to Guides

**Purpose:** Solve specific, real-world problems for users who already have foundational knowledge.

**Characteristics:**
- Addressed to competent users with existing expertise
- Focus is on accomplishing work, not learning concepts
- Reader brings sufficient knowledge to interpret and apply guidance
- Assumes familiarity with fundamentals
- Often includes troubleshooting and edge cases

**When to use:** "How do I solve this specific problem?"

**Examples:** "How to configure frame profiling", "How to troubleshoot deployment issues"

**Reader mindset:** Working mode. "Help me do this task."

### 3. Reference Documentation

**Purpose:** Provide accurate, complete, factual knowledge for lookup and application.

**Characteristics:**
- Contains reliable, precise information free of distraction or interpretation
- Mirrors the structure of what it describes (like a map reflects geography)
- Neutral, applicable across multiple contexts
- Comprehensive rather than explanatory
- Quick lookup, not learning-focused

**When to use:** "What are the facts about this?"

**Examples:** API documentation, command reference, configuration options

**Reader mindset:** Looking up mode. "Tell me the specifics."

### 4. Explanation

**Purpose:** Provide deeper understanding and context, answering "why?" questions.

**Characteristics:**
- Explores subjects in depth, from multiple angles
- Focused on conceptual understanding, not task completion
- Supports skill acquisition and learning
- Can include perspectives, history, reasoning
- Helps readers understand connections and bigger pictures

**When to use:** "Why does this work the way it does?"

**Examples:** "Why consistency matters in distributed systems", "Understanding error budgets"

**Reader mindset:** Learning mode (conceptual). "Help me understand."

## The Two Axes

Diátaxis organizes the four types along two dimensions:

### Axis 1: Action vs. Cognition

- **Action** — Documentation that guides doing (Tutorials, How-to Guides)
- **Cognition** — Documentation that supports understanding (Reference, Explanation)

### Axis 2: Study vs. Work

- **Study** — Documentation that builds skills (Tutorials, Explanation)
- **Work** — Documentation that supports task completion (How-to Guides, Reference)

### The Diátaxis Compass

```
                   STUDY
                     |
                     |
        Tutorials    |    Explanation
        (action +    |    (cognition +
        study)       |    study)
                     |
    ACTION -----------+----------- COGNITION
                     |
        How-to       |    Reference
        Guides       |    (cognition +
        (action +    |    work)
        work)        |
                     |
                   WORK
```

## Implementation Approach

Diátaxis is pragmatic, not prescriptive. The suggested workflow is simple:

1. **Examine** existing documentation
2. **Identify** potential improvements
3. **Select** one small improvement
4. **Execute** it

This iterative cycle compounds — each improvement reveals the next opportunity. No extensive theoretical study is required to begin; start by improving one thing and learn as you go.

## Key Characteristics

- **Pragmatic over theoretical** — Apply it to actual problems, not in isolation
- **Flexible** — The framework is a toolbox, not a rigid system
- **User-centric** — Organized around reader needs and goals, not product structure
- **Iterative** — Improve one thing at a time, learning from each change
- **Universally applicable** — Works for product docs, developer docs, internal knowledge bases, personal wikis

## Why It Matters

Traditional documentation often mixes purposes — tutorials get tangled with reference material, explanations interrupt how-to guides. Readers get confused because they're trying to learn but landing on lookup content, or trying to complete a task but reading conceptual explanations.

Diátaxis solves this by separating purposes. Each type serves a clear reader goal at a clear point in their journey. When readers find the right type of documentation, they succeed faster.

## Contradictions / Open Questions

- How much overlap is acceptable between types? (e.g., a how-to guide that includes explanatory sections)
- How does Diátaxis apply to documentation that serves mixed audiences? (e.g., beginners and experts)
- What's the relationship between Diátaxis structure and page-level best practices?
