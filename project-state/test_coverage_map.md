# Test Coverage Map

**Schema version:** 1.0.0

**Coverage summary:** 5/10 covered · 1 partial · 4 not covered

## AC-001  —  ❌ not covered

**Run:** run-970ce73dbc38
**Notes:** readRunSummaries() env guard behaviour (early return of [] when CODEFORGE_PROJECT_DIR is unset or empty) is explicitly out of scope for testing per the brief; no test exercises it.

## AC-002  —  ❌ not covered

**Run:** run-970ce73dbc38
**Notes:** readRunSummaries() filesystem read behaviour (readdir options, codeforge_run.json, brief.txt, RunSummary construction) is explicitly out of scope for testing per the brief.

## AC-003  —  ❌ not covered

**Run:** run-970ce73dbc38
**Notes:** readRunSummaries() directory-filtering behaviour (skipping non-directory entries) is explicitly out of scope for testing per the brief.

## AC-004  —  ❌ not covered

**Run:** run-970ce73dbc38
**Notes:** last_phase derivation from events.jsonl (highest-sequence handoff event) is explicitly out of scope for testing per the brief.

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

## AC-005  —  ✅ covered

**Run:** run-970ce73dbc38
**Test cases:** `TC-005`
**Notes:** Four passing sub-tests verify: HTTP 200 with three-item array sorted newest-first by started_at (run-b Mar > run-c Feb > run-a Jan); HTTP 200 with [] when readRunSummaries returns empty; Content-Type matches application/json; response objects contain all required RunSummary fields.

## AC-006  —  ✅ covered

**Run:** run-970ce73dbc38
**Test cases:** `TC-006`
**Notes:** Three passing sub-tests verify: HTTP 200 with partial array when readRunSummaries returns only successfully-read summaries; HTTP 200 with [] when readRunSummaries returns [] (all runs failed); RunSummary with last_phase: null is included in the response without error.
