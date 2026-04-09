---
name: fullstack-expertise
description: InfiGroup full-stack reference — Figma-to-code, base_system architecture, design tokens, animation, responsive design, backend patterns. Use when building UI components, translating Figma designs, or working on InfiGroup Next.js projects.
argument-hint: "[frontend | backend | figma | all]"
---

# Full-Stack Web Dev Expertise — InfiGroup Stack

## Role: Expert Full-Stack Web Developer

Operate as a senior full-stack developer who:
- Translates Figma designs to pixel-perfect code with deep understanding of design intent
- Thinks in design tokens, not raw values
- Writes responsive, accessible, performant components by default
- Understands the full pipeline: Figma → tokens → Tailwind → React → production
- Builds robust backend systems: APIs, databases, auth, caching, background jobs
- Knows when to use Server Actions vs API routes vs tRPC
- Implements security at every boundary: validation, auth, rate limiting, CSRF

## Stack Mastery: InfiGroup base_system

### Architecture
- Next.js 16 App Router, TypeScript strict, Tailwind CSS, Shadcn UI
- Modular `src/lib/` system: core (required), auth/database/email/monitoring (opt-in, delete to remove)
- Feature-based organization: `src/features/<feature>/components/` and `sections/`
- Shared UI: `src/components/layout/`, `common/`, `ui/`
- API routes use `withApi` pipeline (auto CSRF, rate limiting, Zod validation, error handling)
- i18n via next-intl with `[locale]` routing
- Env: Zod-validated via `@t3-oss/env-nextjs`, zero required for build, graceful degradation

### Design Token System (CSS Variables → Tailwind)
All projects define tokens in `globals.css` `:root`, mapped to Tailwind `extend`:

```
Colors: --primary-50 to --primary-950, --accent-*, --color-header/body/tag/nav
Typography: --text-h1-size/height through h6, --body-lg/md/sm, --caption, --tag
Spacing: --padding-x-relaxed (40→56→80px), --padding-x-tight, --padding-y-hero/navbar/footer
Layout: --grid-columns, --grid-gutter, --grid-margin (responsive per breakpoint)
Radius: calc-based hierarchy from --radius base (2.5rem)
Fonts: --font-heading (Oswald), --font-body (Poppins), --font-gilroy
```

Mobile-first: defaults in `:root`, overrides at `768px`, `1024px`, `1920px`.

### Component Conventions
- One component per file, PascalCase, props interface above component
- Max 200 lines per component, 800 max per file
- `cn()` from `@/lib/utils` for class merging (clsx + tailwind-merge)
- Never inline styles, never `any`, never manual class concatenation
- Server components by default, `'use client'` only when interactivity needed
- Shadcn UI as foundation, extend via wrapper pattern (never modify base files)

## Figma-to-Code Translation

### Auto-Layout → CSS Mapping
| Figma | CSS |
|-------|-----|
| Vertical direction | `flex-direction: column` |
| Horizontal direction | `flex-direction: row` |
| Gap | `gap` |
| Padding | `padding` |
| Primary axis alignment | `justify-content` |
| Cross axis alignment | `align-items` |
| Fill container | `flex: 1` / `width: 100%` |
| Hug contents | `width: fit-content` |
| Fixed size | explicit `width`/`height` |
| Wrap | `flex-wrap: wrap` |
| Space between | `justify-content: space-between` |

### Reading Designs Accurately
- Spacing follows 4px grid increments — convert px to rem (16px base)
- Don't blindly copy line-height percentages; inspect each text style
- Extract colors as semantic tokens, not raw hex
- Figma "auto" line-height has no CSS equivalent — derive from context
- Check all responsive variants (mobile/tablet/desktop frames)
- Note fill/hug/fixed sizing intent for each element

### Common Mistakes to Avoid
1. Ignoring responsive variants in Figma
2. Using px everywhere instead of rem
3. Hardcoding colors instead of semantic tokens
4. Missing vertical rhythm / baseline grid
5. Not recognizing auto-layout constraints (fill vs hug vs fixed)

## Design System Patterns

### Three-Layer Token Architecture
```
Primitives (raw):    --color-blue-500, --spacing-4
Semantic (intent):   --color-primary, --color-surface, --spacing-component-gap
Component (scoped):  --button-bg, --card-padding
```
Components reference semantic, semantic references primitives. Dark mode swaps semantic values.

### CVA (Class-Variance-Authority) for Variants
```tsx
const buttonVariants = cva("base-classes", {
  variants: { variant: {...}, size: {...} },
  compoundVariants: [...],
  defaultVariants: {...}
});
```

## Animation Patterns (InfiGroup)

### Decision Framework
- **CSS**: hover/focus states, simple fades, transform/opacity transitions
- **Intersection Observer**: scroll-triggered reveals (ShipX/Fyn preferred — lightweight, accessible)
- **Framer Motion**: state-driven, exit animations, drag/gesture, scroll-linked parallax, staggered children
- **Canvas**: organic effects (Portfolio wavy background with simplex noise)
- **Tailwind keyframes**: simple named animations with stagger variants (Astro)

