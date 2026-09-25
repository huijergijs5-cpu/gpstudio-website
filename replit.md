# GP Webstudio

Een professionele Belgische webstudio-website voor GP Webstudio, met portfolio, werkwijze, juridische pagina's en een echte offerte-aanvraagflow.

## Run & Operate

- `pnpm --filter @workspace/api-server run dev` — run the API server (port 5000)
- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from the OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- Required env: `DATABASE_URL` — Postgres connection string

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9
- API: Express 5
- DB: PostgreSQL + Drizzle ORM
- Validation: Zod (`zod/v4`), `drizzle-zod`
- API codegen: Orval (from OpenAPI spec)
- Build: esbuild (CJS bundle)

## Where things live

- `artifacts/gp-webstudio/src/App.tsx` — homepage, juridische routes, formulier en SEO-initialisatie.
- `artifacts/gp-webstudio/src/index.css` — GP Webstudio tokens, responsive styling en motion.
- `lib/api-spec/openapi.yaml` — contract voor de contactaanvraag.
- `artifacts/api-server/src/routes/contact.ts` — server-side validatie, honeypot, rate limiting en opslag.
- `lib/db/src/schema/contact-requests.ts` — bron van waarheid voor opgeslagen offerteaanvragen.

## Architecture decisions

- De publieke site is een presentatiegerichte React/Vite-app op de root preview path.
- Contactaanvragen worden server-side gevalideerd en opgeslagen in PostgreSQL; de ontvanger is configureerbaar via `CONTACT_EMAIL`.
- Portfolio-items zijn bewust als demo-concept gelabeld totdat echte projecten beschikbaar zijn.
- Tracking wordt niet geladen zonder expliciete configuratie en toestemming; daarom is er geen onnodige cookiebanner.

## Product

- Nederlandstalige homepage met diensten, demo-portfolio, werkwijze, over-ons, contactformulier en responsive mobiele navigatie.
- Privacybeleid, cookiebeleid, algemene voorwaarden en een custom route-level 404.
- SEO-basis met route-specifieke metadata, canonical URLs, Open Graph metadata, structured data, robots.txt en sitemap.xml.

## User preferences

_Populate as you build — explicit user instructions worth remembering across sessions._

## Gotchas

- De webapp gebruikt de door het artifact-workflow aangeleverde `PORT` en `BASE_PATH`; een losse Vite-build heeft beide variabelen nodig.

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details
