# Webdesign und Launch (WD, LA)

Regeln für Websites, Landing Pages und Web-Apps: Typografie, Farbe, Layout, Landing-Aufbau, Navigation, Bilder, Lokalisierung, technische Launch-Basics. Schweregrade wie in `regeln-bedienung.md`. **Beleg** = Primärquelle mit Zahl; **Praxis** = Branchenkonvention ohne harte Daten, Zahl ist Richtwert, nicht Gesetz. Quellenkürzel in `quellen.md`.

Wo eine Regel eine Bedienregel nur wiederholt (Kontrast A4, Fokus A1, Trefferfläche T1, `dvh` T4), steht hier nur der Verweis.

---

## WD-A. Typografie

**WD1 (H) Zeilenlänge Fließtext 45 bis 90 Zeichen, Ziel 60 bis 75.** Textcontainer `max-width` zwischen `45ch` und `75ch`.
Prüfen: Desktop 1440 px, kein Absatz mit mehr als 90 Zeichen pro Zeile.
Quelle: BUT (Beleg), WCAG 1.4.8 (AAA, 80 Zeichen).

**WD2 (H) Zeilenhöhe Fließtext 1,4 bis 1,6, einheitenlos.** Überschriften enger (1,1 bis 1,25). Bei `line-height: 1.5` darf nichts abgeschnitten werden (WCAG 1.4.12).
Quelle: BUT nennt 120 bis 145 % (Satzspiegel, eher Druck); 1,4 bis 1,6 ist Web-Praxis für Bildschirmtext; WCAG 1.4.12.

**WD3 (H) Fließtext mindestens 16 px, Sekundärtext nie unter 14 px, Eingabefelder 16 px (FO15).** Größen in `rem`/`clamp()`, nie fixe `px` für Text, damit Browser-Schriftgröße und 200 % Zoom greifen (T10).
Quelle: BUT (15 bis 25 px), WCAG 1.4.4.

**WD4 (M) Eine Typo-Skala mit 6 bis 8 Stufen,** Verhältnis 1,125 bis 1,333 (z. B. 14/16/20/24/32/40/56). Jede Überschriftenebene mindestens 1,25-mal größer als die nächste.
Prüfen: Anzahl verschiedener `font-size`-Werte auf der Seite höchstens 8.
Quelle: MAT3 Type Scale (Praxis).

**WD5 (M) Höchstens 2 Schriftfamilien und 2 bis 4 Schnitte (Ziel: 2 für Ladezeit),** selbst gehostet als WOFF2, `font-display: swap` oder `optional`, Fallback-Metrik angepasst (`size-adjust`), damit kein Layoutsprung entsteht.
Quelle: BUT, R24 (Ziel zwei Schnitte), web.dev (Praxis).

**WD6 (M) Versalien nur für einzeilige Labels, dann mit 5 bis 12 % Laufweite** (`letter-spacing: .05em` bis `.12em`). Fließtext nie in Versalien. Blocksatz nur mit `hyphens: auto` und `lang`; zentriert nur bei höchstens 3 Zeilen.
Quelle: BUT.

**WD7 (N) Optische Korrektur:** Play-Dreieck leicht nach rechts versetzen, Icons optisch statt mathematisch zentrieren; Überschriften `text-wrap: balance` (X5).
Quelle: R30.

---

## WD-B. Farbe, Kontrast, Dark Mode

**WD8 (K) Kontrast nach A4 und Information nie nur über Farbe (Z6).** Links im Fließtext zusätzlich unterstrichen. Text über Bildern an der hellsten Stelle messen; Gradient-Text (`background-clip: text`) am schwächsten Punkt messen und mit Fallback-Farbe versehen.
Quelle: WCAG 1.4.1/1.4.3/1.4.11.

**WD9 (M) Weder reines Schwarz noch reines Weiß als Fläche mit Text in Gegenfarbe.** Hell: Text etwa `#111` bis `#222` (oder HSL-Lightness 8 %) auf `#fff`/`#fafafa`. Dunkel: Hintergrund HSL-Lightness ca. 8 % bzw. `#121212` bis `#1a1a1a`, Text ca. 94 % Lightness bzw. `#e0e0e0` bis `#f0f0f0`. Kontrast bleibt über 4,5:1.
Prüfen: `background-color: #000` mit `color: #fff` (oder umgekehrt) auf großen Flächen ist ein Befund.
Quelle: R28, R30, MAT2 Dark Theme (Praxis), W16.

