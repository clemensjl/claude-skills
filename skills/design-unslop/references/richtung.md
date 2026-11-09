# Richtung festlegen

Die Richtung kommt aus dem Produkt, nie aus dem, was gerade im Trend ist. Sie wird vor der ersten Codeänderung geschrieben und dem Nutzer gezeigt.

## 1. Signale lesen `[t]`

1. **Seitentyp:** Landing (SaaS, Consumer, Agentur, Event), Portfolio, Redesign, Editorial, App, Dashboard.
2. **Stimmungswörter** des Nutzers: "ruhig", "Linear-artig", "Awwwards", "verspielt", "seriös B2B", "Apple-artig".
3. **Referenzen:** verlinkte Seiten, Screenshots, genannte Produkte, Wettbewerber.
4. **Publikum:** Einkaufsgremium, designbewusste Konsumenten, Recruiter. Das Publikum wählt die Ästhetik, nicht der eigene Geschmack.
5. **Vorhandene Marke:** Logo, Farbe, Schrift, Fotografie. Bei Redesigns Ausgangsmaterial, nicht optional.
6. **Stille Randbedingungen:** Barrierefreiheit, Behörde, reguliert, Kinder, vertrauensbasierter Handel. Sie schlagen jede Geschmacksfrage.

Eine Marke ist echt, wenn sie nicht selbst Slop ist. Ein Violett-Blau-Verlauf, Sparkles und Glow bleiben Slop, auch wenn sie im Logo sitzen, außer der Nutzer sagt ausdrücklich, dass sie Marke sind `[u]`.

## 2. Design Read (eine Zeile) `[t]`

`Reading this as: <Seitentyp> für <Publikum>, mit <Stimmung>, Richtung <Design-System oder Ästhetikfamilie>.`

Ist der Brief wirklich mehrdeutig, genau eine Frage stellen, nie eine Liste ("Eher ruhig wie Linear oder experimentell wie eine Agenturseite?"). Lässt er sich sicher ableiten, nicht fragen.

## 3. Dials (nur Modus L) `[t]`

- `DESIGN_VARIANCE` 1 bis 10: 1 strenge Symmetrie, 10 Kunstchaos
- `MOTION_INTENSITY` 1 bis 10: 1 statisch, 10 filmisch
- `VISUAL_DENSITY` 1 bis 10: 1 Galerie, 10 Cockpit

| Signal / Anwendungsfall | VARIANCE | MOTION | DENSITY |
|---|---|---|---|
| Landing SaaS, Mainstream | 7 | 5 | 4 |
| Landing Agentur, kreativ | 9 | 7 | 3 |
| Landing Premium-Consumer | 7 | 5 | 3 |
| Portfolio Designer, Studio | 8 | 6 | 3 |
| Portfolio Entwickler | 6 | 4 | 4 |
| Editorial, Blog | 6 | 3 | 3 |
| "minimalistisch, ruhig, Linear-artig" | 5 bis 6 | 3 bis 4 | 2 bis 3 |
| Behörde, reguliert, Barrierefreiheit zuerst | 3 | 2 | 5 |
| Redesign, Marke erhalten | wie bisher | wie bisher | wie bisher |
| Redesign, neu aufsetzen | +2 | +1 | wie bisher |
| App, Dashboard (Modus A) | kein Dial | kein Dial | 5 bis 8 |

Die MOTION-Werte liegen ein bis zwei Stufen unter taste's Original, weil unslops Bewegungsregeln gelten (Begründung in `entscheidungen.md`). Die Werte werden genannt und begründet, nicht stillschweigend übernommen.

Was die Dials steuern:

- **VARIANCE 1 bis 3:** symmetrisches Raster, gleiche Abstände, zentriert. **4 bis 7:** Überlappungen, unterschiedliche Bildformate, linksbündige Headlines über zentrierten Daten. **8 bis 10:** asymmetrische Raster (`2fr 1fr 1fr`), große Leerzonen. Ab 4 fällt alles unter 768px auf eine Spalte.
- **MOTION 1 bis 3:** keine automatische Animation, nur Hover und Press. **4 bis 7:** ein Einstieg beim Laden, Scroll-Reveal auf zwei bis drei Schlüsselabschnitten, benannte Transitions. **8 bis 10:** Scroll-Choreografie (Sticky-Stack, Pin, Scrub), jede mit benanntem Zweck. Ab 4 muss die Seite sich wirklich bewegen; kann das nicht sauber gebaut werden, Dial auf 3 und eine ruhige statische Seite liefern.
- **DENSITY 1 bis 3:** Abschnittsabstände 96 bis 128. **4 bis 7:** 64 bis 96. **8 bis 10:** enge Paddings, keine Kartenrahmen, Linien trennen Daten, Zahlen in Mono.

