# Tokens

Startwerte für die Durchgänge. Hat das Projekt ein gutes System oder eine `DESIGN.md`, deren Werte behalten und nur die Verwendung korrigieren. Kein Hausstil: die Richtung darf die Werte verschieben.

## Abstandsskala `[u]`

4, 8, 12, 16, 20, 24, 32, 40, 48, 64, 80, 96, 128

- In einem Control: 4 bis 12
- Zwischen verwandten Elementen (Listenzeilen): 2 bis 8
- Zwischen Gruppen (Label und Liste, zwei Karten): 12 bis 24
- Zwischen Abschnitten: 32 bis 64 in Apps, auf Landing Pages nach `VISUAL_DENSITY` (1 bis 3: 96 bis 128, 4 bis 7: 64 bis 96)
- Zeilenhöhen: 32 kompakt, 36 Standard, 40 bis 44 Touch
- Hero: Navigation bis Headline 64 bis 96 Desktop, 48 bis 64 mobil

## App-Layout `[u]`

- Sidebar 240 bis 280, Inhalt fluid mit Seitenpadding 24 bis 32, gedeckelt um 1440 bis 1600.
- Topbar oder Seitenkopf 56 bis 64.
- Nav-Zeilen 32 bis 36, Abstand 2 bis 4, Section-Labels 24 oben, 8 unten.
- Stat-Karten einer Reihe teilen die Höhe, meist drei oder vier.
- Hauptchart mindestens zwei Drittel der Inhaltsbreite, 280 bis 360 hoch. Daneben Liste oder Tabelle, schmaler.

## Neutral-Rampen `[u]`

Apps und Dashboards: Graphit oder gleich grau für alle Flächen. Landing Pages: die Rampe, deren Tönung zur Welt passt. Warm für Papier, Holz, Essen, Handwerk, Menschliches. Ink für Nacht, Himmel, Wasser, Technisches. Eigene Rampen gleich tönen, Sättigung sehr niedrig, so dass eine Fläche nie für sich als Farbe liest.

Achtung `[t]`: Die helle Warm-Rampe liegt nah an der verbotenen Premium-Consumer-Familie (Katalog F13). Für Premium-Consumer-Briefs nicht als Default nehmen, nur wenn die Welt wirklich Papier oder Essen ist und kein Messing-Akzent dazukommt.

### Dunkel

| Rolle | Graphit | Warm | Ink |
| --- | --- | --- | --- |
| Tiefste Fläche (Sidebar) | #0f0f10 | #12110f | #07080d |
| Seitenhintergrund | #141415 | #161513 | #0b0d14 |
| Karte | #19191b | #1c1a18 | #11141c |
| Erhöht (aktive Zeile, Input) | #232325 | #262421 | #1a1e28 |
| Haarlinie | Primärtext 8 % | Primärtext 8 % | Primärtext 8 % |
| Primärtext | #ededed | #efe9de | #eef0f5 |
| Sekundärtext | #a1a1a6 | #aaa398 | #a3a9b8 |
| Gedämpft, Icons | #85858b | #8a847a | #7a8296 |

### Hell

| Rolle | Graphit | Warm | Ink |
| --- | --- | --- | --- |
| Seitenhintergrund | #fafafa | #f7f4ee | #f5f7fa |
| Karte | #ffffff* | #fdfbf7 | #ffffff* |
| Erhöht (aktive Zeile, Input) | #f4f4f5 | #efe9df | #eceff4 |
| Haarlinie | Primärtext 8 % | Primärtext 8 % | Primärtext 8 % |
| Primärtext | #171717 | #1f1b16 | #111827 |
| Sekundärtext | #525252 | #5e554a | #4b5565 |
| Gedämpft, Icons | #737373 | #7b7266 | #6b7487 |

\* Reines Weiß nur als Karte auf getöntem Seitenhintergrund, nie als Seitenfläche (Katalog F10).

Gedämpfter Text nur für Meta und Captions, um 4,5:1 auf seiner Fläche. Fließtext primär oder sekundär.

Semantik, gedämpft: positiv #4cc38a dunkel, #16a34a hell; negativ #e5484d dunkel, #dc2626 hell.

## Akzent `[u+t]`

- Echte Markenfarbe behalten. Ein Hue-zu-Hue-Glow-Verlauf ist keine Markenfarbe.
- Ohne Marke aus der Welt: warm Bernstein, Koralle, Glutorange; kühl Kobalt, Petrol, klares Himmelblau; natürlich Moos, Salbei. Violett-Blau meiden, außer die Marke ist wirklich lila.
- Sättigung unter 80 %, Text auf Akzent mindestens 4,5:1.
- Akzent auf wenigen Prozent der Fläche.
- Palettenfamilien für Premium-Consumer statt Creme plus Messing `[t]`, rotieren: Cold Luxury (Silbergrau, Chrom, Rauch), Forest (Tiefgrün, Knochen, Bernstein), Schwarz und Tan, Kobalt plus Creme ohne Messing, Terrakotta plus Schiefer, Oliv plus Ziegel plus Papier, Monochrom plus ein satter Akzent.

## Buttons `[u]`

