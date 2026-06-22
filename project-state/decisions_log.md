# Decisions Log

**Schema version:** 1.0.0

## 95fb3869-8c54-4690-8ab1-709b43b0565b  —  🤖 agent decision

**Run:** run-935bbb649746  
**Created:** 2026-06-22T02:58:22.185110+00:00
**Source agent:** security_reviewer

**Decision:** This is a small Next.js client-component codebase with a very narrow attack surface. No secrets are hardcoded, no SQL or shell execution exists, React JSX escaping prevents XSS, and the CSS colour values rendered from API data are all hardcoded constants rather than user-controlled strings. One informational observation is raised: the fetch chain in HistoryTable does not check response.ok before calling .json(), so a non-2xx JSON error response is silently treated as empty data rather than surfaced as a fetch failure. The Array.isArray guard means nothing harmful is rendered, but the omission is worth noting as a hardening opportunity.

**Rationale:** pass_with_notes

## 26ff2e85-5f4a-4dc7-8271-2e1511af3ac7  —  🤖 agent decision

**Run:** run-935bbb649746  
**Created:** 2026-06-22T02:56:59.637213+00:00
**Source agent:** code_reviewer

**Decision:** HistoryTable correctly implements both must-priority ACs: fetch('/api/runs') fires exactly once on mount via a useEffect with an empty dependency array; when the response is non-empty, one <tr> per RunSummary is rendered using only the fetched data; when the array is empty (including initial render during in-flight fetch, which is acceptable per the out-of-scope loading-state constraint), the exact text 'No runs found.' is rendered with no data rows. All architecture interface contracts are satisfied: 'use client' directive, zero-props JSX.Element signature, correct fetch URL, five correct column headers, and no RunData import. One info-level observation on the unvalidated runtime type cast; does not affect correctness given the out-of-scope error-handling constraint.

**Rationale:** pass_with_notes

## 3cfdd6e9-dce7-4e38-ae40-dbacd84adfd4  —  🤖 agent decision

**Run:** run-935bbb649746  
**Created:** 2026-06-22T02:52:10.564983+00:00
**Source agent:** security_reviewer

**Decision:** The HistoryTable component is a narrow client component with no auth, no secrets, no direct DB or shell access, and correct React-based output escaping. One warn-level finding: the package.json specifies next: "^14" which includes Next.js versions below 14.2.25 that are affected by CVE-2025-29927 (middleware authentication bypass). The lockfile should be verified to confirm a patched version is installed.

**Rationale:** pass_with_notes

## 2f887ea0-1916-4af2-94aa-8e412c29943f  —  🤖 agent decision

**Run:** run-935bbb649746  
**Created:** 2026-06-22T02:51:00.264253+00:00
**Source agent:** code_reviewer

**Decision:** HistoryTable correctly implements AC-001 (fetch on mount, one row per RunSummary, no getRunRecords dependency) and AC-002 (exact 'No runs found.' empty state). All architecture interface contracts are satisfied: 'use client' directive, zero-props JSX.Element signature, useEffect empty-dep-array trigger, correct fetch URL, and all five column headers. One info-level observation about the unverified runtime type cast in the fetch .then callback; does not affect correctness given the out-of-scope error handling.

**Rationale:** pass_with_notes

## 75cdc458-2727-4a6d-926d-12e472060abd  —  🤖 agent decision

**Run:** run-935bbb649746  
**Created:** 2026-06-22T02:49:32.094949+00:00
**Source agent:** architecture_designer

**Decision:** HistoryTable uses the native browser fetch API with useState and useEffect (empty dependency array) to load run data on mount. No external data-fetching library (SWR, React Query, etc.) is introduced.

**Rationale:** Requirements explicitly name useState and useEffect. Native fetch is sufficient for a single endpoint call on mount. Avoids adding a library dependency for a minimal use case.

## 7e140203-b2b0-452a-aafe-c4f6a01a58fd  —  🤖 agent decision

**Run:** run-935bbb649746  
**Created:** 2026-06-22T02:49:32.094932+00:00
**Source agent:** architecture_designer

**Decision:** Vitest + React Testing Library (@testing-library/react) + jsdom as the test environment.

**Rationale:** Vitest is the confirmed test runner. React Testing Library is the standard companion for component tests. jsdom allows DOM assertions in a Node environment. Components must be 'use client' to be mountable in jsdom.

## ff9d4cb3-8631-422f-b11c-2aece7b3dbd1  —  🤖 agent decision

**Run:** run-935bbb649746  
**Created:** 2026-06-22T02:49:32.094893+00:00
**Source agent:** architecture_designer

