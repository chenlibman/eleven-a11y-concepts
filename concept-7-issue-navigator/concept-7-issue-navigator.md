# Concept 7: Issue Navigator — Persistent Nav Bar

## Overview
A persistent horizontal navigation bar of issue pills sits between the verdict and the detail area. Every issue is visible at a glance — colored by severity, marked by status — letting developers jump to any issue instantly. The selected issue opens in a full detail view below. After resolving, the nav auto-advances to the next open issue.

## Key Differentiator
**Always-visible issue map.** Unlike list-based views where resolved items scroll away, or card stacks where only one card is visible, the nav bar keeps the full picture accessible at all times. Developers always know where they are, what's done, and what's left — like a breadcrumb trail for accessibility issues.

## User Flow

```
┌──────────────────────────────────────────────────────────┐
│  ELEVEN  Accessibility Audit    PR #482    ☀ Dark Mode   │
├──────────────────────────────────────────────────────────┤
│  VERDICT: Blocked — 5 new issues    ██████░░ 3/5         │
├──────────────────────────────────────────────────────────┤
│  NAV BAR:                                                 │
│  [✓ 1 btn-name] [✓ 2 img-alt] [►3 contrast] [4 kbd] [5] │
│   ──────────── ─── Pre-existing ─── [7] [8] [9]         │
├──────────────────────────────────────────────────────────┤
│  DETAIL: Insufficient color contrast     ◆ SERIOUS       │
│  @wix/wsr-text · axe-core                                │
│                                                           │
│  [Why] [Where] [How]                                     │
│  Text with contrast ratio 2.8:1 fails WCAG AA...        │
│                                                           │
│  [✨ Fix with AI]  [🔧 Fix manually]  [⏭ Skip]           │
│                                                           │
│  [← Previous]                          [Next →]          │
└──────────────────────────────────────────────────────────┘
```

## Screens & States

### 1. Nav Bar
- Horizontal row of pill-shaped buttons, one per issue
- Each pill: issue number + severity dot (shape+color) + truncated rule name
- **Active**: bold border, elevated, inverted number badge
- **Open**: default styling, clickable
- **Fixed**: green checkmark, dimmed opacity
- **AI Fixed**: purple checkmark, dimmed
- **Skipped**: grey, strikethrough text, dimmed
- Pre-existing issues separated by a visual divider with "Pre-existing" label
- Pre-existing pills use dashed borders
- Sticky — stays visible while scrolling detail content
- Keyboard: arrow left/right to navigate between pills

### 2. Detail View
- Full-width panel below the nav bar for the selected issue
- Header: rule name, severity badge (shape+color+label), package badge, category
- Three tabs: **Why** / **Where** / **How**
  - Why: human impact description + technical explanation
  - Where: code location with file path + CSS selector + code snippet
  - How: numbered fix steps + WCAG criterion link
- Action buttons: Fix with AI / Fix manually / Skip
- Previous/Next navigation at the bottom

### 3. Fix with AI
- Click "Fix with AI" → inline diff panel expands below actions
- Shows red (removed) / green (added) code lines
- "Apply fix" resolves the issue and auto-advances
- "Dismiss" closes the diff panel

### 4. Skip Flow
- Skip button → dropdown with 4 reasons
- After skip: nav pill updates to skipped state, auto-advances to next open
- Undo toast appears for 5 seconds

### 5. Bulk Fix All with AI
- Button in the toolbar opens modal
- Shows all open issues with toggle switches and AI diffs
- "Apply selected fixes" resolves all toggled issues

### 6. Progress & Gamification (Light)
- Progress bar below verdict showing resolution percentage
- XP counter + streak badge in header (lightweight, not dominant)
- Confetti animation on all-resolved

### 7. All Passing State
- Green verdict banner
- Empty nav bar replaced with celebration message

## Requirement Coverage

| Req | Status | How |
|-----|--------|-----|
| R1 Overview Dashboard | ✅ | Verdict banner + progress bar |
| R2 Package summary | ✅ | Package badge per issue in detail view |
| R3 Violations breakdown | ✅ | Nav bar sorted by severity with colored indicators |
| R4 Issue detail | ✅ | Three-tab Why/Where/How with code snippets |
| R5 Skip flow | ✅ | Inline dropdown with mandatory reason |
| R6 Unskip | ✅ | Undo toast with working undo button |
| R7 Benchmark mode | ✅ | Pre-existing issues in separate nav section with dashed pills |
| R8 All passing | ✅ | Celebration state with confetti |
| R9 Dark mode | ✅ | CSS variable theme toggle |
| R10 Standalone HTML | ✅ | Single file, vanilla JS, no deps |
| R11 Professional design | ✅ | Clean developer-tool aesthetic |
| R12 Information overload | ✅ | One detail at a time; nav bar for orientation |
| R13 Benchmark vs skip | ✅ | Pre-existing = dashed border section; Skip = manual with reason |
| R14 Accessible indicators | ✅ | Shape + color + label for severity badges |
| R15 Multiple audiences | ✅ | Nav bar overview for leads; detail view for devs |

## Pros
- **Constant orientation** — always know where you are in the issue list
- **Random access** — jump to any issue, no sequential constraint
- **Status at a glance** — resolved/open/skipped visible across all issues simultaneously
- **Familiar pattern** — tab/breadcrumb navigation is well-understood by developers
- **Scales visually** — 5 issues or 20 issues, the nav bar adapts (horizontal scroll)

## Cons
- **Horizontal space** — many issues make pills small or require scrolling
- **Long rule names truncated** — pill labels can't show full issue names
- **Nav bar height** — takes vertical space away from the detail area
- **Less gamified** — lighter gamification than Concept 6 (XP exists but not dominant)
- **Pre-existing section** — divider in nav bar may confuse if benchmark concept is unfamiliar

## Design Considerations
- Nav bar pills use severity-colored dots (shape+color) for instant visual scanning
- Active pill is clearly distinguished with border + elevated shadow
- Sticky positioning ensures the nav bar is always reachable during long detail content
- Arrow key navigation makes rapid issue switching possible without mouse
- Auto-advance after resolve keeps the flow moving without manual clicking
- Pre-existing issues are visually separated but still accessible in the same nav bar
