# Website-Redesign-Pitch — Rezept

> Wiederverwendbarer Prompt für Claude. Kopiere ihn an den Anfang eines
> neuen Projekts, ersetze die Platzhalter `<…>` und passe die
> Branchen-Sektion an. Quellprojekt: SK Styling Redesign (Mai 2026).

---

## Prompt zum Kopieren

```
Ich möchte die Bestandswebsite <ORIGINAL_URL> komplett überarbeiten als
Pitch für den Kunden. Output am Ende:

1. Ein Pitch-Deck als Marp-Markdown unter docs/pitch/<projekt>.md, exportierbar zu PDF/PPTX.
2. Ein lauffähiger Prototyp auf einer Vercel-Preview-URL, den der Kunde live
   anschauen kann.

Stelle vor dem Loslegen folgende Fragen einmal nach (über AskUserQuestion,
Mehrfach-Auswahl wo sinnvoll), DANACH leg los:

- Original-Sprache der Site (DE/EN/beides)?
- One-Pager oder Multi-Page-Struktur?
- Branchenspezifisches Kern-Feature (Booking, Lead-Form, Galerie, Shop, …)?
- CMS-Bedarf: Voll-CMS (Sanity), Light-CMS (MDX) oder rein statisch?
- Dark/Light-Mode-Switch erwünscht?
- Online-Zahlungen geplant (jetzt / Phase 2 / nie)?

Tech-Stack-Default (anpassbar nach Antworten):
- Next.js 16 (App Router) + TypeScript + Tailwind + shadcn/ui
- Sanity CMS, embedded Studio unter /studio
- next-sanity + GROQ + ISR
- next-themes für Theme-Switch
- Vercel Hobby (Region fra1) + GitHub Preview-Integration
- Resend für transaktionale Mails (optional)
- Stripe Checkout für Zahlungen (Phase 2)

Vorgehensweise:

STAGE 1 — Research (eine Session)
- Bestandssite analysieren: per WebFetch oder curl. Wenn die Sandbox die Domain
  blockt (HTTP 403 oder host_not_allowed), versuche: Aggregator-Sites (Mapcarta,
  GelbeSeiten, branchenspezifische Verzeichnisse), Google-Search-Snippets,
  Wayback Machine. Wenn nichts klappt: User direkt nach Screenshots / Texten fragen.
- Extrahieren: Firmenname, Adresse, Telefon, E-Mail, Öffnungszeiten/Verfügbarkeit,
  Leistungen, Team, Bilder, Tonalität der Original-Texte.
- 4-6 Hauptprobleme identifizieren (UX, Mobile, Performance, A11y, GDPR, SEO, Tech, CMS).
- Geo-Koordinaten via Wikipedia/Mapcarta falls eine Karte benötigt wird.

STAGE 2 — Pitch-Deck (eine Session)
Marp-Markdown unter docs/pitch/<projekt>.md mit folgenden Slides:
1. Cover (Projekt-/Kundenname, Pitcher-Name, Datum)
2. Wer wir sind / unser Angebot (1 Slide)
3. Status Quo (Screenshot Original + 3-5 Bullet-Points zu Kernproblemen)
4. Tiefer-Slides pro Pain-Point: UX, Mobile, Performance/Lighthouse,
   Accessibility, GDPR, CMS-/Pflegbarkeits-Lücke, SEO
5. Vision (1-2 Slides mit Mockup-Screenshots vom Prototyp / Hero / Mobile-View)
6. Tech-Stack-Erklärung in Laien-Sprache (Next.js + Sanity + Vercel — warum)
7. Mehrwert für den Kunden (Mobile-First, selbst pflegbar, SEO-Boost,
   DSGVO-konform, automatisierte Kommunikation)
8. Paket-Übersicht als 3-Spalten-Tabelle (Starter/Pro/Premium mit Preisen,
   Inhalt, Lieferzeit)
9. Hosting & laufende Kosten (transparent: Vercel Hobby 0€, Sanity Free 0€,
   Resend Free 0€, Domain ~12€/Jahr, optional Wartung)
10. Nächste Schritte + Kontakt

Style: hell, professionell, ein klares Brand-Akzent. Schriften: Inter +
eine passende Serif (Fraunces für Premium, Source Serif für seriös).

STAGE 3 — PRD + Feature-Specs (eine Session)
- docs/PRD.md mit Vision, 3 Zielgruppen, Erfolgs-Metriken, Constraints, Non-Goals
- features/INDEX.md mit P0/P1-Features als PROJ-IDs
- Pro Feature features/PROJ-N-<slug>.md mit User Stories, Acceptance Criteria,
  Edge Cases, technischen Notes
- CHANGELOG.md-Eintrag pro abgeschlossenem Feature

STAGE 4 — Build (mehrere Sessions, feature für feature)
Typische Reihenfolge:
1. Design System (Brand-Tokens in Tailwind, Logo als SVG-Komponente,
   Dark/Light-Mode mit next-themes, Header (scroll-aware), Footer)
2. Sanity Setup (Schemas, embedded Studio, Seed-Daten als NDJSON)
3. Hero + Sticky-Mobile-Nav
4. Branchenspezifische Kern-Sektionen (siehe unten)
5. SEO (JSON-LD Schema.org, sitemap.ts, robots.ts, Metadata-API)
6. Impressum + Datenschutz (Mustertexte mit TODO-Marker für Rechtsanwalt-Review)
7. Optional Phase-2-Features (siehe Pakete)

STAGE 5 — Deploy
- vercel.json mit Region fra1, X-Frame-Options SAMEORIGIN, X-Content-Type-Options,
  Referrer-Policy, X-Robots-Tag noindex für /studio und /buchung
- GitHub-Integration: Production-Branch = main, Feature-Branches als Previews
- Env-Vars im Dashboard, NICHT committen: Sanity-IDs (public), Sanity-Write-Token,
  Resend-Key, Stripe-Keys, Site-URL

Branchenspezifische Adaptionen:

- Salon/Beauty/Wellness/Restaurant: Online-Booking-System (Sanity-basiert mit
  Slot-Berechnung + Stripe-Anzahlung optional)
- Handwerk (Elektriker, Maler, Sanitär): Lead-Anfrage-Formular mit
  Service-Auswahl + PLZ-Filter + Notdienst-CTA prominent + Referenz-Galerie
- Coach/Berater: Calendly-Embed oder eigenes Buchungssystem + Newsletter (Resend)
- Onlineshop: Shopify-Headless oder Stripe-Checkout, ansonsten Schaufenster ohne
  Kasse als Phase-1
- Verein/NGO: Spenden-Funktion (Stripe), Mitgliederbereich (Sanity Auth)

Preis-Pakete (kalibriere zur Branche, hier Default-Vorschlag):

- Starter (400-600 €): Redesign + Sanity CMS + Vercel-Hosting + Impressum/
  Datenschutz + SEO-Basis. Stock-Imagery erlaubt. Lieferzeit ~2-3 Wochen.
- Pro (700-900 €): Starter + 1-2 branchenspezifische Features (Booking
  light, Lead-Form, Gallerie mit Lightbox, Newsletter-Integration).
  Lieferzeit ~4-5 Wochen.
- Premium (1000-1500 €): Pro + Custom-Erweiterungen (Multi-Mitarbeiter-
  Kalender, Stripe-Zahlungen, eigenes Admin-Dashboard, automatisierte
  Erinnerungs-Mails/SMS). Lieferzeit ~6-8 Wochen.

Hosting + CMS laufen auf den kostenlosen Tarifen (Vercel Hobby + Sanity
Free), das reicht für kleine lokale Sites mit < 100k Page-Views/Monat.
Domain bringt der Kunde mit oder wird für ~12-15 €/Jahr neu registriert.

Optional als Recurring: Wartungs-Paket 20-50 €/Monat (Updates, kleine
Inhaltsänderungen, Monitoring, Backups).

Output-Standards:

- Deutsche Texte, sofern Original-Site nicht anderssprachig ist.
- Echte Kunden-Bilder als TODO markieren wenn Stock-Imagery verwendet wird.
- Lighthouse-Ziel >= 95 in allen vier Kategorien.
- Cookie-Banner NUR wenn Tracking aktiv ist; bei reinen CMS-Sites reicht
  ein "technisch notwendige Cookies"-Hinweis im Datenschutz.
- Impressum + Datenschutz IMMER mit "Vor Live-Schalten durch DSGVO-
  Anwalt prüfen"-Marker.
- Originaltöne der Bestandssite respektvoll übernehmen (Tonalität, Slogans),
  nicht durch generische Marketing-Floskeln ersetzen.
- Commits klein und fokussiert, jeder mit aussagekräftiger Message.

Wenn du beim Research auf Probleme stößt (Domain blockiert, fehlende Infos),
sage es transparent und schlage 2-3 Workarounds vor — nicht stillschweigend
weitermachen oder erfinden.
```