**Decision:** Next.js 14 App Router. All page and layout files live under app/. Client-interactive components are marked 'use client'.

**Rationale:** Seeded locked decision from stack guidance. App Router is confirmed. HistoryTable is a pure client component (no async server data), making it fully compatible with Vitest + jsdom.

## 292b3775-adf9-4a38-89c7-e75668753369  —  🤖 agent decision

**Run:** run-935bbb649746  
**Created:** 2026-06-22T02:49:32.094860+00:00
**Source agent:** architecture_designer

**Decision:** TypeScript throughout — all source files use .ts/.tsx.

**Rationale:** Seeded locked decision from stack guidance.

## 959fd18d-e835-497e-89f7-cc78215782a3  —  🤖 agent decision

**Run:** run-d5f2cf06a491  
**Created:** 2026-06-19T15:37:10.966716+00:00
**Source agent:** security_reviewer

**Decision:** This is a purely static UI scaffold with no API routes, no user-supplied input processed server-side, no authentication surface, no secrets, no database access, and no external data fetching at runtime. All rendered content derives from hardcoded TypeScript literals. React escapes text nodes by default, and no user data flows into style properties. One info-level observation is raised: no dependency lock file is included in the artifact, meaning semver-range installs could silently pick up newer patch/minor versions. No exploitable security issues were found.

**Rationale:** pass_with_notes

## 54593542-5ccf-4675-80d3-a0e136cebeaa  —  🤖 agent decision

**Run:** run-d5f2cf06a491  
**Created:** 2026-06-19T15:36:10.949337+00:00
**Source agent:** code_reviewer

**Decision:** All five modules implement their architecture contracts correctly. AC-001 (header), AC-002 (history table with 7 rows and correct oklch accents), AC-003 (tab switching), and the supporting infrastructure are fully addressed. The single notable gap is that no Vitest test file is present in the artifact, so AC-004 cannot be verified as passing from this artifact alone; the coder's firewall delegates test authoring to the Test Designer, which is appropriate but should be actioned before the pipeline closes.

**Rationale:** pass_with_notes

## 479f59d2-f310-4425-8d05-c6253475fd04  —  🤖 agent decision

**Run:** run-d5f2cf06a491  
**Created:** 2026-06-19T15:30:12.653853+00:00
**Source agent:** architecture_designer

**Decision:** JetBrains Mono loaded via next/font/google and applied to the root layout body class.

**Rationale:** Requirements specify JetBrains Mono (Google Fonts). next/font/google is the idiomatic App Router approach; it avoids external network requests at runtime and provides CSS variable injection.

## ba6b41ec-68e6-42dd-baeb-1af92d53dc98  —  🤖 agent decision

**Run:** run-d5f2cf06a491  
**Created:** 2026-06-19T15:30:12.653839+00:00
**Source agent:** architecture_designer

**Decision:** Active tab state managed with React useState in DashboardPage. No URL routing or persistent storage for tab state.

**Rationale:** Requirements explicitly exclude persistent tab state. Local state is the simplest correct solution.

## 1647a78b-cf24-4f52-83cb-1dc63c6393f5  —  🤖 agent decision

**Run:** run-d5f2cf06a491  
**Created:** 2026-06-19T15:30:12.653824+00:00
**Source agent:** architecture_designer

**Decision:** Vitest + React Testing Library (@testing-library/react) + jsdom as the test environment.

**Rationale:** AC-004 explicitly names Vitest. React Testing Library is the standard companion for component smoke tests. jsdom allows DOM assertions in a Node environment. Components must be 'use client' to be mountable in jsdom (no async server component APIs used). This supersedes any Jest default that ships with Next.js.

## 001cf8d3-1939-4b1a-8473-9ff872248b6e  —  🤖 agent decision

**Run:** run-d5f2cf06a491  
**Created:** 2026-06-19T15:30:12.653805+00:00
**Source agent:** architecture_designer

**Decision:** Next.js 14 App Router. All page and layout files live under app/. Client-interactive components are marked 'use client'.

**Rationale:** Seeded locked decision from stack guidance. App Router is confirmed. HistoryTable and AppHeader are pure client components (no async server data), making them fully compatible with Vitest + jsdom.

## d09ed7a6-1dfd-4a5b-8642-441ac61d42a5  —  🤖 agent decision

**Run:** run-d5f2cf06a491  
**Created:** 2026-06-19T15:30:12.653775+00:00
**Source agent:** architecture_designer

**Decision:** TypeScript throughout — all source files use .ts/.tsx.

**Rationale:** Seeded locked decision from stack guidance.
