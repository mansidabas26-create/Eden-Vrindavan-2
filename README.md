# Eden Vrindavan

Cinematic, premium website for Eden Vrindavan. Built with Next.js 16 (App
Router), TypeScript, Tailwind CSS v4, and (installed, not yet wired) GSAP,
Lenis, Three.js / React Three Fiber.

## Status: Phase 2 complete (static homepage)

Per `CLAUDE.md`'s phased development process:

- ✅ Phase 1 — Repository inspection + implementation plan (approved)
- ✅ Phase 2 — Static homepage, all sections, responsive, forms functional
- ⏳ Phase 3 — GSAP/ScrollTrigger cinematic choreography (Temple → Window → Clouds → Road → Building)
- ⏳ Phase 4 — Gate / walkthrough enhancement
- ⏳ Phase 5 — Amenities cinematic scroll motion
- ✅ Phase 6 — Enquiry form (functional, not yet wired to a real backend)
- ✅ Phase 7 — `/residences` overview
- ✅ Phase 8 — Floor selector / floor plans (illustrative placeholder data)
- ✅ Phase 9 — SEO (metadata, sitemap, robots, canonical URLs)
- ⏳ Phase 10 — Performance/accessibility audit pass
- ⏳ Phase 11 — Final polish

## Getting started

```bash
npm install
npm run dev      # http://localhost:3000
npm run build    # production build
npm run start    # serve the production build
npm run lint
```

## Replacing temporary assets

Everything temporary is isolated so it can be swapped without touching
component code:

| What | Where | How to replace |
|---|---|---|
| Amenity photography (6 spaces) | `public/images/amenities/*.jpg` + `lib/constants.ts` → `AMENITIES` | Drop in new images at the same paths (or update the `image` field), keep `alt` accurate, and remove `isPlaceholder: true` once real. |
| Lobby / interior photo | `public/images/interior/lobby.jpg` + `lib/constants.ts` → `EXPERIENCE_ASSETS.lobby` | Same as above. |
| Floor plans & unit facts | `lib/residences.ts` | Replace `outline` SVG coordinates with real geometry and the placeholder facts (`[UNIT CONFIGURATION]`, `[AREA TO BE CONFIRMED]`, etc.) with confirmed data. |
| Property facts (description, distances, possession date, etc.) | `lib/constants.ts` → `PLACEHOLDER`, and inline placeholders in `app/location/page.tsx` | Replace only with client-confirmed facts — never invent numbers (CLAUDE.md §26). |
| Enquiry form submission | `components/enquiry/EnquiryForm.tsx` | Currently logs to console and shows a success state. Wire `onSubmit` to a real API route / CRM / email service. |
| 3D model or walkthrough video | `public/models/`, `public/videos/` | Currently empty. If supplied, `components/experience/GateEntry.tsx` and a new `Walkthrough.tsx` are the intended upgrade points (see CLAUDE.md §23–24). |

All amenity and lobby imagery currently in the repo is **original abstract/
architectural artwork** generated for this build — not stock photography,
and never presented as real photographs of Eden Vrindavan. Every instance
carries `isPlaceholder: true` in code and a visible "illustrative" caption
in the UI.

## Architecture notes

- Two-layer separation (CLAUDE.md §10): every cinematic `components/experience/*`
  section renders real semantic HTML (`h1`/`h2`/`p`) alongside its visuals —
  nothing SEO-relevant lives only inside a canvas/WebGL context. No WebGL is
  in use yet in Phase 2.
- `lib/constants.ts` is the single source of truth for site copy, nav links,
  the Sanskrit shloka, and the amenities data structure.
- `lib/residences.ts` holds the illustrative floor/unit placeholder data —
  clearly marked as non-final throughout the UI.
