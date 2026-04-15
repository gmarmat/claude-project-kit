# Vibe Coding Kit — Journey Map

**Authors:** Gaurav Marmat & Claude
**Last updated:** 2026-03-10

> **Internal doc.** Ships with the kit in `docs/meta/` but is not referenced by StartHere.md or any skill. Safe to keep — won't surface during bootstrap. Use this to refine the kit and explain the flow to friends.

---

## How to Share the Kit

| Method | Command | Best For |
|--------|---------|----------|
| GitHub template | Friend clicks "Use this template" | Tech-savvy friends |
| Git clone | `git clone <repo-url> myproject` | Friends with git |
| Zip/AirDrop | Send the folder | Non-technical friends |
| Manual copy | `cp -r kit/ ~/myproject/` | Local sharing |

**What ships:**
```
myproject/
├── .claude/
│   ├── commands/
│   │   └── advise.md
│   └── skills/
│       ├── startnow/SKILL.md
│       ├── updatenow/SKILL.md
│       ├── localcompact/SKILL.md
│       └── l3/SKILL.md
├── docs/
│   ├── arch.md.template
│   └── features/
│       └── _template.md
├── CLAUDE.md.template
└── StartHere.md            <-- THE ENTRY POINT
```

**Also ships but hidden from bootstrap** (not referenced by StartHere.md or any skill):
```
docs/meta/                  <-- This folder (journey map, internal notes for kit refinement)
```

---

## Friend's Journey

```
 STEP 1: GET THE KIT                    STEP 2: INSTALL CLAUDE CODE
 ┌───────────────────┐                  ┌───────────────────────────┐
 │ Clone/copy/unzip  │                  │ npm install -g            │
 │ into project dir  │ ──────────────►  │   @anthropic-ai/          │
 │                   │                  │   claude-code             │
 └───────────────────┘                  └─────────────┬─────────────┘
                                                      │
                                                      ▼
 STEP 3: SAY THE MAGIC WORDS            STEP 4: CLAUDE BOOTSTRAPS
 ┌───────────────────────────┐          ┌───────────────────────────┐
 │ $ cd myproject            │          │ Claude reads StartHere.md │
 │ $ claude                  │          │ and runs 5 phases:        │
 │                           │ ──────►  │                           │
 │ > "Read StartHere.md and  │          │ [1] Environment check     │
 │    set up this project"   │          │ [2] Get PRD from user     │
 └───────────────────────────┘          │ [3] Scaffold arch.md      │
                                        │ [4] Customize skills      │
                                        │ [5] Ready to build        │
                                        │                           │
                                        │ Progress tracked in       │
                                        │ StartHere.md itself.      │
                                        │ Cannot skip phases.       │
                                        └─────────────┬─────────────┘
                                                      │
                                                      ▼
 STEP 5: VIBE CODING LOOP (daily)
 ┌──────────────────────────────────────────────────────────────┐
 │                                                              │
 │   /advise [topic]  ──► pick option ──► BUILD IT ──►          │
 │       │                                    │                 │
 │       │                               /updatenow            │
 │       │                                    │                 │
 │       │                                 commit               │
 │       │                                    │                 │
 │       ◄────────── next feature ◄───────────┘                 │
 │                                                              │
 │   Maintenance:                                               │
 │     /localcompact  ──► trim arch.md when > 250 lines         │
 │     /l3 [issue]    ──► debug when something breaks           │
 │     /startnow      ──► reload context at session start       │
 │                                                              │
 └──────────────────────────────────────────────────────────────┘
```

---

## Quick Pitch (what to tell your friend)

> "I made a starter kit for Claude Code. Copy this folder into your project, open Claude, and say 'Read StartHere.md and set up this project.' It'll ask you about your app, set up all the docs, and teach you the workflow. After that you just describe features and build."

---

## TL;DR for the friend

| Step | What | Time |
|------|------|------|
| 1 | Get the kit (clone/copy) | 1 min |
| 2 | Install Claude Code (`npm i -g @anthropic-ai/claude-code`) | 2 min |
| 3 | `cd myproject && claude` then "Read StartHere.md and set up this project" | 10-15 min |
| 4 | Start building: `/advise` then code then `/updatenow` then commit then repeat | ongoing |
