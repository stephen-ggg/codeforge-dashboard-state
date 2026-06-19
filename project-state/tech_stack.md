# Tech Stack

**Schema version:** 1.0.0

## Locked Decisions

_These decisions are immutable and require human override to change._

### TD-001  —  language

**Decision:** TypeScript throughout — all source files use .ts/.tsx.

**Rationale:** Seeded locked decision from stack guidance.

**Run:** run-d5f2cf06a491
**Confirmed at:** 2026-06-19T15:30:12.653522+00:00

### TD-002  —  framework

**Decision:** Next.js 14 App Router. All page and layout files live under app/. Client-interactive components are marked 'use client'.

**Rationale:** Seeded locked decision from stack guidance. App Router is confirmed. HistoryTable and AppHeader are pure client components (no async server data), making them fully compatible with Vitest + jsdom.

**Run:** run-d5f2cf06a491
**Confirmed at:** 2026-06-19T15:30:12.653574+00:00

### TD-003  —  testing

**Decision:** Vitest + React Testing Library (@testing-library/react) + jsdom as the test environment.

**Rationale:** AC-004 explicitly names Vitest. React Testing Library is the standard companion for component smoke tests. jsdom allows DOM assertions in a Node environment. Components must be 'use client' to be mountable in jsdom (no async server component APIs used). This supersedes any Jest default that ships with Next.js.

**Run:** run-d5f2cf06a491
**Confirmed at:** 2026-06-19T15:30:12.653589+00:00
