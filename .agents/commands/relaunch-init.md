---
description: Startet ein Website-Relaunch-Projekt — Frage-Flow, Audit, PRD, Build-Plan (Next.js + Vercel + Sanity)
argument-hint: [URL der Bestandswebsite]
---

Du startest ein neues Website-Relaunch-Projekt auf Basis dieses Starter-Repos.
Das vollständige Vorgehen steht in `docs/RECIPE-Website-Relaunch.md` — lies
diese Datei JETZT zuerst vollständig, sie ist die verbindliche Arbeitsgrundlage.

Bestandswebsite (falls als Argument übergeben): $ARGUMENTS

## Schritt 1 — Frage-Flow (Pflicht, bevor irgendetwas gebaut wird)

Stelle mir per AskUserQuestion die folgenden Fragen. Bündele sie in
2-3 Aufrufe (max. 4 Fragen pro Aufruf). Überspringe nur, was sich aus
dem Argument oder meiner Eingabe bereits eindeutig ergibt.

**Runde 1 — Projekt-Basics:**
1. URL der Bestandswebsite? (nur fragen, wenn kein Argument übergeben —
   sonst bestätigen)
2. Branche/Kategorie? (Optionen: Salon/Beauty/Wellness, Handwerk/Bau,
   Coach/Beratung/Praxis, Einzelhandel — plus "Other" für Freitext)
3. Seitenstruktur? (One-Pager (Recommended für lokale Betriebe) /
   Multi-Page / Entscheide nach Audit)
4. Sprachen? (Nur Deutsch (Recommended) / DE+EN / wie Original)

**Runde 2 — Features & Stack-Details:**
5. Branchen-Kern-Feature? (multiSelect — Optionen passend zur Branche aus
   Runde 1, z. B.: Online-Booking-System, Lead-/Angebots-Formular,
   Referenz-/Projekt-Galerie, Produkt-Schaufenster, News/Aktionen, Keins)
6. Dark/Light-Mode-Switch? (Ja (Recommended) / Nur Light / Nur Dark)
7. Transaktionale Mails via Resend? (Ja, sofort / Phase 2 / Nicht nötig)
8. Online-Zahlungen via Stripe? (Phase 2 (Recommended) / Sofort / Nie)

**Runde 3 — Pitch & Preise:**
9. Pitch-Deck (Marp → PDF/PPTX) miterstellen? (Ja, mit Audit-Slides
   (Recommended) / Nur Prototyp)
10. Preisrahmen für die Pakete? (400-1200 € (Recommended, Default
    Starter/Pro/Premium) / 600-2000 € / Eigene Angabe via Other)

**Nicht fragen — fixe Defaults (nur erwähnen):**
- Stack: Next.js App Router + Vercel (fra1) + Sanity Voll-CMS (embedded
  Studio unter /studio) — gesetzt.
- Content: 1:1-Übernahme von der Bestandswebsite (Texte wortgleich,
  Preise/Daten exakt, keine Umformulierung). Stock-Bilder nur als
  markierte Platzhalter — gesetzt.
- Route-Group `(site)` für Website-Layout, Root-Layout minimal — gesetzt.
- DSGVO-Basics (Impressum/Datenschutz mit Anwalts-TODO, kein Tracking,
  OSM statt Google Maps) — gesetzt.

## Schritt 2 — Ist-Stand-Audit

Führe Stage 1 aus dem Rezept aus: Bestandssite + Unterseiten analysieren,
alle Inhalte 1:1 extrahieren und sichern, `docs/AUDIT.md` mit Bewertung
je Dimension schreiben (SEO, AEO, A11y, Mobile, Performance, UI/UX,
DSGVO, Tech/Pflegbarkeit, Conversion).

Wenn die Domain in der Sandbox blockiert ist (403 / host_not_allowed):
Aggregatoren und Suche versuchen; wenn das scheitert, mich explizit um
Screenshots aller Seiten + Bild-URLs bitten und auf die Antwort warten.

## Schritt 3 — Plan vorlegen

Erstelle `docs/PRD.md` + `features/INDEX.md` + Feature-Specs nach Stage 2
des Rezepts und fasse mir den Plan kompakt zusammen (Features, Reihenfolge,
was Phase 2 ist). Warte auf mein OK, bevor du mit dem Build (Stage 3)
beginnst.

## Schritt 4 — Build & Deploy

Nach Freigabe: Stage 3-4 aus dem Rezept, feature-für-feature mit Commit
je Etappe, Qualitäts-Gates vor jedem Push (tsc, next build, keine toten
Anker-Links, tel:/mailto: verifiziert). Am Ende: vercel.json, Hinweise
für GitHub-Preview-Integration und benötigte Env-Vars, ggf. Pitch-Deck.
