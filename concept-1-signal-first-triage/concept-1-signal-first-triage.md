# Concept 1: Signal-First Triage

## Overview
A triage-optimized dashboard that prioritizes the developer's primary question: "Is my PR blocked, and what do I need to fix?" The entire interface is organized around a binary verdict banner, delta-first stats, and inline violation expansion with a three-tab detail pattern (Why / Where / How to fix).

## Key Differentiator
**Inline everything.** No modals, no page changes, no context switching. The developer can triage every issue from a single scrollable page — expand a package, expand a violation, read the fix, skip or resolve — all without navigating away.

## User Flow

```
┌─────────────────────────────────────┐
│  VERDICT BANNER: Blocked — 3 new    │
├─────────────────────────────────────┤
│  STATS: 3 new │ 1 fixed │ 12 pre   │
├─────────────────────────────────────┤
│  SCOPE: [This PR] [Full Audit]      │
├─────────────────────────────────────┤
│  FAILED PACKAGES (3)                │
│  ┌─ @wix/editor-elements-library ──┐│
│  │  ▲ Blocked │ 2 new │ 5 pre     ││
│  │  ┌─ Violation 1 ──────────────┐││
│  │  │  [Why] [Where] [How]       │││
│  │  │  + Skip dropdown           │││
│  │  └────────────────────────────┘││
│  └─────────────────────────────────┘│
│  PASSED PACKAGES (42) ▸ collapsed   │
└─────────────────────────────────────┘
```

## Screens & States

### 1. Dashboard — Blocked State
- Hero verdict: red banner "Blocked — 3 new accessibility issues"
- Stats strip: New (red) / Fixed (green) / Pre-existing (grey) / Packages / Pass rate
- Scope toggle: "This PR" (default) / "Full Audit"
- Failed packages table (expanded by default)
- Passed packages (collapsed)

### 2. Package Drill-Down (Inline Expansion)
- Click a failed package row → violations list expands below
- Each violation shows: title, severity badge (shape+color+label), category tag, element count
- New violations are full-opacity; pre-existing are dimmed with "Pre-existing" tag

### 3. Violation Detail (Three-Tab Pattern)
- Click a violation → detail panel expands with three tabs:
  - **Why is this an issue?** — Human impact ("Who this affects") + technical explanation
  - **Where is it?** — Code snippet + CSS selector
  - **How to fix** — Numbered steps + WCAG link at bottom

### 4. Skip Flow (Inline Dropdown)
- "Skip" button on each violation → dropdown (not modal):
  - "Skip for this PR" — temporary, returns next time
  - "Not relevant" — permanent dismissal
- Selecting either shows mandatory reason textarea + Confirm button
- After skip: card dims, gains left border accent, shows "Unskip" link

### 5. All Passing State
- Green verdict banner: "All checks passed"
- Centered celebration: checkmark icon + "No new accessibility issues"
- Pre-existing count shown for reference

## Requirement Coverage

| Req | Status | How |
|-----|--------|-----|
| R1 Overview Dashboard | ✅ | Verdict banner + stats strip |
| R2 Package summary | ✅ | Failed/passed package tables |
| R3 Violations breakdown | ✅ | Inline expansion per package |
| R4 Issue detail | ✅ | Three-tab Why/Where/How pattern |
| R5 Skip flow | ✅ | Inline dropdown + reason textarea |
| R6 Unskip | ✅ | "Unskip" link on skipped items |
| R7 Benchmark mode | ✅ | Pre-existing items dimmed with tag; scope toggle |
| R8 All passing | ✅ | Celebration state with green banner |
| R9 Dark mode | ✅ | CSS variable theme toggle |
| R10 Standalone HTML | ✅ | Single file, vanilla JS, no deps |
| R11 Professional design | ✅ | Developer-tool aesthetic |
| R12 Information overload | ✅ | Progressive disclosure (collapsed packages/violations) |
| R13 Benchmark vs skip | ✅ | Pre-existing = automatic tag; Skip = manual action with reason |
| R14 Accessible indicators | ✅ | Shape + color + label for all status badges |
| R15 Multiple audiences | ✅ | Scope toggle for dev view (This PR) vs full audit |

## Pros
- **Fastest triage flow** — everything inline, zero navigation
- **Familiar pattern** — resembles Lighthouse/SonarQube, low learning curve
- **Clear hierarchy** — verdict → stats → packages → violations → detail
- **Minimal cognitive load** — progressive disclosure hides complexity until needed

## Cons
- **Can get long** — many packages with many violations = lots of scrolling
- **Single-axis grouping** — packages only; no grouping by rule or severity across packages
- **Limited lead/team view** — scope toggle is binary, no role-based customization
- **No trend data** — point-in-time snapshot only

## Design Considerations
- The three-tab detail pattern (Why/Where/How) is directly inspired by SonarQube's issue detail architecture, validated as the clearest info structure in UX research
- Skip dropdown (not modal) minimizes interruption — inspired by GitHub Code Scanning's dismiss flow
- Delta-first stats (new issues as the hero number) follows the 94% pattern identified in research
- Pre-existing items are visible but dimmed — never hidden — to prevent silent accumulation
