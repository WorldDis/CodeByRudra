# GROWBOND Website Implementation Plan

## Context
Empty repository (only Jekyll .gitignore and .kilo/plans). Node/npm/git available. Plan mode only: plan file, no source edits.

## Goal
Production-ready Next.js + TypeScript + Tailwind site for GROWBOND (IT Services, Networking, CCTV, Hardware, Digital Services) at growbond.in, near ₹0 cost, with 13 pages, forms, SEO, security, accessibility.

## Architecture
- Next.js 14 App Router, TypeScript, Tailwind CSS, shadcn/ui-style reusable components.
- Route groups: (marketing) pages. Shared layout: Navbar, Footer, FloatingWhatsApp, Cookie/privacy banner.
- Forms: Next.js Server Actions with zod validation; email via Resend free tier (fallback: mailto link + WhatsApp). Optional Supabase (free tier) for enquiry storage; env-gated.
- No fake data, no fake login. Admin panel deferred to phase 2 with real auth.
- SEO: per-route metadata, OG image, sitemap.ts, robots.ts, JSON-LD LocalBusiness.
- Security headers via next.config.js; CSP; honeypot + rate limit on forms.
- 3D: optional R3F hero with static fallback + prefers-reduced-motion.

## Pages
Home, About, IT Support, Networking Solutions, CCTV Solutions, Hardware and Products, Digital Services, AMC Enquiry, Request a Quote, Contact, FAQ, Privacy Policy, Terms, plus custom 404.

## Implementation Steps
1. Scaffold: `npx create-next-app@latest` (TS, Tailwind, App Router, ESLint) into /workspace/app; clean default.
2. Configure tailwind theme (navy/cyan), fonts (Inter via next/font), globals.
3. Build reusable components: Button, Card, Input, Textarea, Select, Badge, Section, Container, Navbar, MobileMenu, Footer, FloatingWhatsApp, FormStatus.
4. Create route pages with content derived only from prompt (no invented credentials).
5. Implement forms (contact, quote, product enquiry, AMC) as Server Actions with zod; store to Supabase if env present else email/mailto fallback; show success/error.
6. Add SEO files, metadata, JSON-LD, favicon, og image (generated SVG/PNG).
7. Security: headers, honeypot, rate limit, env validation, .env.example.
8. Accessibility: semantic HTML, keyboard nav, reduced-motion, contrast.
9. README with Windows 11 setup, deploy steps, env vars, checklist, free-tier limits.
10. Run lint/typecheck/build; fix errors; document testing report.

## Env Vars (.env.example)
NEXT_PUBLIC_SITE_URL, RESEND_API_KEY, CONTACT_EMAIL, SUPABASE_URL, SUPABASE_ANON_KEY, WHATSAPP_NUMBER, NEXT_PUBLIC_GA_ID (optional).

## Free-tier Limits
Vercel hobby, Supabase free (500MB DB, pausing), Resend free (100 emails/day). Note domain DNS at GoDaddy preserved for Professional Email (MX/TXT) when adding Vercel A/CNAME.

## Risks
- No verified phone number given: use placeholder format clearly marked TODO in env, not hardcoded fake. Ask user for WhatsApp number before deploy.
- No real testimonials: omit.
- CSC authorization unverified: label "subject to authorization".

## Open Questions
1. WhatsApp number and primary contact email? (needed for CTAs)
2. Preferred hosting: Vercel (recommended) vs other?
3. Do you want Supabase persistence now or email-only MVP?

## Validation
- `npm run lint`, `npm run typecheck`, `npm run build`
- Manual: nav links, forms (success/error), mobile, reduced-motion, 404, sitemap.

## Out of Scope (phase 2)
Admin panel, CMS, payments, CSC authorization claims.
