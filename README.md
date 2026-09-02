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

## Roadmap
Roadmap: add create LP (oss product wf)
