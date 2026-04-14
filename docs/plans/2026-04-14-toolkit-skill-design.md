# /toolkit Skill Design — Research & Options

**Date:** 2026-04-14 | **Status:** Decision needed | **Scope:** claude-project-kit

---

## Problem Statement

Every production app needs two things the kit doesn't provide today:

1. **PM Intelligence Hub** — Business intelligence for the product owner: market research, pricing economics, competitive analysis, go-to-market strategy, sales tools. All researched, generated, and cited — not blank templates. Makes the builder an actual PM of their product with presentation-ready data for investors/executives.

2. **Product Feature Tiers** — App infrastructure that every production app reinvents: KPI dashboards, analytics, monitoring, cost tracking, A/B testing, admin panels, settings systems.

**Reference implementations:**
- Boris (`/bors/admin/internal-docs`) — 7-tab PM Intelligence Hub with sales calculator, market data, pricing models, competitive analysis, technical positioning, demo mode. All hardcoded HTML/JS with cited sources.
- PrepRight (`/jotrack-v2/`) — Product infrastructure: monitoring dashboard (4 tabs), A/B testing framework (5 DB tables), admin dashboards (4 pages), AI insights (6 views), settings system (8 tabs + audit log).

---

## Constraints

- **Generic** — No personal data, no company-specific info. Works for any project type.
- **Stack-agnostic** — Kit doesn't prescribe React/Vue/Python. Output must work anywhere.
- **Research-driven** — Intelligence Hub must actively research and cite, not just template.
- **Dual output** — Local HTML for non-web apps, super-admin route recommendation for web apps.

---

## Options

### Option A: Single `/toolkit` Skill, Guided Flow (Recommended)

One skill with two subcommands that share project context:

```
/toolkit research    → PM Intelligence Hub (standalone HTML)
/toolkit features    → Product Feature Tiers (specs + optional scaffolding)
/toolkit             → Guided flow: asks what you want, runs both if desired
```

**Intelligence Hub output:** Self-contained HTML file at `docs/toolkit/index.html`
- Vanilla JS + Chart.js (CDN) — no build step, opens in any browser
- Tab navigation: Dashboard, Market, Competitive, Pricing, Go-to-Market, Technical, Sales Tools
- Collapsible source citations on every section
- Print-friendly CSS for investor decks
- Uses kit design tokens if adopted, otherwise ships minimal embedded CSS
- Interactive calculator (JS) for pricing/margin scenarios

**Feature Tiers output:** Specification docs + optional code generation
- Reads arch.md for stack, generates stack-appropriate specs
- T1/T2/T3 tier selection
- For known stacks (Next.js + Supabase): can scaffold actual routes, components, migrations
- For other stacks: generates detailed specs in `docs/features/product-infrastructure.md`

**Research pipeline (Intelligence Hub):**
1. Read PRD → extract domain, users, value prop, features
2. Read arch.md → extract stack, infrastructure, data model
3. Ask user → confirm/provide infrastructure costs, pricing model
4. WebSearch (5-8 queries) → market size, competitors, pricing benchmarks, industry trends
5. Generate → all tabs with real researched data
6. Cite → every web source in collapsible `<details>` sections

| Criteria | Rating |
|----------|--------|
| Complexity | Medium-High |
| Time to build | ~3 sessions |
| User learning curve | Low (one command) |
| Reusability | High (both modes share context) |
| Wow factor | High (researched, interactive HTML) |

**Pros:**
- One skill to learn, natural flow (research → features)
- Shared context reading (arch.md, PRD read once)
- Extensible — can add more modes later
- Follows kit philosophy of guided workflows

**Cons:**
- Largest single skill (~250 lines)
- HTML generation is complex (tab layout, charts, calculator)
- Web research quality depends on search results

---

### Option B: Two Separate Skills

```
/pmhub              → PM Intelligence Hub only
/productfeatures    → Product Feature Tiers only
```

**Same outputs as Option A**, but split into two independent skills (~150 lines each).

| Criteria | Rating |
|----------|--------|
| Complexity | Medium |
| Time to build | ~3 sessions |
| User learning curve | Medium (two commands) |
| Reusability | Medium (no shared context) |
| Wow factor | High |

**Pros:**
- Clean separation of concerns
- Each skill is focused and maintainable
- Can run independently without the other

**Cons:**
- Two skills to remember
- Both need to read arch.md and PRD independently (duplicate work)
- Naming is awkward (`/pmhub`? `/bizhub`? `/intelligence`?)
- Harder to guide users through the natural flow

---

### Option C: `/toolkit` for Intelligence Hub + Extend `/audit` for Features

```
/toolkit            → PM Intelligence Hub (same as Option A research mode)
/audit features     → Recommends + scaffolds product infrastructure
```

**Intelligence Hub:** Same as Option A.
**Feature Tiers:** Added as a new focus area in the existing `/audit` skill.

