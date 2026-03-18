# Design System Reference

**Version:** 1.0 | **File:** `design/globals.css`

---

## Architecture

```
┌─────────────────────────────────────────────────────────────┐
│  Layer 3: Component Tokens                                  │
│  (KPI cards, data tables, badges, filter pills, timeline)   │
│  (+ your domain-specific tokens: categories, statuses)      │
├─────────────────────────────────────────────────────────────┤
│  Layer 2: Semantic Tokens                                   │
│  (--ext-primary, --ext-success, --ext-bg-*, theme-aware)    │
│  (shared across all features — never override per-feature)  │
├─────────────────────────────────────────────────────────────┤
│  Layer 1: Color Primitives                                  │
│  (raw values: --ext-blue-500, --ext-gray-100, etc.)         │
└─────────────────────────────────────────────────────────────┘
```

**Token prefix:** `--ext-*`
**CUSTOMIZE:** Replace `--ext-` with your project prefix (e.g., `--myapp-`, `--ds-`).

**Framework:** Tailwind CSS v4 + Shadcn/UI. Custom tokens extend Tailwind's `@theme`. Shadcn provides base components. Custom tokens handle layout and dashboard-specific styling.

**Dark/light mode:** Controlled via `data-theme="dark"` or `data-theme="light"` attribute on `<html>` or a parent element. Not the `.dark` class.

---

## Layer 1: Color Primitives

8 color scales, values chosen for WCAG 2.1 AA compliance.

| Scale | Use |
|-------|-----|
| `--ext-blue-*` | Primary actions, links, brand |
| `--ext-gray-*` | Neutrals, backgrounds, borders |
| `--ext-green-*` | Success, positive, active |
| `--ext-yellow-*` | Warning, pending, caution |
| `--ext-orange-*` | Accent, escalation, highlight |
| `--ext-red-*` | Danger, error, critical |
| `--ext-purple-*` | Tertiary info, special states |
| `--ext-cyan-*` | Info, neutral callouts |

Full hex values in `globals.css` Layer 1 section.

---

## Layer 2: Semantic Tokens

Use these in components — never reach for Layer 1 primitives directly in UI code.

### Status

| Token | Light | Dark |
|-------|-------|------|
| `--ext-primary` | blue-600 | blue-500 |
| `--ext-success` | green-700 | green-500 |
| `--ext-warning` | yellow-700 | yellow-400 |
| `--ext-danger` | red-600 | red-500 |
| `--ext-info` | cyan-600 | cyan-400 |
| `--ext-*-subtle` | 50-shade bg | 15% rgba bg |

### Text

| Token | Purpose |
|-------|---------|
| `--ext-text-primary` | Main content |
| `--ext-text-secondary` | Labels, secondary |
| `--ext-text-muted` | Placeholders, hints |
| `--ext-text-inverse` | Text on colored bg |

### Backgrounds

| Token | Purpose |
|-------|---------|
| `--ext-bg-primary` | Page/main background |
| `--ext-bg-secondary` | Sidebar, panel bg |
| `--ext-bg-tertiary` | Table headers, hover states |

### Borders & Cards

| Token | Purpose |
|-------|---------|
| `--ext-border-default` | Standard borders |
| `--ext-border-muted` | Subtle separators |
| `--ext-border-strong` | Emphasized borders |
| `--ext-card-bg` | Card background |
| `--ext-card-border` | Card border |
| `--ext-card-shadow` | Card shadow |
| `--ext-card-shadow-hover` | Card hover shadow |

### Forms & Focus

| Token | Purpose |
|-------|---------|
| `--ext-input-bg` | Input background |
| `--ext-input-border` | Input border |
| `--ext-input-focus-ring` | Input focus shadow |
| `--ext-focus-ring` | WCAG 2.4.7 focus ring |

### Spacing, Radius, Transitions

```css
/* Spacing */
--ext-spacing-xs: 0.25rem   --ext-spacing-sm: 0.5rem
--ext-spacing-md: 1rem      --ext-spacing-lg: 1.5rem
--ext-spacing-xl: 2rem      --ext-spacing-2xl: 3rem

/* Radius */
--ext-radius-sm: 0.25rem    --ext-radius-md: 0.5rem
--ext-radius-lg: 0.75rem    --ext-radius-xl: 1rem
--ext-radius-full: 9999px

/* Transitions */
--ext-transition-fast: 150ms ease
--ext-transition-normal: 250ms ease
--ext-transition-slow: 350ms ease
```

---

## Layer 3: Component Classes

### KPI Cards

```html
<div class="ext-kpi-card">
  <div class="ext-kpi-icon primary">📊</div>
  <div class="ext-kpi-value">1,234</div>
  <div class="ext-kpi-label">Total Records</div>
  <span class="ext-kpi-delta positive">+12%</span>
</div>
```

Icon variants: `primary`, `danger`, `success`, `warning`
Delta variants: `positive`, `negative`, `neutral`

---

### Status Badges

