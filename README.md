# Utpost

A platform for outdoor destinations. Editorial guides, users' own tours, and photos.

## Getting started

Requires Node 22.18+ and Docker Desktop. Two ways to run it, from the repo root.

**All of Utpost in Docker** (Postgres, MongoDB, API, and client):

```bash
docker compose up --build -d
docker compose exec api npm run seed
```

The client is then at http://localhost:3001 and the API at http://localhost:4000.

**Databases only in Docker**, the app on your computer:

```bash
docker compose up -d postgres mongo
npm install
npm run seed
npm run dev:api
npm run dev:client
```

The API on your computer uses `localhost:5433` and `localhost:27017`, the ports Compose publishes. The client is at http://localhost:3001 and the API at http://localhost:4000.

## Structure

- `api/` – Express + Postgres (Drizzle). Requires **Node 22.18+** (routes are written in TypeScript and run directly by Node, with no build step)
- `web/` – React + Vite
- `shared/` – **the API contract as TypeScript types** (`@utpost/shared`). Used by both `api/` and `client/`. When a response changes, the type changes in the same PR.
- `client/` – **new Vue 3 + Vue Router client** (port 3001), migrating to TypeScript: `api.ts`, `GuideCard`, `GuidesView`, and `GuideDetailView` are TS; `ToursView` and `TourDetailView` are still JS (`allowJs`). Lint, format check, typecheck, tests, and build run in the pipeline on every PR.

## Commands (run from the root)

    npm run dev:client        # Vue client on :3001 (the API must be running: npm run dev:api)
    npm run lint              # ESLint on client/
    npm run format:check      # Prettier – check only, changes nothing
    npm run typecheck         # vue-tsc in client/ + tsc in api/ – no compile, check only
    npm test                  # Vitest, once, then exits
    npm run build             # vite build of client/

## Deploy

Ask Marcus.
