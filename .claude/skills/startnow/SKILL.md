---
name: startnow
description: Load project context at the start of a session. Reads architecture docs, project rules, and structure, and surfaces any new upstream commits since your last session.
argument-hint:
disable-model-invocation: false
allowed-tools: Read, Glob, Grep, Bash
---

# StartNow — Session Context Loader

You are a context-building agent. When invoked at the start of a session, you systematically read the key project documents so you have full working knowledge before any coding begins.

## Goal

Read and internalize the project's architecture docs, rules, and structure so you can work effectively without the user manually pointing you to files.

<!-- CUSTOMIZE: Update the YAML description above to start with "[ProjectName]" prefix.
     Example: description: "[TaskApp] Load task tracker context — reads arch.md, feature docs, and Supabase schema."

     WHY: Skills inherit from parent directories. When working in a project, you'll see both
     project skills AND workspace skills in the / menu. The prefix tells you which is which:
       /startnow  [TaskApp] Load task tracker context...         ← project-specific
       /startnow  [Workspace] Load multi-project workspace...    ← inherited from parent

     Without prefixes, you can't tell them apart in the skill picker. -->

## Execution Steps

### Step 1: Identify the Project

1. Note the current working directory (this is the project root).
2. Run `git remote -v` to identify the repository.
3. Run `git log --oneline -5` to see recent activity.
4. Run `git branch --show-current` to know the active branch.

### Step 1b: Check for Upstream Activity (Teammate / Cross-Session Awareness)

This step makes `/startnow` useful both for solo work resumed after time away AND for projects shared with collaborators. Skip silently if any sub-step fails (no remote, no upstream tracking, offline, etc.) — the skill must never error out because of network or remote state.

1. **If `git remote -v` showed any remote in Step 1**, run `git fetch --quiet` to update remote refs. Ignore failures.
2. Run `git log --oneline HEAD..@{u}` to list commits that exist on the upstream branch but are not yet in local `HEAD`. These are commits added since you last pulled — by you on another machine, or by a collaborator.
3. If step 2 returned any commits, run `git log --name-only HEAD..@{u}` (or `git diff --name-only HEAD..@{u}`) to capture which files changed. Pay particular attention to:
   - `docs/arch.md` (and any `arch.md` / `architecture.md` variants)
   - `CLAUDE.md`
   - Anything under `docs/features/`
   - `.claude/skills/*/SKILL.md`
4. Note the authors of upstream commits (`git log --pretty=format:'%h %an %s' HEAD..@{u}`) so the summary can credit collaborators.

If the project has no remote, no upstream tracking, or no new upstream commits, all of the above is a no-op and produces an empty result. Surface that as "no new upstream activity" in the summary rather than skipping the line entirely — the *absence* of upstream changes is itself useful information.

### Step 2: Read Architecture Docs

Search for the architecture index in this priority order. Read the **first one found**:

1. `docs/arch.md`
2. `docs/architecture.md`
3. `arch.md`
4. `architecture.md`
5. `ARCHITECTURE.md`
6. `docs/ARCHITECTURE.md`

If none exist, look for `README.md` as a fallback.

Use Glob to search: `**/arch.md`, `**/architecture.md`, `**/ARCHITECTURE.md`

**Read the entire file.** This is the primary context source — it contains tech stack, data model, API routes, key patterns, and references to detailed feature docs.

### Step 3: Read Feature Docs & Plans (if referenced)

If the architecture doc links to feature docs (e.g., `docs/features/*.md`):
- Read the **Feature Index table** to understand what exists
- Do NOT read all feature docs upfront — only read them when working on that feature
- Note which features exist and their status (planned/in-progress/done)

Check for project plans and artifacts:
- Use Glob to check `docs/plans/*.md` — these contain architecture plans, migration scripts, diagrams, and research from previous sessions
- List available plans in the summary so the user knows what context exists
- Do NOT read all plans upfront — only read them when working on that feature

### Step 4: Read Project Rules

Search for Claude configuration and rules:

1. `CLAUDE.md` (root-level rules — most common)
2. `.claude/CLAUDE.md` (project-level rules)
3. `.claude/settings.json` or `.claude/settings.local.json` (project settings)

Read any that exist. These contain coding conventions, commit rules, and project-specific constraints.

### Step 5: Read Key Config Files

<!-- CUSTOMIZE: Replace or extend this list with your project's actual config files.
     Example for a Python project: pyproject.toml, requirements.txt, alembic.ini
     Example for a mobile app: Info.plist, build.gradle, Podfile -->

Quickly scan these for tech stack confirmation:

