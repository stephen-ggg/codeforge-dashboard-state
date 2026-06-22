# Tech Stack

**Schema version:** 1.0.0

## Locked Decisions

_These decisions are immutable and require human override to change._

### TD-001  —  language

**Decision:** TypeScript throughout — all source files use .ts/.tsx.

**Rationale:** Seeded locked decision from stack guidance.

**Run:** run-935bbb649746
**Confirmed at:** 2026-06-22T02:49:32.094539+00:00

### TD-002  —  framework

**Decision:** Next.js 14 App Router. All page and layout files live under app/. Client-interactive components are marked 'use client'.

**Rationale:** Seeded locked decision from stack guidance. App Router is confirmed. HistoryTable is a pure client component (no async server data), making it fully compatible with Vitest + jsdom.

**Run:** run-935bbb649746
**Confirmed at:** 2026-06-22T02:49:32.094592+00:00

### TD-003  —  testing

**Decision:** Vitest + React Testing Library (@testing-library/react) + jsdom as the test environment.

**Rationale:** Vitest is the confirmed test runner. React Testing Library is the standard companion for component tests. jsdom allows DOM assertions in a Node environment. Components must be 'use client' to be mountable in jsdom.

**Run:** run-935bbb649746
**Confirmed at:** 2026-06-22T02:49:32.094608+00:00
