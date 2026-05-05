# Concept 5: Adaptive Report Hub (Experimental)

## Overview
The ambitious, full-featured version. The Adaptive Report Hub opens pre-filtered based on context (GitHub check → new issues only) and adds role-based view presets (Developer / A11y Lead / Team Lead), trend sparklines per stat, bulk skip with preview, and AI-suggested fix prioritization. It implements the full three-category model with a celebratory "Fixed" section and cross-package grouping options.

## Key Differentiator
**Role-adaptive interface.** A single report that reshapes itself based on who's viewing it. Developers see a focused fix list; A11y Leads see cross-package patterns and bulk actions; Team Leads see a health table with trend data. The experimental concept pushes beyond the current requirements to explore what a mature version of ELEVEN could become.

## User Flow

```
┌──────────────────────────────────────────────────────────┐
│  ELEVEN  [Developer ▾] [A11y Lead] [Team Lead]  ☀ Theme │
├──────────────────────────────────────────────────────────┤
│  VERDICT: Blocked — 3 new a11y issues                    │
├──────────────────────────────────────────────────────────┤
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐    │
│  │ New: 3   │ │ Fixed: 1 │ │ Pre: 5   │ │ Pkgs: 45 │    │
│  │ ~~~~↗    │ │ ~~~~→    │ │ ~~~~↘    │ │          │    │
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘    │
├──────────────────────────────────────────────────────────┤
│  DEVELOPER VIEW:                                          │
│  ┌─ @wix/editor-elements ──────────────────────────────┐ │
│  │  ▼ Critical: Missing alt text                        │ │
│  │    [Why] [Where] [How]   [Skip ▾]                    │ │
│  │  ▶ Serious: Keyboard trap                            │ │
│  └──────────────────────────────────────────────────────┘ │
│                                                            │
│  A11Y LEAD VIEW:                                          │
│  Cross-package grouping by rule + bulk skip actions       │
│                                                            │
│  TEAM LEAD VIEW:                                          │
│  Package health table with trend arrows + pass rates      │
└──────────────────────────────────────────────────────────┘
```

## Screens & States

### 1. Dashboard — Developer View (Default)
- Hero verdict banner: blocked (red) or passing (green)
- Stats strip with trend sparklines (SVG mini-charts showing last N runs)
- Package accordion: failed packages expanded, each with violation cards
- Three-tab detail per violation (Why / Where / How)
- Skip/Unskip inline controls per violation

### 2. A11y Lead View
- Cross-package violation grouping: same rule across all packages
- Bulk skip: select multiple violations, apply skip reason once
- Category filters: axe-core, keyboard nav, focus ring, tab reachability
- Severity distribution chart

### 3. Team Lead View
- Package health table: name, pass rate, new issues, trend arrow (↑↓→), delta from last run
- Sortable columns
- At-a-glance monorepo health assessment
- No individual violation details — aggregated metrics only

### 4. Stat Cards with Sparklines
- Each stat (New, Fixed, Pre-existing, Packages) has a mini trend line
- Sparklines show last 5 runs for context
- Trend direction indicated with arrow + color

### 5. Skip Flow (Inline with Bulk Option)
- Single skip: inline dropdown with "Skip for this PR" / "Not relevant"
- Bulk skip (Lead view): select multiple → "Skip selected" → single reason for all
- Mandatory reason textarea + Confirm
- After skip: card dims, "Unskip" link

### 6. All Passing State
- Green verdict banner: "All checks passed — no new issues"
- Celebratory animation
- Fixed count highlighted as positive signal
- Sparklines show improvement trend

## Requirement Coverage

| Req | Status | How |
|-----|--------|-----|
| R1 Overview Dashboard | ✅ | Verdict banner + sparkline stat cards |
| R2 Package summary | ✅ | Package accordion (dev) + health table (lead) |
| R3 Violations breakdown | ✅ | Per-package + cross-package grouping options |
| R4 Issue detail | ✅ | Three-tab Why/Where/How |
| R5 Skip flow | ✅ | Inline dropdown + bulk skip in lead view |
| R6 Unskip | ✅ | "Unskip" link on skipped items |
| R7 Benchmark mode | ✅ | Pre-existing dimmed; three-category model throughout |
| R8 All passing | ✅ | Green banner + celebration + positive sparkline |
| R9 Dark mode | ✅ | CSS variable theme toggle |
| R10 Standalone HTML | ✅ | Single file, vanilla JS, no deps |
| R11 Professional design | ✅ | Developer-tool aesthetic with data visualization |
| R12 Information overload | ✅ | Role-based filtering reduces noise per audience |
| R13 Benchmark vs skip | ✅ | Pre-existing = automatic baseline; Skip = manual with reason |
| R14 Accessible indicators | ✅ | Shape + color + label on all badges; ARIA roles |
| R15 Multiple audiences | ✅+ | Three explicit role presets: Developer / A11y Lead / Team Lead |

## Expanded Features (Beyond Requirements)
- **Trend sparklines** — Historical context for each metric (last N runs)
- **Role-based views** — Three distinct views in one report instead of scope toggle
- **Bulk skip** — Lead efficiency: apply one reason to multiple violations
- **Cross-package grouping** — Same rule failing across packages surfaced as a pattern
- **Team Lead health table** — Aggregated metrics with sortable columns and trend arrows
- **Run metadata** — Run number, timestamp, branch/commit reference in top bar
- **"Experimental" badge** — Self-identifies as the ambitious variant

## Pros
- **Most complete solution** — addresses all requirements plus forward-looking features
- **Role-based views** — genuine multi-audience support, not just a toggle
- **Trend context** — sparklines answer "is this getting better or worse?" at a glance
- **Bulk operations** — dramatically speeds up lead workflows
- **Scalable architecture** — role-based views can evolve independently

## Cons
- **Highest complexity** — more code, more states, more edge cases
- **Sparklines need historical data** — first run has no trends to show
- **Role detection** — how does the report know who's viewing? (Could default to Developer)
- **Feature creep risk** — some expanded features may not justify implementation cost
- **Learning curve** — three views means three mental models to understand

## Design Considerations
- Role switcher uses tab-like buttons in the top bar — always visible, easy to discover
- Sparklines are small SVG polylines — no charting library needed, works standalone
- Team Lead view is intentionally aggregate-only — prevents leads from micromanaging individual violations
- "Experimental" badge sets expectations that this is the ambitious variant
- All expanded features have clear rationale tied to research insights (bulk actions from Code Climate, trend data from SonarQube dashboards, role presets from Datadog)
