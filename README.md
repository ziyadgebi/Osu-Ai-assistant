# OSU AI Assistant

Production-grade foundation for the official AI assistant of **Oromia State University** (https://osu.edu.et).

Answers must come **only** from official university knowledge (website, PDF/Word/Excel documents, research, policies, news, media). No hallucinations, always cited, and an explicit "no official information" response when nothing is retrievable.

## Stack

- React 19 + TypeScript (strict, no `any`)
- TanStack Start / TanStack Router (file-based routing) + TanStack Query
- Tailwind CSS v4 design tokens + shadcn/ui primitives
- Planned backend: Lovable Cloud (PostgreSQL, pgvector, storage, auth, realtime, edge functions)

> Routing note: this stack uses TanStack Router, not `react-router-dom`. Route files live in `src/routes/` and the URL is derived from the filename.

## Structure

```
src/
  assets/            static imagery
  components/
    common/          brand, theme toggle, language switcher, placeholders
    layout/          navbar, footer, container
    ui/              design-system primitives (shadcn + custom)
  config/            app.config.ts, env.ts, navigation.config.ts
  features/
    admin/ ai/ analytics/ auth/ chat/ documents/
    i18n/ knowledge-base/ voice/ website-sync/
      components/ hooks/ services/ types/ providers/
  hooks/             cross-feature hooks (use-theme, use-translation, use-auth)
  layouts/           public-layout, admin-layout
  lib/               logger, validation, rate-limiter, utils
  providers/         theme, i18n, auth, app-providers
  routes/            file-based routes (pages + server routes)
  types/             common.types, domain.types, i18n.types
  styles.css         the design system (all colors/gradients/shadows)
```

## Pages

`/` `/chat` `/login` `/profile` `/offline` `/sitemap.xml`
`/admin` `/admin/analytics` `/admin/knowledge-base` `/admin/documents` `/admin/training` `/admin/website-sync` `/admin/ai-providers` `/admin/conversations` `/admin/users` `/admin/settings`
Unmatched URLs render the 404 route in `src/routes/__root.tsx`.

## Services (placeholders returning `NOT_IMPLEMENTED`)

`AIService` · `DocumentService` · `KnowledgeService` · `WebsiteService` · `ConversationService` · `AdminService` · `AuthService` · `AnalyticsService` · `LanguageService` · `VoiceService`

Every service returns the typed `Result<T>` union — expected failures are values, not exceptions.

## AI providers

One interface (`AIProvider`: `chat` / `embed` / `translate` / `speech`) implemented by Gemini, Addis AI, OpenRouter, Ollama, OpenAI, Claude and DeepSeek. See `src/features/ai/`.

## Environment

Browser values use `VITE_` prefixes (`VITE_SUPABASE_URL`, `VITE_SUPABASE_PUBLISHABLE_KEY`). Server secrets — `OPENROUTER_API_KEY`, `GOOGLE_API_KEY`, `ADDIS_AI_KEY`, `OLLAMA_URL`, `VECTOR_DATABASE`, `SUPABASE_SERVICE_ROLE_KEY` — are stored as backend secrets and read inside server handlers. Never hardcoded.

## Docs

- [Architecture](./docs/ARCHITECTURE.md)
- [Coding standards](./docs/CODING_STANDARDS.md)
- [Roadmap](./docs/ROADMAP.md)