- Hero-Buttons 44 bis 48 hoch, Nav-Buttons 32 bis 36, seitlich 16 bis 20 Padding.
- Primär dunkel: Off-White aus der Rampe mit dunklem Text oder Akzent. Primär hell: Primärtextfarbe als Fläche mit hellem Text oder Akzent.
- Sekundär: erhöhte Fläche mit Haarlinie, Primärtext.
- Auf dunklen Buttons gibt `inset 0 1px 0 rgba(255,255,255,0.12)` Tiefe ohne Glow.

## Schriftfamilien `[u+t]`

Nach Charakter wählen. Alle frei verfügbar.

| Charakter | Oberfläche | Optionaler Partner |
| --- | --- | --- |
| Präzise, technisch, ruhig | Geist, IBM Plex Sans, Inter (nur Modus A oder neutraler Brief) | Geist Mono, IBM Plex Mono, JetBrains Mono für Zahlen und Meta |
| Warm, freundlich, menschlich | Instrument Sans, DM Sans, Figtree, Outfit | Newsreader für die Hero-Headline, nur bei echtem Editorial-Anteil |
| Editorial, literarisch, handwerklich | Instrument Sans oder Geist für die Oberfläche | Serif aus dem Pool unten, begründet |
| Verspielt, kräftig | Space Grotesk, Bricolage Grotesque, Cabinet Grotesk | ein Mono für kleine Labels |
| Marke, Display ohne Serif | Satoshi, Cabinet Grotesk, General Sans | Geist Mono, JetBrains Mono |

Nicht als Default: Fraunces, Instrument Serif (die zwei LLM-Lieblingsserifen), Inter auf Landing Pages ohne neutralen Brief.

Serif-Pool, falls ein Serif begründet ist, nicht zweimal hintereinander dieselbe `[t]`: Newsreader, EB Garamond, Cormorant Garamond, Playfair Display, Recoleta, Tiempos Headline, PP Editorial New, GT Sectra Display, Reckless Neue, Canela, Domaine Display. Lizenzpflichtige Schriften nur, wenn das Projekt eine Lizenz hat.

Ein Display-Serif gehört nur an große Headlines, nie an Labels oder Buttons.

## Typo-Skala `[u]`

| Verwendung | Größe | Zeilenhöhe | Gewicht |
| --- | --- | --- | --- |
| Kleine Labels, Meta, Zähler | 12 | 16 | 400, Mono willkommen |
| Sekundärtext, Captions | 13 bis 14 | 20 | 400 |
| Fließtext, Nav-Einträge | 14 bis 16 | 20 bis 24 | 400 bis 500 |
| Logo-Wortmarke | 16 bis 18 | 1 | 500 bis 600 |
| Hero-Subhead | 18 bis 20 | 28 bis 30 | 400, Sekundärfarbe, höchstens 36rem breit |
| Kartenzahlen | 28 bis 32 | 1 | 500, tabular |
| Seitentitel | 28 bis 36 | 1.15 | 400 bis 500 |
| Hero-Headline | 48 bis 60 Desktop (bis 72 bei drei bis fünf Wörtern), 36 bis 44 mobil | 1.02 bis 1.08, mit Kursiv 1.1 | 400 bis 500 |

Laufweite 0 unter 16px, leicht positiv (0.01em) für kleinen gedämpften Text in Ordnung. Display ab 40px bis -0.02em, ab 56px bis -0.03em.

## Radien `[u]`

| Element | Radius |
| --- | --- |
| Keycap, Tag, kleiner Button | 4 bis 6 |
| Zeile, Input, Button | 8 bis 10 |
| Karte | 12 bis 16 |
| Panel, Fenster | 14 bis 20 |

Verschachtelt: innen = außen minus Padding, nie unter 4. Eine 16er-Karte mit 8 Padding enthält Elemente mit 8 Radius. Alternative Systeme (alles eckig, Pill nur für Interaktives) sind erlaubt, wenn sie als Regel festgelegt und überall befolgt werden `[t]`.

## Icons

16 oder 18px, Strichstärke 1.5, Farbe der gedämpften oder sekundären Textrolle, 8 bis 10 Abstand zum Label. Set nach `entscheidungen.md`.

## Tiefe `[u]`

- Dunkel: Flächenstufen plus Haarlinie. Aktive Zeile darf `inset 0 1px 0 rgba(255,255,255,0.12)` tragen.
- Hell: `0 1px 2px rgb(var(--shadow) / 0.05)` für Kleines, `0 8px 24px rgb(var(--shadow) / 0.06)` für Schwebendes, `--shadow` ist die dunkelste Stufe der Rampe.

## Bewegung `[u]`

Eine Kurve für alles: `cubic-bezier(0.22, 1, 0.36, 1)`.

| Verwendung | Dauer |
| --- | --- |
| Hover, Press, Toggles | 120 bis 180ms |
| Menüs, Popover, Tooltips | 160 bis 220ms |
| Einstiege, Sheets, Layoutwechsel | 300 bis 500ms |
| Stagger zwischen Elementen | 40 bis 60ms, höchstens sechs Elemente |

- Steigweg beim Einstieg 6 bis 12px. Press-Skalierung 0.97 bis 0.98.
- Nur Farbe, Hintergrund, Rahmen, Deckkraft, Transform.

---

Teile übersetzt und angepasst aus unslop von Damir Sokolovsky ([@heydamir](https://x.com/heydamir)), CC BY 4.0, und aus taste-skill von Leonxlnx (MIT).
