# Product Vision Document: AI-Native Enterprise SaaS Theme

## 1. Executive Summary
The AI-Native Enterprise SaaS Theme is a bleeding-edge, multi-tenant digital headquarters designed for B2B SaaS and high-end local appointment-based businesses (e.g., medical offices, specialized clinics). It is built to replace fragmented marketing and operational tools with a unified, AI-first infrastructure that guarantees extreme performance, intelligent patient/lead intake, and Answer Engine Optimization (AEO).

## 2. The Turborepo Architecture
The product relies on a highly modular, decoupled Turborepo workspace to ensure separation of concerns while maximizing code reuse.

### Applications (`apps/*`)
*   **`apps/marketing`**: The public-facing marketing site. Powered by Next.js 16 and statically generated via Sanity CMS. Features AI-driven interactive widgets (Generative UI) and strict local schema markup.
*   **`apps/saas`**: The core multi-tenant application dashboard. Powered by Next.js 16 Server Actions, handling secure billing, organization management, and user data.
*   **`apps/docs`**: The documentation site, decoupled from the CMS and powered strictly by **Fumadocs** and local `.mdx` files for the ultimate developer/user reading experience.
*   **`apps/studio`**: The isolated **Sanity Studio** environment where marketing teams and clinic staff manage site content, leveraging Sanity AI Assist.
*   **`apps/mail-preview`**: A dedicated environment for building and previewing transactional emails using **React Email** (with HubSpot/Marketo integrations mapped for the roadmap).

### Shared Packages (`packages/*`)
*   **`packages/ui`**: Centralized **shadcn/ui** and **Tailwind CSS v4** component library.
*   **`packages/db`**: Shared **Drizzle ORM** schemas (Users, Tenants, Subscriptions).
*   **`packages/auth`**: Shared **Better Auth** configuration.
*   **`packages/sanity`**: Shared GROQ queries and Sanity client.

## 3. The Core Tech Stack
*   **Frontend**: Next.js 16, React 19, Tailwind v4, shadcn/ui.
*   **Backend / API**: Next.js Server Actions & Route Handlers (No legacy Hono/Express).
*   **Database**: PostgreSQL (e.g., Neon) managed by Drizzle ORM.
*   **Authentication**: Better Auth (handling RBAC and multi-tenancy).
*   **Validation & i18n**: Zod, next-intl.
*   **Deployment**: Vercel (Edge-ready).

## 4. AI-Native Primitives
This theme does not just "add AI"; it is fundamentally architected around it.
*   **Orchestration**: **Vercel AI SDK** handles all streaming, tool execution, and Generative UI components.
*   **Routing**: **OpenRouter** serves as the LLM gateway, allowing seamless switching between OpenAI, Anthropic (Claude 3.5 Sonnet), and open-source models without changing application code.
*   **Semantic Memory**: **Pinecone** serves as the vector database, instantly vectorizing marketing and documentation content for Retrieval-Augmented Generation (RAG).

## 5. Differentiating Features & Value Proposition

### A. Conversational Lead Qualification & Intake
Replaces static Typeform intakes with AI concierges built via the Vercel AI SDK. The concierge streams UI components directly into the chat (e.g., calendar booking widgets, pricing sliders) to overcome objections and pre-sell high-ticket services before a human is involved.

### B. Generative SEO & AEO (Answer Engine Optimization)
Built specifically to feed LLMs (ChatGPT, Perplexity). The architecture outputs an `llms.txt` file, semantic HTML, and strict Schema.org markup. When users ask AI for "the best specialized chiropractor near me," this theme ensures the client's data is machine-readable and highly cited.

### C. Seamless Multi-Tenancy & Vendor Consolidation
By unifying the marketing site, billing (Stripe), and app logic in a single repo, this theme replaces the need for clinics to duct-tape together WordPress, scheduling apps, and separate CRMs. 
