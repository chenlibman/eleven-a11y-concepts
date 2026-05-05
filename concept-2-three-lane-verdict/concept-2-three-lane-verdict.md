# Concept 2: Three-Lane Verdict Board

## Overview
A Kanban-inspired layout that spatially separates issues into three distinct lanes — **New** (blocking), **Fixed** (resolved), and **Persisting** (reference baseline). The three-lane model draws from Trivago's three-category approach identified in UX research, giving developers an immediate visual map of what needs attention vs. what's already handled vs. what's pre-existing.

## Key Differentiator
**Spatial categorization.** Instead of a single list with status tags, issues live in physically separate columns. Developers' eyes go to the "New" lane; the other two lanes provide context without competing for attention. Skip/unskip moves cards between lanes with clear visual feedback.

## User Flow

```
┌─────────────────────────────────────────────────┐
│  VERDICT BANNER: Blocked — 3 new issues         │
├─────────────────────────────────────────────────┤
│  STATS: 3 new │ 1 fixed │ 5 persisting │ 45 pkg│
├─────────────────────────────────────────────────┤
│  ┌──── NEW (3) ────┬── FIXED (1) ──┬── PERSISTING (5) ──┐ │
│  │ ▪ Violation card │ ▪ Fixed card  │ ▪ Pre-existing card│ │
│  │ ▪ Violation card │              │ ▪ Pre-existing card│ │
│  │ ▪ Violation card │              │ ▪ Pre-existing card│ │
│  │                  │              │ ▪ ...dimmed        │ │
│  │  [Expand detail] │              │                    │ │
│  └──────────────────┴──────────────┴────────────────────┘ │
└─────────────────────────────────────────────────┘
```

## Screens & States

### 1. Dashboard — Blocked State
- Hero verdict: red banner "Blocked — 3 new accessibility issues"
- Stats strip: New (red) / Fixed (green) / Persisting (grey) / Packages / Pass rate
- Three-lane layout with tinted backgrounds (red tint for New, green tint for Fixed, grey for Persisting)
- Each lane has a header with count and color-coded border

### 2. Violation Cards
- Each card shows: rule name, severity badge (shape+color+label), package name, element preview
- New cards are full-opacity in the "New" lane
- Persisting cards are slightly dimmed with "Pre-existing" tag
- Fixed cards show green checkmark with "Resolved this PR" note

### 3. Card Expansion (Inline Detail)
- Click a card → expands to show three-tab detail (Why / Where / How to fix)
- **Why** — Human impact description + technical explanation
- **Where** — CSS selector + code snippet with highlighted element
- **How** — Numbered fix steps + WCAG reference link

### 4. Skip Flow (Inline on Card)
- "Skip" button on each New lane card → inline dropdown:
  - "Skip for this PR" — temporary dismissal
  - "Not relevant" — permanent dismissal
- Mandatory reason textarea + Confirm
- After skip: card visually moves/transitions to a "Skipped" sub-section within the lane
- "Unskip" link restores the card to its original position

### 5. All Passing State
- Green verdict banner: "All checks passed"
- Empty "New" lane with celebration message
- Fixed lane shows resolved items; Persisting lane shows reference baseline

## Requirement Coverage

| Req | Status | How |
|-----|--------|-----|
| R1 Overview Dashboard | ✅ | Verdict banner + stats strip |
| R2 Package summary | ✅ | Package grouping within each lane |
| R3 Violations breakdown | ✅ | Cards organized by category within lanes |
| R4 Issue detail | ✅ | Three-tab Why/Where/How on card expansion |
| R5 Skip flow | ✅ | Inline dropdown on New lane cards |
| R6 Unskip | ✅ | "Unskip" link on skipped items |
| R7 Benchmark mode | ✅ | Persisting lane = pre-existing baseline; New lane = delta |
| R8 All passing | ✅ | Green banner + empty New lane celebration |
| R9 Dark mode | ✅ | CSS variable theme toggle |
| R10 Standalone HTML | ✅ | Single file, vanilla JS, no deps |
| R11 Professional design | ✅ | Developer-tool aesthetic with lane tints |
| R12 Information overload | ✅ | Spatial separation reduces cognitive load |
| R13 Benchmark vs skip | ✅ | Persisting = automatic baseline; Skip = manual action with reason |
| R14 Accessible indicators | ✅ | Shape + color + label for severity badges |
| R15 Multiple audiences | ✅ | Developers focus on New lane; leads see all three |

## Pros
- **Instant visual mapping** — three categories are spatially obvious, no mental filtering needed
- **Natural workflow** — New lane is the "to-do list," mirrors how developers think about PR blockers
- **Clear three-category model** — strongest research-backed categorization (New/Fixed/Persisting)
- **Lane metaphor is familiar** — Kanban/Trello mental model requires zero learning

## Cons
- **Horizontal space pressure** — three columns need wide viewport; collapses to stacked on mobile
- **Fixed/Persisting lanes may feel empty** — if most issues are new, two lanes sit nearly empty
- **No package-level grouping** — violations are grouped by status, not by package
- **Card density** — many violations in one lane can still create scrolling fatigue

## Design Considerations
- Lane tints (red/green/grey backgrounds) provide ambient status without requiring reading
- Three-category model validated by Trivago and research as clearer than binary new/existing
- Cards are the primary interaction unit — expandable without page navigation
- Responsive layout stacks lanes vertically on narrow viewports with New lane always first