1. `package.json` — dependencies, scripts, project name
2. `tsconfig.json` or equivalent — language config
3. `.env.example` or `.env.local` (structure only — note which vars exist, NEVER read values)
4. `Dockerfile`, `railway.json`, `vercel.json`, `wrangler.toml` — deployment target

Read `package.json` always. Read others only if they exist (use Glob to check).

### Step 6: Scan Project Structure

Run a quick directory listing to understand the layout:

```bash
ls -la          # root level
ls app/ || ls src/   # main source directory (whichever exists)
```

### Step 6b: Audit Project Scaffolding

Check the health of the project's scaffolding and skill customization:

**Folder structure check:**

| Expected | Check | Status |
|----------|-------|--------|
| `CLAUDE.md` | Does it exist? Is it customized (not template)? | present/missing/template |
| `docs/arch.md` | Does it exist? Version? Line count? | present (vX.Y, N lines) / missing |
| `docs/PRD.md` | Does it exist? Is it filled in or template? | present/missing/template |
| `docs/features/` | Does dir exist? How many feature docs? | N docs / empty / missing |
| `docs/plans/` | Does dir exist? How many plan docs? | N docs / empty / missing |
| `.claude/skills/` | Does dir exist? | present / missing |
| `.claude/settings.local.json` | Does it exist? | present / missing |

**Skill customization check:**

For each skill in `.claude/skills/*/SKILL.md`:
1. Read the YAML frontmatter `description` field
2. Check if it still contains generic/template language (e.g., "Load project context" instead of a project-specific description)
3. Check if `<!-- CUSTOMIZE -->` comments are still present (means not yet customized)

Classify each skill:

| Skill | Status | Notes |
|-------|--------|-------|
| startnow | Customized / Generic | [what's missing if generic] |
| updatenow | Customized / Generic | |
| advise | Customized / Generic / Missing | |
| l3 | Customized / Generic / Missing | |

**Missing scaffolding = action items.** Flag anything that's missing or still generic so the user can decide whether to customize now or later.

### Step 7: Check for Memory Files

Look for persistent memory that carries context across sessions:

1. Check the auto-memory directory for `MEMORY.md`
2. Check for topic-specific memory files (e.g., `debugging.md`, `patterns.md`)

### Step 8: Summarize Context

<!-- CUSTOMIZE: Add project-specific fields to the summary template below.
     Examples: "Deploy target: Railway (production)", "Active sprint: Sprint 3",
     "Pending migrations: 2", "Open PRD questions: 3" -->

Present a concise summary to the user:

```
Project: [name] ([repo URL])
Branch:  [current branch]
Stack:   [framework, language, DB, hosting]
Recent:  [last 3-5 commits summarized in one line each]
Upstream: [N new commits since your last session, by [authors]]
          [or "no new upstream activity" / "no remote configured"]

Docs:
  - arch.md (vX.Y, updated YYYY-MM-DD, [N] lines)
  - CLAUDE.md / project rules
  - PRD.md [present/missing/template]
  - [N] feature docs | [N] plan docs

Scaffolding:
  | Item | Status |
  |------|--------|
  | CLAUDE.md | ✓ customized / ⚠ template / ✗ missing |
  | arch.md | ✓ v0.3 (142 lines) / ⚠ template / ✗ missing |
  | PRD.md | ✓ filled in / ⚠ template / ✗ missing |
  | /startnow | ✓ customized / ⚠ generic |
  | /updatenow | ✓ customized / ⚠ generic |
  | /advise | ✓ customized / ⚠ generic / ✗ missing |

[If upstream commits touched arch.md / CLAUDE.md / docs/features/ / .claude/skills/:
  "Heads-up: project context shifted upstream. Review the changed docs before starting your session — your local mental model may be out of date."]

[If any scaffolding items are ⚠ or ✗: "Some scaffolding is incomplete. Customize the generic skills by reading the kit templates and filling in CUSTOMIZE markers."]
[If arch.md > 250 lines: "arch.md is [N] lines (limit: 300). Consider /localcompact."]

What are we working on today?
```

## Important Notes

- This is a **read-only** skill — do NOT modify any files
- Do NOT read `.env.local` values — only note which env vars are configured (keys, not values)
- If arch.md is very large (500+ lines), still read it — it's the primary context source
- If you find multiple architecture docs, read the most detailed one and note the others
- Keep the summary concise — the user wants to start working, not read a report
- If the project has no architecture doc, say so and suggest creating one with `/advise`
- The upstream-activity check (Step 1b) is read-only against the remote (`git fetch` only updates local refs, never modifies remote). Always run silently — if the network is down or the remote is unreachable, skip without surfacing an error
