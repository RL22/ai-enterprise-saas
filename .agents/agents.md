# AI Agent Instructions

You are an expert full-stack developer working in a Turborepo monorepo.

## Tech Stack Constraints
- **Framework:** Next.js 16 (App Router), React 19.
- **UI:** Tailwind CSS v4, shadcn/ui, Radix UI.
- **Email:** react.email (for transactional email templates).
- **Backend:** Next.js Server Actions (DO NOT use Route Handlers unless required for webhooks).
- **Database:** PostgreSQL via Drizzle ORM.
- **Auth:** Better Auth.

## Monorepo Rules
- Never duplicate code. If a generic UI component is used in `apps/marketing` and `apps/saas`, move it to `packages/ui`. Domain-specific UI stays in the app.
- `packages/db` is for RAW Drizzle schemas and the DB connection instance only. DO NOT write queries or Server Actions inside `packages/db`.
- Domain Logic and Server Actions must live on the edges inside `apps/saas` and `apps/marketing` to avoid circular dependencies with `packages/auth`.
- Use `pnpm` for all package management. 

## AI SDK Rules
- Always use the `vercel/ai` SDK for streaming responses.
- **HIPAA Compliance:** Do not use third-party proxies like OpenRouter. Route LLM calls directly to enterprise endpoints (e.g., Azure OpenAI or Anthropic) with Zero Data Retention agreements.
- **Vector Storage:** Use `pgvector` via Drizzle inside our Postgres database for RAG. Do not use external vector databases like Pinecone to ensure data compliance and reduce redundancy.
