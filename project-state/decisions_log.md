# Decisions Log

**Schema version:** 1.0.0

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
