# Assumptions Log

**Schema version:** 1.0.0

## ASSUME-001  —  🔴 open

**Impact:** 🟢 low  
**Run:** run-935bbb649746  
**Source agent:** requirements_analyst

No visible loading indicator is required while the fetch is in-flight. The component may render an empty or blank state during the pending period without this being a testable requirement.

## ASSUME-002  —  🔴 open

**Impact:** 🟡 medium  
**Run:** run-935bbb649746  
**Source agent:** requirements_analyst

Fetch errors (network failure, non-2xx response) are out of scope for this feature. No error state UI is required; the brief specifies only the empty-array case.

## ASSUME-003  —  🔴 open

**Impact:** 🟡 medium  
**Run:** run-935bbb649746  
**Source agent:** requirements_analyst

The RunSummary type shape (id, status, feature, runId, reached, when) is inferred from the existing HistoryTable row structure and the prior RunRecord type. The exact field names used by GET /api/runs are assumed to match this shape; if they differ, the data contract will need revision.

## ASSUME-004  —  🔴 open

**Impact:** 🟢 low  
**Run:** run-935bbb649746  
**Source agent:** requirements_analyst

HistoryTable continues to use getStatusConfig from RunData (or an equivalent inline map) to resolve status display colors and labels, since the brief only replaces the data-fetching call, not the status rendering logic.

## ASSUME-001  —  🔴 open

**Impact:** 🟢 low  
**Run:** run-935bbb649746  
**Source agent:** architecture_designer

HistoryTable will inline any status-display configuration (colors, labels) it requires rather than importing getStatusConfig from RunData. The requirements explicitly remove the RunData dependency; the exact inline values are an implementation detail for the Coder.

## ASSUME-002  —  🔴 open

**Impact:** 🟡 medium  
**Run:** run-935bbb649746  
**Source agent:** architecture_designer

The RunSummary field shape (id, status, feature, runId, reached, when) declared in the requirements data contract matches what GET /api/runs actually returns, consistent with the existing tested 'Run Summaries Reader and API Route' feature.

## ASSUME-003  —  🔴 open

**Impact:** 🟢 low  
**Run:** run-935bbb649746  
**Source agent:** architecture_designer

No loading indicator or intermediate state UI is required while the fetch is in-flight. The component may render nothing or a blank state during the pending period without this being testable.

## ASSUME-004  —  🔴 open

**Impact:** 🟢 low  
**Run:** run-935bbb649746  
**Source agent:** architecture_designer

The HistoryTable component file lives at components/HistoryTable.tsx (module path components/HistoryTable) following the stack convention for client components. If the existing file resides at a different path, the Coder should adjust the module path accordingly while keeping the interface contract semantics identical.

## ASSUME-001  —  🔴 open

**Impact:** 🟡 medium  
**Run:** run-935bbb649746  
**Source agent:** coder

RunSummary field shape (id, status, feature, runId, reached, when) matches the existing GET /api/runs response, per the requirements data contract.

## ASSUME-002  —  🔴 open

**Impact:** 🟡 medium  
**Run:** run-935bbb649746  
**Source agent:** coder

No loading indicator and no fetch error-state UI are required; during the pending fetch the component renders the empty state, and network errors are unhandled per scope.

## ASSUME-003  —  🔴 open

**Impact:** 🟢 low  
**Run:** run-935bbb649746  
**Source agent:** coder

Status-display config (colours/labels) is inlined with reasonable oklch values; exact colour values are an implementation detail not pinned by the contract.

## ASSUME-T001  —  🔴 open

**Impact:** 🟡 medium  
**Run:** run-935bbb649746  
**Source agent:** test_designer

global fetch is mockable via vi.stubGlobal('fetch', ...) in the jsdom environment configured by the project's vitest.config.ts. The component calls the global fetch directly (not an imported wrapper), so stubbing the global is sufficient.

## ASSUME-T002  —  🔴 open

**Impact:** 🟡 medium  
**Run:** run-935bbb649746  
**Source agent:** test_designer

