# Assumptions Log

**Schema version:** 1.0.0

## ASSUME-001  —  🔴 open

**Impact:** 🟢 low  
**Run:** run-d5f2cf06a491  
**Source agent:** requirements_analyst

The call-budget progress bar uses hardcoded values (e.g. 12 current, 50 ceiling) since the brief specifies the visual component but not the scaffold values. These are display-only and carry no functional contract.

## ASSUME-002  —  🔴 open

**Impact:** 🟢 low  
**Run:** run-d5f2cf06a491  
**Source agent:** requirements_analyst

The distribution of the 7 hardcoded rows across the 4 status states is left to the implementer, provided all four states appear at least once. A reasonable spread (e.g. 2 succeeded, 1 running, 2 awaiting_human, 2 failed_terminal) is acceptable.

## ASSUME-003  —  🔴 open

**Impact:** 🟢 low  
**Run:** run-d5f2cf06a491  
**Source agent:** requirements_analyst

The 'reached' column values use plausible pipeline phase names (e.g. 'requirements', 'architecture', 'coder', 'reviewer') as hardcoded strings, since the brief does not enumerate phase names.

## ASSUME-004  —  🔴 open

**Impact:** 🟡 medium  
**Run:** run-d5f2cf06a491  
**Source agent:** requirements_analyst

The Vitest smoke test uses React Testing Library with a jsdom environment, which is the standard testing companion for Next.js 14 TypeScript projects. No alternative test renderer was specified.

## ASSUME-005  —  🔴 open

**Impact:** 🟢 low  
**Run:** run-d5f2cf06a491  
**Source agent:** requirements_analyst

Tab state is managed with local React component state (useState). No URL-based routing or persistent storage for the active tab was requested.

## ASSUME-001  —  🔴 open

**Impact:** 🟢 low  
**Run:** run-d5f2cf06a491  
**Source agent:** architecture_designer

HistoryTable takes no props and internally imports getRunRecords/getStatusConfig from lib/run-data. This makes the Vitest smoke test a zero-prop mount, which is the simplest form matching AC-004's description.

## ASSUME-002  —  🔴 open

**Impact:** 🟢 low  
**Run:** run-d5f2cf06a491  
**Source agent:** architecture_designer

callCurrent (e.g. 12) and callCeiling (e.g. 50) are hardcoded constants in DashboardPage and passed as props to AppHeader. The requirements specify a visual display of these values but provide no data source.

## ASSUME-003  —  🔴 open

**Impact:** 🟡 medium  
**Run:** run-d5f2cf06a491  
**Source agent:** architecture_designer

All interactive components (AppHeader, HistoryTable, RunPlaceholder, DashboardPage) are marked 'use client'. Since none use async server data fetching and the test environment is jsdom, this is both safe and necessary for Vitest compatibility.

## ASSUME-004  —  🔴 open

**Impact:** 🟢 low  
**Run:** run-d5f2cf06a491  
**Source agent:** architecture_designer

The distribution of 7 rows across the 4 status states is left to the Coder to decide, subject to the constraint that all 4 statuses appear at least once. A spread such as 2 succeeded, 2 running, 2 awaiting_human, 1 failed_terminal is acceptable.

## ASSUME-005  —  🔴 open

**Impact:** 🟢 low  
**Run:** run-d5f2cf06a491  
**Source agent:** architecture_designer

Global styles (body background #0a0b0e, text color #cdd2db, JetBrains Mono) are applied in app/layout.tsx via a CSS module or inline style, not in any of the named modules above. app/layout.tsx is a Next.js convention file and does not need a separate module entry.

## ASSUME-001  —  🔴 open

**Impact:** 🟢 low  
**Run:** run-d5f2cf06a491  
**Source agent:** coder

Call-budget values are hardcoded as 12 / 50 in DashboardPage and passed as props to AppHeader, per the architecture's display-only intent.

## ASSUME-002  —  🔴 open

**Impact:** 🟢 low  
**Run:** run-d5f2cf06a491  
**Source agent:** coder

The 7 records are distributed as 2 succeeded, 2 running, 2 awaiting_human, 1 failed_terminal — all four statuses appear at least once.

## ASSUME-003  —  🔴 open

**Impact:** 🟢 low  
**Run:** run-d5f2cf06a491  
**Source agent:** coder

Uppercase status labels chosen: SUCCEEDED, RUNNING, AWAITING HUMAN, FAILED. The brief required uppercase but did not enumerate exact label text.

## ASSUME-004  —  🔴 open

**Impact:** 🟢 low  
**Run:** run-d5f2cf06a491  
**Source agent:** coder

Styling is applied with inline React style objects rather than CSS modules, keeping color values directly assertable and self-contained per component.

## ASSUME-001  —  🔴 open

**Impact:** 🟢 low  
**Run:** run-d5f2cf06a491  
**Source agent:** coder

callCurrent=12 and callCeiling=50 hardcoded in DashboardPage and passed to AppHeader as props, per the architecture's display-only contract.

## ASSUME-002  —  🔴 open

**Impact:** 🟢 low  
**Run:** run-d5f2cf06a491  
**Source agent:** coder

Row distribution: 2 succeeded, 2 running, 2 awaiting_human, 1 failed_terminal — all four statuses appear at least once across the 7 records.

## ASSUME-003  —  🔴 open

**Impact:** 🟡 medium  
**Run:** run-d5f2cf06a491  
**Source agent:** coder

Per the firewall, I do not author test files; the Test Designer writes the AC-004 smoke test. HistoryTable is a zero-prop 'use client' component rendering exactly 7 'tbody tr' elements so document.querySelectorAll('tbody tr') yields 7, making it mountable in jsdom and satisfiable by the smoke test.

## ASSUME-004  —  🔴 open

**Impact:** 🟢 low  
**Run:** run-d5f2cf06a491  
**Source agent:** coder

Global styles (body bg #0a0b0e, text #cdd2db, JetBrains Mono) applied inline in app/layout.tsx rather than a separate CSS module, per architecture ASSUME-005.

## ASSUME-001  —  🔴 open

**Impact:** 🟡 medium  
**Run:** run-d5f2cf06a491  
**Source agent:** test_designer

HistoryTable applies row accent colors as inline styles on <tr> elements (e.g. style={{ borderLeft: '2px solid oklch(...)' }}), making them queryable via getAttribute('style') in jsdom. If colors are applied via CSS classes, the border-color test in TC-002 will fail.

## ASSUME-002  —  🔴 open

**Impact:** 🟡 medium  
**Run:** run-d5f2cf06a491  
**Source agent:** test_designer

The page-level component that wires AppHeader, HistoryTable, and RunPlaceholder together is not exposed in the interface manifest. TC-003 tests only the AppHeader callback contract; the full hide/show behavior of AC-003 is not testable from the manifest alone.

## ASSUME-003  —  🔴 open

**Impact:** 🟢 low  
**Run:** run-d5f2cf06a491  
**Source agent:** test_designer

AppHeader tab buttons are rendered as <button> elements with accessible names 'Run' and 'History', making them queryable via getByRole('button', { name: ... }).

## ASSUME-004  —  🔴 open

**Impact:** 🟢 low  
**Run:** run-d5f2cf06a491  
**Source agent:** test_designer

The call-budget text is rendered as a single text node or element containing the pattern '{callCurrent} / {callCeiling} calls', queryable via a regex in screen.getByText.
