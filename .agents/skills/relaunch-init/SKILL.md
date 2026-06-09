---
name: relaunch-init
description: Initialize a website-relaunch project from an existing legacy site. Performs an IST-Stand audit, drafts PRD + feature specs, and locks in a fixed Next.js + Vercel + Sanity stack with content taken 1:1 from the source. Use at project kickoff when the goal is rebuilding an existing website.
argument-hint: [URL of the existing website to relaunch]
user-invocable: true
allowed-tools: Read, Write, Edit, Glob, Grep, Bash, WebFetch, WebSearch, AskUserQuestion
model: fable, opus
---

# Website Relaunch Initializer

## Role
You are a senior web consultant pitching a complete relaunch of an existing
legacy website. Your goal in this skill: turn the source URL into a fully
documented, ready-to-build relaunch project — audit, PRD, feature specs —
on a fixed tech stack, with content taken verbatim from the original.

## Hard Rules (do not negotiate these — only confirm in passing)

1. **Fixed stack**: Next.js (App Router) + TypeScript + Tailwind + shadcn/ui
   (from this Starter-Repo) + Sanity Voll-CMS (embedded Studio at `/studio`)
   + Vercel hosting (region `fra1`) + GitHub-based Preview deploys.
2. **Content is 1:1**: All copy, prices, opening hours, contact details and
   tonality are taken **verbatim** from the legacy site. No marketing
   rewrites, no invented facts, no fluff. Stock imagery is allowed only as
   clearly marked placeholders (`// STOCK — replace with real photo`).
   Editorial improvements are Phase 2 after the client signs off.
3. **Quality bar**: target Lighthouse ≥ 95 in all four categories,
   WCAG 2.1 AA, DSGVO-compliant, mobile-first.
4. **Reading order**: read `docs/RECIPE-Website-Relaunch.md` **first** if
   present — it is the binding playbook. This skill orchestrates the
   kickoff; the recipe carries the build details.

## Before Starting

1. Check if `docs/RECIPE-Website-Relaunch.md` exists and read it fully.
   If missing, fall back to the inlined playbook below.
2. Read `docs/PRD.md` and `features/INDEX.md` to detect an already-running
   project.

**If the PRD is still the empty template** → continue with the Init Flow
below (this is a fresh relaunch project).

**If the PRD is already filled out** → stop and tell the user:
> "This project already has a PRD. Use `/requirements` to add a single
> feature, or `/architecture` to design the next planned feature."

---

## INIT FLOW

### Phase 1 — Project Basics (AskUserQuestion, round 1)

Use a single `AskUserQuestion` call with these 4 questions:

1. **URL der Bestandswebsite?** — only ask if `$ARGUMENTS` is empty;
   otherwise just confirm the URL.
2. **Branche/Kategorie?** Options:
   - Salon / Beauty / Wellness / Gastro
   - Handwerk / Bau (Elektro, Sanitär, Maler, …)
   - Coach / Beratung / Praxis
   - Einzelhandel
   - (free text via Other)
3. **Seitenstruktur?** One-Pager (Recommended für lokale Betriebe) /
   Multi-Page / Decide after audit.
4. **Sprachen?** Nur Deutsch (Recommended) / DE + EN / Match original.

### Phase 2 — Features & Stack Details (AskUserQuestion, round 2)

Adapt the feature options to the industry from Phase 1.

5. **Branchen-Kern-Feature?** (multiSelect — adapt to industry):
   - Salon/Beauty/Gastro: Online-Booking-System, News/Aktionen,
     Galerie/Lookbook
   - Handwerk: Lead-/Angebots-Formular, Notdienst-CTA, Referenzprojekt-
     Galerie, Einsatzgebiet-Sektion
   - Coach/Beratung: Termin-Buchung, Newsletter, Testimonials
   - Einzelhandel: Produkt-Schaufenster (ohne Checkout), News/Aktionen
6. **Dark/Light-Mode-Switch?** Ja (Recommended) / Nur Light / Nur Dark.
7. **Transaktionale Mails via Resend?** Ja, sofort / Phase 2 /
   Nicht nötig.
8. **Online-Zahlungen via Stripe?** Phase 2 (Recommended) / Sofort /
   Nie.

### Phase 3 — Pitch & Pricing (AskUserQuestion, round 3)

9. **Pitch-Deck (Marp → PDF/PPTX) miterstellen?** Ja, mit Audit-Slides
   (Recommended) / Nur Prototyp.
10. **Preisrahmen für die Pakete?** 400–1200 € (Recommended Default
    Starter/Pro/Premium) / 600–2000 € / Eigene Angabe (Other).

### Phase 4 — IST-Stand Audit

Fetch the legacy URL and all reachable subpages. Strategy:

1. Try `WebFetch` on the main URL and obvious subpages
   (impressum, datenschutz, kontakt, leistungen/services, team, ueber-uns).
2. If sandboxed (HTTP 403 / `host_not_allowed`):
   - Try aggregators: Mapcarta, GelbeSeiten, branchenspezifische
     Verzeichnisse, Google snippets via `WebSearch`, Wayback Machine.
   - If everything fails: ask the user explicitly for screenshots and
     image URLs. **Screenshots from the user are the reliable Plan B.**
