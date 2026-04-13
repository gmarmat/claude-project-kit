# Tutorial: Build Your First App with Claude Code

> **Time:** ~2 hours | **Result:** A deployed task manager app | **Prerequisite:** Claude Code CLI installed

This tutorial walks you through building a real app using every pattern and skill in this kit. By the end, you'll have a deployed task manager AND muscle memory for the structured AI development workflow.

---

## What You'll Learn

| Step | Pattern | Skill Used |
|------|---------|-----------|
| 1 | Project bootstrapping | `StartHere.md` |
| 2 | PRD-first workflow | PRD template |
| 3 | Architecture scaffolding | arch.md template |
| 4 | Research before deciding | `/advise` |
| 5 | The build loop | `/startnow` + commit discipline |
| 6 | Debugging with AI | `/l3` |
| 7 | Production readiness | `/audit` |
| 8 | Documentation maintenance | `/updatenow` |

---

## Before You Start

1. Install Claude Code: `npm i -g @anthropic-ai/claude-code`
2. Fork or clone this kit:
   ```bash
   git clone https://github.com/gmarmat/claude-project-kit.git my-task-app
   cd my-task-app
   ```
3. Have a GitHub account ready
4. Optional: Supabase account (free tier) for the database

---

## Step 1: Bootstrap the Project

**Pattern: Project Scaffolding**

Launch Claude Code and start the bootstrap:

```bash
claude
```

Tell Claude:

> Read StartHere.md and follow the bootstrap process. We're building a simple task manager app.

Claude will walk you through 5 phases:
1. Environment check
2. PRD creation (you'll do this in Step 2)
3. Architecture scaffolding
4. Skill customization
5. Ready to build summary

**Don't skip phases.** The bootstrap is designed to build context in order.

---

## Step 2: Write Your PRD

**Pattern: PRD-First Workflow** — Never code without a plan.

When Claude asks for your PRD, describe the app:

> I want to build a simple task manager. Users can:
> - Create, edit, and delete tasks
> - Mark tasks as complete
> - Filter by status (all, active, completed)
> - Tasks are saved to a database (Supabase)
> - Single user for now (no auth needed for MVP)
>
> Tech stack: Next.js, Tailwind CSS, Supabase
> Deploy to: Vercel or Railway

Claude will interview you, generate a PRD draft, and iterate 2-3 rounds.

**Key moment:** When Claude presents the PRD, check for:
- A **Boundaries table** (ALWAYS / ASK FIRST / NEVER)
- **Acceptance criteria** for each feature
- **P0/P1/P2 priorities**

If any are missing, ask Claude to add them. This is the quality bar.

> **Why this matters:** The PRD becomes Claude's instruction manual for the entire project. A good PRD means Claude builds what you actually want. A vague PRD means you'll waste time fixing misunderstandings.

---

## Step 3: Scaffold Architecture

**Pattern: Documentation System**

After the PRD is confirmed, Claude will create `docs/arch.md` from the template. Check that it:

- Is under 300 lines (the token budget)
- Has a tech stack table
- Has a data model section
- Has a feature index linking to `docs/features/*.md`

Claude will also create feature doc stubs for each feature in the PRD.

> **Why this matters:** arch.md is Claude's map of your project. Every future session starts by reading this file. If it's bloated or outdated, Claude gets confused.

---

## Step 4: Research a Decision with /advise

**Pattern: Research Before Deciding**

Before building, let's practice the research workflow. Ask Claude:

```
/advise Should we use Supabase's built-in Row Level Security or handle auth in Next.js middleware? Consider: single user MVP now, multi-user later, simplicity vs security.
```

Claude will:
1. Research the options
2. Present a comparison table
3. Make a recommendation
4. Save the analysis to `docs/plans/`

**Pick an option** and tell Claude to proceed. You just made an informed architecture decision with evidence — not a guess.

> **Why this matters:** Every architecture decision should go through `/advise`. The research is saved to `docs/plans/` so you never lose the reasoning behind a choice. When you revisit this in 3 months, the full analysis is there.

---

## Step 5: Build with the Build Loop

**Pattern: The Build Loop**

Now start building. Begin every work session with:

```
/startnow
```

Claude loads your full context (arch.md, CLAUDE.md, git status, recent commits).

**Build the first feature** (task CRUD). Give Claude a structured instruction:

```
Build the task list feature per docs/features/task-crud.md.
Use Supabase for the database.
Create the table migration first, then the API routes, then the UI.
Follow the tech stack in arch.md.
```

After Claude builds each sub-task:
1. **Test it** — open in browser, verify it works
2. **Commit** — `git add . && git commit -m "feat: task CRUD with Supabase"`
3. **Repeat** for the next sub-task

After the feature is complete:

```
/updatenow
```

Claude updates arch.md, feature docs, and version history.

> **Why this matters:** The loop — `/startnow` → build → test → commit → `/updatenow` — is the core rhythm. It keeps your docs current, your commits small, and your context clean.

---

## Step 6: Debug with /l3

**Pattern: Systematic Debugging**

At some point, something will break. When it does, don't guess — use the L3 pattern:

```
/l3 [paste the exact error message here]
```

Claude will:
1. Form hypotheses (ranked by probability)
2. Trace the code flow
3. Check recent git changes
4. Identify root cause with evidence
5. Propose a minimal fix

**Try it now:** Intentionally break something (comment out a key line) and use `/l3` to fix it. This builds the debugging muscle.

> **Why this matters:** Structured debugging is faster than guessing. Claude traces the actual code path instead of pattern-matching on the error message.

---

## Step 7: Audit Before Launch

**Pattern: Production Readiness**

Before deploying, run the audit:

```
/audit security
/audit quality
```

Claude checks for:
- Exposed secrets, missing RLS, auth gaps
- Dead code, duplicated logic, missing error handling
- Performance bottlenecks

Fix the top 3 findings, then deploy.

> **Why this matters:** The audit catches things you'd miss in a manual review. Run it before every deploy and periodically during development.

---

## Step 8: Deploy

Push to GitHub and deploy:

```bash
git push origin main
```

If using Vercel:
```bash
npx vercel
```

If using Railway, connect your GitHub repo in the Railway dashboard.

Open the live URL. **Your app is on the internet.**

---

## What You Just Practiced

| Pattern | Where You Used It |
|---------|------------------|
| **Docs before code** | PRD → arch.md → then build |
| **Research before deciding** | `/advise` for auth strategy |
| **The build loop** | `/startnow` → build → test → commit → `/updatenow` |
| **Structured debugging** | `/l3` with evidence-based root cause analysis |
| **Production readiness** | `/audit` before deploy |
| **Token-optimized docs** | arch.md under 300 lines, feature docs for details |
| **Commit discipline** | Small commits after each sub-task |

---

## Next Steps

1. **Add more features** — work through the P1 items in your PRD
2. **Customize skills** — edit `/advise` to include your domain context
3. **Try `/localcompact`** — when arch.md grows past 300 lines
4. **Read the guides** in `docs/meta/`:
   - [Cheat Sheet](docs/meta/cheat-sheet.md) — 1-page reference
   - [Communication Guide](docs/meta/communication-guide.md) — how to give Claude better instructions
   - [Anti-Patterns](docs/meta/anti-patterns.md) — mistakes to avoid
   - [Token Budgets](docs/meta/token-budgets.md) — keep docs lean

---

## Managing Multiple Projects?

If you're working on several projects, check out [claude-workspace-kit](https://github.com/gmarmat/claude-workspace-kit) — it adds workspace-level context management across all your projects.
