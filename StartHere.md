# StartHere — Claude Code Project Bootstrap

> **For Claude:** This is a sequential bootstrap script. Follow each phase in order. **Do NOT skip ahead.** Mark each phase complete as you finish it. Do NOT start building features until ALL phases are done.

---

## Progress Tracker

<!-- Claude: Update this table as you complete each phase. Change status to "done" and add the date. -->

| Phase | Status | Completed |
|-------|--------|-----------|
| 1. Environment Check | pending | |
| 2. Gather PRD | pending | |
| 3. Scaffold arch.md | pending | |
| 4. Customize Skills | pending | |
| 5. Ready to Build | pending | |

**Current phase:** 1

---

## Gate Rules

- **You MUST complete phases in order.** No skipping.
- **Update the Progress Tracker** after each phase (change status to "done", add date, bump "Current phase").
- **Phase 2 is a hard gate.** Do NOT proceed to Phase 3 until the user has confirmed their PRD is final and it's saved to `docs/PRD.md`.
- **Phase 4 is a hard gate.** Do NOT present the "Ready to Build" summary until all skills are customized.
- **Once Phase 5 is complete**, tell the user: "StartHere.md is done. You can delete it or archive it to `docs/meta/StartHere.md.archive`."
- **After Phase 5**, never re-read this file. Use `/startnow` for future sessions.

---

## Phase 1: Environment Check

### 1.1 Verify Kit Files

Confirm these exist (they ship with the kit):
```
.claude/skills/advise/SKILL.md
.claude/skills/startnow/SKILL.md
.claude/skills/updatenow/SKILL.md
.claude/skills/localcompact/SKILL.md
.claude/skills/l3/SKILL.md
.claude/skills/audit/SKILL.md
design/globals.css
design/design-system.md
docs/arch.md.template
docs/PRD.md.template
docs/features/_template.md
CLAUDE.md.template
```

If any are missing, stop and tell the user.

### 1.2 Git Setup

If not already a git repo:
```bash
git init
git add -A
git commit -m "Initial project setup with Claude skills kit"
```

Recommend the user create a GitHub repo:
```bash
gh repo create <repo-name> --private --source=. --push
```

### 1.3 MCP Connections

Tell the user:

> **Recommended MCP servers:**
>
> 1. **GitHub** — built into Claude Code (no setup)
> 2. **Supabase** — `npx @anthropic-ai/claude-code mcp add supabase -- npx -y @supabase/mcp-server`
> 3. **Railway** — `npx @anthropic-ai/claude-code mcp add railway -- npx -y @anthropic-ai/claude-code-railway-mcp`
>
> Set these up now if you know your stack. You can add them later.

### 1.4 Design System (Optional)

Ask the user:

> **This kit includes a pre-built design system** (`design/globals.css` + `design/design-system.md`):
> - 3-layer token architecture: Primitives → Semantic → Component
> - Light/dark mode via `data-theme` attribute
> - WCAG 2.1 AA compliant
> - Tailwind CSS v4 + Shadcn/UI compatible
> - Generic components: KPI cards, badges, data tables, filter pills, timeline, empty states
>
> **Do you want to use this design system for your project?**
> - **Yes** → Copy `design/globals.css` to your app's CSS entry point (e.g., `app/globals.css`). Rename `--ext-` prefix to your project prefix if desired.
> - **No** → Skip. The `design/` folder can be deleted.

If yes, note it in `CLAUDE.md` (see next step).

### 1.5 CLAUDE.md Setup

Rename `CLAUDE.md.template` to `CLAUDE.md`. Walk through project-specific rules:

> 1. **External APIs** — any that need read-only or rate-limited access?
> 2. **Auth model** — magic links, OAuth, API keys, JWT?
> 3. **Data sensitivity** — PII, encryption, audit logging?
> 4. **Deploy constraints** — approval flow, preview deploys, branch protection?
> 5. **Third-party libraries** — banned or required packages?
> 6. **Naming conventions** — files, components, DB tables?

Fill in what the user knows. Skip unknowns — they get filled in after PRD review.

If the user adopted the design system in step 1.4, add a `Design System` section to CLAUDE.md noting the token prefix and `data-theme` dark mode convention.

**Mark Phase 1 done in the Progress Tracker. Move to Phase 2.**

---

## Phase 2: Gather Project Context

> **HARD GATE:** Do NOT proceed past this phase until the PRD is confirmed and saved.

### 2.1 Ask for the PRD

> Share your PRD (Product Requirements Document). You can:
> - Paste it directly
> - Point me to a file (e.g., `docs/PRD.md`)
> - Describe the project and I'll help you draft one

### 2.2 PRD Review Loop

Once the user provides a PRD:

1. Read it carefully — domain, users, features, constraints
2. Ask clarifying questions — gaps, ambiguities, assumptions
3. Suggest improvements — missing sections, risks
4. Iterate — 2-3 rounds is normal

