# Concept 3: Focused Fix Sequence

## Overview
A guided, one-issue-at-a-time flow that replaces the traditional list-based dashboard with a sequential fixing experience. After the hero verdict, developers step through issues one by one (most critical first), seeing full context for each violation before moving to the next. Optimized for the "fix and move on" developer mindset.

## Key Differentiator
**Single-issue focus.** Instead of presenting all violations at once and letting developers choose where to start, this concept queues issues by priority and presents them one at a time with full context — like a code review tool that walks you through changes file by file.

## User Flow

```
┌─────────────────────────────────────────────────┐
│  VERDICT: Blocked — 3 new issues to fix         │
├─────────────────────────────────────────────────┤
│  PROGRESS: ●──●──○  (1 of 3)                   │
├─────────────────────────────────────────────────┤
│  CURRENT ISSUE:                                  │
│  ┌─────────────────────────────────────────────┐│
│  │  ■ Critical: Missing alt text               ││
│  │  @wix/editor-elements-library                ││
│  │                                              ││
│  │  [Why] — Human impact + technical detail     ││
│  │  [Where] — Code snippet + selector           ││
│  │  [How] — Numbered fix steps                  ││
│  │                                              ││
│  │  [ Skip ▾ ]    [ Mark Fixed ]  [ Next → ]   ││
│  └─────────────────────────────────────────────┘│
│                                                  │
│  ── Review complete! All 3 issues addressed ──   │
└─────────────────────────────────────────────────┘
```

## Screens & States

### 1. Verdict + Progress Bar
- Hero verdict: red banner "Blocked — 3 new accessibility issues"
- Stats strip: New / Fixed / Pre-existing counts
- Visual progress indicator: dots or bar showing current position (e.g., "Issue 1 of 3")
- Progress dots use filled/empty circles for completed/pending

### 2. Single Issue View
- Full-width card showing one violation at a time
- Title + severity badge (shape + color + label) + package name + category tag
- Detail sections visible by default (not tabbed — full context shown):
  - **Why is this an issue?** — Human impact description
  - **Where is it?** — Code snippet with CSS selector
  - **How to fix** — Numbered fix steps + WCAG link
- Action buttons: Skip / Next

### 3. Skip Flow (Inline)
- "Skip" button → inline dropdown (not modal):
  - "Skip for this PR" — temporary
  - "Not relevant" — permanent
- Mandatory reason textarea + Confirm
- After skip: issue marked as skipped, auto-advances to next
- Unskip banner appears with undo link

### 4. Review Complete State
- After all issues reviewed: celebration message
- Summary of actions taken: X fixed, Y skipped
- Links to review skipped items or view full audit

### 5. All Passing State
- Green verdict banner: "All checks passed"
- Centered celebration with checkmark
- Pre-existing count shown for reference

## Requirement Coverage

| Req | Status | How |
|-----|--------|-----|
| R1 Overview Dashboard | ✅ | Verdict banner + stats strip + progress bar |
| R2 Package summary | ✅ | Package name shown per issue; summary at review complete |
| R3 Violations breakdown | ✅ | Sequential presentation, severity-ordered |
| R4 Issue detail | ✅ | Full context visible per issue (Why/Where/How) |
| R5 Skip flow | ✅ | Inline dropdown with reason textarea |
| R6 Unskip | ✅ | Unskip banner with undo link |
| R7 Benchmark mode | ✅ | Pre-existing issues shown after new issues; dimmed with tag |
| R8 All passing | ✅ | Green banner + celebration state |
| R9 Dark mode | ✅ | CSS variable theme toggle |
| R10 Standalone HTML | ✅ | Single file, vanilla JS, no deps |
| R11 Professional design | ✅ | Clean, focused developer-tool aesthetic |
| R12 Information overload | ✅ | One issue at a time eliminates overload entirely |
| R13 Benchmark vs skip | ✅ | Pre-existing = automatic; Skip = manual with reason |
| R14 Accessible indicators | ✅ | Shape + color + label on severity badges |
| R15 Multiple audiences | ✅ | Developer-first sequential flow; progress tracking for leads |

## Pros
- **Zero information overload** — one issue at a time is the most aggressive progressive disclosure possible
- **Guided experience** — developers never wonder "where do I start?"
- **Full context always visible** — no tabs or expansion needed for the current issue
- **Progress tracking** — clear sense of how much work remains
- **Fast triage** — Skip/Next pattern enables rapid decision-making

## Cons
- **No overview of all issues** — can't scan for patterns across violations
- **No package-level view** — violations are decontextualized from their package grouping
- **Sequential constraint** — some developers prefer to choose their own order
- **Back-navigation** — revisiting a previous issue breaks the forward flow
- **Single issue may feel slow** — for small PR diffs, the overhead of stepping through feels heavy

## Design Considerations
- Inspired by GitHub's PR review flow (file-by-file stepping) and code review tools
- Progress indicator provides orientation without requiring a full list view
- Critical issues are presented first, matching the 94% delta-first pattern from research
- The "review complete" summary gives a sense of accomplishment and clear next steps
- Pre-existing issues can optionally be included in the sequence as informational items (dimmed)