3. Extract verbatim and save in working notes:
   - Firmendaten (Name, Inhaber:in, Adresse — verify district via 2+
     sources!), Telefon, E-Mail, USt-Hinweise
   - Öffnungszeiten / Erreichbarkeit / Notdienst
   - Alle Leistungen mit Preisen, Beschreibungen, Kategorien
   - Team, Über-uns-Texte (wortgleich), Partner/Marken
   - Bilder (URLs notieren), Anfahrt/Lage (ÖPNV, Auto, Parken)
   - Bestehende Buchungs-/Kontakt-Kanäle (prüfen ob noch aktiv!)

Write `docs/AUDIT.md` with a Schulnote (1–6) + 2–3 evidence bullets per
dimension:

1. **SEO** — Meta, headings, sitemap, structured data, indexability
2. **AEO (Answer-Engine-Optimization)** — Schema.org coverage,
   FAQ-tauglicher Content, semantic HTML, machine-readable facts
   (hours/prices), llms.txt
3. **Accessibility** — contrast, alt text, keyboard nav, ARIA,
   touch targets, skip links
4. **Mobile** — responsive layout, viewport meta, tap-to-call,
   readability
5. **Performance** — estimated Lighthouse, image sizes, render-blocking
6. **UI/UX** — information architecture, CTA flow, imagery, design age
7. **DSGVO / Recht** — Impressum, Datenschutz, cookies, third-party
   embeds
8. **Tech & Pflegbarkeit** — CMS? who can change content?
9. **Conversion / Leads** — how does an inquiry happen today, what
   are the hurdles?

Add an **Auffälligkeiten**-block: critical issues (broken services,
dead links, GDPR violations).

### Phase 5 — SOLL-Stand: PRD + Feature Specs

Create `docs/PRD.md` covering:

- **Vision** (2–3 sentences)
- **Target Users** (3 personas)
- **Soll-Stand per dimension** as measurable goals
  (e.g. "Lighthouse Mobile ≥ 95", "Inhaberin ändert Preise in < 5 Min
  ohne Entwickler")
- **Core Features Roadmap** as P0/P1/P2 table
- **Success Metrics** (concrete, measurable)
- **Constraints** (Free-Tier: Vercel Hobby + Sanity Free + Resend Free)
- **Non-Goals** + **Phase 2 Backlog** (explicit, against scope creep)

Then split into individual features following Single Responsibility.
Typical P0 stack for every relaunch:

- PROJ-1 Design System & Foundation (Brand-Tokens, Logo, Header, Footer,
  Dark/Light, Route-Group `(site)`)
- PROJ-2 Sanity CMS Setup (Schemas, Studio, Seed NDJSON, Server-Client)
- PROJ-3 Hero & Sticky Mobile-Nav
- PROJ-4..N Industry sections (from Phase 1/2 answers)
- PROJ-N+1 SEO + AEO (JSON-LD, sitemap, robots, FAQ, llms.txt, A11y)
- PROJ-N+2 Impressum & Datenschutz (Anwalts-TODO sichtbar)
- PROJ-N+3 (optional) Pitch-Deck (Marp + QR + Screenshots via thum.io)

Create one feature spec per file in `features/PROJ-X-<slug>.md` using
the standard template (`requirements/template.md`). Update
`features/INDEX.md` with all features, statuses, dependencies, and
recommended build order. Update PRD roadmap table to match.

### Phase 6 — User Review & Approval Gate

Present the full plan and **stop** for explicit approval:

> "Audit, PRD und Feature-Specs liegen vor. Zusammenfassung:
> - Wichtigste Audit-Findings: …
> - Roadmap: PROJ-1 … PROJ-N
> - Phase 2 Backlog: …
> - Empfohlener Start: PROJ-1 (Design System)
>
> Soll ich mit dem Build (Stage 3 des Rezepts) starten, oder zuerst
> Änderungen einbauen?"

Do NOT start building until the user says "go" / "approved".

### Phase 7 — Handoff

After approval, hand off to `/architecture` for PROJ-1:

> "Project setup complete. Next step: `/architecture` to design the
> technical approach for PROJ-1 (Design System & Foundation)."

### Git Commit

```
feat: Initialize <projekt> relaunch — audit, PRD and feature specs

- IST-Stand-Audit in docs/AUDIT.md (9 Dimensionen)
- PRD with vision, target users, soll-stand metrics, constraints
- N feature specs (PROJ-1 … PROJ-N), Phase 2 Backlog explizit
- Content 1:1 von <ORIGINAL_URL> übernommen
```

---

## CRITICAL Don'ts

- **NEVER write production code in this skill** — handoff to
  `/architecture` → `/frontend` / `/backend`.
- **NEVER invent content** — if information is missing from the legacy
  site, mark it as TODO and ask the user, do not guess.
- **NEVER skip the approval gate** — even if the audit findings seem
  obvious. The user must explicitly approve the plan before build.
- **NEVER rewrite the original copy** in this phase. The 1:1 rule is
  the foundation of client trust during the pitch.

## Checklist Before Completion

- [ ] All Phase 1–3 questions answered (or confirmed from `$ARGUMENTS`)
- [ ] Legacy site analyzed; if blocked, screenshots requested and
      received from user
- [ ] `docs/AUDIT.md` written with 9 dimensions + Schulnoten + evidence
- [ ] All extracted content saved verbatim (no rewrites)
- [ ] `docs/PRD.md` filled (Vision, Users, Soll-Stand, Roadmap,
      Metrics, Constraints, Non-Goals, Phase 2 Backlog)
- [ ] Feature specs in `features/` cover all P0 work
- [ ] `features/INDEX.md` updated with statuses, dependencies, order
- [ ] User has explicitly approved before any build starts
- [ ] Git commit done with the message above
