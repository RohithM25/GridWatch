# GridWatch

A simulated battery-plant monitoring & control application — field-facing software for
commissioning, monitoring, and controlling a single battery installation (not a
fleet-aggregation "many customers' devices" model).

> Status: Phase 0 (scaffolding).

## Architecture

_TBD — filled in as the system takes shape. Will cover: backend API design, device
simulation/ingestion, normalization layer, frontend data flow, and how the pieces
talk to each other._

## Why this project

_TBD — the fuller "why" writeup lands in Phase 6, alongside a design-decisions doc.
For the short version, see [docs/decisions/0001-stack-choice.md](docs/decisions/0001-stack-choice.md)._

## Stack

- **Backend:** Python, FastAPI
- **Frontend:** React (Vite)

## Running locally

### Backend

```bash
cd backend
python -m venv .venv
.venv/Scripts/activate   # or source .venv/bin/activate on macOS/Linux
pip install -r requirements.txt
uvicorn app.main:app --reload --port 8000
```

Health check: `http://localhost:8000/health`

### Frontend

```bash
cd frontend
npm install
npm run dev
```

App: `http://localhost:5173`

The frontend reads the backend URL from `VITE_API_BASE` (see `frontend/.env.example`);
defaults to `http://localhost:8000`.
