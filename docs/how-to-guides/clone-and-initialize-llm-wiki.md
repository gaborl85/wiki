---
title: "How to Clone and Initialize an LLM Wiki for Your Team"
type: how-to
created: 2026-06-07
last_updated: 2026-06-07
tags: [wiki, setup, git, initialization, team, onboarding]
sources: ["2026-06-07-llm-wiki-design.md"]
related: ["[[CLAUDE.md]]", "[[Documentation Best Practices]]"]
---

# How to Clone and Initialize an LLM Wiki for Your Team

## What This Guide Does

This guide helps you **clone a template LLM Wiki and get it running in under 10 minutes** by using a simple prompt to Claude. Your team members can follow these steps to initialize their own personal wiki or team knowledge base.

**Time to complete:** 5-10 minutes  
**What you'll have:** A fully configured wiki ready for your first ingest  
**For:** Team members with git access and Claude available

---

## Who This Is For

This guide assumes you:
- Have cloned the wiki repository to your machine
- Have access to Claude (web or IDE integration)
- Have a markdown editor or Obsidian installed
- Want to initialize the wiki infrastructure quickly

---

## What You're About to Set Up

You'll initialize an LLM Wiki — a knowledge base that:
- Grows as you add sources (articles, papers, books, etc.)
- Automatically maintains cross-references between pages
- Flags contradictions and gaps when you lint it
- Compounds knowledge over time (each source touches 10-15 pages)

See [[CLAUDE.md]] to understand the schema. See [[Documentation Best Practices]] to understand how documentation should work.

---

## Step 1: Clone the Repository

Clone the wiki repository to your local machine:

```bash
git clone <wiki-repo-url> my-wiki
cd my-wiki
```

**Replace `<wiki-repo-url>`** with your team's wiki repository URL.

**You'll now have:**
```
my-wiki/
├── CLAUDE.md                 # Wiki schema (don't modify yet)
├── .gitignore                # Exclude OS/IDE files
├── sources/                  # Empty (will hold raw sources)
│   ├── books/
│   ├── papers/
│   ├── articles/
│   └── ... (other source types)
├── research/                 # Living synthesis
│   ├── index.md              # Will list all research pages
│   ├── log.md                # Will log all activity
│   ├── entities/             # Will hold concept pages
│   ├── topics/               # Will hold theme pages
│   └── syntheses/            # Will hold keeper pages
└── docs/                     # Curated documentation
    ├── index.md
    ├── tutorials/
    ├── how-to-guides/
    ├── explanations/
    └── reference/
```

---

## Step 2: Configure Git (One-Time)

If you haven't already, tell git who you are:

```bash
git config user.name "Your Name"
git config user.email "your.email@company.com"
```

This ensures your commits are attributed correctly.

---

## Step 3: Open the Wiki (Optional but Recommended)

For the best browsing experience, open the wiki in **Obsidian**:

1. Open Obsidian
2. Click "Open folder as vault"
3. Select your `my-wiki` directory
4. Enable "Graph view" in the sidebar

This lets you see how pages connect as you build the wiki.

---

## Step 4: Run the Initialization Prompt

Copy this entire block and paste it into Claude:

```
I have cloned an LLM Wiki repository to [/path/to/my-wiki].

Please initialize it by:

1. Verify all directories exist (sources/, research/, docs/ with subdirectories)
2. Confirm CLAUDE.md is present and complete
3. Verify research/index.md and research/log.md exist
4. Check that docs/index.md exists
5. Confirm .gitignore is properly configured
6. Create any missing files or fix any incomplete setup
7. Make a git commit with the message: "chore: initialize llm-wiki setup"

After initialization:
- Tell me the wiki is ready
- Explain what each directory is for
- Tell me how to do my first ingest

Replace [/path/to/my-wiki] with the actual path (e.g., /Users/name/my-wiki or C:\Users\name\my-wiki on Windows).
```

**What to expect:** Claude will verify the setup and either confirm everything is ready or fix any issues. You'll see:

```
✅ Directory structure verified
✅ CLAUDE.md is complete
✅ research/index.md initialized  
✅ research/log.md initialized
✅ docs/index.md initialized
✅ .gitignore configured
✅ Initial commit created (chore: initialize llm-wiki setup)

Your wiki is ready for your first ingest!
```

---

## Step 5: Understand Your New Wiki

After initialization, you have three areas:

### `/sources/` — Immutable Raw Materials
Store your original articles, papers, books, etc. in folders by type:
- `sources/books/` for ebooks or book excerpts
- `sources/articles/` for blog posts, news articles
- `sources/papers/` for research papers, whitepapers
- `sources/transcripts/` for podcasts, interviews, talks
- `sources/videos/` for video transcripts
- `sources/presentations/` for slides, decks
- `sources/notes/` for personal observations
- `sources/tools/` for tools you're studying
- `sources/datasets/` for data, reports

**Rule:** Never edit these files. They're your source of truth.

### `/research/` — Living Knowledge Synthesis
Claude maintains this area as you ingest sources. It contains:
- `index.md` — Catalog of all research pages (Claude updates this)
- `log.md` — Chronological record of all ingests (Claude updates this)
- `entities/` — Pages for specific concepts, tools, people
- `topics/` — Pages for themes connecting multiple sources
- `syntheses/` — Pages for valuable analyses you keep

**Rule:** You can edit these pages, but Claude mostly maintains them.

### `/docs/` — Curated Diátaxis Documentation
As your research matures, you promote pages here. Following [[Documentation Best Practices]], this is organized by:
- `tutorials/` — Hands-on learning guides
- `how-to-guides/` — Solutions to specific problems
- `explanations/` — Conceptual understanding
- `reference/` — Lookup facts and specifications

**Rule:** You decide when to promote research to docs. Claude helps structure it.

---

## Step 6: Prepare Your First Source

Find a document you want to ingest. Convert it to markdown if needed.

**Example sources:**
- A blog post or article (copy-paste into markdown)
- A PDF (convert to markdown using a tool)
- A book excerpt (type or paste the text)
- A transcript (transcript or summarize a video/podcast)

**Save it** to the appropriate `/sources/` folder. For example:
```bash
cp ~/Downloads/my-article.md sources/articles/
```

---

## Step 7: Do Your First Supervised Ingest

This is where the wiki starts to grow. Tell Claude:

```
I want to do a supervised ingest of the source at sources/articles/[filename].md

Please:
1. Read it carefully
2. Summarize the key takeaways
3. Ask me: "What stands out? What contradicts existing knowledge? What should we emphasize?"

Let's start - what are your key takeaways from this source?
```

**What happens next:**

Claude will:
1. **Summarize** the article with 3-5 key points
2. **Ask for guidance** — You tell Claude what to emphasize
3. **Create pages** — Entities (concepts), topics (themes), cross-references
4. **Update the wiki** — research/index.md and research/log.md get updated
5. **Commit changes** — Everything is saved to git

**Example output:**

```
Key takeaways from [article]:
1. Best practice #1: Lead with the answer
2. Best practice #2: Write for your audience
3. Best practice #3: Use examples, not abstraction
4. Best practice #4: Link related content
5. Best practice #5: Keep pages focused

What stands out to you?
What should we emphasize?
Does this contradict anything you already know?
```

---

## Step 8: Guide Claude Through the Ingest

Answer Claude's questions to shape what gets created:

**Example conversation:**

```
You: "Emphasize best practices #1 and #3. 
      These are most relevant to our team.
      Create an entity page for 'Documentation Best Practices'.
      Connect it to any existing pages about writing or communication."

Claude: "Creating entity: [[Documentation Best Practices]]
         Creating topic: [[How to Write Clear Guides]]
         Updating research/index.md
         Updating research/log.md
         
         Here are the pages I created... [shows preview]"

You: "Looks good! Can you add a link from the new topic 
     to [[Communication Principles]] if it exists?"

Claude: "Adding that link now. 
         Ready to commit - approve?"

You: "Yes, commit it."
```

---

## Step 9: Review the Created Pages

After the ingest completes, browse the new pages:

**In Obsidian:**
- Click on a new page name
- See all its cross-references in the backlinks
- View the graph to see connections

**In your editor:**
- Open `research/entities/documentation-best-practices.md`
- Open `research/index.md` to see the new catalog entry
- Open `research/log.md` to see the activity log entry

---

## Step 10: Commit and Share

Commit your ingest to git:

```bash
git add research/
git commit -m "feat: first ingest - [source title]

Ingested [source title].

Pages created:
- [[Entity Name]] — definition and characteristics
- [[Topic Name]] — connections and synthesis

Key insight: [what this teaches your team]"
```

Push to your team repository:

```bash
git push origin main
```

---

## What to Do Next: Choose Your Path

After your first ingest, you have several options:

### Path A: Build Momentum with More Ingests
```
I've added 3 articles about [topic] to sources/articles/.
Please batch ingest them (process all 3 together).
```

Use batch ingests for speed when you have multiple sources.