**WD10 (H) Dark Mode ist eine eigene Palette, keine Invertierung.** Erhöhung über hellere Flächen statt Schatten (Card ca. +4 Prozentpunkte Lightness gegenüber Hintergrund), Akzentfarben entsättigt. Beide Themes gegen A4 prüfen.
Quelle: MAT3 Color Roles, R28.

**WD11 (H) Dark Mode technisch vollständig:** `color-scheme: light dark`, `prefers-color-scheme` plus gespeicherter manueller Umschalter, `<meta name="theme-color">` je Schema, kein weißer Blitz beim Laden, Logos und Bilder mit Dark-Variante geprüft, Autofill gestaltet (FO9).
Quelle: web.dev (Praxis).

**WD12 (M) Farben als Tokens, Palette aus einer Basis abgeleitet.** Eine Primärfarbe, 1 bis 2 neutrale Skalen mit 9 bis 11 Stufen, semantische Farben (Erfolg, Warnung, Fehler, Info). Primärfarbe auf höchstens ca. 10 % der Fläche. Palette in HSL/OKLCH aufbauen: Farbton fix, Helligkeit und Sättigung je Rolle getrennt gesteuert.
Prüfen: Hex-Werte direkt in Komponenten statt Tokens sind ein Befund (M).
Quelle: MAT3, R28 (Praxis).

---

## WD-C. Layout und Hierarchie

**WD13 (M) Abstände aus einer 4/8-Skala** (4, 8, 12, 16, 24, 32, 48, 64, 96 px) bzw. Tokens.
Quelle: MAT3 (Praxis).

**WD14 (H) Nähe zeigt Zusammengehörigkeit:** Abstand innerhalb einer Gruppe kleiner als zwischen Gruppen (Label zu Feld 4 bis 8 px, Feld zu Feld 16 bis 24 px, Sektion zu Sektion 64 bis 96 px). Gruppen sind ohne Linien erkennbar.
Quelle: Gestalt/NNG (Praxis-Zahlen).

**WD15 (H) Ein H1 pro Seite, Überschriften ohne Sprung (h1, h2, h3),** Überschriften nach Bedeutung, nicht nach gewünschter Schriftgröße. Startseiten-H1 sagt, was angeboten wird und für wen bzw. wo, nicht "Herzlich willkommen", "Home" oder nur den Firmennamen.
Prüfen: `document.querySelectorAll('h1').length === 1`; Ebenenfolge im Outline.
Quelle: NNG Layer-Cake (Beleg), R39 (H1-Inhalt, Praxis).

**WD16 (M) Container 1100 bis 1280 px, Seitenrand mindestens 16 px mobil, 24 bis 32 px ab Tablet.**
Quelle: MAT3 Window Size Classes (Praxis).

**WD17 (M) Wichtiges nach oben, aber Scrollen einladen.** Folgeabschnitt ragt bei 1440 × 900 und 390 × 844 sichtbar in den Viewport (keine "Illusion of Completeness"). Hero nie `height: 100vh` (T4): `min-height: 100svh` mit Fallback.
Quelle: NNG Scrolling and Attention (57 % der Betrachtungszeit above the fold, 74 % in den ersten zwei Screens), web.dev Viewport Units.

**WD18 (H) Responsive ab 320 px:** `<meta name="viewport" content="width=device-width, initial-scale=1">` vorhanden, kein `maximum-scale`/`user-scalable=no` (A7), Breakpoints mobile-first in `min-width`, Umbruch nach Inhalt. Screenshots bei 320, 390, 768, 1024, 1440 ohne Überlauf.
Quelle: WCAG 1.4.4/1.4.10.

---

## WD-D. Landing Page, Navigation

**WD19 (H) Hero beantwortet in 5 Sekunden: was, für wen, welcher Nutzen.** Headline konkret, kein Floskelsatz ("Revolutionize your…", "All-in-one platform", "Supercharge"). Darunter ein Beleg (Zahl, Kunde, Zitat) und der primäre CTA.
Prüfen: Hero-Text ohne Produktbild lesen lassen: lässt sich das Angebot in einem Satz nennen?
Quelle: NNG Homepage Design Principles, NNG How Long Users Stay (10 bis 20 s).

