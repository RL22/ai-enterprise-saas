# Premium SaaS Boilerplate Analysis & Reverse Engineering Strategy

## 1. Analysis: Supastarter and MakerKit

Both **Supastarter** and **MakerKit** are premium, production-ready Next.js SaaS boilerplates designed for B2B applications with robust features for multi-tenancy, billing, authentication, and AI integrations.

### Supastarter Architecture
- **Monorepo Structure**: Uses **Turborepo** to separate concerns into modular applications (`apps/marketing`, `apps/saas`) and shared internal packages (UI, core logic, configs).
- **Authentication**: Leverages **Better Auth** for self-hosted, full-stack authentication (OAuth, magic links, passkeys). User data remains in the proprietary database, avoiding vendor lock-in. Includes built-in Role-Based Access Control (RBAC).
- **Billing**: Features a unified billing interface supporting multiple providers simultaneously (Stripe, Lemon Squeezy, Polar, Creem, Dodo Payments). Allows seamless provider switching.
- **Multi-Tenancy**: Models tenants as "Organizations". Uses a shared-database, shared-schema approach (typically via a `tenantId` or `organizationId` column). Supports per-tenant feature flags and custom domains.
- **AI Integrations**: Often incorporates pre-built integrations for AI via standard API routes but leans heavily on allowing developers to drop in tools like Vercel AI SDK seamlessly into its modular structure.

### MakerKit Architecture
- **Monorepo Structure**: Also built on **Turborepo** for a highly modular, TypeScript-optimized environment. Strict linting and type-safety across the monorepo.
- **Authentication**: Depending on the stack, supports **Supabase Auth** or **Better Auth**. Features MFA, social logins, and extensive session management.
- **Billing**: Provides an abstracted billing layer that wraps Stripe, Lemon Squeezy, and Paddle. Supports tiered, flat-rate, and per-seat subscription models.
- **Multi-Tenancy**: Deeply integrated into the database layer. In its Supabase stack, MakerKit enforces multi-tenancy at the database level using **Row Level Security (RLS)**, ensuring robust data isolation.
- **AI Integrations**: Highly optimized for AI-assisted development. Includes an **MCP (Model Context Protocol) server** and specific rules (`.cursor/rules` or `AGENTS.md`) for AI coding agents to extend the codebase safely.

---

## 2. Reverse Engineering Outline

To replicate these core enterprise capabilities from scratch using standard open-source tools and the **Vercel AI SDK**, follow this step-by-step strategy:

### Step 1: Scaffold a Modular Monorepo
- **Tool**: [Turborepo](https://turbo.build/repo)
- **Action**: Create a monorepo workspace containing separate apps for the marketing site (`apps/web`) and the main SaaS application (`apps/app`). Create shared packages for UI components (Shadcn UI + Tailwind), database schemas, and shared utilities.

### Step 2: Set Up Database and Multi-Tenancy (RLS)
- **Tools**: Postgres, [Drizzle ORM](https://orm.drizzle.team/), Supabase (optional, for built-in RLS)
- **Action**: Define an `Organizations` (tenants) table and a `Users` table. Link them via a many-to-many relationship for RBAC. Implement Row Level Security (RLS) on all core tables to enforce that queries only return data where `tenant_id` matches the authenticated user's active organization.

### Step 3: Implement Authentication and RBAC
- **Tool**: [Better Auth](https://www.better-auth.com/)
- **Action**: Set up Better Auth to handle user sessions, magic links, and OAuth. Utilize Better Auth's plugins for Organization Management and Role-Based Access Control to handle multi-tenant user invites, roles (Owner, Admin, Member), and session management.

### Step 4: Abstracted Billing Layer
- **Tools**: Stripe, Lemon Squeezy
- **Action**: Create a shared `packages/billing` interface. Define a standard schema for `Subscriptions` and `Plans`. Set up webhooks in Next.js API routes to sync subscription statuses, limits, and AI credit balances to your database when payments succeed or fail.

### Step 5: Vercel AI SDK Integration
- **Tool**: [Vercel AI SDK](https://sdk.vercel.ai/docs)
- **Action**: Implement streaming API routes (e.g., `app/api/chat/route.ts`). Use the `generateText` or `streamText` functions. Tie AI execution to a tenant-based credit system—before initiating a completion, verify the tenant has sufficient credits via your database, and decrement credits upon successful generation using the AI SDK's token usage callbacks. Provide pre-configured prompt management and agent tooling specific to the active tenant's context.

---

## 3. Free / Open-Source Alternatives

To avoid paying the premium price for boilerplate features, here are high-quality, open-source alternatives that provide similar enterprise capabilities:

### 1. [nextjs/saas-starter](https://github.com/nextjs/saas-starter)
- **Description**: An official-style Next.js starter repository maintained by the Next.js community/Vercel.
- **Features**: Includes built-in support for Postgres (via Drizzle ORM), Stripe billing integration, Shadcn UI, multi-tenancy (team/organization structures), and Role-Based Access Control. A fantastic, clean baseline.

### 2. [ixartz/SaaS-Boilerplate](https://github.com/ixartz/SaaS-Boilerplate)
- **Description**: A highly popular and actively maintained open-source boilerplate.
- **Features**: Offers robust out-of-the-box features including multi-tenancy, RBAC, social login, i18n support, and a comprehensive test suite. Extremely useful for hitting the ground running with standard enterprise requirements.

### 3. [MakerKit (Lite Version)](https://github.com/makerkit/makerkit)
- **Description**: The open-source foundational core of MakerKit.
- **Features**: While missing some of the premium pre-built components, it provides the Turborepo monorepo structure, core authentication, and foundational multi-tenant data modeling, making it an excellent starting point for advanced architectures.
