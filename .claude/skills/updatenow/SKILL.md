---
name: updatenow
description: Update arch.md and feature docs with recent session changes. Invoke with no arguments to auto-detect changes, or pass a note to add specific content.
argument-hint: [optional note, e.g. "add auth feature details"]
disable-model-invocation: false
allowed-tools: Read, Edit, Write, Grep, Glob, Bash
---

<!-- CUSTOMIZE: Update the YAML description above to start with "[ProjectName]" prefix.
     Example: description: "[PrepRight] Update arch.md and feature docs after job tracker changes." -->

# UpdateNow — Architecture & Feature Doc Updater

You maintain the project's living documentation. When invoked, you review the current session's changes and update all applicable docs to stay current.

## What You Update

### 1. `docs/arch.md` — Architecture Index

**Purpose:** LLM-optimized index for the entire project. Developers and AI agents read this to understand the system quickly. It should stay lean (<300 lines) and link to detailed feature docs.

**Structure (preserve the existing structure — update sections, don't reorganize):**
```
# [Project Name] — Architecture
**Version:** X.Y | **Updated:** YYYY-MM-DD

## Quick Reference
  ### What Is This?              — 1-paragraph summary
  ### Tech Stack                 — table: Component | Technology | Notes
  ### Project Structure          — directory tree with comments
  ### Environment Variables      — env var names (never values)

## Domain Concepts               — key business terms and rules
## Data Model                    — tables/collections with key columns
## API Routes                    — tables by domain
## Key Patterns                  — numbered architectural patterns
## Feature Index                 — table linking to docs/features/*.md
## Version History               — table at the very end
```

**Version rules:**
- Version numbers: major.minor (e.g. 1.3). Bump minor for most changes, major for architecture shifts
- Date format: YYYY-MM-DD
- Changes column: bold lead phrase + details. Use `**Feature name.**` pattern
- Keep descriptions concise but complete — every new table, endpoint, component, or pattern gets mentioned

**What to update based on change type:**

| Change Type | Sections to Update |
|------------|-------------------|
| New DB table/migration | Data Model, Version History |
| New API route | API Routes, Version History |
| New component/page | Project Structure, Version History |
| New feature started | Feature Index (add row), Version History |
| New key pattern | Key Patterns (add numbered entry), Version History |
| Bug fix / refactor | Version History only (unless it changes architecture) |
| New env var | Environment Variables, Version History |

### 2. `docs/features/*.md` — Detailed Feature Docs

**Purpose:** Deep-dive documentation for each feature/module. Contains everything Claude needs to understand and work on that feature: data model, components, API routes, flows, decisions, gotchas.

**Structure (update the relevant feature doc):**
```markdown
# [Feature Name]

**Status:** planned | in-progress | done
**Last updated:** YYYY-MM-DD

## Overview
[What this feature does]

## Design
[Data model, components, API routes, flows]

## Code Map
| File | Purpose |
|------|---------|
| [actual file paths filled in as code is written] | |

## Decisions
[Architecture decisions with reasoning]

## Notes
[Gotchas, edge cases, things to remember]
```

**What to update:**
- When a feature is being built: update Design, Code Map sections
- When an architecture decision is made: add to Decisions section
- When a gotcha is discovered: add to Notes section
- When a feature is complete: update Status to "done"

### 3. In-App Guide Pages (if they exist)

<!-- CUSTOMIZE: Once your project has in-app guide/help pages, add their paths and structure here.
     Example:

     ### 3. `app/(app)/guide/_components/GuideClient.tsx` — In-App Guide

     **Purpose:** User-facing documentation inside the app.
     **What to update:** [describe which sections map to which change types]
     **Styling rules:** [describe component patterns to preserve]
-->

If the project has in-app guide pages, check if changes affect user-visible behavior and update accordingly. Skip if no guide pages exist yet.

## Execution Steps

### Step 1: Gather Context

1. Read the recent git log to understand what changed:
   ```
   git log --oneline -10
   ```
2. Read the current version history in arch.md (last 5 entries) to know the current version number
3. If the user provided a specific note, use that as the primary change description

### Step 2: Update arch.md

**arch.md is an index, not a detail doc.** Every entry should be 1 line (table row or bullet). If you need more than 1 line to describe something, put the details in `docs/features/*.md` or `docs/plans/*.md` and add a link in arch.md instead.

1. Read the relevant sections that need updating (use Grep to find them)
2. Apply edits using the Edit tool — surgical updates only, don't rewrite entire sections
3. **Keep entries minimal:** table row or 1-liner + link to detail doc. Never add multi-line explanations.
4. Bump the version number (minor bump, e.g. 1.1 → 1.2)
5. Update the `**Updated:**` date in the header
6. Add a new row to the Version History table at the bottom

### Step 3: Update Feature Docs (if applicable)

1. Identify which feature was changed based on the git log and file paths
2. Read the corresponding `docs/features/*.md` file
3. Update the relevant sections (Code Map, Design, Decisions, Notes)
4. Update the `**Last updated:**` date
5. If no feature doc exists for this feature, create one from the template

### Step 3b: Store Project Artifacts

If the session produced any of these artifacts, save them to the project's docs folder:

| Artifact | Store in | Link from |
|----------|----------|-----------|
| Architecture plans / research | `docs/plans/[feature]-plan.md` | Feature doc Decisions section |
| Migration scripts / SQL | `docs/plans/[feature]-migrations.md` | Feature doc Design section |
| Code diagrams / flow charts | `docs/plans/[feature]-diagrams.md` | Feature doc Design section |
| API design / contracts | `docs/plans/[feature]-api.md` | Feature doc Design section |

- Create `docs/plans/` if it doesn't exist
- Reference the stored artifact from the relevant feature doc (not arch.md)
- This ensures plans, migrations, and diagrams are never lost between sessions

### Step 4: Update Guide Pages (if applicable)

1. Only update if the changes affect user-visible behavior AND guide pages exist
2. Read the guide component file
3. Edit the specific section that needs updating
4. Preserve all styling patterns exactly

### Step 5: Report

Tell the user what you updated, summarized in a few bullet points:
```
Updated:
  - arch.md v1.2 → v1.3: [what changed]
  - docs/features/auth.md: [what changed]
  - [guide page if updated]
```

After reporting, check the arch.md line count. If > 250 lines, append this warning:
```
arch.md is [N] lines (limit: 300). Consider running /localcompact to trim.
```

## Important Notes

- NEVER delete existing content unless it's factually wrong or superseded
- NEVER change the document structure or section ordering
- NEVER add emojis to documents
- NEVER add multi-line descriptions to arch.md — use a 1-liner + link to a detail doc
- When in doubt about whether a change warrants a doc update, skip it
- **arch.md = index only.** 1-line entries + links. Details go in `docs/features/*.md` or `docs/plans/*.md`
- If there are no meaningful changes to document, say so and don't make unnecessary edits
- Feature docs can be verbose — they're for deep context. arch.md should be concise — it's an index.
- Always store plans, migrations, and diagrams in `docs/plans/` — never let session artifacts disappear