> **PRDs evolve — that's normal.** Real projects go through 3-8 PRD versions as requirements get clearer. Don't try to make the first draft perfect. Get the vision right, then refine in later rounds as you learn from building. Each version gets more focused.

Key sections to look for (suggest adding if missing):
- Problem statement & target users
- Core features (MVP scope)
- Technical constraints (stack, hosting, integrations)
- Non-functional requirements (performance, security, scale)
- Out of scope (explicitly)

### 2.3 Save the Final PRD

Once the user says the PRD is final, save to `docs/PRD.md`.

**Confirm with user:** "PRD saved. Ready to scaffold the architecture?"

**Mark Phase 2 done. Move to Phase 3.**

---

## Phase 3: Scaffold arch.md

### 3.1 Create Architecture Index

Based on the confirmed PRD, create `docs/arch.md` from `docs/arch.md.template`:

- Fill in project name, tech stack, structure
- Keep it under 300 lines — 1-line entries + links to feature docs
- Set version to 0.1

### 3.2 Create Feature Doc Stubs

For each major feature in the PRD, create a stub in `docs/features/` using `docs/features/_template.md`.

### 3.3 Create docs/plans/

```bash
mkdir -p docs/plans
```

This folder stores research, migration scripts, diagrams, and architecture plans from `/advise` sessions.

**Mark Phase 3 done. Move to Phase 4.**

---

## Phase 4: Customize Skills

### 4.1 /advise — Add project context

Edit `.claude/skills/advise/SKILL.md` — find the `<!-- CUSTOMIZE -->` comment and add a Context section with project-specific domain, constraints, and key docs to read before advising.

### 4.2 /startnow — Add project-specific config files

Edit `.claude/skills/startnow/SKILL.md` Step 5 — add any project-specific config files (e.g., `wrangler.toml`, `supabase/config.toml`).

### 4.3 /updatenow — Remove placeholder, add project name

Edit `.claude/skills/updatenow/SKILL.md`:
- Remove the `<!-- CUSTOMIZE -->` guide page placeholder section
- Add the project name to the skill description

### 4.4 /l3 — Add project-specific debug areas

Edit `.claude/skills/l3/SKILL.md`:
- Replace the placeholder investigation areas table with actual project paths and common issues

### 4.5 Update CLAUDE.md

Add any project-specific rules discovered during PRD review that weren't covered in Phase 1.

**Mark Phase 4 done. Move to Phase 5.**

---

## Phase 5: Ready to Build

### 5.1 Summary

Present to the user:

```
Project: [name]
Stack:   [tech stack from arch.md]
Repo:    [GitHub URL if created]

Files created:
  docs/arch.md              — architecture index (v0.1)
  docs/PRD.md               — confirmed PRD
  docs/features/*.md        — feature doc stubs
  docs/plans/               — for research + migration artifacts
  CLAUDE.md                 — project rules

Available commands:
  /advise [topic]     — research a problem, get options + recommendation
  /startnow           — load project context at session start
  /updatenow          — update arch.md + feature docs after changes
  /l3 [issue]         — investigate and debug issues
  /localcompact       — trim arch.md back under 300 lines (dry-run by default)
  /audit [focus]      — project health check (security, cost, performance, quality, infra)

Ready to build. What feature should we start with?
```

### 5.2 Update GitHub Repo Info

If a GitHub repo was created in Phase 1, update it to reflect the actual project:

1. **Write a README.md** — Replace the kit README with a project-specific one:
   - What the project does (1-2 sentences)
   - Tech stack table
   - Architecture highlights (3-5 bullet points on interesting technical decisions)
   - Project structure overview
   - Keep it public-friendly — no internal jargon, no controversial framing

2. **Set repo description** — One-line summary for the GitHub repo page:
   ```bash
   gh repo edit OWNER/REPO --description "Short description of what this project does and key technologies used."
   ```

3. **Add topics** — Help discoverability:
   ```bash
   gh repo edit OWNER/REPO --add-topic nextjs --add-topic typescript --add-topic ai
   ```
   Add 5-10 relevant topics based on the tech stack and domain.

### 5.3 Recommended Workflow

```
/advise [feature] → pick option → build → /updatenow → commit → repeat
```

### 5.4 Cleanup

Tell the user:

> **Setup complete.** StartHere.md is no longer needed. You can:
> - Delete it: `rm StartHere.md`
> - Archive it: `mv StartHere.md docs/meta/StartHere.md.archive`
>
> From now on, start each session with `/startnow`.

**Mark Phase 5 done. Stop reading this file in future sessions.**

---

## Appendix: Post-Bootstrap Checklist

Things to do after you start building (not during bootstrap):

- [ ] Update README.md as the project evolves (new features, architecture changes)
- [ ] Update GitHub repo description if the project scope changes
- [ ] Add a `.gitignore` appropriate for your stack
- [ ] Set up CI/CD if needed (GitHub Actions, Railway auto-deploy)
- [ ] Run `/audit` after first deploy to check security, cost, and performance
