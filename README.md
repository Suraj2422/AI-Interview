# AI Interviewer

AI Interviewer is a full-stack monorepo for running a voice-based technical interview experience. A user enters a GitHub profile, the backend gathers repository context, and the app launches a live AI interview session with real-time audio, transcription, and post-interview evaluation.

## What it does

- Starts a voice interview from a GitHub profile URL
- Uses a real-time AI interviewer for the session
- Stores interview messages and metadata in PostgreSQL
- Generates a score and written feedback after the conversation
- Presents the transcript and results in a React-based UI

## Architecture

- Frontend: React + TypeScript + Bun + Tailwind + shadcn-style UI components
- Backend: Express + TypeScript + Prisma + PostgreSQL
- AI services:
  - OpenAI Realtime API for the live interview session
  - Gemini for interview scoring and feedback
  - GitHub scraping for profile/repository context

## Repository structure

- apps/frontend: interview UI, voice flow, result page
- apps/backend: Express server, Prisma models, interview orchestration, AI integrations
- packages/ui: shared UI primitives
- packages/eslint-config and packages/typescript-config: workspace tooling

## Prerequisites

- Bun 1.3+
- Node.js 18+
- PostgreSQL database
- API keys for:
  - OpenAI
  - Gemini

## Environment variables

Create environment variables for the backend before running it.

```bash
DATABASE_URL=postgresql://USER:PASSWORD@HOST:5432/DB_NAME
OPENAI_KEY=your_openai_key
GEMINI_API_KEY=your_gemini_key
PROXY_URL=optional_proxy_url_for_github_scraping
```

## Installation

From the repository root:

```bash
bun install
```

## Database setup

Run Prisma migrations from the backend app:

```bash
cd apps/backend
bunx prisma generate
bunx prisma migrate deploy
```

## Running the app

Start the backend:

```bash
cd apps/backend
bun run index.ts
```

Start the frontend in a second terminal:

```bash
cd apps/frontend
bun run dev
```

The frontend will launch its Bun dev server, and the backend will run on port 3001.

## Development notes

- The frontend expects the backend at http://localhost:3001
- The interview flow is driven by the backend endpoints under /api/v1
- The result page polls the backend until the interview has been evaluated

## Notes

The current implementation uses the OpenAI Realtime API for the voice session and Gemini for evaluation. If you want to use live transcription beyond the current setup, make sure the relevant transcription integration is configured in the frontend interview flow.
