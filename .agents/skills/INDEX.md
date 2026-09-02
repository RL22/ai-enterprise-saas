# AI-Native Enterprise SaaS: Meta-Skills Index

This index acts as a router for the monorepo's core architectural meta-skills. Agents must read the relevant skill before executing structural changes, UI generation, or data modeling.

---

```yaml
name: monorepo-architect
description: >
  Boundary discipline and dependency routing. Use when scaffolding new features, deciding whether code belongs in an app or a shared package, or wiring cross-workspace imports.
```

```yaml
name: ai-native-ux
description: >
  Generative UI and streaming interfaces. Use when building chat interactions, dynamic widgets, conversational intake forms, or working with Vercel AI SDK and shadcn/ui.
```

```yaml
name: server-first-data
description: >
  Data mutations and backend execution. Use when implementing Next.js 16 Server Actions, interacting with Drizzle ORM, or performing secure server-edge operations. Prohibits client-side data fetching.
```

```yaml
name: headless-content-modeling
description: >
  Sanity CMS architecture and data fetching. Use when defining CMS schemas in the studio, writing GROQ queries, or building the marketing site's dynamic page builder.
```

```yaml
name: b2b-identity-and-billing
description: >
  Multi-tenancy and subscription management. Use when configuring Better Auth for organizations/RBAC, managing tenant context, or mapping Stripe webhooks to the Postgres database.
```

```yaml
name: generative-seo-and-docs
description: >
  Answer Engine Optimization (AEO) and RAG preparation. Use when writing Fumadocs MDX, configuring Schema.org markup, generating llms.txt, or pushing content into Pinecone for semantic search.
```
