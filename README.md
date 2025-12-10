# TapIn

TapIn is a full-stack application for recording/transcribing audio and turning it into searchable, summarized notes. This repository contains a frontend (Vite + React + TypeScript), a backend (Express + TypeScript + Prisma), worker services for summarization, and a small Python-based transcriber service.

**Quick links**

- **Frontend:** `frontend`
- **Backend:** `backend`
- **Summarizer worker:** `summarizer-worker`
- **Transcriber (Python):** `transcriber`

**Tech highlights**

- Frontend: Vite + React + TypeScript
- Backend: Express (TypeScript), Prisma ORM
- Background worker: Node TypeScript worker consuming Redis
- Transcription: Python Flask service using Whisper (local model)

## Repository Structure

Top-level folders you’ll work with:

- `frontend/` — React + Vite application (UI)
- `backend/` — Express API, Prisma schema and migrations
- `summarizer-worker/` — Worker service that reads from Redis and summarizes
- `transcriber/` — Flask app that converts uploaded audio to text using Whisper
- `common/` — shared TypeScript packages used by backend/worker

## Prerequisites

- Node.js >= 18 (LTS recommended)
- npm (comes with Node.js)
- For local transcription: Python 3.9+ with required packages and a Whisper model (installation steps below)
- Redis (for worker/transcriber integration)

On Windows PowerShell, you can check versions:

```powershell
node -v
npm -v
python --version
redis-server --version
```

## Environment variables

Create `.env` files in services that need them (`backend/`, `summarizer-worker/`). Typical variables used by the backend and worker:

- `PORT` — port for the service (backend default: `3000`)
- `JWT_SECRET` — secret string for signing JWTs
- `SALT` — random string used for hashing passwords
- `FE_URL` — frontend URL (e.g. `http://localhost:5173`)
- `DATABASE_URL` — Prisma database connection URL
- Redis variables (if used by worker): `REDIS_URL` or host/port config

Example `.env` (backend):

```
PORT=3000
JWT_SECRET=supersecretjtw
SALT=random_salt_value
FE_URL=http://localhost:5173
DATABASE_URL=file:./dev.db
```

## Backend (Express + Prisma)

1. Open a terminal and install dependencies:

```powershell
cd backend
npm install
```

2. Prepare the database and Prisma (local development):

- If using SQLite (example dev DB):

```powershell
npx prisma generate
npx prisma migrate dev --name init
```

- If using a production DB or existing migrations:

```powershell
npx prisma generate
npx prisma migrate deploy
```

3. Start the backend in dev mode:

```powershell
npm run dev
```

This project exposes endpoints under `/api/v1/*`. The backend expects a cookie-based JWT named `token` for routes after authentication.

## Frontend (Vite + React)

1. Install dependencies and run the dev server:

```powershell
cd frontend
npm install
npm run dev
```

2. Open the app in your browser at the Vite URL (usually `http://localhost:5173`).

## Summarizer Worker

The worker consumes a Redis queue and triggers summarization logic. To run locally:

```powershell
cd summarizer-worker
npm install
npm run dev
```

Make sure Redis is running and the `DATABASE_URL` / Prisma migrations are applied if the worker needs DB access.

## Transcriber (Python + Whisper)

The transcriber is a small Flask app that accepts audio uploads and pushes transcribed text to Redis for the worker.

1. Create a virtual environment and install dependencies (example):

```powershell
cd transcriber
python -m venv .venv
. .venv/Scripts/Activate.ps1
pip install --upgrade pip
pip install flask pydub redis requests
# Whisper and its dependencies (you may prefer the official Whisper or OpenAI alternatives):
pip install -U openai-whisper
# You may need torch for whisper; see https://github.com/openai/whisper for platform-specific instructions
```

2. Start the service:

```powershell
python main.py
```

The Flask server will listen on its default Flask dev port (5000) unless changed. The service expects a running Redis instance reachable at `localhost:6379` by default.

Notes: Whisper installs and model downloads can be large. For reliable production transcription, consider using a hosted speech-to-text API or a dedicated GPU environment.

## Running the full stack locally

1. Start Redis.
2. Start the database (or use SQLite) and run Prisma migrations (`backend`).
3. Run the backend: `cd backend; npm run dev`.
4. Run the summarizer worker: `cd summarizer-worker; npm run dev`.
5. Run the transcriber (Python): `cd transcriber; python main.py`.
6. Run the frontend: `cd frontend; npm run dev`.

## Development notes

- Backend uses cookie-based authentication with JWT (`token` cookie).
- Sensitive values (JWT secret, SALT, DB credentials) must never be committed; use `.env` or a secrets manager.
- Prisma migrations are in `backend/prisma/migrations`.

## Contributing

- Create an issue for bugs or features.
- Open a pull request with a clear description and tests if applicable.

## License & Contact

This project does not include a license file by default — add a `LICENSE` (for example MIT) to make terms explicit.

If you want help running or polishing this README (examples, badges, CI, Docker), tell me what to add and I’ll update it.
