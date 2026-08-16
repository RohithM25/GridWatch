# 0001 — Backend and frontend stack

## Status
Accepted

## Context
GridWatch needs a backend and frontend for a battery-plant monitoring/control demo,
targeting entry/associate full-stack SWE roles in climate tech. The plan called for
choosing between Python and Go for the backend.

## Decision
- **Backend:** Python + FastAPI
- **Frontend:** React (Vite)

## Rationale
- Python/FastAPI scaffolds fast, has first-class async support (needed later for the
  message-queue phase), and is the more common stack for entry-level full-stack roles
  — makes the project's code more immediately legible to a wider set of reviewers.
- FastAPI's typed request/response models and auto-generated OpenAPI docs are a good
  fit for demonstrating REST API design decisions explicitly.
- Go was the other option on the table — it maps more directly onto Form Energy's
  actual stack and would read a bit stronger for the industrial-protocol phase
  (Modbus-style register interface), but costs more scaffolding time and is a less
  common expectation at the junior level. Revisit if a Go rewrite of a specific
  service (e.g. the Modbus device simulator) becomes worth it as a standalone
  portfolio signal.
- React (Vite) chosen over alternatives mainly because Vite's dev experience is fast
  and the ecosystem is the most common one to be asked about in interviews.

## Consequences
- Async/event-driven patterns (Phase 4) will use Python's asyncio ecosystem rather
  than goroutines/channels.
- The Modbus-style device (Phase 2) will be simulated in Python; this is a smaller
  "industrial protocol" story than doing it in Go, and worth being upfront about in
  interviews rather than overclaiming.
