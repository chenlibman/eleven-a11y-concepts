# Concept 4: Package Health Grid

## Overview
A visual grid of package tiles gives an instant spatial overview of the entire monorepo's health. Each tile is a clickable card showing package name, issue count, and pass/fail status. Clicking a tile opens a sidebar panel with accordion-based violations and fix details. A scope toggle switches between "This PR" (delta view) and "Full Audit" (all issues).

## Key Differentiator
**Spatial package overview.** Instead of a flat table or list, packages are rendered as a grid of tiles — giving developers a bird's-eye view of which packages are healthy and which need attention. The grid + sidebar pattern keeps the overview visible while drilling into details.

## User Flow

```
┌─────────────────────────────────────────────────────────┐
│  VERDICT BANNER: Blocked — 3 new issues in 2 packages   │
├─────────────────────────────────────────────────────────┤
│  SCOPE: [This PR] [Full Audit]   ☀ Theme Toggle         │
├────────────────────────────┬────────────────────────────┤
│  PACKAGE GRID              │  SIDEBAR (when tile open)  │
│  ┌──────┐ ┌──────┐ ┌────┐ │  ┌────────────────────────┐│
│  │editor│ │design│ │core│ │  │ @wix/editor-elements   ││
│  │ ■ 2  │ │ ● 0  │ │● 0│ │  │ ─────────────────────  ││
│  │ fail │ │ pass │ │pass│ │  │ ▼ Violation 1          ││
│  └──────┘ └──────┘ └────┘ │  │   [Why] [Where] [How]  ││
│  ┌──────┐ ┌──────┐ ┌────┐ │  │ ▶ Violation 2          ││
│  │theme │ │utils │ │api │ │  │ ▶ Violation 3          ││
│  │ ■ 1  │ │ ● 0  │ │● 0│ │  │                        ││
│  │ fail │ │ pass │ │pass│ │  │ [ Skip ▾ ] [ Details ] ││
│  └──────┘ └──────┘ └────┘ │  └────────────────────────┘│
└────────────────────────────┴────────────────────────────┘
```

## Screens & States

### 1. Dashboard — Grid View
- Verdict banner at top: blocked (dark) or passing (green)
- Scope toggle: "This PR" (default, delta view) / "Full Audit" (all issues)
- Package grid: responsive auto-fill grid of clickable tiles
- Each tile shows: package name (truncated), issue count, status badge (shape + color + label)
- Failed packages appear full-opacity; passing packages are dimmed
- Pre-existing-only packages have dashed borders and reduced opacity

### 2. Package Tile States
- **Failed** — bold border, issue count in red, "Fail" badge
- **Passed** — subtle border, green checkmark, "Pass" badge
- **Selected** — inverted colors (dark bg, white text) to show active selection
- **Pre-existing only** — dashed border, dimmed, "Pre-existing" tag

### 3. Sidebar Detail Panel
- Opens when a tile is clicked (grid area shrinks to accommodate)
- Package name + status at top
- Accordion list of violations:
  - Each accordion header: rule name, severity badge, category tag
  - Expanded: three-tab detail (Why / Where / How)
- Skip button per violation with inline dropdown
- Close button returns to full-width grid

### 4. Skip Flow (In Sidebar)
- "Skip" button on each violation → inline dropdown:
  - "Skip for this PR" / "Not relevant"
- Mandatory reason textarea + Confirm
- After skip: violation card dims, "Unskip" link appears

### 5. All Passing State
- Green verdict banner
- All tiles show green "Pass" status
- Centered celebration message overlaying the grid

## Requirement Coverage

| Req | Status | How |
|-----|--------|-----|
| R1 Overview Dashboard | ✅ | Verdict banner + grid provides instant health overview |
| R2 Package summary | ✅ | Grid tiles = visual package summary with status |
| R3 Violations breakdown | ✅ | Sidebar accordion with category grouping |
| R4 Issue detail | ✅ | Three-tab Why/Where/How in sidebar |
| R5 Skip flow | ✅ | Inline dropdown in sidebar per violation |
| R6 Unskip | ✅ | "Unskip" link on skipped items |
| R7 Benchmark mode | ✅ | Pre-existing tiles dimmed with dashed borders; scope toggle |
| R8 All passing | ✅ | Green banner + all-pass grid celebration |
| R9 Dark mode | ✅ | CSS variable theme toggle |
| R10 Standalone HTML | ✅ | Single file, vanilla JS, no deps |
| R11 Professional design | ✅ | Clean grid aesthetic, developer-tool style |
| R12 Information overload | ✅ | Grid shows overview; details are on-demand in sidebar |
| R13 Benchmark vs skip | ✅ | Pre-existing = visual treatment on tiles; Skip = manual with reason |
| R14 Accessible indicators | ✅ | Shape + color + label on all status badges |
| R15 Multiple audiences | ✅ | Scope toggle + grid overview serves leads; sidebar serves devs |

## Pros
- **Bird's-eye view** — grid instantly shows which packages need attention in a monorepo
- **Overview stays visible** — sidebar pattern keeps the grid context while drilling down
- **Scales well** — grid handles 5 or 50 packages without layout changes
- **Spatial memory** — developers learn package positions over time, speeding up repeat visits
- **Scope toggle** — clean separation of PR delta vs full audit

## Cons
- **Sidebar space** — detail panel compresses the grid on smaller screens
- **Two-click minimum** — tile click + violation expand to see details (vs inline expansion in Concept 1)
- **Tile names truncated** — long package names don't fit well in small tiles
- **No cross-package violation grouping** — same rule failing in multiple packages isn't surfaced
- **Grid can feel sparse** — if most packages pass, the grid is mostly green with few actionable tiles

## Design Considerations
- Grid uses `auto-fill` with `minmax(240px, 1fr)` for responsive tile sizing
- Selected tile uses inverted colors for clear focus indication
- Sidebar appears on the right (60% width), grid shrinks to accommodate
- Pre-existing tiles use dashed borders — a visual convention that differs from "skip" (amber accent)
- Accordion in sidebar uses progressive disclosure to manage violation density
