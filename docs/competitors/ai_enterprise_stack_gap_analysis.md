# AI-Native Enterprise Marketing Stack
*Bridging the gap between a base Sanity CMS starter (SanityPress / Clean Starter) and a premium SaaS boilerplate (MakerKit / Supastarter) to build an AI-native B2B SaaS marketing engine.*

---

## 1. The Starting Point (The Base)
We are starting with either **SanityPress** or the **Official Clean Sanity Template**. 
**What we get out of the box:**
* Next.js 15 App Router & React Server Components
* Tailwind CSS
* Sanity Studio (embedded at `/studio`)
* Live Visual Editing & Presentation Tool
* GROQ querying setup

## 2. The Missing Enterprise SaaS Infrastructure
To match the robust, multi-tenant application infrastructure of MakerKit or Supastarter, we must manually integrate the following application layers alongside our Sanity content layer:

### A. Authentication & Identity
*   **The Gap:** MakerKit ships with complex organization (B2B) authentication.
*   **The Addition:** **Clerk** (Enterprise-ready, B2B organization support out of the box) or **Auth.js** (formerly NextAuth, if strictly open-source is required).
*   **Implementation:** Wrap the app in `<ClerkProvider>`, setup `/sign-in`, `/sign-up`, and protect the `/dashboard` routes using Next.js Middleware.

### B. Relational Database & ORM (App State)
*   **The Gap:** Sanity handles our *marketing content*, but we need a transactional database for user accounts, billing states, and app data.
*   **The Addition:** **PostgreSQL** (hosted on **Neon** or **Supabase**) managed via **Drizzle ORM**.
*   **Implementation:** Create schemas for `users`, `organizations`, `subscriptions`, and `api_usage`. Use Drizzle CLI for migrations.

### C. Payments & Billing
*   **The Gap:** SaaS boilerplates come with subscription management.
*   **The Addition:** **Stripe** + **Stripe Webhooks**.
*   **Implementation:** Create API routes (`/api/webhooks/stripe`) to listen for `invoice.paid` and `customer.subscription.updated` to update the user's status in our Postgres DB.

---

## 3. The AI-Native Integrations (The Differentiator)
This is where we *surpass* standard boilerplates by making the stack fundamentally AI-native from day one.

### A. AI-Assisted Content Authoring
*   **Integration:** **Sanity AI Assist**.
*   **Functionality:** Install the native Sanity AI plugin. This allows marketing teams to use AI directly inside the CMS to generate blog outlines, translate content, auto-tag resources, and generate SEO metadata without leaving Sanity Studio.

### B. Vercel AI SDK & Edge Streaming
*   **Integration:** **Vercel AI SDK** (`ai` package).
*   **Functionality:** The nervous system for AI on the site. Used to build streaming UI components (Generative UI) rather than just returning blocks of text. Allows the marketing site to feature interactive AI widgets (e.g., "Ask our documentation" or dynamic pricing calculators).

### C. Semantic Search & RAG (Vector DB)
*   **Integration:** **Pinecone** (Serverless Vector DB) + **OpenAI Embeddings**.
*   **Functionality:** Traditional search is keyword-based. We will vectorize all Sanity content (Docs, Resource Center) upon publish via a Sanity Webhook. When users search, they are doing a semantic vector search, allowing the AI to synthesize an answer instantly.

### D. AI Observability & Cost Control
*   **Integration:** **Vercel AI Gateway**.
*   **Functionality:** Routes all LLM requests through a proxy to track token usage per user/tenant, implement caching (saving money on repeated queries), and enforce rate limiting.

---

## 4. B2B SaaS Marketing Content Architecture
To build a complete enterprise marketing footprint, we must architect the following schemas in Sanity and map them to dynamic Next.js routes:

### A. The Core Pages (Dynamic Page Builder)
*   **Sanity Schema:** Create a modular `page` document type with an array of `pageBuilder` blocks (Hero, Feature Highlight, Testimonials, Pricing Grid, FAQ).
*   **Next.js Route:** `app/[slug]/page.tsx`
*   **AI Feature:** Connect the Pricing Grid block to the AI SDK to allow users to dynamically calculate their ROI or custom enterprise pricing via chat.

### B. The Resource Center (Hub & Spoke)
*   **Sanity Schema:** `post`, `author`, `category`, `whitepaper`, `caseStudy`. 
*   **Next.js Route:** `app/resources/[category]/[slug]/page.tsx`
*   **AI Feature:** Auto-generate "TL;DR Summaries" and audio-readings of case studies using Sanity AI Assist and Text-to-Speech APIs. Vectorize all posts for semantic search discovery.

### C. The Documentation (Docs as Code + CMS)
*   **Sanity Schema:** `docArticle`, `docCategory`. (Alternatively, if docs are highly technical, use MDX with **Fumadocs** integrated alongside Sanity).
*   **Next.js Route:** `app/docs/[...slug]/page.tsx`
*   **AI Feature:** An "Ask the Docs" floating action button. Uses the Vercel AI SDK and Pinecone to perform RAG over the documentation schema, answering developer/user questions instantly with cited sources.
