# Utpost

Plattform för friluftsdestinationer. Redaktionella guider, användarnas egna turer och bilder.

## Kom igång

```bash
npm install
docker compose -f docker-compose.dev.yml up -d
npm run seed
npm start
```

Appen ligger sen på http://localhost:3000 och API:et på http://localhost:4000.

## Struktur

- `api/` – Express + Postgres (Drizzle). Kräver **Node 22.18+** (routes skrivs i TypeScript och körs direkt av Node, utan byggsteg)
- `web/` – React + Vite
- `shared/` – **API-kontraktet som TypeScript-typer** (`@utpost/shared`). Används av både `api/` och `client/`. Ändras ett svar ändras typen, i samma PR.
- `client/` – **ny klient i Vue 3 + Vue Router** (port 3001), under migrering till TypeScript: `api.ts`, `GuideCard`, `GuidesView` och `GuideDetailView` är TS, `ToursView` och `TourDetailView` är fortfarande JS (`allowJs`). Lint, formatkontroll, typkontroll, tester och bygge körs av pipelinen på varje PR.

## Kommandon (kör från roten)

    npm run dev:client        # Vue-klienten på :3001 (API:et måste köra: npm run dev:api)
    npm run lint              # ESLint på client/
    npm run format:check      # Prettier – bara kontroll, ändrar inget
    npm run typecheck         # vue-tsc i client/ + tsc i api/ – ingen kompilering, bara kontroll
    npm test                  # Vitest, en gång, avslutar
    npm run build             # vite build av client/

## Deploy

Fråga Marcus.
