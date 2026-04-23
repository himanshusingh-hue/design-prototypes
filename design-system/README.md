---
title: "Ethos Partnerships Design System — Folder Guide"
last_updated: "2026-04-02"
---

# Ethos Partnerships Design System

## How to use this folder

All HTML mockups need two stylesheets. Link them in this exact order:

```html
<!-- 1. Tokens + fonts + all EDS component classes (.eds-*) -->
<link rel="stylesheet" href="../design-system/ds.css">

<!-- 2. Portal-specific patterns (sidebar, navbar, tables, etc.) — only for portal pages -->
<link rel="stylesheet" href="../design-system/shared-components.css">
```

`ds.css` is a single flat file — fonts, tokens, and all `.eds-*` classes are inlined directly, no imports. `shared-components.css` is portal-only; omit it for non-portal mockups (e.g. Agent Assisted Application funnel, standalone widgets).

---

## What's in this folder

| File | Purpose |
|------|---------|
| `ds.css` | Single flat file — all tokens, fonts, and `.eds-*` component classes in one place |
| `shared-components.css` | Portal-specific patterns not in EDS (Sidebar, NavBar, PageHeader, DataTable, etc.) |
| `fonts/` | Brand font files (woff/woff2) — referenced by `ds.css`, not linked separately |
| `shared-components-reference.html` | Canonical worked example — portal shell with DataTable, SummaryCardStrip, badges |
| `eds-preview.html` | Visual preview of all `.eds-*` component classes |

---

## Component coverage — what exists where

Scan this table before writing any CSS. If the component exists, use its class — never reinvent it.

| What you need | File | Class(es) |
|---------------|------|-----------|
| **Button** (13 variants, 5 sizes) | `ds.css` | `.eds-btn .eds-btn-primary`, `.eds-btn-secondary`, `.eds-btn-gray-outline`, etc. + `.eds-btn--sm/md/lg` |
| **Badge** (15 variants, 3 sizes) | `ds.css` | `.eds-badge .eds-badge-primary-solid`, `.eds-badge-info-light`, etc. + `--sm/md/lg` |
| **Alert** (5 variants) | `ds.css` | `.eds-alert`, `.eds-alert--success/info/warning/error` |
| **MessageBar** (7 variants) | `ds.css` | `.eds-message-bar--primary/info/warning/error/success/gray/white` |
| **Banner** | `ds.css` | `.eds-banner`, `.eds-banner-heading`, `.eds-banner-text` |
| **Modal** | `ds.css` | `.eds-modal-overlay`, `.eds-modal`, `.eds-modal-header`, `.eds-modal-body`, `.eds-modal-footer` |
| **TextInput** (3 sizes, 4 states) | `ds.css` | `.eds-input-wrapper`, `.eds-input`, `.eds-input--sm/md/lg`, `.eds-input--error` |
| **TextArea** | `ds.css` | `.eds-textarea`, `.eds-textarea--sm/md/lg` |
| **Dropdown** | `ds.css` | `.eds-dropdown`, `.eds-dropdown__control`, `.eds-dropdown__menu` |
| **Checkbox** | `ds.css` | `.eds-checkbox-wrapper`, `.eds-checkbox`, `.eds-checkbox--checked`, `.eds-content-checkbox` |
| **RadioButton** | `ds.css` | `.eds-radio-wrapper`, `.eds-radio`, `.eds-radio--checked`, `.eds-square-radio`, `.eds-square-radio--checked` |
| **Toggle** | `ds.css` | `.eds-toggle` (off), `.eds-toggle.eds-toggle--on` (on) |
| **Spinner** (5 sizes) | `ds.css` | `.eds-spinner`, `.eds-spinner--xs/sm/md/lg/xl`, `.eds-spinner--inverted` |
| **Accordion** | `ds.css` | `.eds-accordion`, `.eds-accordion__trigger`, `.eds-accordion__content`, `.eds-accordion--open` |
| **ProgressBar** | `ds.css` | `.eds-progress-bar`, `.eds-progress-bar__fill` |
| **ProgressSteps** | `ds.css` | `.eds-progress-steps`, `.eds-step`, `.eds-step--current/complete/next` |
| **FileUpload zone** | `ds.css` | `.eds-file-upload`, `.eds-file-upload--error` |
| **Portal Sidebar + TopNav** | `shared-components.css` | `.portal-sidebar`, `.top-nav`, `.top-nav-back`, `.main-content` |
| **PageHeader** | `shared-components.css` | `.page-header`, `.breadcrumb`, `.page-title` |
| **SummaryCardStrip** | `shared-components.css` | `.summary-card-strip`, `.summary-card`, `.summary-card--active/inactive` |
| **DataTableCard + Toolbar** | `shared-components.css` | `.data-table-card`, `.toolbar`, `.view-switcher`, `.table-pagination` |
| **StatusBadge** (app status pills) | `shared-components.css` | `.status-badge .status-badge--approved/submitted/lapsed/pending/premium-paying` etc. |
| **Customer360 shell** | `shared-components.css` | `.c360-layout`, `.c360-main`, `.c360-panel`, `.identity-bar` |
| **Numeric/% badge chip** | `shared-components.css` | `.badge`, `.badge--success/warning/error` (different from `.eds-badge`) |
| Toast / Snackbar | ❌ not in DS | Use `.eds-message-bar--*` instead |
| Drawer / Sheet / Sidebar panel | ❌ not in DS | Use `.eds-modal` (overlay pattern) |
| Tooltip | ❌ no CSS-only viable | Render as inline dark chip in static mockups |

