# Architecture

**Schema version:** 1.0.0  
**Last updated run:** run-935bbb649746

## Modules

### RunData

**Responsibility:** Define the RunRecord and StatusConfig TypeScript types, export an array of exactly 7 hardcoded RunRecord objects via getRunRecords, and export the STATUS_CONFIG map via getStatusConfig that resolves each status key to its display color and uppercase label.

**Exposes:** getRunRecords, getStatusConfig

### HistoryTable

**Responsibility:** A 'use client' React component that fetches run data from GET /api/runs on mount using useEffect and useState. Renders a scrollable table with columns STATUS, FEATURE, RUN ID, REACHED, WHEN and one row per RunSummary when the response array is non-empty. Renders the exact text 'No runs found.' when the response array is empty. Does not depend on RunData; any status-display configuration is inlined.

**Exposes:** HistoryTable

### AppHeader

**Responsibility:** Render the fixed 50px header containing the green logo dot, bold CODEFORGE label, Run and History tab buttons, and the call-budget progress bar. Accepts activeTab and onTabChange as props to drive tab button active states.

**Exposes:** AppHeader

### RunPlaceholder

**Responsibility:** Render the placeholder div displayed when the Run tab is active. No props required.

**Exposes:** RunPlaceholder

### DashboardPage

**Responsibility:** Root Next.js page. Owns the activeTab useState. Composes AppHeader (passing tab state and handler), and conditionally renders HistoryTable (History tab active) or RunPlaceholder (Run tab active). Applies global font and body styles via the root layout.

**Dependencies:** AppHeader, HistoryTable, RunPlaceholder
**Consumes:** AppHeader, HistoryTable, RunPlaceholder

## Interfaces

### getRunRecords  `function`  ✅ stable

**Owner:** RunData

### getStatusConfig  `function`  ✅ stable

**Owner:** RunData

### HistoryTable  `function`  ✅ stable

**Owner:** HistoryTable

### AppHeader  `function`  ✅ stable

**Owner:** AppHeader

### RunPlaceholder  `function`  ✅ stable

**Owner:** RunPlaceholder

## Data Flow

- **FetchRunSummaries:** `HistoryTable` → `GET /api/runs` via `fetch('/api/runs')`
  On mount, HistoryTable fires fetch('/api/runs') exactly once via useEffect. The response is a RunSummary array; if non-empty each element maps to one table row; if empty the component renders the text 'No runs found.'.
- **TabStateToHeader:** `DashboardPage` → `AppHeader` via `AppHeader`
  activeTab string ('run' | 'history'), onTabChange callback, callCurrent (hardcoded e.g. 12), and callCeiling (hardcoded e.g. 50) are passed as props.
- **TabChangeToPage:** `AppHeader` → `DashboardPage` via `AppHeader`
  onTabChange callback fires with the clicked tab key, triggering a useState update in DashboardPage that re-renders the active view.
- **ConditionalHistoryRender:** `DashboardPage` → `HistoryTable` via `HistoryTable`
  DashboardPage renders HistoryTable only when activeTab === 'history'. No props passed; HistoryTable sources its own data via fetch('/api/runs').
- **ConditionalRunRender:** `DashboardPage` → `RunPlaceholder` via `RunPlaceholder`
  DashboardPage renders RunPlaceholder only when activeTab === 'run'. No props passed.
