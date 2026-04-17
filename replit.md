# AI Monorepo — AI Proxy Gateway

## Overview

A full-stack AI proxy gateway that exposes a unified OpenAI-compatible API endpoint, forwarding requests to OpenAI, Anthropic, Gemini, and OpenRouter via Replit AI Integrations. Includes a management portal for monitoring, model group configuration, logs, and version tracking.

## Stack

- **Monorepo tool**: pnpm workspaces
- **Node.js version**: 24
- **Package manager**: pnpm
- **TypeScript version**: 5.9
- **API framework**: Express 5
- **Database**: PostgreSQL + Drizzle ORM
- **Validation**: Zod (`zod/v4`), `drizzle-zod`
- **API codegen**: Orval (from OpenAPI spec)
- **Build**: esbuild (CJS bundle)
- **Frontend**: React + Vite + Tailwind CSS

## Artifacts

- `artifacts/api-server` — AI proxy API server (port 8080, path `/api`)
- `artifacts/api-portal` — Management portal frontend (port 24927, path `/`)

## AI Integrations (All Active)

| Integration | Env Vars |
|---|---|
| OpenAI | `AI_INTEGRATIONS_OPENAI_API_KEY`, `AI_INTEGRATIONS_OPENAI_BASE_URL` |
| Anthropic | `AI_INTEGRATIONS_ANTHROPIC_API_KEY`, `AI_INTEGRATIONS_ANTHROPIC_BASE_URL` |
| Gemini | `AI_INTEGRATIONS_GEMINI_API_KEY`, `AI_INTEGRATIONS_GEMINI_BASE_URL` |
| OpenRouter | `AI_INTEGRATIONS_OPENROUTER_API_KEY`, `AI_INTEGRATIONS_OPENROUTER_BASE_URL` |

All keys are automatically provisioned by Replit AI Integrations — no user API keys needed.

## Authentication

- `PROXY_API_KEY` secret — required for all `/api/v1/*` endpoints
- Pass as `Authorization: Bearer <key>` or `x-goog-api-key` header or `?key=` query param

## Key API Endpoints

- `GET /api/healthz` — Health check
- `GET /api/setup-status` — Integration & config status
- `GET /api/version` — Version info + update check
- `GET /api/v1/models` — List enabled models (auth required)
- `POST /api/v1/chat/completions` — Chat completions proxy (auth required)
- `GET /api/admin/logs` — Request logs (auth required)
- `GET /api/admin/model-groups` — Model group config
- `POST /api/admin/model-groups` — Update model groups (auth required)
- `GET /api/stats` — Usage stats (auth required)

## Key Commands

- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- `pnpm --filter @workspace/api-server run dev` — run API server locally
- `pnpm --filter @workspace/api-portal run dev` — run portal locally

## Source

Deployed from: https://github.com/Direet1/smdjajd.git
Original upstream: https://github.com/Akatsuki03/AI-Monorepo