> **For exact class names, size modifiers, HTML structure, and variant options:** read the EDS component sections in `ds.css` directly (Section 4) — each section has a usage block with copy-paste HTML examples.
>
> **For portal pattern anatomy** (what goes inside a DataTableCard, column structure, IdentityBar layout): read `context-docs/domain/agent-portal/design-reference/patterns.md`.

---

## Key usage rules

- **One primary action per page** — `.eds-btn-primary` is for the single most important action only. All other buttons use secondary, outline, or link variants.
- **MessageBar vs Alert** — use `.eds-message-bar` for inline contextual feedback within a form or card; use `.eds-alert` for page-level feedback above content.
- **Status pills** — always use `.status-badge .status-badge--[modifier]` from `shared-components.css` for application status. Never custom-style application statuses.
- **Numeric badges** — use `.badge .badge--success/warning/error` (from `shared-components.css`) for numeric/% chips in tables. Use `.eds-badge` for standalone label badges.
- **Stylesheet order** — `ds.css` must be first. `shared-components.css` must be second. Wrong order breaks layout.
- **Never re-implement** — if a class exists in either CSS file, use it. Override with a page-scoped rule if size/spacing adjustment is needed, don't create a new class.
- **Interactive states** — Toggle, Accordion, Checkbox, RadioButton use CSS modifier classes only. Add/remove `.eds-toggle--on`, `.eds-accordion--open`, `.eds-checkbox--checked` to show state. No JS needed in static mockups.
- **No hardcoded values** — never write a raw color, spacing, radius, or font-size in any `<style>` block or inline `style=""` attribute. Always use a CSS variable from `ds.css`. This applies to scaffold/wrapper styles too, not just DS component classes:
  ```css
  /* Correct */
  color: var(--neutrals-night-100);
  gap: var(--spacing-md);
  border-radius: var(--radii-2);
  font-size: var(--font-size-sm);

  /* Wrong */
  color: #272727;
  gap: 12px;
  border-radius: 8px;
  font-size: 13px;
  ```
  If no token matches exactly, use the nearest token and note the deviation in a comment.

---

## Compliance rules (IUL / Sahara features)

These rules apply to any feature that displays IUL illustration data:

1. **"For agent use only"** — any panel showing illustration highlights or the graph must carry this label.
2. **Non-guaranteed disclosure** — graph disclosure text is fixed: _"The values shown in the graph do not include guaranteed values - for agent use only."_ Do not paraphrase or omit.
3. **Tax disclaimer** — _"Clients should consult their tax advisor for tax guidance."_ Required at the bottom of any page where IUL products are visible. Not required on WL-only variants.
4. **Assumed rate label** — any KPI tile showing a rate must include "assumed non-guaranteed" qualifier.

---

## Token quick-reference

All tokens are defined in `ds.css`. Key prefixes:

**Colors**
- `--primary-cypress-*` — brand green (100 = #056257, 150 = #04463e, 5/10/25/50 = tints)
- `--neutrals-night-*` — greys (100 = near-black #272727, 60 = #7e7e7e, 10 = #e9e9e9, 5 = #f4f4f4)
- `--secondary-ocean-*` — blue/info
- `--secondary-spearmint-*` — light green/success
- `--secondary-salamander-*` — orange/warning
- `--utility-error-carmine-red-*` — error red
- `--utility-warning-royal-orange-*` — warning orange
- `--theme-*` — semantic aliases (e.g. `--theme-fg-default`, `--theme-bg-subtle`, `--theme-accent-default`)

**Spacing** — `--spacing-xs` (4px) → `--spacing-4xl` (64px)

**Sizing** — `--sizing-xs` (24px) → `--sizing-xl` (64px)

**Radii** — `--radii-0` (2px) → `--radii-9` (500px). Most components use `--radii-2` (8px).

**Font sizes** — `--font-size-xs` (11px), `--font-size-sm` (13px), `--font-size-md` (16px), `--font-size-lg` (19px), or numbered `--font-size-0` through `--font-size-11`.

**Shadows** — `--shadow-xs` through `--shadow-3xl`.
