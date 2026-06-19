# Architecture

**Schema version:** 1.0.0  
**Last updated run:** run-d5f2cf06a491

## Modules

### RunData

**Responsibility:** Define the RunRecord and StatusConfig TypeScript types, export the array of exactly 7 hardcoded RunRecord objects, and export the STATUS_CONFIG map that resolves each status key to its display color and uppercase label.

**Exposes:** getRunRecords, getStatusConfig

### HistoryTable

**Responsibility:** Render the scrollable history table with exactly the five column headers (STATUS, FEATURE, RUN ID, REACHED, WHEN) and one row per RunRecord. Each row applies a 2px left-border accent, a colored status dot, and an uppercase label derived from the status config. Internally sources data from RunData.

**Dependencies:** RunData
**Exposes:** HistoryTable
**Consumes:** getRunRecords, getStatusConfig

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

- **RunRecordsToTable:** `RunData` → `HistoryTable` via `getRunRecords`
  Array of 7 RunRecord objects flows into HistoryTable at render time. Each record supplies the row data: id (React key), status, feature, runId, reached, when.
- **StatusConfigToTable:** `RunData` → `HistoryTable` via `getStatusConfig`
  Status config map flows into HistoryTable. Each row looks up its status key to resolve the accent color (oklch string) and uppercase display label.
- **TabStateToHeader:** `DashboardPage` → `AppHeader` via `AppHeader`
  activeTab string ('run' | 'history'), onTabChange callback, callCurrent (hardcoded e.g. 12), and callCeiling (hardcoded e.g. 50) are passed as props.
- **TabChangeToPage:** `AppHeader` → `DashboardPage` via `AppHeader`
  onTabChange callback fires with the clicked tab key, triggering a useState update in DashboardPage that re-renders the active view.
- **ConditionalHistoryRender:** `DashboardPage` → `HistoryTable` via `HistoryTable`
  DashboardPage renders HistoryTable only when activeTab === 'history'. No props passed; HistoryTable sources its own data.
- **ConditionalRunRender:** `DashboardPage` → `RunPlaceholder` via `RunPlaceholder`
  DashboardPage renders RunPlaceholder only when activeTab === 'run'. No props passed.