```html
<span class="ext-badge ext-badge--success">Active</span>
<span class="ext-badge ext-badge--warning">Pending</span>
<span class="ext-badge ext-badge--danger">Error</span>
<span class="ext-badge ext-badge--info">Info</span>
<span class="ext-badge ext-badge--neutral">Inactive</span>
<span class="ext-badge ext-badge--primary">Featured</span>
```

Role badges: `ext-badge--super-admin`, `ext-badge--admin`, `ext-badge--viewer`

---

### Status Cards (left-border accent)

```html
<div class="ext-status-card status-success">...</div>
<div class="ext-status-card status-warning">...</div>
<div class="ext-status-card status-danger">...</div>
<div class="ext-status-card status-info">...</div>
<div class="ext-status-card status-neutral">...</div>
```

---

### Data Table

```html
<table class="ext-data-table">
  <thead><tr><th>Name</th><th>Value</th></tr></thead>
  <tbody>
    <tr><td>Item A</td><td class="amount">$1,234.00</td></tr>
  </tbody>
</table>

<!-- Compact variant -->
<table class="ext-data-table ext-data-table--compact">...</table>
```

---

### Filter Bar

```html
<div class="ext-filter-bar">
  <div class="ext-filter-group">
    <span class="ext-filter-label">Status</span>
    <button class="ext-filter-pill active">All</button>
    <button class="ext-filter-pill">Active</button>
    <button class="ext-filter-pill">Pending</button>
  </div>
</div>
```

---

### Empty State

```html
<div class="ext-empty-state">
  <div class="icon">📭</div>
  <h5>No items found</h5>
  <p>Try adjusting your filters or add a new item.</p>
</div>
```

---

### Upload Zone

```html
<div class="ext-upload-zone" tabindex="0">
  Drop files here or click to upload
</div>
```

Add `drag-over` class on dragenter/dragover events.

---

### Timeline

```html
<div class="ext-timeline">
  <div class="ext-timeline-item">
    <div class="ext-timeline-dot success"></div>
    <p>Event description</p>
  </div>
  <div class="ext-timeline-item">
    <div class="ext-timeline-dot danger"></div>
    <p>Error event</p>
  </div>
</div>
```

Dot variants: `success`, `warning`, `danger`, `neutral` (default: primary)

---

### Utility Animations

```html
<div class="ext-animate-slide-in">Slides up + fades in</div>
<div class="ext-animate-float-up">Floats up (notifications)</div>
<div class="ext-animate-dot-bounce">Typing indicator dot</div>
<div class="ext-animate-ticker">Horizontal scroll ticker</div>
<svg><circle class="ext-animate-donut-draw" .../></svg>
```

All animations are disabled for `prefers-reduced-motion`.

---

### Focus Ring

Apply to any interactive element for WCAG 2.4.7 compliance:

```html
<button class="ext-focus-ring">Accessible button</button>
```

---

## Tailwind Usage with ext-* tokens

These tokens are mapped into Tailwind's `@theme` so you can use them as utilities:

```html
<!-- Text colors -->
<p class="text-ext-text-primary">Main text</p>
<p class="text-ext-text-secondary">Secondary</p>

<!-- Background colors -->
<div class="bg-ext-bg-secondary">Panel</div>
<div class="bg-ext-primary">Primary action bg</div>

<!-- Border colors -->
<div class="border border-ext-border-default">...</div>

<!-- Status colors -->
<span class="text-ext-success bg-ext-success-subtle">Active</span>
```

---

## Shadcn/UI Integration

`globals.css` maps all `--ext-*` semantic tokens to Shadcn's expected CSS vars (`--background`, `--primary`, `--destructive`, etc.) in both light and dark modes. Shadcn components pick up theme changes automatically via `data-theme` attribute.

**Chart colors:** `--chart-1` through `--chart-9` are mapped for Shadcn's `<ChartContainer>`.
**Sidebar:** `--sidebar-*` vars are mapped for Shadcn's sidebar component.

---

## Adding Domain-Specific Tokens

Add your app's domain tokens in the designated section at the bottom of `globals.css`:

```css
/* LAYER 3: Domain-Specific Tokens */
:root {
  --ext-status-active: var(--ext-green-500);
  --ext-status-archived: var(--ext-gray-400);
  --ext-priority-high: var(--ext-red-500);
  --ext-priority-medium: var(--ext-yellow-500);
  --ext-priority-low: var(--ext-blue-400);
}

.ext-badge--active { background-color: var(--ext-success-subtle); color: var(--ext-success); }
.ext-badge--archived { background-color: var(--ext-bg-tertiary); color: var(--ext-text-muted); }
```

**Rule:** Layer 3 domain tokens reference Layer 2 semantic tokens, not Layer 1 primitives.

---

## Renaming the Prefix

To rename `--ext-` to your project's prefix (e.g., `--myapp-`):

```bash
# In your project's globals.css — find and replace:
# --ext- → --myapp-
# .ext- → .myapp-
# Also update @theme inline section and any component files using the classes
```

Keep it short (4-6 chars) to minimize CSS verbosity.
