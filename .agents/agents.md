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
- Never duplicate code. If a component is used in `apps/marketing` and `apps/saas`, move it to `packages/ui`.
- All database schemas and queries must live in `packages/db`. Do not write Drizzle code inside `apps/`.
- Use `pnpm` for all package management. 

## AI SDK Rules
- Always use the `vercel/ai` SDK for streaming responses.
- Default to `OpenRouter` for LLM routing using the `@ai-sdk/openai` compatibility layer.
