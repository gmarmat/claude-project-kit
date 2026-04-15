# TaskFlow — Product Requirements Document (Example)

**Version:** 1.0 | **Updated:** 2026-01-15 | **Status:** Confirmed

> This is a **completed example** of what a PRD looks like after going through the StartHere.md process. Use it as a reference when writing your own PRD from `docs/PRD.md.template`.

---

## LLM Quick Start

- **What:** A personal task manager with natural language input and smart prioritization
- **Who:** Solo professionals managing 20-50 tasks across work and personal life
- **Stack:** Next.js 15, Supabase, Tailwind CSS, Vercel
- **Key constraint:** Single-user MVP — no teams, no sharing, no collaboration
- **Data strategy:** All data in Supabase. AI summarization via Claude API (BYOK).

---

## Executive Summary

TaskFlow is a task manager that lets you type tasks in natural language ("Call dentist Tuesday morning", "Review PR for auth feature by Friday") and automatically extracts due dates, priorities, and categories. Unlike Todoist or Things, it doesn't force you into a rigid structure — it adapts to how you naturally describe work.

### Value Proposition

| Stakeholder | Value |
|-------------|-------|
| Solo professional | Capture tasks in natural language without switching to "task manager mode" |
| Busy multitasker | Smart prioritization surfaces what matters today without manual sorting |

### Success Metrics

| Metric | Target | Measurement |
|--------|--------|-------------|
| Daily active usage | 5 days/week | Login frequency |
| Task capture speed | < 5 seconds per task | Time from open → task saved |
| Weekly task completion | > 70% of due tasks completed | Completed / total due |

---

## Problem Statement

### Current State

Solo professionals use a mix of sticky notes, email flags, calendar reminders, and task apps. No single tool captures tasks as fast as thinking them.

### Pain Points

| # | Pain Point | Who Feels It | Severity |
|---|-----------|-------------|----------|
| 1 | Switching to "task mode" breaks flow — have to pick project, set date, choose priority | Everyone | High |
| 2 | Tasks pile up without prioritization — everything feels urgent | Busy professionals | High |
| 3 | Existing apps are overbuilt — 80% of features are for teams, not individuals | Solo users | Medium |

### Desired State

Type a task in plain English. It's captured, categorized, prioritized, and shows up when it's relevant — without manual sorting.

---

## Target Users & Roles

| Role | Description | Key Permissions |
|------|-------------|----------------|
| User | Solo professional, 20-50 active tasks | Full CRUD on own tasks |

### Access Model

Email/password signup via Supabase Auth. Single user, no teams.

---

## Boundaries

| Category | Rule |
|----------|------|
| **ALWAYS** | Parse natural language input for dates, priorities, categories |
| **ALWAYS** | Show "today" view as default — what's due and what's overdue |
| **ASK FIRST** | Before deleting completed tasks older than 30 days |
| **NEVER** | Share task data with other users or third parties |
| **NEVER** | Require manual date/priority selection (always offer NLP as primary) |

---

## Core Features

### Phase 1 — MVP

**Goal:** Capture and manage tasks with natural language input
**Timeline:** 2-3 weeks

| # | Feature | Acceptance Criteria | Priority |
|---|---------|-------------------|----------|
| 1.1 | Natural language task input | Type "Call dentist Tuesday 2pm" → creates task with due date Tue 2pm | P0 |
| 1.2 | Today view | Shows tasks due today + overdue, sorted by priority | P0 |
| 1.3 | Task CRUD | Create, edit, complete, delete tasks | P0 |
| 1.4 | Smart categories | Auto-detect: work, personal, health, finance from task text | P0 |
| 1.5 | Priority detection | "urgent", "important", "asap" → high priority. Default: medium. | P1 |
| 1.6 | Upcoming view | Tasks due this week, grouped by day | P1 |

### Phase 2 — Intelligence

**Goal:** AI-powered prioritization and summaries
**Depends on:** Phase 1 complete

| # | Feature | Acceptance Criteria | Priority |
|---|---------|-------------------|----------|
| 2.1 | AI daily brief | Morning summary: "You have 5 tasks today. Top priority: [X]" | P1 |
| 2.2 | Smart reschedule | Suggest rescheduling overdue tasks based on today's load | P2 |
| 2.3 | Weekly review | End-of-week summary: completed, carried over, trends | P2 |

---

## Non-Functional Requirements

| Category | Requirement | Target |
|----------|-------------|--------|
| Performance | Page load | < 2s |
| Performance | Task creation | < 500ms |
| Security | Auth | Supabase Auth, RLS on all tables |
| Cost | Monthly infra | < $25 (Supabase free + Vercel free) |

---

## Out of Scope

| Feature | Why Not Now | Target Version |
|---------|-----------|----------------|
| Team collaboration | Single-user MVP | v2 |
| Mobile app | Web-first, responsive | v2 |
| Calendar sync | Complexity, auth flows | v2 |
| Recurring tasks | NLP complexity | v1.5 |

---

## Open Questions

| # | Question | Impact | Status |
|---|----------|--------|--------|
| 1 | Which NLP approach: regex patterns or Claude API? | Cost vs accuracy | Resolved — regex for dates, Claude for categories |
| 2 | Should completed tasks archive or delete? | UX + storage | Resolved — archive, auto-delete after 90 days |

---

## Revision History

| Ver | Date | Changes |
|-----|------|---------|
| 0.1 | 2026-01-10 | Initial draft from StartHere.md Phase 2 |
| 0.2 | 2026-01-12 | Added boundaries table, refined NLP scope |
| 1.0 | 2026-01-15 | Confirmed after 3 rounds of iteration |
