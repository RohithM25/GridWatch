# GridWatch — Implementation Plan

## What this is

A simulated battery-plant monitoring & control application, modeled on the kind of software
Form Energy's Plant Software team builds: field-facing software for commissioning, monitoring,
and controlling a single battery installation (not a fleet-aggregation "many customers' devices"
model like EnergyHub's).

## Why this shape

Built to demonstrate, in one coherent app: REST API design, full-stack ownership (React frontend
+ backend API), authentication/authorization, CI/CD + automated tests, async/event-driven patterns
(without overclaiming "distributed systems at scale"), and a real external data integration —
while staying scoped enough to actually finish and polish rather than sprawl.

Target roles: entry-level/associate SWE in climate tech, primarily Form Energy-style
(full-stack, Python/Go, industrial protocols, ownership mindset) rather than EnergyHub-style
(Java/Spring, multi-device VPP aggregation).

## Working style

Agile, MVP-first: each phase below is a shippable, demoable increment. Stopping after any
phase still leaves something coherent to show — later phases add on, they aren't required to
make the earlier ones "count."

## Phases

### Phase 0 — Scaffolding
- Repo setup, GitHub Issues/Projects board
- Skeleton backend (Python or Go) and skeleton React app
- README placeholder (architecture + "why" section to fill in later)
- First design-decision log entry: why this stack

### Phase 1 — MVP: one device, end-to-end
Thinnest possible vertical slice — prove the full pipeline before adding breadth.
- One simulated device (e.g. a single battery module) emitting fake telemetry
- Backend REST API storing/serving its current state
- One React page showing that device's status
- No auth, no queue, no multiple device types yet

### Phase 2 — Make it an actual "plant"
- Expand to 2-3 simulated device types with different raw data shapes
- One device exposed via a Modbus-style register interface (not plain REST) — hits the
  industrial-protocol angle specifically
- Normalization layer translating all device types into one common schema
- Dashboard becomes a fleet/plant view, not just one device
- "Commissioning" flow to register a new device to the plant

### Phase 3 — Make it behave like production software
- Auth: JWT login, two roles (viewer / operator)
- Command flow: operator-only charge/discharge commands (authz-protected)
- Fault history view + explicit handling when a device goes offline or throws a fault
  (not just happy-path)

### Phase 4 — Scale patterns + real-world data
- Message queue (Kafka or SQS) between ingestion and storage, decoupling device polling
  from persistence
- Real external API integration (WattTime / ElectricityMaps / EIA) driving a suggested
  charge/discharge schedule

### Phase 5 — Engineering hygiene
- CI/CD: GitHub Actions running tests on every push
- Automated tests: unit tests on core logic (normalization, scheduling, authz),
  at least one integration test
- Observability: structured logs + a simple metrics dashboard (Grafana/Prometheus or
  a lightweight alternative)

### Phase 6 — Polish for applications
- Rewrite README: architecture diagram, short demo GIF, "why this matters" framing
- Design-decisions/trade-offs write-up (also doubles as interview prep notes)
- Deploy a live demo (free-tier hosting)
- Optional: custom domain

## Cost

Effectively $0 — everything here runs on free tiers (hosting, DB, APIs). Optional custom
domain would run ~$10-15/year.

## Skills this is meant to cover
REST API design, full-stack (React + backend), auth/authz, CI/CD + automated testing,
async/event-driven pipeline patterns, real external API integration, basic observability,
SDLC habits (issue tracking, PR-based workflow, design docs) — demonstrated through how the
project is built, not a single feature.