### Path B: Query Your Growing Knowledge Base
```
Based on the research pages I now have, 
what are the best practices for [specific question]?

If the answer is valuable, create a keeper page.
```

Queries synthesize knowledge from existing pages.

### Path C: Maintain Wiki Health with Linting
```
Lint the research wiki.

Check for:
- Orphaned pages (no inbound links)
- Contradictions (conflicting claims)
- Missing cross-references
- Coverage gaps (topics mentioned but lacking pages)
```

Lint every 5-10 ingests to keep things organized.

---

## Common Issues and Solutions

### Issue: File Not Found or Path Error

**Symptom:** Claude says "I can't find sources/articles/my-file.md"

**Solution:** 
- Verify the file exists: `ls sources/articles/my-file.md`
- Provide the full absolute path: `/Users/name/my-wiki/sources/articles/my-file.md`
- Ensure filename matches exactly (case-sensitive on Mac/Linux)

**Example:**
```
I've saved the file at /Users/alice/my-wiki/sources/articles/documentation.md

Please read it and ingest it.
```

### Issue: Changes Aren't Showing Up

**Symptom:** You see changes in Claude's response but not in the files

**Solution:**
- Claude might be waiting for your approval to commit
- Look for "Ready to commit?" and respond "Yes, commit it"
- Verify with `git status` to see uncommitted changes
- Run `git log -1` to see the latest commit

### Issue: Merge Conflicts When Pulling Updates

**Symptom:** `git pull` shows merge conflicts

**Solution:**
- This happens if your team is updating the wiki simultaneously
- Resolve by hand or ask Claude: "Fix the merge conflict in research/index.md"
- Then commit: `git add . && git commit -m "chore: resolve merge conflict"`

### Issue: Wiki Feels Disorganized After Several Ingests

**Symptom:** Pages exist but feel scattered, hard to navigate

**Solution:**
- Run a lint pass: "Lint the research wiki"
- Claude will identify missing cross-references and orphans
- Add connections: "Add cross-references between [[Topic A]] and [[Topic B]]"

---

## Understanding the Flow

Here's the typical workflow:

```
1. Find a source → 2. Save to sources/ → 3. Prompt Claude
              ↓
4. Claude reads and asks questions → 5. You provide guidance
              ↓
6. Claude creates 10-15 wiki pages → 7. You review
              ↓
8. Claude commits → 9. You push to team → 10. Team sees new knowledge
```

Each cycle adds depth. After 3 ingests, you'll see connections. After 10 ingests, gaps become obvious. After 30 ingests, your wiki is a valuable knowledge asset.

---

## Example: Full Workflow from Start to Finish

Here's what your first 30 minutes looks like:

```bash
# 1. Clone (1 minute)
git clone https://github.com/myteam/llm-wiki my-wiki
cd my-wiki

# 2. Configure git (1 minute)
git config user.name "Alice"
git config user.email "alice@company.com"

# 3. Open in Obsidian (1 minute)
# Obsidian → Open Vault → my-wiki directory

# 4. Paste initialization prompt into Claude (2 minutes)
# Claude verifies and commits

# 5. Prepare first source (2 minutes)
cp ~/Downloads/documentation-article.md sources/articles/

# 6. Prompt Claude for ingest (15 minutes)
# Claude reads → asks questions → you answer → creates pages
# You review → Claude commits

# 7. Check what was created (3 minutes)
git log -1  # See the commit
ls research/entities/
ls research/topics/

# 8. Push to team (1 minute)
git push origin main
```

---

## Best Practices While Using Your Wiki

1. **Lead with examples** — When you ingest, ask Claude to emphasize examples over abstraction
2. **Keep descriptions concise** — Pages should answer questions quickly, then provide detail
3. **Use consistent terminology** — If you say "API documentation" once, use it consistently
4. **Link actively** — Ask Claude to "add cross-references between [Topic A] and [Topic B]"
5. **Lint regularly** — Every 5-10 ingests, check for gaps and contradictions
6. **Commit with context** — Describe *why* you're ingesting, not just *what*

For more guidance, see [[Documentation Best Practices]].

---

## After Your First Week

Once you've done 3-5 ingests:

1. **You'll see the graph** — In Obsidian, the graph view shows how pages connect
2. **Patterns emerge** — Themes appear across sources
3. **Gaps become obvious** — The lint pass shows what to explore next
4. **You'll want to promote** — Move polished research to `/docs/`
5. **Your team benefits** — Shared knowledge becomes discoverable

---

**Ready to initialize?** Start with Step 1, follow the prompt in Step 4, and Claude will guide you through the rest!
