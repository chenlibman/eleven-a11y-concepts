# Concept 8: Sidebar Navigator — Grouped Rule List + Detail Panel

## Overview
A two-panel layout with a persistent left sidebar containing filter tabs and a rule-grouped issue list. Clicking a rule group shows all its violations in the main content area. Each violation card displays the CSS selector, file location, and quick action buttons (Fix with AI / Skip). Inspired by the current ELEVEN dark-mode design language.

## Key Differentiator
**Rule-based grouping with sidebar navigation.** Instead of listing individual violations, issues are grouped by WCAG rule in the sidebar (e.g., "Interactive elements must be keyboard accessible — 5 new · 0 baseline"). This reduces cognitive load by clustering related issues, letting developers fix all instances of one rule type before moving to the next.

## Layout

### Top Bar
- ELEVEN logo + PR reference
- Summary stats: NEW count | CRITICAL count | SERIOUS count | BASELINE count
- Dark mode toggle (dark mode is default)

### Left Sidebar (always visible, independently scrollable)
- **Filter grid** (2×2): ALL / NEW / BASELINE / SKIPPED — counts update in real-time
- **Rule group list**: Each group shows rule name, WCAG criterion, category, new/baseline counts
- Clicking a group filters the main area to show only that rule's violations
- Active group is highlighted

### Main Content Area (independently scrollable)
- Header with selected rule name + violation count
- Violation cards showing:
  - Severity badge (● CRITICAL / ◆ SERIOUS / ○ MODERATE) + [NEW] or [BASELINE] tag
  - Rule name + WCAG reference
  - CSS selector in a code badge (e.g., `button.cta-primary`)
  - File location + package + category
  - **FIX WITH AI** and **SKIP** action buttons (right-aligned, outlined)

## Requirement Coverage

| Req | Status | How |
|-----|--------|-----|
| R1 Overview Dashboard | ✅ | Top bar stats + progress bar |
| R2 Package summary | ✅ | Package shown per violation card |
| R3 Violations breakdown | ✅ | Rule-grouped sidebar + individual violation cards |
| R4 Issue detail | ✅ | Violation cards with selector, location, WCAG ref |
| R5 Skip flow | ✅ | Inline dropdown with reasons per card |
| R6 Unskip | ✅ | Unskip button on skipped cards |
| R7 Benchmark mode | ✅ | BASELINE filter tab + baseline counts per rule group |
| R8 All passing | ✅ | Celebration when all new issues resolved |
| R9 Dark mode | ✅ | Dark mode default, light mode toggle |
| R10 Standalone HTML | ✅ | Single file, vanilla JS, no deps |
| R11 Professional design | ✅ | Clean, minimal developer-tool aesthetic |
| R12 Information overload | ✅ | Rule grouping reduces clutter; filters narrow scope |
| R13 Benchmark vs skip | ✅ | BASELINE = automatic tag; SKIPPED = manual with reason |
| R14 Accessible indicators | ✅ | Shape + color + label for severity |
| R15 Multiple audiences | ✅ | Sidebar overview for leads; violation detail for devs |

## Pros
- **Familiar two-panel pattern** — IDE-like layout developers already know
- **Rule grouping** — related issues clustered, enabling batch fixing
- **Filter tabs** — one click to see only NEW, BASELINE, or SKIPPED
- **Real-time counts** — sidebar and top bar update as issues are resolved
- **Dark mode default** — matches developer tool expectations

## Cons
- **Sidebar takes horizontal space** — less room for violation detail on narrow screens
- **No individual issue navigation** — must browse through cards in main area
- **Rule grouping may hide severity mix** — a rule group can contain critical and moderate issues
- **Fix with AI is per-card** — no bulk action across a rule group

## Design Considerations
- Dark mode as default matches the developer tool aesthetic and the reference design
- CSS selector badges in monospace font provide instant recognition of the affected element
- File location + line number helps developers jump to the exact source
- Filter counts as live indicators create a sense of progress
- Independent scrolling for sidebar and main area prevents context loss
