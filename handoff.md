# 🚀 Handoff: AI-Enterprise-SaaS Turborepo

**Date:** 2026-09-02
**Context:** Handoff documentation for the free OSS AI Native Next.js starter repo.

This repository has been fully scaffolded, architecturally vetted by a skeptic review council, and pre-configured with agent-native rules. The baseline marketing and product vision have been codified.

---

## 📁 Critical Documents & Assets

All artifacts and research generated during this session have been migrated into this repository for future reference:

### 1. Architectural Remediation & Scaffolding
*   **[Agent-Native Scaffold](docs/competitors/agent_native_scaffold.md):** The original blueprint for making this repo readable by AI assistants.
*   **[Remediation Map](docs/handoff/remediation_map.md):** Mermaid diagrams illustrating the vertical agent restructuring and the decoupling of `packages/db` and `packages/auth` to prevent circular dependencies.
*   **[Install & Stack Guide](docs/competitors/install.md):** The Turborepo build sequence and final tech stack choices (Next 16, Drizzle, Better Auth, Sanity, pgvector).

### 2. Product Marketing & Landing Page
*   **[Product Marketing Context](.agents/product-marketing.md):** The canonical positioning document targeting indie hackers and agencies, mapping our free offering against $300+ premium boilerplates.
*   **[Landing Page Wireframe](docs/handoff/landing_page_wireframe.html):** A self-contained, single-page HTML/Tailwind prototype of the high-converting landing page.
*   **[AI-Native PVD](docs/competitors/ai_native_pvd.md):** The Product Vision Document outlining the bleeding-edge architecture (Generative UI, RAG via Pinecone/pgvector, AEO).

### 3. Competitor Research & Gap Analysis
*   **[Repo Analysis](docs/competitors/repo_analysis.md):** Reverse-engineering analysis of Supastarter and MakerKit.
*   **[Stack Gap Analysis](docs/competitors/ai_enterprise_stack_gap_analysis.md):** Gap analysis detailing how to bridge standard Sanity starters to Enterprise SaaS.
*   **Competitor Profiles:** Research on chiropractic marketing agencies (`docs/competitors/proactive-marketing.md`, `docs/competitors/chirocandy.md`, `docs/competitors/chirox-marketing.md`, `docs/competitors/chirobasix.md`).

---

## 🤖 The Agent-Native Setup

This repo is equipped with an `.agents/` directory that strictly enforces architectural boundaries to prevent LLM hallucinations:
*   **`teams.yaml`**: Defines 6 vertical agent roles (e.g., `Core_App_Engineer`, `Marketing_Growth_Engineer`).
*   **`skills/index.yaml`**: Defines the 6 core meta-skills required to operate the repo (`server-first-data`, `headless-content-modeling`, etc.).
*   **`agents.md`**: Global rules enforcing HIPAA compliance (no OpenRouter, use `pgvector`) and strict UI/DB package boundaries.

---

## 🛣️ Roadmap / Next Steps

1.  **Frontend Generation:** Convert `landing_page_wireframe.html` into React Server Components within `apps/marketing` using shadcn/ui.
2.  **Schema Configuration:** Scaffold the initial Drizzle schemas in `packages/db` (Users, Tenants, Subscriptions).
3.  **CMS Handoff:** Initialize the Sanity Studio in `apps/studio` and wire up the GROQ queries to `apps/marketing`.