| Criteria | Rating |
|----------|--------|
| Complexity | Low-Medium |
| Time to build | ~2 sessions |
| User learning curve | Lowest (leverages existing skill) |
| Reusability | High (audit already has infrastructure) |
| Wow factor | Medium (audit extension feels less special) |

**Pros:**
- Minimal new surface area (one new skill + one extension)
- `/audit features` is a natural fit ("what product infrastructure am I missing?")
- Audit already has WebSearch and analysis patterns

**Cons:**
- Audit becomes overloaded (6 focus areas → 7)
- Feature scaffolding is generative, not analytical — doesn't fit audit's nature
- Can't guide the user through tiers interactively (audit is report-style)
- Harder to re-run feature scaffolding iteratively

---

## Recommendation: Option A

**Single `/toolkit` skill with guided flow.** Reasons:

1. **One command** — `/toolkit` is easy to remember and type
2. **Natural flow** — Research the business first, then build the infrastructure
3. **Shared context** — Both modes need the same project docs
4. **Extensibility** — Can add `/toolkit demo` or `/toolkit pitch` later
5. **Matches kit philosophy** — Guided, structured, one step at a time

---

## Intelligence Hub Tab Design (Generalized from Boris)

| Tab | Content | Data Sources | Interactive Elements |
|-----|---------|--------------|---------------------|
| **Dashboard** | Executive summary, key metrics, strategic positioning, quick nav | PRD + arch.md | Copy-to-clipboard summary |
| **Market Analysis** | TAM/SAM/SOM, target segments, market size, growth trends | WebSearch + PRD | None (reference) |
| **Competitive Landscape** | Alternatives table, positioning matrix, differentiation | WebSearch | Sortable table |
| **Pricing & Economics** | Pricing tiers, cost model, gross margins, unit economics | User input + infra costs + WebSearch | Sensitivity sliders, margin calculator |
| **Go-to-Market** | Launch strategy, channels, messaging, timeline | WebSearch + PRD | Checklist |
| **Technical** | Architecture highlights, integration guide, security model | arch.md + feature docs | Collapsible deep dives |
| **Sales Tools** | Deal calculator, talking points, objection handlers, demo guide | All above synthesized | Interactive calculator |

**Source citation pattern (from Boris):**
```html
<details class="sources-section">
  <summary>Sources & References</summary>
  <ul>
    <li><a href="URL" target="_blank">Source Title</a> — Retrieved YYYY-MM-DD</li>
  </ul>
</details>
```

---

## Product Feature Tiers (Generalized from PrepRight)

### T1: MVP (Day 1)

| Feature | What | DB Tables | Routes |
|---------|------|-----------|--------|
| KPI Dashboard | Key metrics cards, recent activity | Uses existing tables | `/admin/dashboard` |
| Settings System | Profile, preferences, theme | `user_settings` + `user_settings_history` | `/settings/*` |
| Audit Log | Track all user/system actions | `audit_log` | `/admin/audit` |
| Version Display | App version in footer/settings | `lib/version.ts` | — |

### T2: Growth (After first users)

| Feature | What | DB Tables | Routes |
|---------|------|-----------|--------|
| Analytics | Usage trends, feature adoption, daily actives | `analytics_events` | `/admin/analytics` |
| Monitoring | Cost tracking, cache performance, error rates | `cache_metrics`, `operation_metrics` | `/admin/monitoring` |
| A/B Testing | Experiments, variants, segments, metrics | `experiments`, `variants`, `user_variants`, `segments`, `metrics` | `/admin/experiments` |
| Notifications | Email/in-app notification preferences | `notification_preferences` | `/settings/notifications` |

### T3: Enterprise (When selling to orgs)

| Feature | What | DB Tables | Routes |
|---------|------|-----------|--------|
| Multi-Tenant Admin | Tenant CRUD, isolation, switching | `tenants`, RLS policies | `/admin/tenants` |
| User Management | Invite, roles, permissions | `users` + RBAC policies | `/admin/users` |
| RBAC | Role-based access, middleware guards | `roles`, `permissions` | Middleware |
| Developer/API | API key management, rate limits, docs | `api_keys`, `rate_limits` | `/settings/developer` |
| Compliance | Data export, retention policies, GDPR | `data_exports` | `/settings/privacy` |

---

## Integration Points with Existing Kit

| File | Change |
|------|--------|
| `README.md` | Add toolkit to "What's Included" section (7th skill) |
| `StartHere.md` | Add recommendation at end of Phase 5: "After core features, run /toolkit" |
| `docs/meta/cheat-sheet.md` | Add `/toolkit` to skills table |
| `docs/meta/product-toolkit.md` | **NEW** — Reference doc explaining the concept, tabs, tiers |
| `.claude/skills/toolkit/SKILL.md` | **NEW** — The skill itself |

---

## HTML Output Architecture

**Self-contained single file:** `docs/toolkit/index.html`

