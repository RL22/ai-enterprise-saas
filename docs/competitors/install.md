# AI-Native Enterprise SaaS - Installation & Setup Guide

This guide outlines the step-by-step sequence to bootstrap, configure, and deploy the AI-Native Enterprise monorepo.

## System Prerequisites
*   **Node.js:** v20+
*   **Package Manager:** `pnpm` (v9+)
*   **CLI Tools:** Vercel CLI, Sanity CLI

---

## Phase 1: Monorepo Initialization

### 1. Scaffold the Turborepo
Create the foundational monorepo structure using pnpm workspaces.
```bash
npx create-turbo@latest ai-enterprise-saas --use-pnpm
cd ai-enterprise-saas
```

### 2. Configure the Workspace Structure
Ensure your `pnpm-workspace.yaml` maps to our approved architecture:
```yaml
packages:
  - "apps/*"
  - "packages/*"
```
Create the missing directories:
```bash
mkdir -p apps/marketing apps/saas apps/docs apps/studio apps/mail-preview
mkdir -p packages/ui packages/db packages/auth packages/email packages/sanity packages/config
```

---

## Phase 2: Package Setup (`packages/*`)

### 1. `packages/ui` (shadcn/ui + Tailwind v4)
Initialize Shadcn UI. This package will export all standard UI components to the apps.
```bash
cd packages/ui
npx shadcn-ui@latest init
```
*Note: Configure `components.json` to use Tailwind v4 and React 19.*

### 2. `packages/db` (Drizzle ORM)
Install Drizzle and configure the PostgreSQL connection (e.g., Neon).
```bash
cd ../db
pnpm add drizzle-orm postgres
pnpm add -D drizzle-kit
```
*Action:* Define schema in `schema.ts` (Users, Tenants, Subscriptions).

### 3. `packages/auth` (Better Auth)
Configure Better Auth to connect to the Drizzle database.
```bash
cd ../auth
pnpm add better-auth
```

### 4. `packages/sanity`
Initialize the shared Sanity client and GROQ queries to be consumed by `apps/marketing`.
```bash
cd ../sanity
pnpm add next-sanity @sanity/client
```

---

## Phase 3: Application Setup (`apps/*`)

### 1. `apps/saas` (The Core App)
Initialize Next.js 16.
```bash
cd ../../apps
npx create-next-app@latest saas
```
*Link dependencies:* Add `workspace:*` references to `@repo/ui`, `@repo/db`, `@repo/auth` in `package.json`.

### 2. `apps/marketing` (Public Site)
Initialize Next.js 16 and connect to Sanity.
```bash
npx create-next-app@latest marketing
```
*Link dependencies:* Add `@repo/ui`, `@repo/sanity`.

### 3. `apps/studio` (Sanity Authoring)
Initialize the Sanity Studio.
```bash
npm create sanity@latest -- --template clean --create-project "AI Enterprise" --dataset production --output-path studio
```

### 4. `apps/docs` (Fumadocs)
Initialize the documentation site.
```bash
npx create-fumadocs-app docs
```

---

## Phase 4: AI Infrastructure Setup

### 1. Vercel AI SDK & OpenRouter
Install the AI SDK in `apps/saas` and `apps/marketing`.
```bash
pnpm add ai @ai-sdk/openai
```
*Configuration:* Set `OPENROUTER_API_KEY` in `.env`. Configure the AI SDK to route requests through OpenRouter (which exposes the OpenAI-compatible API format) for LLM routing.

### 2. Pinecone Vector DB (RAG)
Initialize Pinecone for semantic search in `apps/docs` and `apps/marketing`.
```bash
pnpm add @pinecone-database/pinecone
```

---

## Phase 5: Environment Variables & Deployment

Create a `.env.local` at the root and populate the following keys:
```env
# Database (Neon/Supabase)
DATABASE_URL=""

# Authentication (Better Auth)
BETTER_AUTH_SECRET=""
BETTER_AUTH_URL="http://localhost:3000"

# Sanity CMS
NEXT_PUBLIC_SANITY_PROJECT_ID=""
NEXT_PUBLIC_SANITY_DATASET="production"
SANITY_API_READ_TOKEN=""

# AI & Vector DB
OPENROUTER_API_KEY=""
PINECONE_API_KEY=""
PINECONE_INDEX=""
```

### Vercel Deployment
Deploy the monorepo to Vercel, ensuring each app (`saas`, `marketing`, `docs`, `studio`) is deployed as a separate Vercel project pointing to the same GitHub repository, but with the specific `apps/*` configured as the Root Directory.
