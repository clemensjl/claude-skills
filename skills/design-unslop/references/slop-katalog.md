# Slop-Katalog

Jede Gruppe durchgehen, jeden Fund mit ID und Ort notieren. Jede Zeile: **Merkmal** (prüfbar), **Suche** (Muster für `rg -n`, Tailwind und CSS), **Fix**. Suchtreffer sind Hinweise; Befund ist erst, was am Screenshot sichtbar ist. Fehlende Treffer beweisen nichts, deshalb jede Gruppe auch am Screenshot prüfen.

Spalte **Modus**: `L` nur Landing/Portfolio, `A` nur App/Dashboard, ohne Angabe beide.

Herkunft: `[u]` unslop, `[t]` taste-skill, `[u+t]` beide.

## F: Fläche und Farbe

- **F1** Verlauf von einem Farbton zum anderen (violett nach blau, violett nach pink) auf Hintergrund, Karte, Button oder aktivem Nav-Eintrag `[u+t]`. Suche: `bg-gradient-to-|bg-linear-to-|linear-gradient\(|from-(purple|violet|indigo|fuchsia|pink)`. Fix: eine Neutralfläche, Akzent nur wo er etwas bedeutet. Erlaubt ist nur ein Tonwertschritt innerhalb eines Neutraltons (#2b2b2b nach #1f1f1f).
- **F2** Verlaufstext in Headline, Zahl oder Logo `[u+t]`. Suche: `bg-clip-text|text-transparent|background-clip:\s*text`. Fix: einfarbig in der primären Textfarbe.
- **F3** Farbige Glows, farbige Schatten, `drop-shadow` auf Emoji oder Pills `[u+t]`. Suche: `shadow-\[0_0_|shadow-(purple|violet|indigo|blue|pink)-|drop-shadow|box-shadow:[^;]*rgba\((1[0-9]{2}|2[0-9]{2}),\s*\d+,\s*2[0-9]{2}`. Fix: entfernen. Tiefe über Flächenstufen und Haarlinien (dunkel) bzw. kleine neutrale Schatten (hell).
- **F4** Radiale Farbwolken, verschwommene Blobs hinter Inhalt, Mesh- oder Aurora-Hintergrund ohne Markenbezug `[u+t]`. Suche: `blur-(2xl|3xl)|radial-gradient|filter:\s*blur\(\d{2,}`. Fix: entfernen.
- **F5** Neon- oder kontraststarke farbige Rahmen `[u+t]`. Suche: `border-(purple|violet|cyan|fuchsia)-[4-6]00|border-color:\s*#[a-f0-9]{6}` mit gesättigter Farbe. Fix: Haarlinie, primäre Textfarbe bei 6 bis 10 % Deckkraft.
- **F6** Viele fast gleiche Tönungen derselben Farbe für Text (fünf Lavendeltöne) `[u]`. Prüfung: alle Textfarben zählen. Mehr als drei Rollen plus Akzent und Semantik ist ein Befund. Fix: drei Textrollen aus einer Rampe.
- **F7** Alles hervorgehoben, nichts sticht heraus; Akzent auf mehr als drei Elementtypen je Screen `[u]`. Fix: ein Akzent, ein- bis zweimal je Screen.
- **F8** Mehrere Akzentfarben auf einer Seite, Akzentwechsel zwischen Abschnitten `[t]`. Fix: ein Akzent, auf der ganzen Seite gesperrt.
- **F9** Glass-Karten mit weißem Innenlicht und farbigem Schatten, `backdrop-blur` ohne Anlass `[u+t]`. Suche: `backdrop-blur|backdrop-filter`. Fix: einfache erhöhte Fläche mit Haarlinie. Glass nur, wenn der Brief es ausdrücklich verlangt.
- **F10** Reines `#000000` oder `#ffffff` als Fläche `[t]`. Suche: `#000000|#000\b|bg-black\b|#ffffff|#fff\b|bg-white\b` (Treffer für Text auf Akzent prüfen, nicht blind ersetzen). Fix: Off-Black und Off-White aus der Rampe.
- **F11** Übersättigter Akzent (Sättigung über 80 %) `[t]`. Fix: entsättigen, bis er zu den Neutraltönen passt, Kontrast halten.
- **F12** KI-Lila als Default ohne Markenbezug `[u+t]`. Fix: Akzent aus der Welt des Produkts (siehe `tokens.md`). Ist die Marke wirklich lila, bleibt sie lila, aber ohne Glow und Verlauf.
- **F13** Premium-Consumer-Default `L`: Creme- oder Papierhintergrund plus Messing, Ton, Ochsenblut oder Ocker plus Espresso-Text `[t]`. Suche: `#f5f1ea|#f7f5f1|#fbf8f1|#efeae0|#ece6db|#faf7f1|#e8dfcb|#b08947|#b6553a|#9a2436|#9c6e2a|#bc7c3a|#7d5621|#1a1714|#1a1814|#1b1814`. Fix: andere Palettenfamilie (`tokens.md`), außer die Marke nennt diese Farben.
- **F14** Abschnitt kippt mitten auf der Seite ins andere Theme (helle Creme-Sektion auf dunkler Seite) `[t]`. Fix: ein Theme pro Seite, Tonwertstufen innerhalb desselben Themes sind erlaubt.
- **F15** Flächen in Apps und Dashboards wirken farbig (Hintergrund liest sich orange, braun, blau, grün) `A` `[u]`. Fix: Graphit-Rampe oder gleich graue; Farbe gehört in Akzent, Charts und Momente.

## T: Typografie

- **T1** Headlines in 700 bis 900 `[u]`. Suche: `font-(bold|extrabold|black)|font-weight:\s*(700|800|900)`. Fix: 400 bis 500, Hierarchie über Größe und Farbe; 600 für seltene Betonung.
- **T2** Versal-Labels mit weiter Laufweite (`NAVIGATION`, `PAID THIS MONTH`, Eyebrows) `[u+t]`. Suche: `uppercase.*tracking-|tracking-\[0\.[12]|letter-spacing:\s*0\.[1-3]em|text-transform:\s*uppercase`. Fix: Satzschreibung mit normaler Laufweite. Eyebrows zusätzlich zählen, siehe L7.
- **T3** Zu viele Größen und Gewichte auf einem Screen (mehr als sechs Größen oder mehr als drei Gewichte) `[u]`. Fix: Größen aus der Skala, Gewichte 400 und 500.
- **T4** Zahlen in gemischten Formaten (`$48,210` neben `$124,860.40`, führende Null `07`) ohne `tabular-nums` `[u]`. Suche: fehlendes `tabular-nums|font-variant-numeric`. Fix: ein Format, Tabellenziffern.
- **T5** Negative Laufweite auf Text unter 16px `[u]`. Suche: `tracking-(tight|tighter)` an kleinen Größen, `letter-spacing:\s*-`. Fix: 0 oder leicht positiv; enge Laufweite nur ab 40px.
- **T6** Kursiv zur Betonung im Fließtext und in Labels `[u]`. Fix: Farbe oder Gewicht. Ausnahme in Display-Headlines mit Editorial-Charakter, dann T9 beachten.
- **T7** Inter als ungewählter Default `L` `[t]`. Suche: `Inter\b|font-sans` ohne eigene Konfiguration. Fix: Familie nach Charakter (`tokens.md`). Inter bleibt bei neutralem, Linear-artigem, Behörden- oder App-Brief und wenn es Markenschrift ist.
- **T8** Serif als Reflex für "kreativ" oder "premium", insbesondere Fraunces oder Instrument Serif `L` `[t]`. Suche: `Fraunces|Instrument.?Serif|font-serif`. Fix: Sans-Display; Serif nur bei echtem Editorial-, Luxus-, Heritage-Charakter mit Begründung, dann aus dem Pool in `tokens.md`.
- **T9** Kursives Wort mit Unterlänge (y g j p q) in Display-Type mit `leading-none` oder `leading-[1]`, Unterlänge abgeschnitten `[t]`. Fix: mindestens `leading-[1.1]` plus `pb-1`.
- **T10** Fremde Familie für ein einzelnes betontes Wort in der Headline (ein Serif-Wort in Sans-Headline) `[t]`. Fix: Betonung in derselben Familie über Farbe oder Gewicht.
- **T11** H1, die nur schreit: über fünf Wörter in `text-7xl` und größer `L` `[t]`. Fix: `text-4xl md:text-5xl lg:text-6xl`, `text-6xl md:text-7xl` nur bei drei bis fünf Wörtern.

## I: Icons

- **I1** Emoji als Nav-Icon, Label-Deko oder Status (🏠 📥 🚀 💰 ⚠️ 📈 🔥 ✨) `[u+t]`. Suche: `rg -nP "[\x{1F300}-\x{1FAFF}\x{2600}-\x{27BF}\x{2B50}]"`. Fix: ein Line-Icon aus einem Set oder gar nichts.
- **I2** Emoji in Pills und Zählern (`18 👤`) `[u]`. Fix: nackte Zahl.
- **I3** Icons in mehreren Größen, Strichstärken oder Eigenfarben `[u+t]`. Fix: eine Größe (16 oder 18px), eine Strichstärke (1.5), Farbe der Textrolle.
- **I4** Icons aus der Spalte gerückt, unterschiedliche Icon-Box-Breiten `[u]`. Fix: gleiche Box-Breite in jeder Zeile, fester Abstand 8 oder 10 zum Label.
- **I5** Sparkle für alles mit KI `[u]`. Fix: entfernen oder ein schlichtes Icon nur wo es etwas erklärt.
- **I6** Mehrere Icon-Bibliotheken im selben Baum `[t]`. Suche: Imports aus `lucide-react`, `@phosphor-icons`, `@tabler/icons`, `react-icons`, `@heroicons` zugleich. Fix: eine Familie.
- **I7** Handgezeichnete SVG-Icon-Pfade `[t]`. Suche: `<path d=` in Komponenten, die Icons darstellen. Fix: Icon aus der Bibliothek. Ein einfaches geometrisches Logozeichen ist davon ausgenommen.

## A: Abstände

- **A1** Beliebige Werte außerhalb des 4px-Rasters (`mt-[13px]`, `py-[11px]`, `h-[31px]`) `[u]`. Suche: `-\[\d+px\]` in Tailwind; in CSS `(padding|margin|gap|height|top|inset)[^;]*\d+px` und jeden Wert prüfen, der nicht durch 4 teilbar ist. Tailwind-Stufen mit `.5` (`p-1.5`, `gap-2.5`) ergeben 6 und 10px, sie sind nur in kleinen Controls in Ordnung. Fix: Stufe aus der Skala.
- **A2** Zeilen einer Liste mit unterschiedlicher Höhe oder unterschiedlichem Abstand `[u]`. Fix: eine Höhe, ein Abstand.
- **A3** Gruppen stehen näher am Nachbarn als an den eigenen Einträgen `[u]`. Fix: innen kleiner als zwischen Gruppen (Section-Label 24 oben, 8 unten).
- **A4** Ungleiches Padding in Geschwisterkarten `[u]`. Fix: ein Padding.
- **A5** Großer Leerraum über einem Abschnitt, gequetscht darunter `[u+t]`. Fix: ausgewogener Rhythmus.
- **A6** Elemente mit Streu-`translate` oder Einzel-Margin aus der Linie geschoben `[u]`. Suche: `translate-[xy]-\[|-mt-\[|-ml-\[`. Fix: an der Fluchtlinie ausrichten.

## K: Copy und Text

- **K1** Begrüßungs-Headline (`Welcome back, Damir! 👋`, "Hallo Max!") `A` `[u]`. Fix: Kontext als Titel, Seitenname oder Zeitraum ("Oktober 2026").
- **K2** Ausrufezeichen in Oberflächentext, `!!` `[u]`. Suche: `rg -n "!['\"<]|!!"` in JSX und Strings. Fix: schlichte Aussage.
- **K3** Veränderung ohne Bezug (`+12%!!`, `3 weniger`) `[u]`. Fix: "+12 % ggü. Vormonat".
- **K4** Wortreiche Platzhalter (`Search anything...`, "Durchsuche alles...") `[u]`. Fix: "Suchen".
- **K5** Hype- und Füllwörter `[u+t]`. Suche (i): `supercharge|seamless|unlock|unleash|elevate|revolutioni|game.?chang|next.?gen|magic|effortless|AI.?powered|nahtlos|mühelos|revolutionär|entfessel|auf das nächste Level|KI.?gestützt|smart`. Fix: was das Ding konkret tut.
- **K6** Punkt am Ende von Headline, Label, Button, Caption `[u]`. Fix: ohne Punkt; nur mehrsätzige Absätze behalten ihn.
- **K7** Headline, die zu jedem Produkt passt ("Supercharge your workflow with AI", "Die Zukunft von X") `[u+t]`. Prüfung: Produktnamen gegen einen anderen tauschen. Passt es noch, ist es ein Befund. Fix: was das Produkt für wen tut, mit eigenen Substantiven.
- **K8** Unprüfbare Behauptungen (`Trusted by 10,000+ teams`, `10x faster`, fünf Sterne ohne Quelle) `[u+t]`. Suche: `\d+[.,]?\d*\+|10x|\bx faster|Trusted by|Loved by|★{3,}`. Fix: Nutzer fragen; echt: ruhig und konkret, sonst entfernen. Im Bericht listen.
- **K9** Gedankenstrich als Stilmittel oder Trenner in sichtbarem Text `[t]`. Suche: `—|–` (auch `&mdash;|&ndash;`). Fix: Punkt, Komma, Doppelpunkt, Klammer; Bereiche mit Bindestrich.
- **K10** KI-Kauderwelsch: schief klingende Wortspiele, unklare Bezüge, pseudo-poetische Mikro-Meta ("Die Liste bleibt mit Absicht kurz.") `[t]`. Prüfung: jeden sichtbaren String laut lesen. Fix: schlichter funktionaler Satz.
- **K11** Gemischte Register auf einer Seite (Terminal-Mono, Prosa, Marketing-Punch nebeneinander) `L` `[t]`. Fix: ein Register.
- **K12** Poetische Abschnittslabels ("Field notes", "Aus der Werkstatt", "Quietly trusted by") `L` `[t]`. Fix: funktionales Label ("Kundenstimmen") oder keins.
- **K13** Generische Schrittlabels (Step 1, Stage 1, Phase 01) `[t]`. Fix: das Verb ist das Label ("Installieren", "Einrichten").
- **K14** Doppelte CTA-Absicht ("Kontakt" plus "Lass uns reden" plus "Projekt starten") `L` `[t]`. Fix: ein Label je Absicht, überall gleich.

## D: Daten und Inhalte

- **D1** Fake-Daten mit Platzhaltercharakter (`$123,456`, `[X]`, `1234567`, `99.99%`, `50%`) `[u+t]`. Suche: `123[,.]?456|\[X\]|99\.99|1234567|Lorem`. Fix: plausible, unrunde Werte; Mock-Daten als solche markieren.
- **D2** Erfundene Präzision auf Marketingseiten (`92 %`, `4.1×`, `5.8 mm`) ohne Quelle `L` `[t]`. Fix: aus echten Daten oder weg.
- **D3** Generische Namen und Marken (John Doe, Jane Doe, Max Mustermann, Acme, Nexus, SmartFlow, Cloudly) `[t]`. Suche: `John Doe|Jane Doe|Mustermann|Acme|Nexus|SmartFlow|Cloudly|Lorem`. Fix: realistische, ortsübliche Namen.
- **D4** Generische Avatare (Ei-SVG, User-Icon im Kreis) als Personenbild `[t]`. Fix: glaubwürdiger Platzhalter oder Initialen.

## B: Bauteile

- **B1** Leuchtende Pills für Zähler, Pläne, Shortcuts, Status `[u]`. Fix: ruhiger Mono-Text oder Keycap.
- **B2** Badges `PRO`, `New ✨`, `Beta 🚀`, Versionslabels im Hero (`V0.6`, `EARLY ACCESS`) `[u+t]`. Fix: weg, außer das Produkt braucht sie wirklich; dann ruhiger Text.
- **B3** Alles Pill, von Suche bis Karte; oder Radien ohne Regel gemischt `[u+t]`. Suche: Anzahl `rounded-full` gegen Anzahl Elemente. Fix: Radius nach Größe, verschachtelte Radien, eine dokumentierte Regel.
- **B4** Charts mit Regenbogen-, Glow- oder Pill-Balken in einer Serie, Versal-Tageslabels `[u]`. Fix: eine bis zwei Serien, gedämpftes Raster, Mono-Labels, eine Hervorhebungsfarbe.
- **B5** Jede Serie in Akzentabstufungen, nichts führt `[u]`. Fix: Neutralstufen, Akzent nur auf dem Entscheidenden.
- **B6** Sparklines, Strichlisten, Mini-Balken in jeder Stat-Karte `A` `[u]`. Fix: Label, große Zahl, Veränderung mit Bezug.
- **B7** Gleich breite Karten nebeneinander mit gleichem Inhalt, drei gleiche Feature-Karten `[u+t]`. Fix: ein Hauptchart plus kompakte Stats, variierende Breiten; auf Landing Pages asymmetrisches Raster oder anderer Layouttyp.
- **B8** Logo als Verlaufskachel mit Sparkle, Verlaufs-Wortmarke, glänzende Kugel `[u]`. Fix: Produktname als Text in der Hauptfamilie plus einfaches flaches Zeichen.
- **B9** Farbige Status-Punkte vor jedem Nav-Eintrag, jeder Zeile, jedem Badge `[u+t]`. Fix: null Deko-Punkte; nur für echten Zustand, höchstens einer je Abschnitt.
- **B10** Pills oder Tags über Bildern (`Brand · 02`), Deko-Bildunterschriften (`Plate 03 · Archive`) `L` `[t]`. Fix: Bild für sich oder funktionale Unterschrift darunter.
- **B11** `border-t` und `border-b` an jeder Zeile langer Listen oder Spec-Tabellen `L` `[t]`. Fix: gruppieren, sparsame Trenner oder Karten je Spezifikation.
- **B12** Fortschrittsbalken mit gefüllter Hintergrundspur als Vergleichsvisual auf Marketingseiten `L` `[t]`. Fix: Zahl plus kleiner Balken ohne Spur.
- **B13** Logo-Wand mit Text-Wortmarken statt Logos oder mit Kategorielabel unter jedem Logo `L` `[t]`. Fix: echte SVG-Logos (Simple Icons) nur mit Erlaubnis bzw. echten Kunden, ohne Labels.
- **B14** Fehlende Zustände: nur der Erfolgsfall gebaut, kein Hover, kein sichtbarer Fokus, kein Laden, Leer, Fehler `[u+t]`. Fix: alle Zustände in der Palette, Fokusring sichtbar.
- **B15** Placeholder als Label in Formularen `[t]`. Fix: Label über dem Feld, Fehler darunter.

## H: Hero und Landing (Modus L)

- **H1** Pill-Badge über der Headline (`✨ Introducing X 2.0`) `[u+t]`. Fix: entfernen oder ruhiger Textlink bei echter Neuigkeit.
- **H2** Verlauf oder Shimmer auf der Headline `[u+t]`. Fix: einfarbig.
- **H3** Blobs, Orbs, Raster und Leuchtlinien hinter dem Hero `[u+t]`. Fix: ruhiger Hintergrund oder ein echtes Produktvisual.
- **H4** Alles zentriert gestapelt (Headline, Text, Buttons, Bild darunter) bei `DESIGN_VARIANCE` über 4 `[u+t]`. Fix: asymmetrischer Split oder Text über großer Produktansicht. Ausnahme: kurzes Manifest ohne Visual.
- **H5** Drei oder mehr Buttons, Chips und Avatare unter den Buttons `[u+t]`. Fix: ein primärer, höchstens ein sekundärer CTA.
- **H6** Mehr als vier Textelemente im Hero: Tagline unter den CTAs, Trust-Streifen, Preis-Teaser, Feature-Bullets, Avatar-Reihe `[t]`. Fix: in den Abschnitt direkt darunter.
- **H7** Headline über zwei Zeilen, Subtext über 20 Wörter, CTA erst nach Scrollen sichtbar `[t]`. Fix: kürzen oder Schriftgröße senken.
- **H8** Hero-Padding oben über 96px, Inhalt schwebt mitten im Viewport; oder tote Leerfläche im ersten Screen `[u+t]`. Suche: `pt-(2[8-9]|3[0-9]|4[0-9])|pt-\[1[0-9]{2}px\]`. Fix: höchstens 96px, ersten Screen als Ganzes komponieren.
- **H9** `h-screen` für den Hero `[t]`. Suche: `h-screen|height:\s*100vh`. Fix: `min-h-[100dvh]`.
- **H10** Deko-Textstreifen am Hero-Ende (`DESIGN · BUILD · SHIP`), Orts- und Uhrzeitstreifen, Scroll-Hinweis (`Scroll to explore`, Mausrad-Icon) `[t]`. Fix: entfernen.
- **H11** Feature-Karten mit Emoji, fetter Überschrift und vager Zeile `[u+t]`. Fix: weniger Features, konkrete Copy, Line-Icons oder keine.
- **H12** Hero ohne echtes Visual: Text plus Verlaufsblob oder leere Box `[u+t]`. Fix: siehe `visuals.md`.
- **H13** Navigation zweizeilig auf Desktop, höher als 80px, Login als zweiter Button `[u+t]`. Fix: eine Zeile, 64 bis 72px, Login als ruhiger Textlink.

## L: Seitenlayout (Modus L)

- **L1** Abschnittslayout wiederholt sich: dieselbe Familie (Drei-Karten-Reihe, Split Text/Bild) mehr als einmal; unter vier Familien bei acht Abschnitten `[t]`. Fix: Layoutfamilien variieren.
- **L2** Dritter Zickzack-Split in Folge `[t]`. Fix: Muster brechen (volle Breite, Stapel, Raster).
- **L3** Bento mit leerer Zelle oder mehr Zellen als Inhalt `[t]`. Fix: Zellenzahl gleich Inhaltszahl.
- **L4** Bento aus lauter gleichen Textkarten auf gleicher Fläche `[t]`. Fix: zwei bis drei Zellen mit echtem Inhalt als Variation (Bild, Produktdetail, Chart, Flächenstufe der Rampe). Kein Hue-Verlauf als Variation.
- **L5** Split-Header: links große Headline, rechts kleiner Erklärabsatz, oder schwebender Text oben rechts `[t]`. Fix: Headline und Text untereinander, max. 65ch.
- **L6** Mehr als ein Marquee pro Seite `[t]`. Fix: höchstens eins.
- **L7** Eyebrow über fast jedem Abschnitt, Abschnittsnummern als Eyebrow (`001 · Capabilities`, `06 / how it works`), `01 / 4` auf Bildern `[u+t]`. Zählregel: Eyebrows höchstens `ceil(Abschnitte / 3)`, Hero zählt mit. Fix: streichen, die Headline reicht.
- **L8** Lange Liste (über fünf Einträge) als Standard-`<ul>` mit `divide-y`, Datendump-Tabelle auf Marketingseite `[t]`. Fix: gruppieren, Top 3 bis 5 plus "Alle anzeigen", passendere Komponente.
- **L9** Zitat über drei Zeilen, Zuschreibung nur Vorname `[t]`. Fix: kürzen, Name plus Rolle.
- **L10** Visual auf jedem Abschnitt `[u]`. Fix: ein Visual dort, wo es hilft, meist nur im Hero.

## V: Visuals

- **V1** Glänzende 3D-Blobs, Orbs, Liquid Chrome, violette Nebel als Hero-Visual `[u+t]`. Fix: das Produkt selbst oder eine konkrete Metapher.
- **V2** Stock-Roboter, leuchtende Gehirne, Leiterbahnen, Hologramme für KI `[u]`. Fix: zeigen, was die KI tatsächlich erzeugt.
- **V3** Text, Fake-Buttons oder Fake-Logo im Bild eingebrannt `[u]`. Fix: echter Text in der Seite, Bild ohne Text.
- **V4** Bild mit harter Kante und anderem Schwarz als die Seite `[u]`. Fix: Hintergrund angleichen, weiche Maske.
- **V5** Fake-Produkt-UI aus Div-Rechtecken, Fake-Terminal, Fake-Dashboard, Versions-Footer (`v0.6.2-rc.1`, `last sync 4s ago`) `[t]`. Fix: echter Screenshot, generiertes Bild oder echte Mini-Komponente mit plausiblen Daten (siehe `entscheidungen.md`).
- **V6** Deko-SVG-Illustrationen von Hand `[t]`. Fix: weg oder echtes Bild.
- **V7** Kaputte Bild-URLs, beschriftete Platzhalter im ausgelieferten Stand ("Hero image here") `[u+t]`. Fix: siehe `visuals.md`, Platzhalter ohne Text.

## M: Bewegung

- **M1** `animate-pulse`, `animate-ping`, `animate-bounce`, atmende Glows auf Dingen, die nicht live sind `[u+t]`. Suche: `animate-(pulse|ping|bounce|spin)|@keyframes.*(pulse|glow|float|breath)`. Fix: statisch. Skeleton-Shimmer während echtem Laden ist erlaubt.
- **M2** `transition-all` `[u]`. Suche: `transition-all|transition:\s*all`. Fix: benannte Eigenschaften (`transition-colors`, `transition-[transform,opacity]`).
- **M3** `hover:scale` auf Karten, Bewegung über wenige Pixel bei Hover `[u]`. Suche: `hover:scale-|hover:-translate-y-[2-9]`. Fix: Farb- oder Flächenstufe beim Hover, kleines Skalieren (0.97 bis 0.98) beim Drücken.
- **M4** Federnde Springs und Overshoot in einfacher UI `[u]`. Suche: `type:\s*["']spring|bounce|cubic-bezier\([^)]*1\.[0-9]`. Fix: eine Ease-out-Kurve. Springs nur für Gesten und Drag.
- **M5** Alles fliegt beim Laden aus verschiedenen Richtungen ein `[u+t]`. Fix: ein kurzes Fade-and-Rise für den Hauptinhalt, kleiner Stagger.
- **M6** Parallax, schwebende Loops, Elemente, die beim Scrollen wandern, ohne Grund `[u+t]`. Fix: statisch, oder bei `MOTION_INTENSITY` ab 8 mit benanntem Zweck.
- **M7** Animation von `width`, `height`, `top`, `left`, Margins, großen Blurs `[u+t]`. Fix: `transform` und `opacity`.
- **M8** Kein `prefers-reduced-motion` `[t]`. Suche: fehlendes `prefers-reduced-motion|useReducedMotion|motion-reduce:`. Fix: Schleifen, Parallax, Scroll-Hijack fallen bei `reduce` auf statisch.
- **M9** `window.addEventListener('scroll'`, Scroll-Position in React-State `[t]`. Suche: `addEventListener\(\s*['"]scroll|setScroll|window\.scrollY`. Fix: `useScroll`, ScrollTrigger, IntersectionObserver oder CSS Scroll-driven Animations.
- **M10** Eigener Mauszeiger `[t]`. Suche: `cursor:\s*url|cursor-none`. Fix: Systemcursor.
- **M11** Mehrere Easing-Kurven und beliebige Dauern quer über den Screen `[u]`. Fix: eine Kurve, wenige Dauern (`tokens.md`).

## X: Template-Look (nach dem Umbau prüfen)

Kein Slop im engeren Sinn, aber das, worauf ein bereinigter Screen zurückfällt, wenn niemand entschieden hat `[u+t]`.

- **X1** Reines Grau `#161616`, Inter, weißer Text, alte Markenfarbe auf einem Button, bei einem Produkt mit warmer oder heller Welt. Fix: getönte Rampe und Akzent aus der Welt.
- **X2** Headline passt nach Namenstausch zu einem anderen Produkt. Fix: eigene Substantive.
- **X3** Hero-Visual ist eine leere Box oder ein beliebiges Bild. Fix: Produktvorschau oder Bild aus der Welt.
- **X4** Inter plus `slate-900`, drei gleiche Karten, zentrierter Hero auf dunklem Mesh. Das ist der LLM-Default. Fix: die Richtung entscheiden lassen.
- **X5** Derselbe Look wie das letzte Projekt (gleiche Palette, gleiche Serif, gleiches Layout). Fix: Palettenfamilie und Schrift wechseln.

---

Teile dieses Katalogs sind übersetzt und angepasst aus unslop von Damir Sokolovsky ([@heydamir](https://x.com/heydamir), github.com/heydamir/unslop), CC BY 4.0, und aus taste-skill von Leonxlnx (MIT). Diesen Hinweis in Kopien und Bearbeitungen behalten.
