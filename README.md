# Claude Project Kit

A battle-tested bootstrap kit for starting new projects with [Claude Code](https://claude.ai/claude-code). Fork this repo, run `StartHere.md`, and go from blank folder to fully scaffolded project in one session.

Built from patterns extracted across 10+ real projects across multiple domains. Not theoretical. Every pattern earned its place by surviving real production use.

---

## Philosophy: You Are the Architect

This kit is built on one principle: **you make the decisions, Claude handles the execution.**

```
You (Human)                          Claude (AI)
─────────────                        ──────────
Vision & Goals          ──────>      Understands context via docs
Architecture Decisions  ──────>      Executes within constraints
Review & Course-Correct ──────>      Generates code, docs, plans
Domain Expertise        ──────>      Handles boilerplate + research
Quality Bar             ──────>      Follows your patterns consistently
```

This maps directly to the [Agentic Engineering](https://addyosmani.com/blog/agentic-engineering/) approach — the structured successor to "vibe coding":

| Agentic Engineering Principle | How This Kit Implements It |
|-------------------------------|---------------------------|
| **Plan** before prompting | PRD-first workflow — never code without a plan |
| **Direct** with precision | Communication guide + doc references in every instruction |
| **Review** rigorously | Build loop — test locally, review each sub-task |
| **Test** systematically | `/audit` skill — security, cost, performance, quality |
| **Own** the architecture | `/updatenow` — docs stay current, you stay in control |

> **The difference between vibe coding and building real products is a system.** This kit is that system.

---

## What's Included

### 6 Built-in Skills

Skills are Claude Code's slash commands. Copy these into your project's `.claude/skills/` folder and customize them.

| Skill | What It Does |
|-------|-------------|
| `/startnow` | Loads project context at session start — reads arch.md, CLAUDE.md, feature docs, config files, and surfaces any new upstream commits since your last session |
| `/updatenow` | Updates architecture docs and feature docs after code changes |
| `/advise` | Research agent — presents 2-3 options with costs, risks, and a recommendation |
| `/l3` | Debug agent — root-cause investigation with hypotheses, evidence, and fix |
| `/audit` | Health check — scans for security gaps, cost waste, performance issues, code quality |
| `/localcompact` | Keeps `docs/arch.md` under 300 lines — compacts bloat without losing content |

### 4 Document Templates

| Template | Purpose |
|----------|---------|
| `CLAUDE.md.template` | Project rules — API safety, auth model, data sensitivity, naming conventions |
| `docs/arch.md.template` | Architecture index — LLM-optimized, 300-line budget, links to feature docs |
| `docs/PRD.md.template` | Product requirements — problem, users, features, phases, open questions |
| `docs/features/_template.md` | Per-feature deep-dives — design, code map, decisions, gotchas |

### 1 Design System (opt-in)

| File | What It Is |
|------|-----------|
| `design/globals.css` | Production-ready CSS — 3-layer token system, Tailwind v4 + Shadcn/UI, light/dark mode |
| `design/design-system.md` | Reference doc — all tokens, component classes, usage examples |

During `StartHere.md` onboarding, Claude will ask if you want to adopt the design system. If yes, copy `globals.css` to your app's CSS entry point and get instant access to:
- 8 color scales, semantic token layer, WCAG 2.1 AA focus rings
- KPI cards, status badges, data tables, filter pills, timeline, empty states, upload zones
- Tailwind utility classes for all tokens (`text-ext-primary`, `bg-ext-bg-secondary`, etc.)
- Light + dark mode via `data-theme` attribute (works with Shadcn/UI)

Rename the `--ext-` token prefix to your project prefix at any time.

### 1 Bootstrap Script

`StartHere.md` — a 5-phase guided setup that Claude Code follows sequentially:

```
Phase 1: Environment check + CLAUDE.md setup
Phase 2: PRD review + confirmation (hard gate)
Phase 3: Scaffold arch.md + feature stubs
Phase 4: Customize skills for your project
Phase 5: Ready to build summary
```

---

## How to Use

### Option A: Fork and clone (recommended)

```bash
# Fork this repo on GitHub, then:
git clone https://github.com/YOUR_USERNAME/claude-project-kit.git my-project
cd my-project
claude   # launch Claude Code
```

Tell Claude: "Read StartHere.md and follow the bootstrap process."

### Option B: Use as GitHub Template

Click **"Use this template"** on GitHub → creates a fresh repo with all files → clone → launch Claude Code.

### Option C: Copy manually

**Mac / Linux:**
```bash
cp -r claude-project-kit/ my-project/
cd my-project/
git init
claude
```

**Windows (PowerShell):**
```powershell
Copy-Item -Recurse claude-project-kit\ my-project\
cd my-project
git init
claude
```

**Windows (Command Prompt):**
```cmd
xcopy /E /I claude-project-kit my-project
cd my-project
git init
claude
```

---

## Folder Structure After Bootstrap

```
my-project/
  CLAUDE.md                     # Project rules (from template)
  design/                       # Design system (opt-in)
    globals.css                 # CSS tokens + components — copy to app/globals.css
    design-system.md            # Token reference + usage examples
  docs/
    PRD.md                      # Your product requirements
    arch.md                     # Architecture index (<300 lines)
    features/                   # Per-feature deep-dives
    plans/                      # Research, decisions, ADRs
  .claude/
    skills/
      startnow/SKILL.md         # Customized for your project
      updatenow/SKILL.md        # Customized for your project
      advise/SKILL.md           # Customized for your domain
      l3/SKILL.md               # Customized with your file paths
      audit/SKILL.md            # Customized with your stack
      localcompact/SKILL.md     # Generic — no changes needed
    settings.local.json         # Tool permissions
```

---

## The Workflow (After Bootstrap)

```
/startnow              ← start every session here
/advise [topic]        ← before making architecture decisions
build the feature      ← with full project context loaded
/updatenow             ← keep docs current after changes
commit                 ← frequent, per sub-task
/audit [focus]         ← periodic health checks
/localcompact          ← when arch.md gets long
```

---

## The Build Loop

Every session follows the same pattern. This is the core workflow that makes AI-assisted development predictable:

```
/startnow              ← Load context (arch.md, CLAUDE.md, git status)
    ↓
Review feature index   ← Pick next P0 from PRD
    ↓
/advise [topic]        ← Research before architecture decisions
    ↓
Build the feature      ← One at a time, with doc references
    ↓
Test locally           ← Browser, terminal, whatever fits
    ↓
Commit                 ← After each sub-task, clear message
    ↓
/updatenow             ← Keep docs current
    ↓
Repeat
```

**Starting a new project:** Fork this kit → Run `StartHere.md` → Fill PRD (2-3 rounds) → Scaffold arch.md → Customize skills → First commit

**When something breaks:** `/l3 [error]` → Follow evidence → Minimal fix → Commit → `/updatenow`

**Before launch:** `/audit security` → `/audit cost` → `/audit performance` → Fix top 3 → Deploy

---

## Learnings & Guides

These guides are extracted from real project experience. Find them in `docs/meta/`:

| Guide | What It Covers |
|-------|---------------|
| [Cheat Sheet](docs/meta/cheat-sheet.md) | 1-page quick reference — pin this |
| [Communication Guide](docs/meta/communication-guide.md) | How to give Claude good instructions (bad vs good examples) |
| [Anti-Patterns](docs/meta/anti-patterns.md) | 12 common mistakes and what to do instead |
| [Token Budgets](docs/meta/token-budgets.md) | Line budgets for every doc type — keep Claude fast and focused |

---

## Security Model

This kit is designed with security as a first-class concern:

| Principle | How It's Enforced |
|-----------|------------------|
| **No secrets in docs** | `arch.md.template` and `startnow` skill explicitly list env var *names* only — never values |
| **API safety rules** | `CLAUDE.md.template` has a dedicated section for external API constraints (e.g., read-only mode) |
| **Secret scanning** | `/audit` skill actively greps for common secret patterns (`sk-`, `password=`, `Bearer`, etc.) |
| **RLS enforcement** | `/audit` checks Row-Level Security on all database tables |
| **Input validation** | `/audit` checks API boundaries for input validation |
| **Dependency vulns** | `/audit` runs `npm audit` or equivalent |
| **Env file safety** | `/startnow` reads `.env.example` structure only — never opens `.env.local` |

**What this kit does NOT do:**
- Store, transmit, or log any of your data
- Connect to any external services on its own
- Execute code autonomously without your approval
- Modify files without explicit skill invocation

---

## Requirements

- [Claude Code](https://claude.ai/claude-code) (CLI) — runs on Mac, Linux, and Windows
- A project idea

Optional but recommended:
- Git + GitHub CLI (`gh`)
- Supabase MCP: `claude mcp add supabase -- npx -y @supabase/mcp-server`
- Railway MCP: `claude mcp add railway -- npx -y @anthropic-ai/claude-code-railway-mcp`

### Windows Notes

Claude Code runs natively on Windows. A few things to keep in mind:

| Situation | Windows Equivalent |
|-----------|-------------------|
| `mkdir -p docs/plans` | `mkdir docs\plans` (PowerShell/cmd both work) |
| `rm StartHere.md` | `del StartHere.md` (cmd) or `Remove-Item StartHere.md` (PowerShell) |
| `mv file dest/` | `move file dest\` (cmd) or `Move-Item file dest\` (PowerShell) |
| File paths in docs | Use forward slashes in markdown — they render correctly everywhere |
| SSH to other machines | OpenSSH is built into Windows 10/11 — `ssh user@host` works in PowerShell and cmd |
| Git commands | Identical on all platforms |
| `claude` CLI | Identical on all platforms — install via npm |

> **Tip:** PowerShell is preferred over cmd for working with this kit — better unicode support and tab completion.

---

## Customizing Skills

Every skill has `<!-- CUSTOMIZE -->` markers showing exactly what to change for your project. The key rule: **prefix every skill description with `[ProjectName]`** so inherited skills are identifiable in the slash command menu.

```yaml
# Before (generic template)
description: Load project context at the start of a session.

# After (your project)
description: "[TaskApp] Load task tracker context — arch.md, feature docs, Supabase schema."
```

---

## Tutorial: Build Your First App

New to this kit? Follow [TUTORIAL.md](TUTORIAL.md) — a guided walkthrough that takes you from zero to deployed app in about 2 hours. You'll exercise every skill and pattern the kit ships with.

---

## Part of the Kit Ecosystem

| Kit | Purpose |
|-----|---------|
| **claude-project-kit** (this repo) | Bootstrap **new** projects |
| [claude-workspace-kit](https://github.com/gmarmat/claude-workspace-kit) *(coming soon)* | Manage **multi-project** workspaces |
| [claude-project-rehab](https://github.com/gmarmat/claude-project-rehab) *(coming soon)* | Assess + upgrade **existing** projects, guide **new** ideas |
| [claude-pm-kit](https://github.com/gmarmat/claude-pm-kit) | **PM Twin** — digital peer product manager, full product lifecycle |

Each kit works independently. Together they cover the full journey from idea to launched product.

---

## Contributing

Issues and PRs welcome. If you build something with this kit and improve the templates, share it back.

---

## License

MIT

---

**Created by [gmarmat](https://github.com/gmarmat)**
