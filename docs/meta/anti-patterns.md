# Anti-Patterns: What NOT to Do

These are the most common mistakes when using Claude Code for real projects. Each one is extracted from real experience across 10+ projects.

---

| # | Anti-Pattern | Why It's Bad | Do This Instead |
|---|-------------|-------------|-----------------|
| 1 | **No PRD, just start coding** | Claude makes wrong assumptions about scope and priorities | Write a PRD first, even a rough one — iterate 2-3 rounds |
| 2 | **One giant prompt** | Claude loses focus, misses requirements, generates inconsistent code | Break into sub-tasks — one feature at a time |
| 3 | **No CLAUDE.md** | Claude reinvents conventions every session — different patterns, different style | Set rules once in CLAUDE.md, enforce always |
| 4 | **Bloated arch.md (500+ lines)** | Wastes context tokens, Claude skims instead of reads | Run `/localcompact` — link to feature docs for details |
| 5 | **No version tracking** | Can't tell what changed or when, no rollback safety | Version history in arch.md + frequent git commits |
| 6 | **Vague instructions** | "Make it look better" → random changes you didn't want | Reference specific docs, patterns, and design tokens |
| 7 | **Skipping /updatenow** | Docs drift from reality, next session starts confused | Always update docs after changes — it's not optional |
| 8 | **Letting Claude decide architecture** | It optimizes for "works now" not "scales later" | Use `/advise` for all architecture decisions — you decide, Claude builds |
| 9 | **No boundaries table in PRD** | Claude does things you'd never want (deletes data, exposes keys) | Add ALWAYS / ASK FIRST / NEVER table to every PRD |
| 10 | **Mocking everything in tests** | Tests pass but production breaks — mock/real divergence | Hit the real database in integration tests |
| 11 | **AI attribution in commits** | Clutters git history with no practical value | Clean commit messages — focus on what changed and why |
| 12 | **One massive commit** | Impossible to rollback specific changes, unclear history | Commit after each sub-task — one commit = one logical change |

## The Root Cause

Most anti-patterns come from treating Claude as a magic box instead of a junior developer who needs structure. The fix is always the same: **give Claude better context, clearer boundaries, and smaller tasks.**
