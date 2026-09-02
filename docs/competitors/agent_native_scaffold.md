# Agent-Native Repository Scaffold & README

To make a monorepo truly "agent-native" (meaning AI coding assistants like Antigravity, Cursor, or Copilot can navigate, build, and debug without hallucinating), you must provide explicit machine-readable boundaries and rules.

## 1. The Agent-Native Directory Tree

```text
ai-enterprise-saas/
├── .agents/                    # 🤖 AI-specific instructions and context
│   ├── agents.md               # Global rules for agents (e.g., "Use Next 16 Server Actions")
│   └── architecture.md         # Diagram of how apps interact with packages
├── .cursorrules                # Editor-specific AI rules (points to .agents/agents.md)
├── llms.txt                    # Public-facing machine-readable summary of the repo
├── apps/
│   ├── marketing/              # Next.js 16 - Public site
│   ├── saas/                   # Next.js 16 - Dashboard
│   ├── docs/                   # Fumadocs - MDX documentation
│   ├── studio/                 # Sanity Studio CMS
│   └── mail-preview/           # React Email previews
├── packages/
│   ├── ui/                     # shadcn/ui + Tailwind v4 (Strict export boundaries)
│   ├── db/                     # Drizzle schema + Postgres client
│   ├── auth/                   # Better Auth config
│   ├── sanity/                 # GROQ queries + Sanity client
│   └── config/                 # ESLint, TSConfig, Prettier
├── pnpm-workspace.yaml
└── README.md                   # Human & Agent entrypoint
```

---

## 2. Recommended `.cursorrules` / `.agents/RULES.md`
*Agents read this file automatically on every prompt to understand the tech stack and constraints.*

```markdown
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
```

---

## 3. Recommended Base `README.md`
*This README is designed to be easily parsed by both humans and LLMs indexing the repo.*

```markdown
# AI-Native Enterprise SaaS Monorepo

## Overview
This is a Turborepo workspace powering a multi-tenant, AI-native B2B SaaS platform. It strictly enforces separation of concerns between public marketing, core application logic, and CMS authoring.

## Workspace Architecture

| Workspace | Type | Path | Purpose |
|-----------|------|------|---------|
| `marketing` | App | `/apps/marketing` | Next.js 16 marketing site. Powered by Sanity CMS. |
| `saas` | App | `/apps/saas` | Next.js 16 SaaS dashboard. Powered by Better Auth & Drizzle. |
| `docs` | App | `/apps/docs` | Fumadocs documentation site. |
| `studio` | App | `/apps/studio` | Sanity Studio authoring environment. |
| `@repo/ui` | Package | `/packages/ui` | Shared shadcn/ui and Tailwind v4 components. |
| `@repo/db` | Package | `/packages/db` | Shared Drizzle ORM schemas and Postgres client. |
| `@repo/auth` | Package | `/packages/auth` | Shared Better Auth configuration. |

## Quick Start
1. Install dependencies: `pnpm install`
2. Set up environment variables: `cp .env.example .env.local`
3. Push database schema: `cd packages/db && pnpm db:push`
4. Start development server: `pnpm dev`
```
