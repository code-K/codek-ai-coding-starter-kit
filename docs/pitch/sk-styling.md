---
marp: true
theme: default
html: true
size: 16:9
backgroundColor: "#262626"
color: "#f2f2f2"
header: '<span class="hl"><span class="bk">&lt;</span>&nbsp;CODE&nbsp;K&nbsp;<span class="bk">/&gt;</span></span><img class="hr" src="assets/codek-logo-white.png" />'
footer: '<span>Christian&nbsp;Koch&nbsp;&nbsp;·&nbsp;&nbsp;<b>devs.berlin</b></span><span>Senior&nbsp;Fullstack&nbsp;Web-Developer&nbsp;·&nbsp;Berlin</span><span>Frühjahr&nbsp;2026</span>'
style: |
  @import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;700;800&family=Manrope:wght@400;500;600;700;800&family=Fraunces:ital,opsz,wght@0,9..144,300;0,9..144,400;0,9..144,500;1,9..144,300;1,9..144,400&display=swap');

  :root {
    --bg: #262626;
    --bg-deep: #1d1d1d;
    --surface: #313131;
    --surface-2: #3a3a3a;
    --line: #474747;
    --line-soft: #383838;
    --ink: #f2f2f2;
    --ink-dim: #a6a6a6;
    --ink-mute: #6f6f6f;
    --accent: #74b6ec;
    --accent-deep: #5193cc;
    --accent-bg: #20313f;
    --warn: #e2a45c;
    --warn-bg: #352b1d;
    --mono: 'JetBrains Mono', ui-monospace, 'SFMono-Regular', Menlo, monospace;
    --sans: 'Manrope', -apple-system, system-ui, sans-serif;
    --serif: 'Fraunces', Georgia, 'Times New Roman', serif;
  }

  section {
    background: var(--bg);
    color: var(--ink);
    font-family: var(--sans);
    font-size: 15.5px;
    line-height: 1.5;
    padding: 66px 66px 64px;
    letter-spacing: 0.005em;
  }

  /* ---- brand header / footer (durchgehend auf allen Slides) ---- */
  section > header {
    left: 66px; right: 66px; top: 26px;
    display: flex; justify-content: space-between; align-items: flex-start;
  }
  section > header .hl {
    font-family: var(--mono); font-weight: 800; font-size: 14px;
    letter-spacing: 0.05em; color: var(--ink); margin-top: 4px;
  }
  section > header .hl .bk { color: var(--accent); }
  section > header .hr { height: 80px; width: auto; display: block; }
  section > footer {
    left: 66px; right: 66px; bottom: 28px;
    border-top: 1px solid var(--line-soft); padding-top: 12px;
    display: flex; gap: 26px; align-items: baseline;
    font-family: var(--mono); font-size: 10px; font-weight: 500;
    letter-spacing: 0.05em; color: var(--ink-mute);
  }
  section > footer b { color: var(--ink); font-weight: 700; }

  /* ---- typography ---- */
  h1, h2, h3 { font-family: var(--mono); font-weight: 700; }
  h1 {
    font-size: 33px;
    line-height: 1.16;
    letter-spacing: -0.018em;
    color: var(--ink);
    margin: 0 0 0.5em;
  }
  h2 { font-size: 21px; letter-spacing: -0.01em; margin: 0 0 0.5em; color: var(--ink); }
  h3 { font-size: 15px; letter-spacing: 0.0em; margin: 0 0 0.5em; color: var(--ink); }
  p { margin: 0 0 0.7em; color: #d2d2d2; }
  strong { color: var(--ink); font-weight: 700; }
  a { color: var(--accent); text-decoration: none; }
  ul { margin: 0.2em 0 0.7em; padding-left: 1.1em; }
  li { margin-bottom: 0.34em; color: #d2d2d2; }

  /* ---- eyebrow ---- */
  .eyebrow {
    font-family: var(--mono);
    font-size: 11px;
    font-weight: 700;
    letter-spacing: 0.16em;
    color: var(--accent);
    text-transform: uppercase;
    margin-bottom: 1.0em;
    display: flex; align-items: baseline; gap: 0.6em;
  }
  .eyebrow .num { color: var(--ink-mute); }
  .eyebrow.warn { color: var(--warn); }

  .lead { font-size: 17px; line-height: 1.5; color: #cfcfcf; }
  .serif { font-family: var(--serif); font-weight: 300; font-style: italic; }
  .small { font-size: 12.5px; color: var(--ink-dim); line-height: 1.45; }
  .mono-note {
    font-family: var(--mono); font-size: 11.5px; color: var(--ink-mute);
    letter-spacing: 0.01em;
  }

  /* ---- layout ---- */
  .grid { display: grid; grid-template-columns: 1fr 1fr; gap: 36px; align-items: start; }
  .grid.tilt { grid-template-columns: 1.05fr 0.95fr; }
  .grid.wide-r { grid-template-columns: 0.82fr 1.18fr; }
  .grid-3 { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 20px; }
  .stack > * + * { margin-top: 0.7em; }

  /* ---- portrait / bio intro row ---- */
  .bio-row {
    display: grid;
    grid-template-columns: 128px 1fr;
    gap: 22px;
    align-items: start;
  }
  .bio-row .portrait {
    width: 128px;
    height: 168px;
    object-fit: cover;
    object-position: center 18%;
    border-radius: 12px;
    border: 1px solid var(--line);
    box-shadow: 0 8px 24px rgba(0,0,0,0.35);
    display: block;
  }
  .bio-row .bio-text > * + * { margin-top: 0.6em; }

  /* ---- cards ---- */
  .card {
    background: var(--surface);
    border: 1px solid var(--line);
    border-radius: 14px;
    padding: 22px 24px;
  }
  .card h3 {
    display: flex; align-items: center; gap: 0.5em;
    color: var(--ink);
  }
  .card.solution { border-color: #3c5063; background: linear-gradient(180deg,#2d3a44 0%, var(--surface) 70%); }
  .card.accent {
    background: linear-gradient(165deg,#3a5e7d 0%, #2c4257 100%);
    border-color: var(--accent-deep);
  }
  .card.accent h3, .card.accent .price { color: #fff; }
  .card.flat { background: var(--bg-deep); border-color: var(--line-soft); }

  /* ---- checklist ---- */
  ul.checks { list-style: none; padding-left: 0; }
  ul.checks li {
    position: relative; padding-left: 1.6em; margin-bottom: 0.42em;
    font-size: 13.5px; color: #d6d6d6;
  }
  ul.checks li::before {
    content: "→"; position: absolute; left: 0;
    font-family: var(--mono); font-weight: 700; color: var(--accent);
  }
  ul.problems { list-style: none; padding-left: 0; }
  ul.problems li {
    position: relative; padding-left: 1.6em; margin-bottom: 0.42em;
    font-size: 13.5px; color: #cfcfcf;
  }
  ul.problems li::before {
    content: "×"; position: absolute; left: 0;
    font-family: var(--mono); font-weight: 700; color: var(--warn);
  }

  /* ---- badges / icons ---- */
  .tag {
    display: inline-flex; align-items: center;
    font-family: var(--mono); font-size: 10.5px; font-weight: 700;
    letter-spacing: 0.08em; text-transform: uppercase;
    padding: 4px 9px; border-radius: 6px;
  }
  .tag.warn { background: var(--warn-bg); color: var(--warn); border: 1px solid #5a4427; }
  .tag.ok { background: var(--accent-bg); color: var(--accent); border: 1px solid #2f4a5e; }
  .pmark {
    display: inline-grid; place-items: center;
    width: 30px; height: 30px; border-radius: 8px;
    background: var(--warn-bg); border: 1px solid #5a4427;
    color: var(--warn); font-family: var(--mono); font-weight: 800; font-size: 15px;
    flex: 0 0 auto;
  }
  .callout {
    border-left: 2px solid var(--warn);
    background: var(--warn-bg);
    padding: 12px 16px; border-radius: 0 8px 8px 0;
    font-size: 13.5px; color: #e7d8c2;
  }
  .callout.ok { border-color: var(--accent); background: var(--accent-bg); color: #cfe3f3; }

  /* ---- browser frame ---- */
  .browser {
    border: 1px solid var(--line);
    border-radius: 11px; overflow: hidden;
    background: var(--bg-deep);
    box-shadow: 0 22px 48px rgba(0,0,0,0.46);
  }
  .browser .bar {
    display: flex; align-items: center; gap: 6px;
    padding: 9px 13px; background: #1a1a1a;
    border-bottom: 1px solid var(--line-soft);
  }
  .browser .bar i {
    width: 8px; height: 8px; border-radius: 50%; background: #4a4a4a; display: block;
  }
  .browser .bar .url {
    margin-left: 10px; font-family: var(--mono); font-size: 9.5px;
    color: var(--ink-mute); letter-spacing: 0.02em;
  }
  .browser img { display: block; width: 100%; }
  .shot-tall { height: 312px; object-fit: cover; object-position: top; }
  .shot-wide { height: 318px; object-fit: cover; object-position: top; }

  /* ---- phone frame ---- */
  .phone {
    width: 232px; margin: 0 auto;
    border: 6px solid #111; border-radius: 32px;
    background: #111; overflow: hidden;
    box-shadow: 0 24px 50px rgba(0,0,0,0.5);
  }
  .phone img { display: block; width: 100%; }

  /* ---- price ---- */
  .price {
    font-family: var(--mono); font-size: 30px; font-weight: 800;
    letter-spacing: -0.02em; color: var(--ink);
    line-height: 1; margin: 0.35em 0 0.15em;
  }

  /* ---- timeline ---- */
  .road { display: grid; grid-template-columns: 34px 1fr; gap: 16px 16px; }
  .road .dot {
    display: grid; place-items: center;
    width: 30px; height: 30px; border-radius: 8px;
    background: var(--accent-bg); border: 1px solid #2f4a5e;
    color: var(--accent); font-family: var(--mono); font-weight: 800; font-size: 13px;
  }
  .road .step { padding-top: 2px; }
  .road .step b { font-family: var(--mono); font-size: 13.5px; color: var(--ink); }
  .road .step span { font-size: 13px; color: var(--ink-dim); }

  /* ---- cover ---- */
  section.cover {
    padding: 0;
    background:
      radial-gradient(900px 480px at 80% 6%, rgba(116,182,236,0.14), transparent 62%),
      linear-gradient(165deg, #2c2c2c 0%, #1b1b1b 100%);
  }
  .cover-wrap {
    height: 100%; box-sizing: border-box;
    padding: 64px 72px;
  }
  .logo {
    font-family: var(--mono); font-weight: 800; font-size: 17px;
    letter-spacing: 0.04em; color: var(--ink);
    display: flex; align-items: center; gap: 9px;
  }
  .logo .bk { color: var(--accent); }
  .logo .peace { font-size: 16px; }
  .cover-title { margin-top: 232px; }
  .cover-kicker {
    font-family: var(--mono); font-size: 12px; font-weight: 700;
    letter-spacing: 0.22em; text-transform: uppercase; color: var(--accent);
    margin-bottom: 18px;
  }
  h1.cover-h {
    font-size: 47px; line-height: 1.07; letter-spacing: -0.022em;
    margin: 0;
  }
  h1.cover-h .sk { font-family: var(--serif); font-weight: 400; font-style: italic; color: #fff; }
  .cover-sub {
    margin-top: 26px; font-size: 16px; color: var(--ink-dim);
    max-width: 30em; line-height: 1.55;
  }
  .cover-foot {
    margin-top: 88px; display: flex; gap: 28px; align-items: center;
    font-family: var(--mono); font-size: 11.5px; color: var(--ink-mute);
    letter-spacing: 0.04em;
    border-top: 1px solid var(--line-soft); padding-top: 20px;
  }
  .cover-foot b { color: var(--ink); font-weight: 700; }

  /* ---- closing ---- */
  section.close .eyebrow { color: var(--accent); }
  .qr-box {
    background: #fff; padding: 14px; border-radius: 14px;
    width: 210px; height: 210px; display: grid; place-items: center;
  }
  .qr-box img { width: 100%; height: 100%; }

  /* ---- misc ---- */
  .divider { height: 1px; background: var(--line-soft); margin: 14px 0; }
  .kpi { display: flex; gap: 26px; margin-top: 6px; }
  .kpi .k { font-family: var(--mono); }
  .kpi .k b { display: block; font-size: 26px; font-weight: 800; color: var(--accent); letter-spacing: -0.02em; }
  .kpi .k span { font-size: 11px; color: var(--ink-dim); letter-spacing: 0.04em; }
  .meta-row { display: flex; gap: 8px; flex-wrap: wrap; margin-top: 4px; }
---

<!-- _class: cover -->

<div class="cover-wrap">
<div class="cover-title">
<div class="cover-kicker">Pitch&nbsp;·&nbsp;Website-Relaunch</div>
<h1 class="cover-h"><span class="sk">SK&nbsp;Styling</span><br/>neu&nbsp;gedacht.</h1>
<p class="cover-sub">Ein Vorschlag zur Modernisierung Ihres Online-Auftritts am Breitenbachplatz&nbsp;— mobil, auffindbar und selbst pflegbar.</p>
</div>
</div>

---

## Wer hier pitcht

<div class="grid tilt">
<div class="stack">

<div class="eyebrow"><span class="num">// 00</span> Vorab</div>

<div class="bio-row">
<img class="portrait" src="assets/me.png" alt="Christian Koch" />
<div class="bio-text">

<p class="lead">
Kein Agentur-Apparat — ein fester Ansprechpartner. Ich bin <strong>Christian Koch</strong>, freiberuflicher Senior-Developer aus Berlin und baue seit über 15 Jahren Websites, Shops und CRM-Systeme.
</p>

<p>
Sonst für größere Marken im Einsatz — diesen Relaunch betreue ich vom ersten Entwurf bis zum Go-Live persönlich. Was Sie auf den nächsten Folien sehen, ist <strong>kein Mockup</strong>, sondern ein bereits lauffähiger Prototyp.
</p>

</div>
</div>

</div>
<div class="stack">

<div class="card">
<h3>Was dieser Vorschlag enthält</h3>
<ul class="checks">
<li>Eine ehrliche Analyse der heutigen Website</li>
<li>Fünf konkrete Schwachstellen — und ihre Lösung</li>
<li>Einen fertigen, klickbaren Prototyp</li>
<li>Drei Pakete mit transparenten Festpreisen</li>
</ul>
</div>

<div class="kpi">
<div class="k"><b>15+</b><span>JAHRE WEB-DEV</span></div>
<div class="k"><b>1:1</b><span>ANSPRECHPARTNER</span></div>
<div class="k"><b>0&nbsp;€</b><span>LAUFENDE KOSTEN</span></div>
</div>

</div>
</div>

---

## Status Quo

<div class="grid">
<div class="stack">

<div class="eyebrow"><span class="num">// 01</span> Bestandsaufnahme</div>

<p>
Die heutige Website unter <strong>sk-styling.de</strong> stammt aus den frühen 2000ern — sie funktioniert, transportiert aber nicht mehr, wofür SK Styling heute steht.
</p>

<h3>Drei Punkte fallen sofort auf</h3>
<ul class="problems">
<li>Nicht für Smartphones gemacht — Text winzig, Bedienung mühsam</li>
<li>Bildsprache und Layout wirken aus der Zeit gefallen</li>
<li>Kein Weg, online einen Termin zu sehen oder zu buchen</li>
</ul>

<p class="mono-note">© 2002–2003 — seit über 20 Jahren unverändert</p>

</div>
<div>

<div class="browser">
<div class="bar"><i></i><i></i><i></i><span class="url">sk-styling.de/home.html</span></div>
<img class="shot-tall" src="assets/oldsite-desktop.jpg" alt="Bestandssite sk-styling.de" />
</div>
<p class="small" style="text-align:center;margin-top:10px;">Die Bestandssite — Stand heute</p>

</div>
</div>

---

## Pain-Point 1 — Mobil

<div class="grid">
<div class="stack">

<div class="eyebrow warn"><span class="num">// 02</span> Das Problem</div>

<div style="display:flex;gap:14px;align-items:flex-start;">
<span class="pmark">!</span>
<p style="margin:0;"><strong>Über 70 % aller Anfragen kommen heute vom Smartphone.</strong></p>
</div>

<p>Die aktuelle Seite hat dafür keine Antwort:</p>
<ul class="problems">
<li>Keine responsive Layout-Logik</li>
<li>Schrift wird beim Zoomen unleserlich</li>
<li>Schaltflächen zu klein für den Daumen</li>
<li>Kein „Tippen zum Anrufen"</li>
</ul>

<div class="callout">
Potenzielle Neukundinnen springen ab, bevor sie überhaupt die Telefonnummer entdeckt haben.
</div>

</div>
<div class="card solution stack">

<div class="tag ok">Lösung</div>
<h3>Was wir liefern</h3>
<ul class="checks">
<li>Mobile-First-Design — getestet auf iPhone &amp; Android</li>
<li>Tap-to-Call-Leiste am unteren Bildschirmrand</li>
<li>Touch-optimierte Slots im Buchungs-Flow</li>
<li>Schrift &amp; Buttons in daumentauglicher Größe</li>
</ul>

</div>
</div>

---

## Pain-Point 2 — Auffindbarkeit

<div class="grid">
<div class="stack">

<div class="eyebrow warn"><span class="num">// 03</span> Das Problem</div>

<div style="display:flex;gap:14px;align-items:flex-start;">
<span class="pmark">!</span>
<p style="margin:0;"><strong>Bei „Friseur Breitenbachplatz" rangiert die Seite weit hinten bei Google.</strong></p>
</div>

<ul class="problems">
<li>Lange Ladezeiten (geschätzter Lighthouse-Score &lt; 50)</li>
<li>Keine strukturierten Daten (Schema.org)</li>
<li>Keine Sitemap, keine semantischen Überschriften</li>
<li>Bilder für Google nicht indexierbar</li>
</ul>

<p class="mono-note">Wer nicht gefunden wird, existiert online nicht.</p>

</div>
<div class="card solution stack">

<div class="tag ok">Lösung</div>
<h3>Was wir liefern</h3>
<ul class="checks">
<li>Lighthouse-Ziel ≥ 95 in allen vier Kategorien</li>
<li>Schema.org-Markup: Adresse, Öffnungszeiten, Geo</li>
<li>Sitemap &amp; robots.txt sauber konfiguriert</li>
<li>Bilder über CDN, automatisch komprimiert</li>
<li>Edge-Hosting in Frankfurt — niedrige Latenz</li>
</ul>

</div>
</div>

---

## Pain-Point 3 — Selbst pflegen

<div class="grid">
<div class="stack">

<div class="eyebrow warn"><span class="num">// 04</span> Das Problem</div>

<div style="display:flex;gap:14px;align-items:flex-start;">
<span class="pmark">!</span>
<p style="margin:0;"><strong>Heute ist jede Preisänderung ein Anruf beim Entwickler.</strong></p>
</div>

<ul class="problems">
<li>News &amp; Aktionen nicht spontan ankündbar</li>
<li>Galerie-Bilder müssen manuell ausgetauscht werden</li>
<li>Saison-Aktionen gehen schlicht unter</li>
</ul>

<div class="callout">
Eine Website, die man nicht selbst pflegen kann, veraltet ab dem ersten Tag.
</div>

</div>
<div class="card solution stack">

<div class="tag ok">Lösung</div>
<h3>Was wir liefern</h3>
<ul class="checks">
<li>Voll-CMS auf Basis von Sanity — direkt im Browser</li>
<li>Preise, Texte, Fotos in 2 Minuten geändert</li>
<li>News-Beiträge mit Ablaufdatum</li>
<li>Mehrere Nutzer:innen parallel</li>
<li>Versionierung &amp; Rückgängig eingebaut</li>
</ul>

</div>
</div>

---

## Pain-Point 4 — Rechtssicherheit

<div class="grid">
<div class="stack">

<div class="eyebrow warn"><span class="num">// 05</span> Das Problem</div>

<div style="display:flex;gap:14px;align-items:flex-start;">
<span class="pmark">§</span>
<p style="margin:0;"><strong>Datenschutzerklärung und Impressum sind veraltet oder fehlen.</strong></p>
</div>

<ul class="problems">
<li>Abmahnrisiko durch spezialisierte Kanzleien</li>
<li>Bußgeld bei DSGVO-Verstoß</li>
<li>Vertrauensverlust bei modernen Kund:innen</li>
</ul>

</div>
<div class="card solution stack">

<div class="tag ok">Lösung</div>
<h3>Was wir liefern</h3>
<ul class="checks">
<li>DSGVO-konforme Datenschutzerklärung als Mustertext</li>
<li>Impressum nach § 5 TMG</li>
<li>Cookie-frei wo möglich — kein Tracking</li>
<li>Empfehlung: anwaltliche Prüfung vor Go-Live — wir liefern die Vorlagen</li>
</ul>

</div>
</div>

---

## Pain-Point 5 — Termine

<div class="grid">
<div class="stack">

<div class="eyebrow warn"><span class="num">// 06</span> Das Problem</div>

<div style="display:flex;gap:14px;align-items:flex-start;">
<span class="pmark">‣</span>
<p style="margin:0;"><strong>Telefonisch buchen ist Standard — aber längst nicht mehr Erwartung.</strong></p>
</div>

<ul class="problems">
<li>Jüngere Kundschaft erwartet Online-Buchung</li>
<li>Telefonzeiten kollidieren mit Arbeitszeiten</li>
<li>Fresha als Drittanbieter ist nicht mehr aktiv</li>
</ul>

</div>
<div class="card solution stack">

<div class="tag ok">Lösung</div>
<h3>Was wir liefern</h3>
<ul class="checks">
<li>Eigenes Buchungssystem — kein monatliches Abo</li>
<li>Echtzeit-Verfügbarkeit aus den Öffnungszeiten</li>
<li>Mitarbeiter-Auswahl, jede Person eigener Kalender</li>
<li>Bestätigungs-Mail mit Kalender-Datei</li>
<li>Stornierung per Link — kein Anruf nötig</li>
</ul>

</div>
</div>

---

## Die Vision

<div class="grid wide-r">
<div class="stack">

<div class="eyebrow"><span class="num">// 07</span> Wie es aussehen kann</div>

<h2 class="serif" style="font-size:25px;line-height:1.25;">Ein durchdachter Eindruck — vom ersten Scroll bis zur Terminbestätigung.</h2>

<ul class="checks">
<li>Großflächige, atmosphärische Bildsprache</li>
<li>Klar lesbare Preise &amp; Leistungen</li>
<li>Heller oder dunkler Modus je nach Tageszeit</li>
<li>Ein klarer Handlungsaufruf: „Termin buchen"</li>
</ul>

<p class="small">Alles unter Ihrer eigenen Marke — keine Vorlagen, keine Templated-Optik.</p>

</div>
<div>

<div class="browser">
<div class="bar"><i></i><i></i><i></i><span class="url">sk-styling.de</span></div>
<img class="shot-wide" src="assets/site-hero-desktop.png" alt="Neuer Prototyp — Startseite" />
</div>
<p class="small" style="text-align:center;margin-top:10px;">Prototyp · lauffähig &amp; klickbar</p>

</div>
</div>

---

## Online buchen

<div class="grid wide-r">
<div class="stack">

<div class="eyebrow"><span class="num">// 08</span> Das Herzstück</div>

<h2 class="serif" style="font-size:25px;line-height:1.25;">In vier Schritten zum Termin — Tag und Nacht.</h2>

<ul class="checks">
<li>Leistung wählen — mit Dauer &amp; Preis</li>
<li>Mitarbeiter:in auswählen (oder „egal")</li>
<li>Freien Termin aus dem Live-Kalender picken</li>
<li>Kontaktdaten — Bestätigung kommt sofort per Mail</li>
</ul>

<div class="callout ok">
Kein Drittanbieter, kein monatliches Abo — das System gehört zur Website.
</div>

</div>
<div>

<div class="browser">
<div class="bar"><i></i><i></i><i></i><span class="url">sk-styling.de/#booking</span></div>
<img class="shot-wide" src="assets/site-booking-desktop.png" alt="Buchungs-Flow im Prototyp" />
</div>
<p class="small" style="text-align:center;margin-top:10px;">Buchungs-Flow · Schritt 1 von 4</p>

</div>
</div>

---

## Mobil zuerst gedacht

<div class="grid wide-r">
<div class="stack">

<div class="eyebrow"><span class="num">// 09</span> Smartphone-Ansicht</div>

<h2 class="serif" style="font-size:25px;line-height:1.25;">Dort gestaltet, wo der Daumen es erwartet.</h2>

<p>
Der Prototyp ist für 375–430&nbsp;px Breite entworfen und skaliert von dort nach oben — nicht umgekehrt.
</p>

<ul class="checks">
<li>Tap-to-Call direkt erreichbar</li>
<li>Touch-optimierte Slots im Buchungs-Flow</li>
<li>Sofort lesbare Preise &amp; Leistungen</li>
</ul>

</div>
<div style="display:flex;justify-content:center;">

<div class="phone">
<img src="assets/site-hero-mobile.png" alt="Mobile-Ansicht des Prototyps" />
</div>

</div>
</div>

---

## Tech-Stack — kurz erklärt

<div class="eyebrow"><span class="num">// 10</span> Das Fundament</div>

<div class="grid-3">

<div class="card">
<h3>Next.js + Vercel</h3>
<p class="small">Serverseitig vorgerendert, ausgeliefert von Edge-Servern in Frankfurt. Ladezeiten unter einer Sekunde — auch im Mobilfunknetz.</p>
</div>

<div class="card">
<h3>Sanity CMS</h3>
<p class="small">Ein eingebautes Studio erlaubt jede Inhaltsänderung selbst — direkt im Browser. Kein Entwickler nötig.</p>
</div>

<div class="card">
<h3>DSGVO-Stack</h3>
<p class="small">Alle Datenflüsse in der EU oder vertraglich abgesichert. Mailversand &amp; optionale Zahlungen DSGVO-konform.</p>
</div>

</div>

<div class="card flat" style="margin-top:22px;display:flex;align-items:center;gap:18px;">
<span class="tag ok">0&nbsp;€&nbsp;/&nbsp;Monat</span>
<p style="margin:0;font-size:13.5px;">
<strong>Laufende Kosten: 0&nbsp;€.</strong> Vercel Hobby, Sanity Free und der Mailversand decken den Bedarf einer Salon-Site komplett ab — lediglich die Domain (~12&nbsp;€/Jahr) fällt an.
</p>
</div>

---

## Drei Pakete zur Auswahl

<div class="eyebrow"><span class="num">// 11</span> Transparente Festpreise</div>

<div class="grid-3">

<div class="card stack">
<div class="tag ok">Paket A</div>
<h3>Starter</h3>
<div class="price">390 €</div>
<p class="small" style="margin-top:0;">einmalig, netto · ~2 Wochen</p>
<ul class="checks">
<li>Komplettes Redesign, mobile-first</li>
<li>Sanity-CMS zur Pflege</li>
<li>Impressum + Datenschutz</li>
<li>SEO-Basis + Schema.org</li>
<li>Vercel-Hosting eingerichtet</li>
</ul>
</div>

<div class="card accent stack">
<div class="tag" style="background:#cfe3f3;color:#23425a;">Paket B · empfohlen</div>
<h3>Pro</h3>
<div class="price">790 €</div>
<p class="small" style="margin-top:0;color:#cfe3f3;">einmalig, netto · ~4–5 Wochen</p>
<ul class="checks">
<li>Alles aus Starter</li>
<li>Online-Buchungssystem</li>
<li>Mitarbeiter-Auswahl &amp; Sperrzeiten</li>
<li>Bestätigungs-Mails mit Kalender-Datei</li>
<li>Self-Service-Stornierung</li>
</ul>
</div>

<div class="card stack">
<div class="tag ok">Paket C</div>
<h3>Premium</h3>
<div class="price">1.190 €</div>
<p class="small" style="margin-top:0;">einmalig, netto · ~6–8 Wochen</p>
<ul class="checks">
<li>Alles aus Pro</li>
<li>Anzahlung gegen No-Shows</li>
<li>Drag-&amp;-Drop-Kalender im Admin</li>
<li>Wiederkehrende Sperrzeiten</li>
<li>Lookbook mit Lightbox</li>
</ul>
</div>

</div>

---

## Was nicht im Preis enthalten ist

<div class="grid">
<div class="stack">

<div class="eyebrow"><span class="num">// 12</span> Ehrlich dazugesagt</div>

<p>Damit es keine Überraschungen gibt — optionale Posten, transparent aufgeführt:</p>

<ul class="problems">
<li><strong>Domain</strong> — behalten oder neu, ~12–15 €/Jahr</li>
<li><strong>Profi-Fotoshooting</strong> im Salon — extern, ~300–600 €</li>
<li><strong>DSGVO-Anwaltsprüfung</strong> der Texte — ~150–300 €, empfohlen</li>
<li><strong>Wartung</strong> nach Go-Live — ~30 €/Monat, optional</li>
</ul>

<p class="mono-note">SSL-Zertifikat: in Vercel enthalten — 0 €.</p>

</div>
<div class="card stack">

<h3>Bereits vorbereitet</h3>
<ul class="checks">
<li>Voll funktionsfähige Demo unter einer Vorschau-URL</li>
<li>Originaltexte &amp; Adresse von der Bestandssite übernommen</li>
<li>Logo-Vorschlag auf Basis Ihrer aktuellen Marke</li>
<li>Stock-Bilder als Platzhalter — durch echte Fotos ersetzbar</li>
<li>Beispiel-Buchungen im CMS für die Demo</li>
</ul>

</div>
</div>

---

## Roadmap nach Auftrag

<div class="eyebrow"><span class="num">// 13</span> Vier Schritte zum Go-Live</div>

<div class="road" style="margin-top:18px;">

<div class="dot">1</div>
<div class="step"><b>Woche 1</b> &nbsp;—&nbsp; <span>Kickoff-Termin, Marken-Abstimmung (Farben, Schriften, Tonalität), Auswahl der Bilder.</span></div>

<div class="dot">2</div>
<div class="step"><b>Woche 2</b> &nbsp;—&nbsp; <span>Inhalte ins CMS einpflegen, Preise &amp; Team-Daten sammeln, Anwaltsprüfung anstoßen.</span></div>

<div class="dot">3</div>
<div class="step"><b>Woche 3</b> &nbsp;—&nbsp; <span>Buchungssystem konfigurieren (Pro/Premium), Zahlungen einrichten (Premium), Testläufe.</span></div>

<div class="dot">4</div>
<div class="step"><b>Woche 4+</b> &nbsp;—&nbsp; <span>Soft-Launch auf temporärer URL, Korrekturschleife, dann Domain-Umzug und Go-Live.</span></div>

</div>

---

<!-- _class: close -->

<div class="grid" style="align-items:center;">
<div class="stack">

<div class="eyebrow"><span class="num">// 14</span> Nächster Schritt</div>

<h1 style="font-size:38px;">Lassen Sie uns reden.</h1>

<p class="lead">
Schauen Sie sich die Demo in Ruhe an — ich freue mich auf Ihre Rückmeldung und beantworte gern jede Frage.
</p>

<div class="divider"></div>

<p class="mono-note" style="line-height:1.7;">
<strong style="color:#f2f2f2;">Christian Koch</strong><br/>
koch@code-k.info&nbsp; ·&nbsp; devs.berlin<br/>
‹ CODE·K › — freiberufliche Web-Entwicklung, Berlin
</p>

</div>
<div style="text-align:center;">

<div class="qr-box"><img src="assets/preview-qr.svg" alt="QR-Code zur Live-Demo" /></div>
<p class="small" style="margin-top:12px;"><strong style="color:#f2f2f2;">Demo live ansehen</strong><br/>QR scannen oder URL eintippen</p>

</div>
</div>
