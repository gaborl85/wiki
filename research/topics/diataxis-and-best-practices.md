---
title: "Diátaxis and Best Practices"
type: topic
created: 2026-06-07
last_updated: 2026-06-07
tags: [documentation, framework, best-practices, synthesis]
sources: ["Start here - Diátaxis in five minutes - Diátaxis.md", "What is technical documentation_ Examples, templates and how to write it – GitBook Blog.md"]
related: ["[[Diátaxis Framework]]", "[[Documentation Best Practices]]", "[[Technical Documentation Writing Process]]"]
---

# Diátaxis and Best Practices

## Definition

An exploration of how the Diátaxis framework (four documentation types) and universal documentation best practices work together to create documentation that is both well-structured and well-executed.

Diátaxis answers "What type of documentation should this be?" Best practices answer "How should I write it, regardless of type?" Together, they provide complete guidance.

## How Best Practices Map to Diátaxis Types

### Lead with the Answer

**Application across types:**
- **Tutorials** → Lead with the concrete task. "We're going to build X." Start doing immediately.
- **How-to Guides** → Lead with the solution. "To solve this, do X." Get to the steps fast.
- **Reference** → Lead with the fact or definition. "This parameter does X." No preamble.
- **Explanation** → Lead with the core concept. "This matters because X." Then elaborate.

**Why it works:** Each type has a different "answer" that readers seek. Leading with the right answer for each type improves clarity.

### One Topic Per Page

**Application across types:**
- **Tutorials** → One task or project per page. Keeps focus and flow.
- **How-to Guides** → One problem per page. "How to solve X" not "How to solve X, Y, and Z."
- **Reference** → One conceptual unit per page (one API endpoint, one command, one setting).
- **Explanation** → One concept per page. Depth is fine; breadth is not.

**Why it works:** Readers come with one goal in mind. Mixing multiple topics confuses navigation and dilutes clarity.

### Write for a Specific Audience

**Application across types:**
- **Tutorials** → Written for beginners. Assume no prior knowledge. Define unfamiliar terms.
- **How-to Guides** → Written for competent practitioners. Assume foundational knowledge.
- **Reference** → Written for experienced users. Use technical terminology without definition.
- **Explanation** → Written for learners seeking understanding. Can explore nuance and complexity.

**Why it works:** Diátaxis types naturally serve different audiences. Tutorials serve beginners; reference serves experts. Matching your writing to your audience's expertise level prevents confusion.

### Link Related Pages

**Application across types:**
- **Tutorials** → Link to explanations for readers who want deeper understanding.
- **How-to Guides** → Link to tutorials if a reader needs foundational skills, or reference for specific syntax.
- **Reference** → Link to how-to guides for practical application, explanations for conceptual context.
- **Explanation** → Link to tutorials for hands-on learning, reference for specifics.

**Why it works:** Diátaxis pages naturally reference each other. A reader following a how-to guide might need conceptual context (explanation) or a tutorial on a prerequisite skill. Linking enables readers to navigate between types as needed.

### Use Descriptive Headings

**Application across types:**
- **Tutorials** → Headings name the task steps. "Installing dependencies", "Setting up the environment", "Creating your first object."
- **How-to Guides** → Headings name the sub-problems or steps. "Configuring authentication", "Handling errors", "Deploying to production."
- **Reference** → Headings name the elements being described. "Parameters", "Return values", "Error codes."
- **Explanation** → Headings name the concepts. "Why consistency matters", "The CAP theorem", "Error budgets."

**Why it works:** Each type's headings reflect its purpose. Readers scanning each type look for different things. Good headings let them find what they need quickly.

### Prioritize Examples Over Abstraction

**Application across types:**
- **Tutorials** → Heavy on examples. Show completed steps, working code, visible results.
- **How-to Guides** → Include examples (code samples, screenshots, configuration) to demonstrate the solution.
- **Reference** → Include examples (sample values, example calls, expected output) to clarify syntax.
- **Explanation** → Use concrete examples to illustrate abstract concepts. "X works like Y because..."

**Why it works:** Examples make abstract concepts tangible. Diátaxis types all benefit from concrete examples, though the ratio changes by type (tutorials are mostly examples; reference includes some abstraction).

### Make Troubleshooting Easy to Find

**Application across types:**
- **Tutorials** → Include troubleshooting in the tutorial itself for common setup issues.
- **How-to Guides** → Dedicate a section to "Common issues and solutions" or "Troubleshooting."
- **Reference** → Include an "Error codes" or "Common errors" section.
- **Explanation** → Address common misconceptions in the explanation itself.

**Why it works:** All documentation types serve people who get stuck. How-to guides especially serve people in "something went wrong" mode. Anticipate problems and make solutions easy to find.

### Use Consistent Terminology

**Application across types:**
- Applies universally across all Diátaxis types
- Especially critical when pages reference each other
- Enables readers to transition smoothly between types

**Why it works:** When a reader sees a term in a tutorial and encounters it in a how-to guide, consistent naming helps them connect the concepts.

### Make Your Docs Accessible

**Application across types:**
- Applies universally across all Diátaxis types
- Clear Diátaxis structure itself improves accessibility (different types serve different needs)
- Within each type, follow accessibility practices (alt text, readable structure, scannable formatting)

### Review and Update Regularly

**Application across types:**
- Applies universally across all Diátaxis types
- Especially important as products evolve

## Key Synthesis

**Diátaxis provides the architecture; best practices provide the execution.**

Diátaxis answers structural questions:
- What type of documentation does the reader need?
- How should the four types relate to each other?
- When should readers transition between types?

Best practices answer execution questions:
- How do I write this clearly?
- How do I organize the information?
- How do I help readers scan and understand?

Together, they ensure documentation is:
1. **Well-structured** — Right type for each reader need (Diátaxis)
2. **Well-written** — Clear, scannable, and helpful (best practices)
3. **Well-connected** — Easy to navigate between related content (both)
4. **Well-maintained** — Updated and accurate (both)

## Example: How a Topic Becomes Four Pages

Consider a feature: "Error budgets"

**Diátaxis structure:**

- **Tutorial**: "Understanding Error Budgets: A Hands-On Introduction" (Diátaxis tutorial)
  - Applied best practice: Lead with the concrete example, prioritize examples

- **How-to Guide**: "How to Set Your Error Budget" (Diátaxis how-to)
  - Applied best practice: Lead with the steps, one problem per page

- **Reference**: "Error Budget Parameters and Calculations" (Diátaxis reference)
  - Applied best practice: Descriptive headings, accurate/complete information

- **Explanation**: "Why Error Budgets Matter: Context and Philosophy" (Diátaxis explanation)
  - Applied best practice: Answer "why", use concrete examples to explain abstract concepts

Each page serves a different reader need, applies Diátaxis principles, and follows best practices for its type.

## Open Questions

- How do you handle overlap between types? (e.g., a how-to guide that includes explanatory sections)
- What's the minimum viable implementation of Diátaxis? (Do you need all four types for every topic?)
- How does Diátaxis scale to very large documentation systems?
- When should you update one type vs. all four types in response to a change?
