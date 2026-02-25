# Project Guidance (Codex)

## Non-negotiables
- TypeScript everywhere. Strict mode on.
- Multi-tenant SaaS with shared Postgres schema; every tenant-owned row must be scoped by org_id.
- Use Prisma migrations. No schema drift.
- Never store API key secrets in plaintext—store hash + prefix; show secret only once.
- Stripe webhooks must verify signature using raw body; implement idempotency table.
- All services take an explicit TenantContext { orgId, userId?, role?, apiKeyId? } — no hidden globals.
- Central error handling: stable error shape + requestId; no internal leaks to clients.

## Engineering practices
- Prefer small, safe, incremental diffs.
- Add tests for each module: unit + integration (DB).
- Add structured logging and Sentry hooks (wiring is fine, keys via env).
- Document setup in README and include .env.example.

## Project structure
- Monorepo: apps/web (Next.js), apps/api (Fastify), apps/worker (BullMQ), packages/db (Prisma), packages/shared (zod schemas).