**WD20 (H) Genau ein primärer CTA pro Sicht (N1) mit konkretem Label** ("Kostenlos testen", "Termin anfragen"), nicht "Mehr erfahren", "Get started", "Hier klicken". Derselbe CTA darf weiter unten wiederkehren.
Quelle: NNG (Label, Beleg), R17, R32.

**WD21 (M) Landing-Aufbau** (Praxis, Reihenfolge anpassbar): 1 Hero (Wert, Beleg, CTA), 2 Social Proof (echt, CV14), 3 Nutzen je mit Ergebnis statt Feature-Liste, 4 Ablauf in 3 bis 4 Schritten, 5 Preis bzw. Angebot (CV28), 6 Einwände/FAQ mit 5 bis 8 Fragen, 7 Schluss-CTA, 8 Footer mit Impressum und Datenschutz. Jede Sektion hat eine H2 und ein Ziel. Keine drei gleich großen Feature-Karten mit Emoji-Icons und Ein-Wort-Inhalt.
Quelle: NNG Layer-Cake, R37 (Praxis).

**WD22 (H) Navigation am Desktop sichtbar, nicht im Hamburger.** Aktuelle Seite markiert (`aria-current="page"`), Logo führt zur Startseite, Labels in Nutzersprache. Mobil: wichtigste 3 bis 4 Ziele sichtbar (Tab-Bar) oder Hamburger mit Wort "Menü". Ab ca. 50 Seiten oder Produkten eine Suche.
Quelle: NNG Hamburger Menus (versteckt 27 % Nutzung vs. 48 bis 50 % sichtbar).

**WD23 (M) Keine auto-rotierenden Carousels.** Wenn Carousel: kein Autoplay oder Pause bei Hover und Fokus, große Steuerelemente, Inhalt im HTML.
Quelle: NNG Auto-Forwarding, web.dev Carousels.

**WD24 (M) Betriebs- und Dienstleister-Websites zeigen Vertrauenssignale:** echtes Teamfoto, echte Bewertungen (CV14), Referenzen/Fallbeispiele, Antwortzeit-Versprechen beim Kontaktformular, Karte und Anfahrt bei Standort, echte Kontaktadresse statt nur Formular, Danke-Seite nach Anfrage mit nächstem Schritt.
Quelle: R36, R37 (Praxis).

---

## WD-E. Bilder und Performance

**WD25 (H) Core Web Vitals im grünen Bereich:** LCP ≤ 2,5 s, INP ≤ 200 ms, CLS ≤ 0,1 (p75). Projektbudget: Seite < 1,5 MB, JS < 300 KB, Bilder above the fold < 500 KB.
Quelle: web.dev (Beleg LCP), globale Budgets.

**WD26 (H) LCP-Bild nie `loading="lazy"`,** im HTML sichtbar, `fetchpriority="high"` auf höchstens 1 bis 2 Bildern.
Quelle: web.dev Optimize LCP.

**WD27 (H) Jedes `<img>` mit `width`/`height` oder `aspect-ratio`, `alt` (dekorativ `alt=""`), `srcset`/`sizes`,** unter dem Fold `loading="lazy"`. Formate AVIF/WebP, Fotos nie PNG, Logos/Icons SVG, kein Einzelbild über ca. 200 KB above the fold bzw. 1 MB irgendwo. Platzhalter (BlurHash, LQIP) statt leerer Fläche.
Quelle: web.dev, R41, R35.

**WD28 (M) Drittanbieter-Skripte nach dem Seitenaufbau, JS pro Route gesplittet, ungenutzte Pakete entfernt,** statische Dateien per CDN mit Cache, Brotli/Gzip. Auf billigem Handy mit gedrosseltem Netz testen.
Quelle: R24 (Praxis).

---

## WD-F. Lokalisierung (Deutsch)

