# Website-Relaunch — Master-Rezept (Next.js + Vercel + Sanity)

> Wiederverwendbarer Prompt für Claude Code. Basis: SK-Styling-Relaunch
> (Mai/Juni 2026). Startpunkt ist immer das Starter-Repo
> `code-K/codek-ai-coding-starter-kit` (Next.js 16 App Router, TypeScript,
> Tailwind, shadcn/ui vorinstalliert).
>
> Verwendung: Platzhalter `<…>` ersetzen und als erste Nachricht an Claude
> schicken — oder den interaktiven Frage-Flow über den Slash-Command
> `/relaunch-init` nutzen (siehe `.claude/commands/relaunch-init.md`).

---

## Prompt zum Kopieren

```
Wir relaunchen die Bestandswebsite <ORIGINAL_URL> als modernen Prototyp,
den ich als Pitch zur Kundengewinnung nutze. Projektname: <PROJEKT>.
Branche/Kategorie: <BRANCHE>.

FESTER TECH-STACK (nicht verhandelbar):
- Next.js (App Router) + TypeScript + Tailwind + shadcn/ui (Starter-Repo)
- Sanity als Voll-CMS, Studio embedded unter /studio
- next-sanity + GROQ + ISR (revalidate), Bild-Pipeline über Sanity-CDN
- next-themes für Dark/Light-Switch (sofern nicht abgewählt)
- Vercel (Region fra1) mit GitHub-Preview-Integration
- Resend für transaktionale Mails (wenn das Projekt Mails braucht)
- Stripe Checkout für Zahlungen (typisch Phase 2)

CONTENT-REGEL (wichtigste Regel überhaupt):
Alle Inhalte werden zunächst 1:1 von der Bestandswebsite übernommen —
Texte wortgleich, Leistungen/Preise exakt, Öffnungszeiten/Kontaktdaten
exakt, Tonalität und Slogans unverändert. KEINE Marketing-Umformulierung,
KEINE erfundenen Inhalte. Wo Inhalte fehlen (z. B. Bilder), kuratierte
Stock-Platzhalter mit deutlichem "// STOCK — durch echte Inhalte
ersetzen"-Marker im Code und sichtbarem Hinweis auf der Demo-Seite.
Umformulierungen sind Phase 2 nach Kundenfreigabe.

================================================================
STAGE 1 — IST-STAND-AUDIT der Bestandswebsite
================================================================
Analysiere <ORIGINAL_URL> und ALLE erreichbaren Unterseiten. Wenn die
Sandbox die Domain blockt (403 / host_not_allowed): versuche Aggregatoren
(Branchenverzeichnisse, Mapcarta, GelbeSeiten), Google-Snippets, Wayback —
und wenn das auch scheitert, bitte mich explizit um Screenshots und
Bild-URLs (das funktioniert zuverlässig, Screenshots kann ich posten).

Extrahiere vollständig:
- Firmendaten: Name, Inhaber:in, Adresse (Stadtteil über 2+ Quellen
  verifizieren!), Telefon, E-Mail, USt-Hinweise
- Öffnungszeiten / Erreichbarkeit / Notdienst-Zeiten
- Alle Leistungen mit Preisen, Beschreibungen, Kategorien
- Team, Über-uns-Texte (wortgleich sichern), Partner/Marken-Logos
- Bilder (URLs notieren; Download oft geblockt → als externe URLs
  einbinden + TODO für lokales Mirroring/CMS-Upload)
- Anfahrt/Lage-Infos (ÖPNV, Parken, Autobahn)
- Bestehende Buchungs-/Kontakt-Kanäle (prüfen ob noch aktiv!)

Erstelle danach docs/AUDIT.md mit Ist-Stand-Bewertung je Dimension
(Schulnote + 2-3 Belege):
1. SEO (Meta, Headings-Hierarchie, Sitemap, strukturierte Daten, Indexierung)
2. AEO / Answer-Engine-Optimierung (Schema.org-Abdeckung, FAQ-tauglicher
   Content, semantisches HTML, maschinenlesbare Fakten wie Öffnungszeiten)
3. Accessibility (Kontraste, Alt-Texte, Tastatur-Bedienung, ARIA,
   Touch-Target-Größen, Skip-Links)
4. Mobile (Responsive? Viewport? Tap-to-Call? Lesbarkeit?)
5. Performance (geschätzter Lighthouse-Score, Bildgrößen, Render-Blocking)
6. UI/UX (Informationsarchitektur, CTA-Führung, Bildsprache, Design-Alter)
7. DSGVO/Recht (Impressum, Datenschutz, Cookies, Drittanbieter-Embeds)
8. Tech & Pflegbarkeit (CMS vorhanden? Wer kann Inhalte ändern?)
9. Conversion/Leads (Wie kommt heute eine Anfrage zustande? Hürden?)

================================================================
STAGE 2 — SOLL-STAND: PRD + Feature-Specs
================================================================
- docs/PRD.md: Vision, 3 Zielgruppen, Soll-Stand je Audit-Dimension als
  messbares Ziel (z. B. "Lighthouse Mobile >= 95 alle Kategorien",
  "Inhaberin ändert Preise in < 5 Min ohne Entwickler"), Constraints
  (Free-Tier: Vercel Hobby + Sanity Free + Resend Free), Non-Goals,
  Phase-2-Backlog explizit getrennt (gegen Scope-Creep im Pitch).
- features/INDEX.md mit PROJ-IDs, Status-Tracking, Build-Reihenfolge.
- Pro Feature features/PROJ-N-<slug>.md: User Stories (DE), Acceptance
  Criteria, Edge Cases, Tech-Notes.
- Frage mich VOR Stage 2 per AskUserQuestion nach den offenen
  Architektur-Entscheidungen (siehe Frage-Flow unten), falls noch nicht
  beantwortet.

================================================================
STAGE 3 — BUILD (feature-für-feature, Commit je Etappe)
================================================================
Standard-Reihenfolge (anpassen wo nötig):

1. DESIGN SYSTEM & FOUNDATION
   - Brand-Tokens als CSS-Variablen (HSL) in globals.css + tailwind.config:
     Farbwelt passend zur Branche UND in Anlehnung an die Bestandsmarke
     (Wiedererkennung!). Light + Dark Palette.
   - Typografie: Display-Font (Serif für Premium/Beauty, Grotesk für
     Technik/Handwerk) + Body-Sans via next/font/google.
   - Logo als React-SVG-Komponente. Tipp: typografische Lösung
     (Display-Font + negatives Tracking als Ligatur-Effekt) schlägt
     meist ein gezeichnetes Strichgerüst. tone-Prop ("light"/"auto")
     für transparente Header. Dazu src/app/icon.svg als Favicon.
   - Header: scroll-aware (transparent über Hero, solid + backdrop-blur
     nach ~80px UND auf Unterseiten via usePathname), Skip-Link,
     Theme-Toggle, Mobile-Sheet-Burger. Breakpoint für Desktop-Nav
     ab 5+ Links auf lg statt md legen.
   - Footer: Marke + Kontakt + Nav + Öffnungszeiten + Legal-Links.
   - Section-Wrapper-Komponente (id, eyebrow, headline), Smooth-Scroll
     + scroll-padding-top passend zur Header-Höhe, prefers-reduced-motion.
   - WICHTIG: Route-Group (site) für alle Website-Routen mit eigenem
     Layout (Header/Footer/ThemeProvider/Toaster). Root-Layout minimal
     halten — sonst ragt der Site-Header ins Sanity Studio.

2. SANITY CMS
   - Schemas je nach Content-Modell (siteSettings + openingHours als
     Singletons, dazu Listen-Typen). Structure-Builder mit sinnvollen
     Gruppen. visionTool dazu.
   - Embedded Studio: src/app/studio/[[...tool]]/page.tsx mit
     "use client" + export const dynamic = "force-dynamic".
   - Server-Client (server-only + Write-Token) getrennt vom Public-Client.
   - Seed-Daten als sanity-seed.ndjson mit ALLEN 1:1 übernommenen
     Inhalten. Import-Befehl dokumentieren:
     npx sanity dataset import sanity-seed.ndjson production --replace
   - Jede Frontend-Sektion bekommt Fallback-Daten, damit die Site auch
     OHNE CMS-Verbindung vollständig rendert (Demo-Sicherheit!).
   - .env.local.example mit allen Variablen, .env.local nie committen.

3. SEKTIONEN (Hero → Kern-Sektionen → Kontakt)
   - Hero: vollflächig, Doppel-Overlay für Textkontrast (horizontal +
     vertikal), text-balance auf der Headline, H1 max text-6xl,
     Sticky-Mobile-Call-Bar via IntersectionObserver auf #hero.
   - Branchen-Kern-Feature (siehe Adaptionen unten).
   - Kontakt: Öffnungszeiten-Tabelle mit "Heute geöffnet"-Indikator
     (Europe/Berlin via Intl), Anfahrt-Block (ÖPNV/Auto/Parken aus dem
     Original), OpenStreetMap-iframe statt Google Maps (kein Tracking).
     Karten-Koordinaten am Screenshot verifizieren lassen — Geocoding
     einzelner Quellen ist oft hunderte Meter daneben.
   - tel:-Links exakt prüfen (Ziffer für Ziffer gegen Original).

4. SEO + AEO (cross-cutting, nach den Sektionen)
   - Metadata-API: title.template, description, metadataBase, OG.
   - JSON-LD: passender Schema.org-Typ (HairSalon, Electrician, ...) mit
     Adresse, geo, openingHoursSpecification, priceRange, sameAs,
     potentialAction (ReserveAction/ContactAction).
   - sitemap.ts + robots.ts (Studio disallow).
   - AEO konkret: semantische Heading-Hierarchie, Fakten maschinenlesbar
     (Öffnungszeiten als table, Preise als strukturierte Liste), optional
     FAQ-Sektion mit FAQPage-Schema, prägnante "Antwort-Sätze" am Anfang
     jeder Sektion (Answer-Engine-freundlich), llms.txt erwägen.
   - A11y: aria-labels, aria-expanded auf Burger, role=dialog für
     Lightboxen, Tastatur-Navigation, aria-current auf Heute-Zeile,
     sr-only-Captions, Kontrast >= 4.5:1.

5. RECHT
   - /impressum + /datenschutz als eigene Routen mit pt passend zur
     Header-Höhe. Mustertexte MIT sichtbarem TODO-Banner "vor
     Live-Schaltung anwaltlich prüfen". Datenschutz deckt jeden real
     genutzten Dienst ab (Vercel, Sanity, Resend, Stripe, Google Fonts).
   - Kein Cookie-Banner wenn kein Tracking — stattdessen Hinweis auf
     technisch notwendige Cookies/localStorage in der Erklärung.

6. DEPLOY
   - vercel.json: framework nextjs, regions ["fra1"], Security-Headers
     (X-Content-Type-Options, Referrer-Policy, X-Frame-Options
     SAMEORIGIN, Permissions-Policy), X-Robots-Tag noindex für /studio
     und Buchungs-/Token-Routen, Cache-Control no-store für
     personalisierte API-Responses.
   - GitHub-Integration: Production = main, Feature-Branch = Preview.
   - Env-Vars nur im Vercel-Dashboard. Sanity-CORS um Preview-Domain
     ergänzen (sonst kein Studio-Login auf der Preview).
   - Nach jedem grünen Feature: git commit + push (kleine, fokussierte
     Commits mit aussagekräftiger Message).

================================================================
STAGE 4 — PITCH-DECK (Marp)
================================================================
docs/pitch/<projekt>.md als Marp-Markdown (16:9, Brand-Farben):
Cover → Status Quo (Screenshot Original via thum.io oder lokal) →
1 Slide pro Audit-Pain-Point mit "Was wir liefern"-Card → Vision
(Preview-Screenshots Desktop + iPhone-Mockup) → Tech-Stack in
Laien-Sprache + "0 €/Monat laufende Kosten" → 3 Pakete
(Starter/Pro/Premium) → Nicht-enthalten-Transparenz → Roadmap →
CTA-Slide mit QR-Code zur Preview (qrcode-npm, SVG in Brand-Farben).
Export: npx @marp-team/marp-cli docs/pitch/<projekt>.md --pdf
--allow-local-files (bzw. --pptx).

================================================================
BRANCHEN-ADAPTIONEN (Kern-Feature wählen)
================================================================
- Salon/Beauty/Wellness/Gastro: eigenes Booking-System (Sanity-Bookings,
  Slot-Berechnung aus Öffnungszeiten minus Belegungen minus Sperrzeiten,
  Multi-Mitarbeiter, Bestätigungs-Mail + ICS-Attachment + ICS-Download,
  Token-Self-Cancellation, optional Stripe-Anzahlung mit Webhook,
  Drag&Drop-Kalender-Tool im Studio mit Inline-Edit)
- Handwerk (Elektro, Sanitär, Maler): Lead-/Angebots-Formular mit
  Leistungsauswahl + Foto-Upload, Notdienst-CTA prominent (Tap-to-Call
  über allem), Referenzprojekte-Galerie, Einsatzgebiet/PLZ-Sektion,
  optional Rückruf-Terminwahl
- Coach/Berater/Praxis: Terminbuchung (eigen oder Cal.com-Embed mit
  2-Klick-Consent), Newsletter (Resend Audiences), Testimonials
- Einzelhandel: Produkt-Schaufenster aus Sanity ohne Checkout
  ("Im Laden erhältlich"), Stripe-Shop als Phase 2
- Verein/NGO: Spenden (Stripe Payment Links), Termine/Events aus CMS

================================================================
PREIS-PAKETE (Default — je Branche kalibrieren)
================================================================
- Starter 400-600 €: Redesign + CMS + Hosting-Setup + Recht + SEO-Basis
- Pro 700-900 €: + 1-2 Kern-Features (Booking light / Lead-Form / Galerie)
- Premium 1000-1500 €: + Custom (Multi-Mitarbeiter, Stripe, Admin-Kalender,
  Automatisierungs-Mails)
- Laufend: 0 €/Monat Hosting+CMS (Free Tiers), Domain ~12-15 €/Jahr,
  optional Wartung 20-50 €/Monat

================================================================
QUALITÄTS-GATES (vor jedem Push)
================================================================
- node_modules/.bin/tsc --noEmit fehlerfrei
- node_modules/.bin/next build fehlerfrei (npm run build kann in der
  Sandbox an PATH scheitern — direkt das Binary nutzen)
- Lighthouse-Ziel >= 95 (alle 4 Kategorien) auf der Preview verifizieren
- Mobile-Viewport 390x844 ohne horizontales Scrollen
- Alle Anker-Links treffen existierende Sektionen (kein toter Nav-Link —
  Sektionen, die conditionally null rendern, brauchen Fallback-Content!)
- tel:/mailto: stichprobenartig gegen Originaldaten geprüft

Wenn beim Research etwas blockiert oder fehlt: transparent sagen und
2-3 Workarounds vorschlagen — niemals stillschweigend Inhalte erfinden.
```

---

## Lessons Learned aus SK Styling (fließen oben bereits ein)

| Problem | Lösung |
|---|---|
| Sandbox blockt Bestandsdomain komplett | User um Screenshots + Bild-URLs bitten — funktioniert zuverlässig |
| Site-Header ragte ins Sanity Studio | Route-Group `(site)` mit eigenem Layout; Root-Layout minimal |
| Geocoding-Marker ~600 m daneben | Koordinaten vom User am Karten-Screenshot verifizieren lassen |
| Toter Nav-Link auf leere News-Sektion | Jede Sektion braucht Fallback-Content statt `return null` |
| `npm run build` scheitert (PATH) | `node_modules/.bin/next build` direkt |
| Google-Fonts-TLS im Turbopack-Build | `experimental.turbopackUseSystemTlsCerts: true` |
| react-day-picker v10: Nav unsichtbar | `root: relative`, nav absolut am Root, nicht am Month |
| Tippfehler in tel:-Links | Ziffernweise gegen Original prüfen |
| Stadtteil falsch (Dahlem vs. Wilmersdorf) | PLZ/Stadtteil über 2+ Quellen verifizieren |
| 6+ Nav-Links zu eng bei md | Desktop-Nav-Breakpoint auf lg |