## 4. Fünf Zeilen Richtung `[u]`

- **Produkt.** Was es tut und für wen, ein schlichter Satz.
- **Charakter.** Zwei bis drei konkrete Wörter, etwa `ruhig, genau, etwas warm` oder `schnell, technisch, verspielt`. Verboten: clean, modern, sleek, minimal, premium, hochwertig. Die beschreiben jedes Template.
- **Welt.** Ort oder Material, zu dem das Produkt gehört. Eine Notiz-App lebt bei Papier und Tinte, ein Monitoring-Tool bei Instrumenten und Nachtschicht, eine Reise-App bei Karten und Fensterlicht. Die Welt bestimmt Tönung der Neutralen, Akzent und Visual.
- **Momente.** Ein bis zwei Stellen, an denen der Screen reich wird: ein gerendertes Objekt in der Vorschau, ein Chart, dessen Farben je eine Serie bedeuten, ein Gegenstand aus der Welt neben dem Inhalt. Konkret benennen.
- **Signatur.** Ein kleines Detail, das nur dieses Produkt hätte, konsequent eingesetzt: Live-Status-Punkt beim Monitoring, Keycaps beim Entwicklerwerkzeug, Routenlinie bei der Lieferapp. Eins, nicht fünf.

Die Beispiele zeigen nur die Form. Die Antwort kommt aus dem Produkt, auch wenn ein Beispiel zufällig passt.

## 5. Fundament wählen `[t]`

Ein echtes Design-System hat Vorrang vor selbstgebautem CSS. Ein System pro Projekt, nie zwei mischen. Offizielle Pakete installieren, nicht nachbauen. Vor jedem Import `package.json` prüfen und fehlende Pakete mit Installationsbefehl nennen.

| Brief | Fundament |
|---|---|
| Projekt hat bereits ein System | das vorhandene |
| Moderne SaaS, eigene Komponenten, React | shadcn/ui (nie im Default-Zustand) oder Radix Themes |
| Microsoft-nah, Enterprise | Fluent UI (`@fluentui/react-components`) |
| IBM-artig, dichte Analytics | Carbon (`@carbon/react`) |
| GitHub-artiges Devtool | Primer |
| Behörde UK / US | `govuk-frontend` / `uswds` |
| Shopify-App | Polaris |
| Schnelles MVP für lokale Betriebe | Bootstrap 5.3 |
| Landing, Portfolio ohne System | Tailwind v4 plus Komponentenbibliothek, Ästhetik ehrlich benennen |

Eine Ästhetik (Bento, Editorial, Brutalismus, Glass) ist kein System. Dafür gibt es kein offizielles Paket; im Code ehrlich als Inspiration kennzeichnen.

Wenn eine `DESIGN.md` im Projekt-Root liegt, gilt sie vor den Tokens dieses Skills.

## 6. Redesign-Modus erkennen `[t]`

- **Neubau:** keine bestehende Seite oder ausdrücklicher Neuanfang.
- **Erhalten:** modernisieren ohne Markenbruch. Erst Markentokens auslesen.
- **Neu aufsetzen:** neue visuelle Sprache auf bestehendem Inhalt und bestehender IA.

Unklar: einmal fragen. Bei Redesigns nie ungefragt ändern: URL-Struktur, Nav-Labels, Formularfelder und ihre Reihenfolge, Logo, Rechts- und Consent-Texte, Analytics-relevante IDs und Buttontexte.

---

Teile übersetzt und angepasst aus unslop von Damir Sokolovsky ([@heydamir](https://x.com/heydamir)), CC BY 4.0, und aus taste-skill von Leonxlnx (MIT).
