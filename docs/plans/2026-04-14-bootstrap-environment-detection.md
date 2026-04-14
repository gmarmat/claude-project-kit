# Bootstrap Environment Detection — Phase 1 Enhancement

**Date:** 2026-04-14 | **Status:** Planned | **Scope:** StartHere.md Phase 1

---

## Problem

Phase 1 (Environment Check) currently verifies kit files exist and suggests MCP servers, but doesn't:
- Detect what tools the PRD requires (Supabase, Railway, Stripe, etc.)
- Check if those tools are installed and authenticated
- Guide the user through account creation with direct signup URLs
- Verify setup with actual CLI commands

## Proposed Enhancement

After PRD is reviewed (end of Phase 2 / start of Phase 3), add an **Environment Setup** step:

### Step 1: Detect Required Services

Read PRD for keywords → map to required CLI tools:

| PRD Keyword | CLI Tool | Check Command | Signup URL |
|-------------|----------|---------------|------------|
| Supabase | `supabase` | `supabase projects list` | https://supabase.com/dashboard |
| Railway | `railway` | `railway whoami` | https://railway.app |
| GitHub | `gh` | `gh auth status` | https://github.com/signup |
| Vercel | `vercel` | `vercel whoami` | https://vercel.com/signup |
| Stripe | `stripe` | `stripe config --list` | https://dashboard.stripe.com/register |
| Cloudflare | `wrangler` | `wrangler whoami` | https://dash.cloudflare.com/sign-up |
| Firebase | `firebase` | `firebase projects:list` | https://console.firebase.google.com |
| AWS | `aws` | `aws sts get-caller-identity` | https://aws.amazon.com |

### Step 2: Check Installation

```bash
which supabase && supabase --version || echo "NOT INSTALLED"
which railway && railway --version || echo "NOT INSTALLED"
which gh && gh auth status || echo "NOT INSTALLED or NOT AUTHENTICATED"
```

### Step 3: Guide Setup

For each missing/unauthenticated tool, present:
1. Install command (brew, npm, etc.)
2. Signup URL (direct link)
3. Auth command (`supabase login`, `railway login`, etc.)
4. Verification command

### Step 4: Verify All Green

Run all check commands, present status table:

```
| Service | Installed | Authenticated | Project Linked |
|---------|-----------|---------------|----------------|
| GitHub  | ✓ v2.x   | ✓ gmarmat    | ✓ repo created |
| Supabase| ✓ v1.x   | ✓ logged in   | ✗ needs project|
| Railway | ✗         | —             | —              |
```

## Placement

This runs **after** PRD is confirmed (Phase 2), because we need the PRD to know which services are required. Could be:
- End of Phase 2 (after PRD save, before arch.md scaffold)
- Start of Phase 3 (before scaffolding, ensures infra is ready)
- Separate Phase 2.5

## Implementation

Modify `StartHere.md` to add the detection step. No new skill needed — it's part of the bootstrap flow.
