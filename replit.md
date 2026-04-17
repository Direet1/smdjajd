# AI Monorepo

## Overview

AI Monorepo — an OpenAI-compatible AI proxy that forwards requests to Anthropic (Claude), OpenAI (GPT/o-series), Google (Gemini), and OpenRouter. Includes a management portal (api-portal) and a backend API server.

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
- **Frontend**: React + Vite (api-portal)

## Source

Based on https://github.com/Direet1/smdjajd.git

## Artifacts

- **api-server** (port 8080, path `/api`) — Express API proxy server with AI integrations
- **api-portal** (port 8000, path `/`) — React management portal frontend

## AI Integrations (configured)

- **Anthropic**: `AI_INTEGRATIONS_ANTHROPIC_API_KEY` / `AI_INTEGRATIONS_ANTHROPIC_BASE_URL`
- **OpenAI**: `AI_INTEGRATIONS_OPENAI_API_KEY` / `AI_INTEGRATIONS_OPENAI_BASE_URL`
- **Gemini**: `AI_INTEGRATIONS_GEMINI_API_KEY` / `AI_INTEGRATIONS_GEMINI_BASE_URL`
- **OpenRouter**: `AI_INTEGRATIONS_OPENROUTER_API_KEY` / `AI_INTEGRATIONS_OPENROUTER_BASE_URL`

## Authentication

- `PROXY_API_KEY` = `0110158` — used to authenticate requests to the proxy

## Key Commands

- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- `pnpm --filter @workspace/api-server run dev` — run API server locally
- `pnpm --filter @workspace/api-portal run dev` — run portal locally

## API Usage

Base URL: `https://<your-replit-domain>/api/v1`
Auth: `Authorization: Bearer 0110158`

Example:
```bash
curl https://<domain>/api/v1/models -H "Authorization: Bearer 0110158"
curl https://<domain>/api/v1/chat/completions \
  -H "Authorization: Bearer 0110158" \
  -H "Content-Type: application/json" \
  -d '{"model":"claude-sonnet-4-5","messages":[{"role":"user","content":"Hello"}]}'
```

See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details.