```
┌─────────────────────────────────────────────────────────────────┐
│  <head>                                                         │
│    Embedded CSS (kit design tokens OR minimal fallback)         │
│    Chart.js from CDN                                            │
│    Print-friendly @media rules                                  │
│  </head>                                                        │
│  <body>                                                         │
│    <header> Product name + generation date + version </header>  │
│    <nav> Tab buttons (7 tabs) with URL state sync </nav>        │
│    <main>                                                       │
│      <section id="dashboard"> ... </section>                    │
│      <section id="market"> ... </section>                       │
│      <section id="competitive"> ... </section>                  │
│      <section id="pricing"> ... </section>                      │
│      <section id="gtm"> ... </section>                          │
│      <section id="technical"> ... </section>                    │
│      <section id="sales-tools"> ... </section>                  │
│    </main>                                                      │
│    <footer> Generated by /toolkit • Sources cited inline </footer>│
│    <script>                                                     │
│      Tab navigation + URL state                                 │
│      Calculator logic (pricing/margins)                         │
│      Chart.js initialization                                    │
│      Copy-to-clipboard                                          │
│      Collapsible sections                                       │
│    </script>                                                    │
│  </body>                                                        │
└─────────────────────────────────────────────────────────────────┘
```

**Key patterns from Boris to preserve:**
- `data-bs-toggle="tab"` pattern (adapted to vanilla JS, no Bootstrap dependency)
- `.sources-section` collapsible citations
- `.stats-card` KPI layout
- `.pricing-tier-card` with `.recommended` highlight
- `.deep-dive-section` collapsible `<details>` blocks
- `formatCurrency()`, `formatNumber()`, `formatPercent()` utility functions
- URL state sync on tab change (`?tab=market`)

**Key differences from Boris:**
- No Bootstrap dependency — vanilla CSS + kit tokens
- No Jinja2 — pure HTML (generated by Claude, not templated)
- No server-side auth — standalone file, auth is irrelevant
- Generic domain — no utility-specific terminology
- All data researched at generation time — no hardcoded industry numbers

---

## Research Quality Strategy

**Problem:** Web research quality varies. How do we ensure the Intelligence Hub is useful?

**Approach:**
1. **Multiple search queries** — 5-8 targeted searches, not one generic query
2. **Source verification** — Prefer .gov, .org, industry reports, major publications
3. **Recency filter** — Flag data older than 2 years
4. **Confidence levels** — Mark data as "verified" (multiple sources agree) or "estimated" (single source / calculated)
5. **User review gate** — Present research summary before generating HTML. User confirms or corrects.
6. **Regenerable** — User can run `/toolkit research` again to refresh data

**Search query templates:**
```
"[product domain] market size TAM SAM 2025 2026"
"[product domain] competitors alternatives comparison"
"[product domain] SaaS pricing models benchmarks"
"[product domain] industry trends growth forecast"
"[product domain] customer acquisition cost channels"
"[product domain] [specific technology] adoption rate"
```

---

## Open Questions

| # | Question | Impact | Status |
|---|----------|--------|--------|
| 1 | Should the HTML use the kit's design system CSS or ship its own minimal CSS? | Visual consistency vs portability | **Recommend: ship minimal CSS with optional kit token import** |
| 2 | Should `/toolkit features` generate actual code or just specs? | Scope vs value | **Recommend: specs for unknown stacks, code for Next.js + Supabase** |
| 3 | Should the skill be added to StartHere.md as Phase 6 or just mentioned in Phase 5? | Bootstrap flow | **Recommend: mention in Phase 5, not a new phase** |
| 4 | How to handle non-English markets / non-US research? | Internationalization | **Recommend: default to English/US, note limitation** |
| 5 | Should the calculator support custom formulas or just the Boris pattern? | Flexibility | **Recommend: Boris pattern (tier-based pricing) as default, extensible** |

---

## Sources

- [Tabler Dashboard UI Kit](https://github.com/tabler/tabler) — Open-source HTML dashboard, Bootstrap-based
- [Vanilla JS Dashboard (Medium)](https://medium.com/@michaelpreston515/how-i-built-a-real-time-dashboard-from-scratch-using-vanilla-javascript-no-frameworks-f93f3dce98a9) — No-framework dashboard approach
- [Chart.js Responsive Dashboards](https://medium.com/@francesco-saviano/build-responsive-dashboards-with-chart-js-fc5f7cc42f52) — Chart.js integration patterns
- [ChatPRD PM Templates](https://www.chatprd.ai/templates) — PM template library (competitive analysis, GTM)
- [HubSpot Product Marketing Kit](https://offers.hubspot.com/product-marketing-kit) — 14-template PM toolkit with pricing calculator
- [Competitive Analysis Framework](https://www.aakashg.com/competitive-analysis-framework-template/) — Structured competitive analysis for PMs
- [Dashboard Builder](https://dashboardbuilder.net/) — Export to universal HTML pattern
