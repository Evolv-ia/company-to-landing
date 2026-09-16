# Skill chain

This workflow gets better brand and design results by delegating each phase to a skill that specializes in it. Those skills were written for standalone use: most open with an interview. Here the research has already gathered the answers, so the job is to hand them the evidence and keep the user's interruptions to the two planned moments.

Skill names below are those found in a typical Claude Code setup. Check the available-skills list at runtime: names can carry plugin prefixes (`superpowers:brainstorming`, `frontend-design:frontend-design`) or be missing on other hosts. Load a skill when its phase starts, not all at once.

## Operating rules

- **Evidence mode.** Before invoking a skill, write the context file it reads (below) and include the relevant parts of `company.json`, `BRAND.md` drafts and Instagram signals in the request. State that discovery is done and that only gaps which would change the output should be raised. Collect those gaps for the creative checkpoint instead of asking immediately; in autonomous mode, resolve them as inference and mark them `inferred`.
- **One owner per phase.** Do not load two design-execution skills together (for example `impeccable` with `frontend-design` or `taste-design`). Their rules overlap and contradict, and the page ends up averaging them.
- **Condense.** Brand skills produce full strategist documents. For a landing, merge the essentials into `BRAND.md` and the content file. Produce standalone brand documents (`brand-guidelines`, `brand-manifesto`, a full `brand-strategy` report) only when the user asks.
- **Facts rule wins.** No sub-skill output may add testimonials, statistics, awards, client names or prices that are not approved claims in `company.json`. Creative copy stays labeled as creative.
- **Contain side effects.** Within this workflow, use `superpowers:brainstorming` for its approaches-and-recommendation discipline only; skip its design-doc commit and its hand-off to planning or worktree skills unless the user wants them. gstack skills run their own preambles; follow their rules, but do not let any skill commit, push or deploy unless the repository conventions and the user call for it.

## Phase map

| Phase (SKILL.md step) | Skill | When | Hand it | Result goes to |
|---|---|---|---|---|
| Brand foundation (2) | `brand-context` | Always | Write `.agents/brand-context.md` yourself from evidence (template below); invoking the skill is unnecessary once the file exists | Other brand skills read it automatically |
| Positioning (2) | `brand-positioning` | Always, kept light | Offerings, audience, differentiators, locations | `BRAND.md` positioning |
| Competitive scan (2) | `competitor-branding` | No established brand, rebrand, or a crowded local category | 3-5 sourced competitors from the same sector and area | `BRAND.md` differentiation; ideas for directions |
| Voice (2) | `brand-voice` | Always | Website copy plus Instagram caption voice | `BRAND.md` tone |
| Messaging (2) | `brand-messaging` | Always | Positioning and approved claims only | Content file: hero options, value props, CTA labels |
| Visual identity (2) | `brand-identity` | Always; documents an existing brand, proposes a new one | Website tokens, logo, Instagram imagery style and grid palette | `BRAND.md` visual sections |
| Rebrand (2) | `rebranding` | Only on explicit rebrand request | Existing brand evidence and the reason for change | Replaces identity and voice outputs |
| Creative checkpoint (3) | `superpowers:brainstorming` | Always; waits unless autonomous | `BRAND.md`, media shortlist, conversion goal | `creative-directions.md`, decision in `BRAND.md` |
| Design intelligence (3) | `ui-ux-pro-max` | No established brand, or to check UX rules for the product type | Product type, audience, style keywords | Candidate palettes, pairings, patterns |
| Visual mockups (3) | `design-shotgun` | Only when the user asks | Direction briefs | Mockup board for the choice |
| Build (4) | `impeccable` | Default | `PRODUCT.md` + `DESIGN.md` at the site root | The site |
| Build fallback (4) | `frontend-design` (or `taste-design`) | `impeccable` unavailable | `BRAND.md` and the chosen direction | The site |
| Design QA (5) | `impeccable` critique/audit/polish, or `design-review` | Always, after functional QA | Chosen direction and deployed/preview URL | Fixes and `QA.md` |
| Accessibility depth (5) | `design:accessibility-review` | Accessibility needs a dedicated audit | Preview URL | `QA.md` |

## Bridge files

Write these in the site project root, outside the served directory (`public/`, `dist/` or the framework's equivalent).

### `.agents/brand-context.md`

The brand skills check this path first. Use the structure `brand-context` expects, filled from evidence, with `unknown` rather than guesses:

```markdown
# Brand Context

## Brand
- **Name**:
- **Category**:
- **Description**:
- **Stage**:
- **Website**:
- **Instagram**: @handle (verified: how)

## Audience
- **Primary Audience**:
- **Key Problem**:
- **Their Language**:

## Positioning
- **Differentiation**:
- **Competitors**:
- **Market Position**:

## Brand Personality
- **Personality Words**:
- **Tone**:
- **Voice Admires**:

## Values & Mission
- **Core Values**:
- **Mission**:

## Goals
- **Primary Goal**: the landing's conversion goal
- **Key Metrics**:
```

### `PRODUCT.md`

`impeccable` requires it; without it, it runs its own `teach` interview. Sections, in order: `## Register` (`brand` — a landing is a brand surface), `## Users`, `## Product Purpose`, `## Brand Personality`, `## Anti-references` (include generic-template looks and any competitor style to avoid), `## Design Principles` (3-5, derived from the chosen direction), `## Accessibility & Inclusion`. Keep colors and fonts out of it; they belong in `DESIGN.md`.

### `DESIGN.md`

Follow the format in impeccable's `reference/document.md` (Stitch DESIGN.md: YAML token frontmatter, then Overview, Colors, Typography, Elevation, Components, Do's and Don'ts, in that order). Fill it from `BRAND.md` and the chosen direction and mark it `<!-- SEED -->` before any code exists. After the build, refresh it from the implemented styles (impeccable `document` in scan mode) so it matches the delivered site.

## Fallback rules when a skill is missing

Use these compact rules only for the missing phase, and note the fallback in `QA.md`.

- **Brand context and positioning:** one sentence — for [audience] who [need], [company] is the [category] that [differentiator], because [evidence]. Name the position (premium, value, niche, local specialist) and what the brand explicitly is not.
- **Voice:** 3-4 traits, each with a "sounds like / does not sound like" pair taken from real copy or captions; set person (tu/voi/noi), formality, emoji policy and sentence length.
- **Messaging:** one core message, three value propositions each tied to an approved claim, one primary and one secondary CTA label, objections the FAQ must answer.
- **Visual identity:** choose a color strategy first (restrained, committed, full palette, drenched), define semantic roles, check WCAG AA contrast, at most two type families with fallbacks, a fluid type scale, one radius and spacing rhythm, and an imagery rule grounded in the real photos.
- **Brainstorming:** 2-3 distinct directions with trade-offs and a recommendation, as described in SKILL.md step 3.
- **Build without a design skill:** avoid the template look — no default centered hero with three icon cards, no gratuitous gradients or glassmorphism, no stock-looking filler when real media exists; build hierarchy from type scale and layout, give the page one memorable signature element, and let the company's own photography carry the page.
- **Design QA without a skill:** check hierarchy at a glance, alignment and spacing consistency, contrast, tap target sizes, text length at mobile width, image crops, motion restraint, and whether the page still looks like this specific company with the logo hidden.