---

## Anleitung zur Verwendung

1. Neues Repo aus dem AI-Coding-Starter-Kit erstellen (gleicher Tech-Stack vorinstalliert).
2. Diesen Prompt-Block oben kopieren, `<ORIGINAL_URL>` und `<projekt>` ersetzen.
3. An Claude Code schicken — Claude führt durch die 5 Stages, fragt nach beim
   Branchen-Fokus und liefert am Ende eine Vercel-Preview-URL + Pitch-Slides.
4. Pitch-Slides exportieren: `npx @marp-team/marp-cli docs/pitch/<projekt>.md --pdf`
   bzw. `--pptx` für PowerPoint.

## Lessons Learned aus SK Styling

- **Sandbox blockt oft die Bestandssite** (z. B. via `host_not_allowed`).
  Plan-B: User bitten Screenshots zu posten — funktioniert zuverlässig.
- **Originalfotos** vom Bestand-Server als externe URLs einbinden funktioniert
  für die Preview, aber sollte für Production lokal nach `/public` gemirrort
  oder ins CMS hochgeladen werden.
- **Stadtteil-Recherche** über mehrere Quellen verifizieren — Wikipedia,
  PLZ-Mapping, lokale Branchenverzeichnisse. Eine einzelne Quelle reicht nicht.
- **Logo-Design** als typografische Lösung (CSS-Font + negative tracking)
  ist oft eleganter als ein SVG-Strichgerüst — und billiger zu iterieren.
- **Phase 2-Trennung** im PRD klar dokumentieren, damit der Kunde weiß was
  jetzt vs. später kommt. Verhindert Scope-Creep im Pitch-Termin.
