# App Types — Traditional vs Agentic

**Authors:** gmarmat
**Last updated:** 2026-03-10

> Teaching reference for explaining what kind of app best suits a friend's needs.

---

## The Spectrum

```
Fully Traditional ◄──────────────────────► Fully Agentic

Traditional     AI-Enhanced     AI Decision-Making     Fully Autonomous
(no AI)         (AI as tool)    (AI as router)         (AI as executor)
```

---

## Comparison

| | Traditional (No AI) | AI-Enhanced | AI Decision-Making | Fully Autonomous |
|---|---|---|---|---|
| **Example** | Expense tracker — user enters amounts, sees totals | Recipe app — paste ingredients, AI suggests meals | Email triage — AI reads inbox, labels/prioritizes, drafts replies | Travel agent — "plan my Tokyo trip", books flights/hotels/activities |
| **Who decides next step** | Your code | Your code | The AI | The AI |
| **AI role** | None | Tool at a button click | Router + decision maker | Planner + executor |
| **Path** | Fixed, coded | Fixed, AI fills a gap | AI picks the path | AI picks everything |
| **Output** | Exact same every time | Varies slightly | Varies per context | Varies significantly |
| **Cost** | Hosting only | API calls per feature | Higher API volume | Highest — multi-step chains |
| **Complexity** | Low | Low-Medium | Medium-High | High |

---

## Pros & Cons

| | Traditional | AI-Enhanced | AI Decision-Making | Fully Autonomous |
|---|---|---|---|---|
| **Pro 1** | Predictable. No surprises. | Easy AI win. Low risk. | Saves user real time. | Hands-free magic. |
| **Pro 2** | Cheapest to run. | Users love "smart" features. | Handles complexity for user. | Biggest wow factor. |
| **Pro 3** | Easiest to debug. | One API call per action. | Scales decision load. | Replaces entire workflows. |
| **Con 1** | Manual everything. | API keys to manage. | Harder to debug. | User shares credentials. |
| **Con 2** | No intelligence. | Monitor usage/costs. | Needs guardrails. | Expensive to run. |
| **Con 3** | Doesn't scale decisions. | AI errors are visible. | Users must trust it. | Hardest to test. |

---

## Key Concerns by Type

| Type | What to Watch Out For |
|------|----------------------|
| **Traditional** | None — standard app concerns only |
| **AI-Enhanced** | Manage API keys securely. Never store locally. Monitor spend on provider dashboard + in-app settings page. |
| **AI Decision-Making** | Set boundaries on what AI can/can't do. Log every decision. Human-in-the-loop for high-stakes actions. |
| **Fully Autonomous** | User may grant OAuth/creds to external tools. Audit trail is critical. Cost can spike unpredictably. |

---

## Rule of Thumb

```
More AI autonomy = more power for the user
                 = more risk/cost for you to manage
                 = more trust required from the user
```

Start simple. Add autonomy only when the user's problem demands it.

---

## Core Concept

- **Non-agentic:** You code every step. Same input = same path = same output. Deterministic.
- **Agentic:** You define the goal. AI figures out the steps. The *goal* is fixed, the *execution* varies each run. Intent-preserving, not deterministic.
- **Most real apps are hybrid.** A CRUD app with a summarize button is traditional + one AI-enhanced feature. That's fine. Match the tool to the problem.
