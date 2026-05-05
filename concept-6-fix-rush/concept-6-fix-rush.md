# Concept 6: Fix Rush — Gamified Speed Triage

## Overview
A gamified, speed-optimized triage experience that makes resolving accessibility issues feel fast and rewarding. Issues are presented as a card stack (swipe-through) or list, with prominent "Fix with AI" actions on every card and in bulk. Points, streaks, progress bars, and celebrations turn the audit from a chore into a focused sprint.

## Key Differentiator
**Gamification + AI-assisted fixing.** This is the only concept that adds extrinsic motivation (XP, streaks, levels) and reduces friction to near-zero with one-click AI fix suggestions. Developers don't just _find_ issues — they resolve them without leaving the report.

## User Flow

```
┌─────────────────────────────────────────────────────────┐
│  ELEVEN  ■ 5 issues   🔥 3 streak   ⏱ 1:42   ☀ Theme  │
├─────────────────────────────────────────────────────────┤
│  ████████████░░░░░  340 / 500 XP   Level: Bug Squasher │
│  3 of 5 resolved                                        │
├─────────────────────────────────────────────────────────┤
│  ┌─────────────────────────────────────────────┐        │
│  │  ▲ CRITICAL  Image missing alt text          │        │
│  │  @wix/editor-elements · Perceivable          │        │
│  │                                              │        │
│  │  Why: Screen readers can't describe image    │        │
│  │  Where: <img src="avatar.png">               │        │
│  │  How: Add alt="User profile photo"           │        │
│  │                                              │        │
│  │  [✨ Fix with AI]  [🔧 Fix manually]  [⏭ Skip]│        │
│  └─────────────────────────────────────────────┘        │
│        ┌──────────┐  (stacked cards behind)              │
│        └──────────┘                                      │
├─────────────────────────────────────────────────────────┤
│  [✨ Fix All with AI]    [📋 List view]                   │
└─────────────────────────────────────────────────────────┘
```

## Screens & States

### 1. Card Stack Mode (Default)
- One issue card at a time, stacked depth effect behind
- Each card shows: severity badge (shape+color+label), rule name, package, category
- Condensed Why/Where/How visible on the card
- Three action buttons: **Fix with AI** (primary/purple), **Fix manually** (secondary), **Skip** (tertiary)
- Next/prev navigation for browsing without resolving

### 2. Fix with AI (Per Issue)
- Click "Fix with AI" → card expands to show AI-generated code diff
- Diff view: red lines (removed) / green lines (added) — realistic mock data
- Actions: "Apply fix" (accepts suggestion) / "Dismiss" (closes suggestion)
- Applying a fix awards XP and advances to next card

### 3. Bulk Fix All with AI
- Button in toolbar opens a panel/modal showing all open issues
- Each issue has a toggle switch and its AI-suggested fix preview
- "Apply selected fixes" resolves all toggled issues at once
- XP awarded in bulk — can trigger multi-level jumps

### 4. List View (Power User Toggle)
- Traditional expandable list of all issues with status badges
- Same actions available (Fix with AI, Fix manually, Skip)
- Leads and power users can scan all issues at once
- Toggle between Card Stack and List View

### 5. XP & Progress System
- **XP per severity**: Critical = 30, Serious = 20, Moderate = 10
- **Progress bar**: Visual fill toward "PR Clean" threshold
- **Levels**: PR Reviewer → Getting Started → Bug Squasher → A11y Champion → A11y Legend
- **Streak counter**: 🔥 increments on consecutive resolves, resets on idle/skip

### 6. Skip Flow (Lightweight)
- Skip button → small inline dropdown (not a form)
- Options: False positive / Not applicable / Will fix later / Intentional design
- One click to select reason → done, next card
- Undo toast appears briefly after skip

### 7. Bonus Round (Pre-existing Issues)
- After all new issues resolved, "Bonus Round" section appears
- Pre-existing benchmark issues shown as optional items
- Same card format but with "Pre-existing" tag — resolving earns bonus XP

### 8. Completion Celebration
- Canvas confetti animation when all issues resolved
- Stats summary: issues resolved, total time, avg time per issue
- Achievement-style messaging: "PR is clean! 🎉"
- Level earned displayed prominently

### 9. All Passing State
- Green verdict: "Nothing to fix!"
- Achievement badge: "Clean PR" 
- Fun, celebratory empty state

## Requirement Coverage

| Req | Status | How |
|-----|--------|-----|
| R1 Overview Dashboard | ✅ | Verdict banner + progress bar + XP meter |
| R2 Package summary | ✅ | Package badges on each card |
| R3 Violations breakdown | ✅ | Cards ordered by severity (critical first), filterable |
| R4 Issue detail | ✅ | Condensed Why/Where/How on each card + AI fix diff |
| R5 Skip flow | ✅ | Lightweight inline dropdown with reason selection |
| R6 Unskip | ✅ | Undo toast after skip |
| R7 Benchmark mode | ✅ | "Bonus Round" for pre-existing issues after new ones resolved |
| R8 All passing | ✅ | Celebration + achievement badge |
| R9 Dark mode | ✅ | CSS variable theme toggle |
| R10 Standalone HTML | ✅ | Single file, vanilla JS, no deps |
| R11 Professional design | ✅ | Developer-tool aesthetic with playful gamification layer |
| R12 Information overload | ✅ | One card at a time in stack mode |
| R13 Benchmark vs skip | ✅ | Pre-existing = "Bonus Round"; Skip = manual with reason |
| R14 Accessible indicators | ✅ | Shape + color + label for severity |
| R15 Multiple audiences | ✅ | Devs use card stack; leads toggle to list view |

## Expanded Features (Beyond Requirements)
- **Fix with AI** — one-click AI code suggestion with diff view per issue
- **Bulk Fix All with AI** — resolve multiple issues at once with AI suggestions
- **XP / Points** — extrinsic motivation tied to severity weighting
- **Streak counter** — rewards consecutive resolves
- **Elapsed time** — awareness without pressure
- **Confetti celebration** — dopamine hit on completion
- **Level progression** — gamification arc from PR Reviewer to A11y Legend
- **Severity filters** — focus on Critical/Serious/Moderate individually

## Pros
- **Fastest triage flow** — Fix with AI reduces time-to-resolution dramatically
- **Motivating** — XP, streaks, and celebrations make the audit feel like progress, not punishment
- **Zero overload** — card stack mode shows one issue at a time
- **AI reduces friction** — developers don't need to figure out the fix themselves
- **Dual modes** — card stack for speed, list for overview — both audiences served
- **Bulk operations** — Fix All with AI handles the entire report in one action

## Cons
- **Gamification may feel patronizing** — some senior devs may find XP childish
- **AI dependency** — "Fix with AI" sets expectations for real AI integration (needs backend)
- **Streaks incentivize speed over quality** — could encourage hasty decisions
- **Pre-existing as "Bonus Round"** — may trivialize legitimate baseline issues
- **Most complex concept** — highest implementation effort due to animations, AI mock, gamification state

## Design Considerations
- Gamification layer is opt-in / dismissable — card stack works without XP visible
- AI fixes are presented as suggestions, not auto-applied — developer remains in control
- Streak counter is positive reinforcement only — no penalty for breaking a streak
- Confetti uses lightweight canvas animation — no library, ~30 lines of JS
- "Bonus Round" framing makes pre-existing issues feel approachable rather than overwhelming
- Level names use developer-friendly humor without being unprofessional
