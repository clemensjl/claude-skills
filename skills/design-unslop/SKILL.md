---
name: design-unslop
description: Use when a UI looks AI-generated, generic, templated or "vibecoded", when the user says unslop, de-slop, "sieht nach KI aus", "wirkt generisch", "sieht aus wie jede andere Seite" or "Template-Look", when a landing page, hero, portfolio or dashboard should be upgraded ("aufwerten", "hochwertiger machen", "polish this screen"), or when a screen shows purple gradients, glows, gradient text, emoji icons, sparkle badges, uppercase tracked labels, three equal feature cards, pulsing elements or uneven spacing. React, Next.js, Tailwind, Vue, Svelte, plain HTML/CSS, also a live URL or a screenshot.
license: CC-BY-4.0
metadata:
  version: "1.0.0"
  sources: "unslop by Damir Sokolovsky (CC BY 4.0, github.com/heydamir/unslop); taste-skill by Leonxlnx (MIT, github.com/Leonxlnx/taste-skill)"
---

# Design-Unslop

Macht aus einer KI-generierten Oberfläche eine gestaltete, die nur zu diesem Produkt passt. Zusammengeführt aus **unslop** von Damir Sokolovsky ([@heydamir](https://x.com/heydamir), CC BY 4.0) und **taste-skill** (`design-taste-frontend`) von Leonxlnx (MIT). Herkunft und Änderungen stehen in `README.md`.

**Kernprinzip.** Slop verteilt Farbe und Effekte über die Chrome: Hintergründe, Buttons, Rahmen, Labels. Gestaltung hält die Chrome ruhig und legt den Reichtum in ein bis zwei Momente des Inhalts (ein Produktobjekt, ein sorgfältiger Chart, ein Bild aus der Welt des Produkts). Slop entfernen ist die halbe Arbeit. Ein sauberer Screen, der zu jedem Produkt passen würde, ist das nächste Template.

**Was bleibt:** Features, Inhalte, Reihenfolge der Abschnitte, URLs und Slugs, Navigationslabels, Formularfelder samt Namen, Produktname, ein echtes Logo, Rechts- und Consent-Texte. Änderungen daran nur auf ausdrücklichen Wunsch.

## Modus wählen (vor allem anderen)

| Screen | Modus | Was gilt |
|---|---|---|
| Landing, Hero, Portfolio, Marketing, Editorial | **L** | Design Read, alle drei Dials, taste-Layoutregeln, alle neun Durchgänge |
| App-UI, Dashboard, Admin, Tabellen, Formulare, Einstellungen | **A** | Kein taste-Look. Echtes Design-System (das vorhandene, sonst shadcn/ui, Radix Themes, Fluent, Carbon). Die Durchgänge korrigieren, *wie* dessen Tokens benutzt werden. Nur `VISUAL_DENSITY` als Dial |
| Beides im Projekt | getrennt | Marketing-Seiten Modus L, App-Bereich Modus A, je eigener Audit |

Im Modus A wird kein eigenes Farb- oder Typosystem neben das Design-System gebaut. Tokens des Systems umbelegen (`--primary`, `--radius`, Font-Variable) statt Komponenten nachzubauen. shadcn/ui nie im Default-Zustand ausliefern.

## Ablauf

1. **Ansehen.** Dateien finden, die den Screen rendern. Seite starten und mit **agentfenster** ansehen (`browser`-Tool: öffnen, Screenshot, Text auslesen), Desktop 1440 breit. Nicht Playwright. Nur eine URL ohne Code: in agentfenster öffnen, Screenshot und DOM sichern, eine statische Kopie als Arbeitsstand bauen. Nur ein Screenshot: den Screen als eine statische HTML-Datei möglichst genau nachbauen und das als Original behandeln. In beiden Fällen ist das Ergebnis Code zum Übergeben, das im Bericht sagen.
2. **Erkennen.** `references/slop-katalog.md` vollständig durchgehen. Erst die Suchmuster im Code laufen lassen, dann jeden Treffer am Screenshot bestätigen (ein Treffer im Code ist ein Hinweis, kein Befund). Je Befund eine Zeile: ID, Ort (Datei:Zeile oder Bildbereich), was genau.
3. **Ausmaß einstufen.**
   - **Schwer** (Befunde in Farbe, Typo, Icons und Copy): voller Ablauf.
   - **Leicht** (weitgehend gestaltet, einzelne Befunde): Polish. Nur die Befunde beheben, Richtung aus der vorhandenen Marke ableiten, Palette, Typo, Layout und Visual behalten. Größere Ideen als Vorschlag in den Bericht.
   - **Kein Slop:** so sagen, höchstens drei kleine Verfeinerungen mit exakten Werten vorschlagen, nur auf Zustimmung umsetzen. Einen guten Screen nie umbauen, nur damit er anders aussieht.
4. **Richtung festlegen und anhalten.** Nach `references/richtung.md`: Design Read (eine Zeile), Dials (Modus L), fünf Zeilen Richtung (Produkt, Charakter, Welt, Momente, Signatur). Audit nummeriert plus Richtung zeigen und auf Freigabe warten, weil eine spätere Richtungsänderung alles neu macht. In agent-deck als `[QUESTION]`-Block, sonst über das Frage-Tool. Ohne Warten nur, wenn der Auftrag ausdrücklich "mach einfach" sagt.
5. **Umbauen** in neun Durchgängen, siehe unten. Jeder Durchgang über den ganzen Screen, bevor der nächste beginnt. Ändert sich fast jede Zeile, die Durchgänge in Reihenfolge planen und den Screen in einem Zug neu schreiben, solange jeder Durchgang angewendet ist. Werte aus `references/tokens.md`, Regeln je Durchgang aus `references/durchgaenge.md`.
6. **Prüfen.** `references/preflight.md`: erst die maschinellen Checks (Grep, Zählungen, Kontrast), dann Sichtprüfung mit agentfenster bei 1440 und 390 Breite, hell und dunkel. Jeder Audit-Befund ist abgehakt oder steht begründet im Bericht. Während des Umbaus höchstens drei Render-Runden, die Abschlussprüfung kommt dazu.
7. **Bericht** im Format unten.

## Die neun Durchgänge

Reihenfolge ist fest. Abstände zuerst, weil alles andere anders wirkt, sobald der Rhythmus stimmt. Copy vor Typo und Layout, weil die Länge der Headline ihre Größe und Position bestimmt. Visuals und Bewegung zuletzt, weil sie zu einem Screen passen sollen, der ohne sie schon funktioniert.

1. **Abstände:** 4px-Raster, Gleiches gleich groß, innen kleiner als zwischen Gruppen, eine Fluchtlinie.
2. **Farbe:** eine getönte Neutral-Rampe, drei Textrollen, ein Akzent, kein Hue-zu-Hue-Verlauf, kein Glow.
3. **Icons:** ein Set, eine Größe, eine Strichstärke, Farbe der Textrolle, keine Emoji.
4. **Copy:** sagt, was das Produkt für wen tut. Kein Hype, kein Ausrufezeichen, keine Gedankenstriche, nichts erfunden.
5. **Typo:** Familie nach Charakter, Gewichte 400 bis 600, Satzschreibung statt Versal-Labels, Tabellenziffern.
6. **Layout:** Abschnitte und Reihenfolge bleiben. Hero asymmetrisch oder als Szene, Hero-Disziplin, Abschnittsrhythmus.
7. **Details:** verschachtelte Radien, ruhige Zähler, Charts mit Hierarchie, Zustände (Hover, Fokus, Laden, Leer, Fehler).
8. **Visuals:** Deko-Füllstoff raus, ein Visual, das etwas Wahres zeigt. Siehe `references/visuals.md`.
9. **Bewegung:** Schleifen und Bouncen raus, nur erklärende Bewegung, eine Kurve, `prefers-reduced-motion`.

## Harte Regeln

Gelten in beiden Modi, außer der Auftrag oder eine echte Marke verlangt ausdrücklich anderes.

- Ein Akzent pro Seite, auf wenigen Prozent der Fläche. Kein Verlauf von einem Farbton zum anderen auf Flächen, kein Verlaufstext, keine farbigen Glows oder Schatten, keine Farbblobs hinter Inhalt.
- Keine Emoji in der Oberfläche. Keine `—` und `–` als Trenner in sichtbarem Text.
- Schriftgewichte 400 bis 600. Hierarchie über Größe und Farbe.
- Jeder Abstand auf dem 4px-Raster (2px nur für Feinjustierung in kleinen Controls).
- Hero: Headline höchstens zwei Zeilen, Subtext höchstens 20 Wörter, ein primärer und höchstens ein sekundärer CTA, höchstens vier Textelemente.
- Kein `transition-all`, keine Endlosanimation auf etwas, das nicht live ist, kein `hover:scale` auf Karten. Jede Bewegung respektiert `prefers-reduced-motion`.
- Kontrast mindestens 4,5:1 für Text, auch auf Akzent-Buttons, Platzhaltern und Fehlertexten.
- Nichts erfinden: keine Features, Kennzahlen, Kundenlogos oder Zitate. Unprüfbare Behauptungen ("10.000+ Teams", "10x schneller") erfragen, sonst entfernen.
- Entfernte Deko nicht durch neue Deko ersetzen und keinen Trend gegen den nächsten tauschen (Glass, Grain, Noise, Neon, Bento als Selbstzweck).
- Nicht für jedes Produkt denselben Look. Die Richtung entscheidet Tönung, Schrift und Visual, nicht die Gewohnheit.

## Widersprüche der Quellen

Beide Quellen widersprechen sich an mehreren Stellen. Die Entscheidungen hier gelten, Begründung je Punkt in `references/entscheidungen.md`. Die wichtigsten:

- **Icons:** vorhandenes Set zuerst. shadcn-Projekte behalten lucide. Neu gewählt wird Phosphor oder Tabler.
- **Schrift:** Inter nur für neutrale, App- oder Barrierefreiheits-Briefs. Fraunces und Instrument Serif nicht als Default, Serif nur bei echtem Editorial- oder Heritage-Charakter.
- **Bewegung:** unslops Zurückhaltung schlägt taste's Dial-Defaults. Der Dial bestimmt nur, *wie viel* motivierte Bewegung es gibt, nie ob `transition-all` oder Spring-Loops erlaubt sind.
- **Produktvorschau:** Nachgebaute Vorschau aus echten Projektkomponenten mit plausiblen Daten ist erlaubt. Verboten bleiben Div-Rechtecke als Fake-Screenshot, Fake-Terminals und Versions-Footer.
- **Hero-Abstand oben:** höchstens 96px auf Desktop.

## Bericht

```
Modus: L | A     Ausmaß: schwer | leicht | kein Slop
Design Read: Reading this as: ...
Dials: VARIANCE x / MOTION y / DENSITY z (nur Modus L)
Richtung: Produkt / Charakter / Welt / Momente / Signatur (je eine Zeile)

Audit: | Nr | ID | Ort | Befund | Status (behoben / offen + Grund) |

Durchgänge: je Durchgang zwei bis drei Zeilen, was sich geändert hat
Offen: unbestätigte Behauptungen, fehlende Bilder (Slot, Größe, Prompt), Annahmen
Geprüft: Pre-Flight bestanden x/y, Screenshots (1440 hell/dunkel, 390)
```

## Abgrenzung

- Bewegung im Detail (Timing, Springs, Gesten): `emil-design-eng`, `motion-design`. Fehlende UX-Details (Skeletons, Undo, Safe Areas): `ux-details-audit`. Barrierefreiheit im Ganzen: `accessibility`. Ladezeit: `web-quality-audit`.
- Redesign mit IA- und SEO-Risiko: zusätzlich `redesign-existing-projects` (Audit-Teil). Längere Fließtexte: `humanizer`.
- Logo neu entwerfen: `logo-design`. Hier wird ein Slop-Logo nur flach gezogen.
- Eine Story-Video-Funktion wie im Original-unslop gibt es hier nicht.

## Referenzen

- `references/slop-katalog.md`: alle Slop-Merkmale mit ID, Suchmuster und Fix
- `references/richtung.md`: Design Read, Dials, fünf Zeilen Richtung, Design-System-Wahl
- `references/durchgaenge.md`: Regeln je Durchgang, Layout-Disziplin für Landing Pages
- `references/tokens.md`: Abstandsskala, Neutral-Rampen, Typo, Radien, Bewegung
- `references/visuals.md`: Visual wählen, Bildgenerierung, Platzhalter
- `references/preflight.md`: abhakbare Abschlussprüfung mit Kommandos
- `references/entscheidungen.md`: alle aufgelösten Widersprüche mit Begründung
