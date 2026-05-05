# UX Concepts Overview — ELEVEN A11y Audit Tool

## Feature
ELEVEN — A11y Audit Tool HTML Report Dashboard Redesign

## Problem Statement
ELEVEN's current developer-built HTML report has no professional design, suffers from information overload on the violations page, and presents two overlapping mental models (benchmark vs. skip) without clear visual separation. The redesign must deliver a professional, scannable experience for an accessibility PR gate tool.

## Requirements
1. **R1** Overview Dashboard — Clear pass/fail/blocked status showing whether the PR introduces new a11y issues
2. **R2** Package summary table with pass/fail status, issue counts, drill-down capability
3. **R3** Violations Breakdown — Per-package drill-down grouped by category (axe-core, keyboard nav, focus ring, tab reachability)
4. **R4** Issue Detail — Per-element view with code snippets, screenshots, step-by-step fix instructions, WCAG links
5. **R5** Skip Flow — Mandatory reason, "Skip for this PR" (temporary) vs "Not relevant" (permanent), post-skip states
6. **R6** Unskip/Restore Flow — Ability to undo skip decisions
7. **R7** Benchmark Mode — Visual separation of new blocking issues vs pre-existing reference issues
8. **R8** All Passing State — Positive reinforcement when no issues found
9. **R9** Dark mode support with toggle
10. **R10** Standalone HTML — vanilla JS/CSS, works offline (skip/benchmark require API)
11. **R11** Professional developer-tool aesthetic (Lighthouse/Playwright style, not Wix Design System)
12. **R12** Solve information overload with clear hierarchy and progressive disclosure
13. **R13** Clear distinction between benchmark (automatic baseline) and skip (manual dismissal)
14. **R14** Accessible status indicators (color + shape + label, never color-only)
15. **R15** Serve primary (developers), secondary (a11y team, team leads) audiences

## Key Research Insights
- **Delta-first display** (~94%): Best CI tools lead with "X new issues" not "Y total issues"
- **Three-category model**: New / Pre-existing / Fixed is stronger than binary new/existing
- **SonarQube's three-tab detail**: "Why is this an issue?" / "Where is it?" / "How can I fix it?" — clearest info architecture
- **Skip flow friction**: Dropdown-not-modal, structured reason choice, one-click for common cases
- **Status accessibility**: Color + shape + label, non-negotiable for an a11y tool

## Concept Summaries

### Concept 1: Signal-First Triage
A triage-optimized dashboard leading with a binary verdict banner and delta counts. Violations expand inline with fix guidance in a three-tab pattern (Why / Where / How). Skip is a lightweight inline dropdown — no modal interruption.

### Concept 2: Three-Lane Verdict Board
Three distinct columns — New (blocking), Fixed (resolved), Persisting (reference) — inspired by Trivago's three-category model. Developers see the New lane by default; leads toggle all three. Violations are cards that move between lanes via skip/unskip.

### Concept 3: Focused Fix Sequence
A one-issue-at-a-time guided flow instead of a list-based dashboard. After the hero verdict, developers step through issues sequentially (most critical first). Each screen shows a single violation with full context. Optimized for the "fix and move on" mindset.

### Concept 4: Package Health Grid
A visual grid of package tiles colored by health status for instant spatial overview. Clicking a tile drills into accordion-based violations. A toggle switches between "This PR" (delta) and "Full Audit" (all). Fix details appear in a sidebar panel.

### Concept 5: Adaptive Report Hub
The ambitious version. Opens pre-filtered based on context (GitHub check → new issues only). Adds role-based view presets (Developer / Lead / A11y Team), trend sparklines per package, bulk skip with preview, and AI-suggested fix prioritization. Three-category model with celebratory "Fixed" section.