Always include `prefers-reduced-motion` support.

## Responsive Design Approaches (InfiGroup)

1. **CSS Variable Breakpoints** (ShipX/Fyn — standard) — tokens change at breakpoints
2. **Tailwind Breakpoint Classes** (Astro — standard) — `grid-cols-1 md:grid-cols-2 lg:grid-cols-3`
3. **Viewport-Relative Units** (Portfolio — artistic) — `lg:text-[2vw] md:text-[4vw]`
4. **Container Queries** (modern) — `@container` + `@sm:`, `@md:`, `@lg:` in Tailwind v4
5. **Fluid Typography** — `clamp(1rem, 0.5rem + 1.5vw, 2rem)`

## Section Layout Pattern (Standard)
```tsx
<section className="w-full py-16 px-6 lg:px-margin">
  <div className="max-w-[1248px] mx-auto flex flex-col gap-8 items-center">
    {/* Badge + Title */}
    {/* Content grid/flex */}
  </div>
</section>
```

---

## Backend Expertise

### InfiGroup Backend Projects
| Project | Backend Pattern | Database | Key Features |
|---------|----------------|----------|-------------|
| base_system | withApi pipeline, modular modules | Drizzle ORM + PostgreSQL | CSRF, rate limiting, Zod, BaseRepository |
| DatabaseToolkit-v2 | Next.js API routes + Claude AI | Metabase API (no direct SQL) | Upstash Redis cache, AI analysis pipeline |
| hs-code-api | Vercel serverless functions | None | Multipart uploads, Sharp image processing, Claude classification |
| shipx-next | Payload CMS v3 | PostgreSQL (Payload adapter) | S3 storage, Google OAuth, Lexical rich text |

### API Response Envelope (Universal)
```typescript
interface ApiResponse<T = null> {
  success: boolean;
  data: T;
  error: string | null;
  meta?: PaginationMeta;
}
```

### withApi Pipeline (base_system standard)
```typescript
export const POST = withApi(
  { schema: zodSchema, rateLimit: 'contact', csrf: true, auth: false },
  async ({ data, request, user }) => {
    return successResponse(result);
  },
);
// Auto: CSRF → Rate Limit → Auth → Zod Validation → Handler → Error Handling
```
Rate limit presets: `contact` (5/min), `api` (60/min), `auth` (10/5min), `strict` (3/min).

### Server Actions vs API Routes vs tRPC
| Use Case | Pattern |
|----------|---------| 
| Form mutations (create/update/delete) | Server Actions |
| Public APIs, webhooks, external integrations | REST Route Handlers |
| Complex internal APIs, type-safe client-server | tRPC |
| Data fetching (reads) | Server Components (direct) |

### Database Patterns (Drizzle ORM)
- BaseRepository pattern: `findAll()`, `create()`, `delete()` — extend for custom queries
- Identity columns over serial for PKs: `generatedAlwaysAsIdentity()`
- Relational queries prevent N+1: `db.query.users.findMany({ with: { posts: true } })`
- Connection pooling: use Supabase pgBouncer (transaction mode, disable prepared statements)

### Caching Strategy
- **Next.js `use cache`**: Pair with `cacheTag()` + `revalidateTag()`
- **Upstash Redis**: Rate limiting, session storage, expensive computation cache
- **Rule**: Every mutation MUST be paired with cache invalidation

### Authentication Patterns
- **Supabase Auth + RLS**: Row Level Security mandatory — tables without it are publicly accessible
- **Payload Auth**: Built-in auth collection with Google OAuth flow
- **Always**: Verify auth inside Server Actions and Route Handlers, not just middleware

### Email Architecture (Resend)
| Type | Pattern |
|------|---------| 
| User-triggered (contact form) | Server Action → background job → Resend |
| System-triggered (Stripe webhook) | Route Handler → background job → Resend |
| Templates | React Email components (XSS-safe by default) |

### Observability Stack
| Layer | Tool |
|-------|------|
| Error tracking | Sentry (errors + performance + structured logs) |
| Application logging | Pino (structured JSON) |
| Infrastructure | Vercel Logs (zero-config) |

### 2026 Production Stack Reference
| Layer | Tool |
|-------|------|
| Framework | Next.js 16 (App Router) |
| ORM | Drizzle ORM |
| Database | PostgreSQL (Supabase) |
| Auth | Supabase Auth or Auth.js v5 |
| Internal API | tRPC (type-safe) |
| External API | REST Route Handlers |
| Background jobs | Inngest |
| Caching | `use cache` + Upstash Redis |
| Rate limiting | Upstash @upstash/ratelimit |
| File uploads | Vercel Blob |
| Email | Resend + React Email |
| Realtime | Supabase Realtime |
| Monitoring | Sentry + Pino |
| Deployment | Vercel + Turborepo |
| Validation | Zod (Standard Schema v1) |
