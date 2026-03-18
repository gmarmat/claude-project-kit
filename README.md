# Claude Project Kit

A battle-tested bootstrap kit for starting new projects with [Claude Code](https://claude.ai/claude-code). Fork this repo, run `StartHere.md`, and go from blank folder to fully scaffolded project in one session.

---

## What's Included

### 6 Built-in Skills

Skills are Claude Code's slash commands. Copy these into your project's `.claude/skills/` folder and customize them.

| Skill | What It Does |
|-------|-------------|
| `/startnow` | Loads project context at session start — reads arch.md, CLAUDE.md, feature docs, config files |
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
description: "[PrepRight] Load job tracker context — arch.md, feature docs, Supabase schema."
```

---

## Contributing

Issues and PRs welcome. If you build something with this kit and improve the templates, share it back.

---

## License

MIT

---

**Created by [gmarmat](https://github.com/gmarmat)**
Contact: gmarmat@outlook.com