**WD29 (H) Platz für deutschen Text.** Deutsch ist im Mittel 20 bis 35 % länger als Englisch, kurze Strings bis 2- bis 3-fach. Buttons, Tabs, Navigation ohne feste `width` (`min-width` statt `width`). Zwei Buttons nebeneinander, deren Text wachsen kann, stapeln bei Platzmangel untereinander statt abzuschneiden; nie Aktionslabels mit "…" kürzen, wenn dadurch zwei Aktionen gleich aussehen. Feste Kurzlabels (OK, Ja, Nein) dürfen in einer Zeile bleiben.
Prüfen: Pseudo-Lokalisierung mit +40 % Text; 320 px Breite.
Quelle: Netflix Pseudo-Localization (bis 40 %, Beleg), R29.

**WD30 (M) Lange Komposita brechen:** `lang="de"` am `<html>`, `hyphens: auto`, `overflow-wrap: break-word` an Überschriften und schmalen Karten.
Prüfen: "Donaudampfschifffahrtsgesellschaft" in H1 bei 320 px ohne Überlauf.
Quelle: Praxis.

**WD31 (H) Formate nach Locale** über `Intl.*`: Datum `15.11.2026`, Zahl `1.234,56`, Betrag `39,99 €` (Betrag vor €, geschütztes Leerzeichen), nie `39.99` oder `€39.99` in deutscher UI. Anrede einheitlich (X3).
Quelle: E5, BU, WIG Locale.

---

## LA. Technische Launch-Basics

Gilt vor jedem öffentlichen Livegang. Rechtstexte (Impressum, Datenschutz, AGB) liefert `legal-at`, nicht dieser Skill.

**LA1 (K) Unbekannte URL liefert Status 404** (nicht 200, nicht Redirect auf Start) mit eigener Seite: Erklärung, Suche bzw. Startlink, Navigation.
Prüfen: `curl -sI https://domain/gibt-es-nicht` zeigt `404`.
Quelle: Google Search Central (Soft 404), R36.

**LA2 (H) Jede Seite hat einen eigenen `<title>` (ca. 50 bis 60 Zeichen), `<meta name="description">` (ca. 120 bis 160), `canonical`, `<html lang>`.** Kein "Home", "Vite + React", "React App" als Titel.
Quelle: Google Snippets (Praxis-Längen), R36, R37, X6.

**LA3 (H) Open Graph vollständig:** `og:title`, `og:description`, `og:image` (≥ 1200 × 630, absolute HTTPS-URL), `og:url`, `og:type`, `twitter:card=summary_large_image`.
Prüfen: LinkedIn Post Inspector bzw. Facebook Sharing Debugger.
Quelle: Facebook Sharing Docs, R36.

**LA4 (H) Favicon-Satz:** SVG oder PNG ≥ 48 × 48, `apple-touch-icon` 180 × 180, Manifest-Icons 192/512, `theme-color`; `/favicon.ico` antwortet 200. Kein Framework-Standard-Favicon.
Quelle: Google Favicon Docs, R36.

**LA5 (H) `robots.txt` und `sitemap.xml`:** Sitemap mit absoluten kanonischen 200er-URLs, in `robots.txt` per `Sitemap:` eingetragen; Produktion nie `Disallow: /`, Staging per Auth oder `noindex`.
Quelle: Google Sitemaps, R36.

**LA6 (H) HTTPS überall, eine kanonische Host-Variante per 301,** höchstens ein Redirect-Hop.
Prüfen: `curl -sIL http://domain`.
Quelle: Google HTTP Status Codes.

**LA7 (K) Pflichtseiten im Footer jeder Seite:** Impressum, Datenschutzerklärung, bei Shop AGB, Widerrufsbelehrung und Versand/Rückgabe; Cookie-Einwilligung nur, wo nicht notwendige Cookies gesetzt werden; keine Links zur abgeschalteten EU-ODR-Plattform. Inhalt über `legal-at`.
Quelle: R36, R37, legal-at.

**LA8 (H) Analytics eingerichtet und einwilligungskonform** (ohne Einwilligung nur cookielose, nicht personenbezogene Messung). Ohne Messung lässt sich keine Conversion- oder Retention-Regel nachweisen.
Quelle: R36 (Praxis), legal-at.

**LA9 (M) Abnahmelauf:** Lighthouse Mobile ≥ 90 in allen vier Kategorien, axe ohne kritische Fehler, keine Konsolenfehler und kein Mixed Content, "Zum Inhalt springen"-Link, Formularfehler- und Ladezustände vorhanden, Danke-Seite nach jedem Formular.
Quelle: R41, R36 (Praxis).