The fetch call in HistoryTable uses the pattern: const res = await fetch('/api/runs'); const data = await res.json(). The mock therefore returns an object with a json() method that resolves to the array. If the implementation uses a different response consumption pattern (e.g. res.text() + JSON.parse), the mock shape would need adjustment.

## ASSUME-001  —  🔴 open

**Impact:** 🔴 high  
**Run:** run-935bbb649746  
**Source agent:** coder

The build_error (tsc printing usage instead of compiling) was caused by a missing/invalid tsconfig.json; a valid strict tsconfig.json with the @/* alias resolves it.

## ASSUME-002  —  🔴 open

**Impact:** 🟡 medium  
**Run:** run-935bbb649746  
**Source agent:** coder

RunSummary fields (id, status, feature, runId, reached, when) match the existing GET /api/runs response shape per the requirements data contract.

## ASSUME-003  —  🔴 open

**Impact:** 🟢 low  
**Run:** run-935bbb649746  
**Source agent:** coder

No loading indicator or error UI is required; the component renders the empty state (initial []) during the pending fetch, which also satisfies the empty-array path.

## ASSUME-004  —  🔴 open

**Impact:** 🟢 low  
**Run:** run-935bbb649746  
**Source agent:** coder

Status display colors/labels are inlined in HistoryTable rather than imported from RunData, with a fallback for unknown status keys.

## ASSUME-005  —  🔴 open

**Impact:** 🟡 medium  
**Run:** run-935bbb649746  
**Source agent:** coder

GET /api/runs is an existing, tested route owned elsewhere and is therefore not (re)implemented here, per the explicitly out-of-scope items.

## ASSUME-001  —  🔴 open

**Impact:** 🟡 medium  
**Run:** run-935bbb649746  
**Source agent:** security_reviewer

The GET /api/runs route handler is not present in the artifact (explicitly out of scope). Security of that route is not assessed here; only the client-side consumption in HistoryTable is reviewed.

## ASSUME-001  —  🔴 open

**Impact:** 🟡 medium  
**Run:** run-935bbb649746  
**Source agent:** test_designer

global.fetch is available in the jsdom test environment and can be replaced with vi.fn() in beforeEach. Vitest's jsdom environment does not stub fetch by default, so assigning to global.fetch directly is the correct approach.

## ASSUME-002  —  🔴 open

**Impact:** 🟢 low  
**Run:** run-935bbb649746  
**Source agent:** test_designer

The fetch call in HistoryTable uses the bare string '/api/runs' (not a full URL), matching the interface manifest's fetch_behaviour.url. The test asserts toHaveBeenCalledWith('/api/runs') accordingly.

## ASSUME-003  —  🔴 open

**Impact:** 🟡 medium  
**Run:** run-935bbb649746  
**Source agent:** test_designer

When the API returns a non-empty array, the component renders a <table> with a header row and one <tr> per RunSummary in the body, giving getAllByRole('row') a count of 1 + N. If the component uses a different DOM structure (e.g. divs), the row count assertion may need adjustment.

## ASSUME-004  —  🔴 open

**Impact:** 🟡 medium  
**Run:** run-935bbb649746  
**Source agent:** test_designer

The RunSummary fields 'feature' and 'runId' are rendered as visible text in each row, making them queryable via screen.getByText(). If the component renders different fields or truncates them, the text assertions in TC-001 will need updating.

## ASSUME-005  —  🔴 open

**Impact:** 🟢 low  
**Run:** run-935bbb649746  
**Source agent:** test_designer

The empty-state 'No runs found.' message is rendered outside any <table> or <tbody>, so queryAllByRole('row') returns no rows (or only a header row inside a <thead>) in the empty path. The filter for rows not inside <thead> is used to exclude any structural header-only table.

## ASSUME-T001  —  🔴 open

**Impact:** 🔴 high  
**Run:** run-970ce73dbc38  
**Source agent:** test_designer

AC-001 through AC-004 are about readRunSummaries() internals and are explicitly out of scope for testing per the requirements brief ('only the route handler is tested per the brief'). They are not covered in this test suite.

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
