# Test Coverage Map

**Schema version:** 1.0.0

**Coverage summary:** 3/4 covered · 1 partial · 0 not covered

## AC-003  —  ⚠️ partial

**Run:** run-d5f2cf06a491
**Test cases:** `TC-003`
**Notes:** TC-003 passes and confirms onTabChange is called with 'run' and 'history' respectively on button click. However, the AC also requires that clicking Run hides the History table and shows the Run placeholder, and vice versa — only one view visible at a time. This conditional rendering is untested because no page-level or dashboard-level component is exposed in the interface manifest. The test suite explicitly acknowledges this gap.

## AC-001  —  ✅ covered

**Run:** run-d5f2cf06a491
**Test cases:** `TC-001`
**Notes:** Both sub-tests pass: CODEFORGE label, Run and History buttons, call-budget text pattern, and <header> root element all verified in jsdom.

## AC-002  —  ✅ covered

**Run:** run-d5f2cf06a491
**Test cases:** `TC-002`
**Notes:** All eight assertions pass: getRunRecords returns exactly 7 records covering all four status values with required non-empty fields; getStatusConfig returns correct oklch colors and uppercase labels; HistoryTable renders five column headers, 7 tbody rows, all status labels, and correct inline border-color accent styles per row.

## AC-004  —  ✅ covered

**Run:** run-d5f2cf06a491
**Test cases:** `TC-004`
**Notes:** Smoke test passes: HistoryTable mounts in jsdom and exactly 7 tbody rows are present in the rendered output.
