# Die neun Durchgänge

Wie ein Designer beim Redline-Review: eine Ebene nach der anderen, jede über den ganzen Screen. Konkrete Werte stehen in `tokens.md`. Hat das Projekt ein gutes eigenes System, dessen Werte behalten und nur die Verwendung korrigieren.

## 1. Abstände `[u]`

- Alles auf dem 4px-Raster. Margins, Paddings, Gaps und feste Höhen sind Vielfache von 4; 28 oder 104 sind in Ordnung, auch wenn sie nicht in der Skala stehen. 2px nur für Feinjustierung in kleinen Controls. Ein ungerader Wert, der etwas exakt zentriert, bleibt.
- Gleiches gleich groß: alle Zeilen einer Liste eine Höhe und ein Abstand, alle Karten einer Reihe ein Padding.
- Abstand zeigt Gruppierung: innerhalb einer Gruppe kleiner als zwischen Gruppen.
- Fluchtlinien: Icons in einer Spalte, Labels auf einer Linie, Zahlen rechtsbündig in einer Spalte. Nichts mit Streu-`translate` verschoben.
- Padding folgt Dichte: kompakte Panels und Sidebars um 16, Karten 20 bis 24, Seitenränder 24 bis 32.
- Navigation ist der dichteste Teil einer App: Zeilen 32 bis 36 hoch, 2 bis 4 dazwischen, Section-Label 24 oben und 8 unten. Die Sidebar nach dem Durchgang nachmessen, dort bricht Abstand am häufigsten.
- Einzelwerte wie `mt-[13px]` durch Stufen der Skala ersetzen.
- Layout-Mechanik `[t]`: CSS Grid statt Flex-Prozentrechnung (`w-[calc(33%-1rem)]`), Container `max-w-7xl` oder `max-w-[1400px] mx-auto`, Standard-Breakpoints.

## 2. Farbe `[u+t]`

- Eine Neutral-Rampe, getönt zur Welt aus der Richtung. Hintergrund, erhöhte Flächen, Rahmen und Text kommen aus ihr. Eine Palette pro Projekt, kein Wechsel zwischen warmen und kalten Grautönen.
- **Modus A:** Flächen, Rahmen und Text bleiben neutral (Graphit oder gleich grau). Menschen sehen stundenlang darauf, die Farbe trägt der Inhalt. **Modus L:** Flächen dürfen weiter zur Welt getönt sein.
- Drei Textrollen: primär, sekundär, gedämpft.
- In der Chrome ein Akzent, selten eingesetzt: primäre Aktion, Auswahl, die eine Zahl, auf die es ankommt. Er gilt auf der ganzen Seite gleich.
- Die Momente sind die Ausnahme: dort darf Farbe reich sein (mehrere Farbtöne im Chart, ein Objekt mit echtem Material), solange sie in der Welt bleibt und jede Farbe etwas bedeutet.
- Echte Markenfarbe wird zum Akzent und verlässt die Flächen. Ohne Markenfarbe kommt der Akzent aus der Welt.
- Kontrast: Text auf Akzent mindestens 4,5:1, sonst Akzent abdunkeln oder dunklen Text nehmen. Akzent als Textfarbe auf heller Fläche braucht dasselbe, also eine dunklere Stufe.
- Dunkles Theme: primärer Button darf Off-White aus der Rampe mit dunklem Text sein, der Akzent lebt dann in Auswahl oder Kennzahl.
- Semantische Farben tragen nur Bedeutung (Grün für gut, Rot für Fehler) und sind gedämpft.
- Raus: Hue-Verläufe auf Flächen, Verlaufstext, farbige Glows und Schatten, Farbwolken, Neonrahmen.
- Rahmen: Haarlinie, primäre Textfarbe bei 6 bis 10 %.
- Tiefe: dunkel über Flächenstufen und Haarlinien, hell über kleine neutrale Schatten. Schatten nehmen die dunkelste Farbe der (getönten) Rampe, nie Akzentfarbe, nie reines Schwarz.
- Hell und dunkel `[t]`: Seiten für Endkunden in beiden Modi entwerfen (`prefers-color-scheme`), Tokens als CSS-Variablen oder `dark:`-Variante, eine Strategie pro Projekt. Ein Theme pro Seite, kein Abschnitt kippt. Ausnahme: Projekt hat bewusst nur ein Theme.

## 3. Icons `[u+t]`

- Jedes Emoji als Icon oder Label-Deko wird ein Line-Icon aus einem Set oder fällt weg. Ausnahme nur, wenn der Nutzer ausdrücklich einen verspielten, chatartigen Stil will.
- Welches Set: siehe `entscheidungen.md` (vorhandenes Set, bei shadcn lucide, sonst Phosphor oder Tabler). Eine Familie pro Projekt.
- Eine Größe, eine Strichstärke: 16 oder 18px, 1.5.
- Farbe der Textrolle, meist sekundär oder gedämpft. Keine Eigenfarben.
- Gleiche Icon-Box-Breite in jeder Zeile, fester Abstand 8 oder 10 zum Label.
- Icons, die nichts sagen, streichen (Emoji in jedem Kartentitel). Kategorien, die Farbe brauchen, bekommen einen kleinen Status-Punkt, nur wenn die Kategorie echten Zustand trägt.
- Keine handgezeichneten Icon-Pfade.

## 4. Copy `[u+t]`

- Headlines sagen, was das Produkt für wen tut, in einfachen Worten, so dass sie zu keinem anderen Produkt passen. Nur Fakten, die schon auf der Seite stehen.
- Keine Ausrufezeichen in Oberflächentext.
- Keine Begrüßungs-Headlines. Der Titel nennt den Kontext.
- Kurze Labels: "Suchen", nicht "Durchsuche alles...".
- Veränderungen nennen ihren Bezug: "+12 % ggü. Vormonat".
- Headlines, Subheads, Labels, Buttons, Captions ohne Schlusspunkt. Nur mehrsätzige Absätze behalten Punkte.
- Kein Hype (siehe Katalog K5), kein "KI-gestützt" auf allem.
- Unprüfbare Behauptungen: fragen. Echt: ruhig und konkret. Sonst entfernen. Im Bericht listen.
- Keine `—` oder `–` als Stilmittel oder Trenner; Bereiche mit Bindestrich (`2018-2026`). In deutschem Fließtext eines Kunden, der den Halbgeviertstrich als Bis-Strich bewusst nutzt, bleibt er; als Pausenzeichen nie.
- CTA-Labels: höchstens drei Wörter, eine Zeile auf Desktop, ein Label je Absicht auf der ganzen Seite.
- Abschnittsinhalt Modus L: Headline höchstens acht Wörter, Absatz höchstens 25 Wörter, ein Visual oder ein CTA.
- Copy-Selbstprüfung vor Abschluss: jeden sichtbaren String lesen (Headlines, Buttons, Alt-Texte, Footer, Fehlermeldungen). Grammatisch schief, unklarer Bezug, KI-Wortspiel, pseudo-poetische Mikro-Meta: durch schlichten funktionalen Satz ersetzen. Langweilige Copy schlägt niedliche KI-Copy.
- Mock-Daten wirken echt: plausible, unrunde Zahlen, ortsübliche Namen, nie `[X]` oder `123,456`. Auf Marketingseiten keine erfundene Präzision.
- Badges wie `PRO`, `Neu ✨` weg, außer das Produkt braucht sie; dann ruhiger Text.

## 5. Typo `[u+t]`

- Schrift nach dem Charakter aus der Richtung, Familien in `tokens.md`. Projektschrift behalten, wenn sie Teil einer echten Marke ist. Eine Familie für die Oberfläche plus höchstens ein Partner (Mono für Zahlen und Meta oder Display für große Headlines).
- Wenige Größen aus der Skala, Gewichte 400 und 500, 600 höchstens für seltene Betonung. Keine 700 bis 900.
- Hierarchie über Größe und Farbe.
- Satzschreibung überall. Versal-Labels mit weiter Laufweite werden normal geschrieben.
- Kleine Schrift nie mit negativer Laufweite. Enge Laufweite nur für Display ab 40px.
- Zahlen mit `tabular-nums`, ein Format auf dem ganzen Screen.
- Kursiv: nicht zur Betonung in Fließtext und Labels. In Display-Headlines nur bei Editorial-Charakter, mit Unterlängen-Reserve (`leading-[1.1]`, `pb-1`).
- Betonung in einer Headline in derselben Familie über Farbe oder Gewicht, nie ein fremdes Serif-Wort.
- Fließtext höchstens 65ch breit.
- Schriften selbst hosten (`next/font` oder `@font-face` mit `font-display: swap`), nicht per Google-Fonts-`<link>` in Produktion.

## 6. Layout `[u+t]`

Allgemein:

- Abschnitte und Reihenfolge bleiben. Innerhalb eines Abschnitts dürfen Ausrichtung und Proportionen sich ändern, wenn es klarer wird.
- Lange Headlines linksbündig. Zentriert nur bei ein bis zwei kurzen Zeilen.
- Unter 768px stapelt alles in Lesereihenfolge, je Abschnitt ausdrücklich festgelegt. Die Headline fällt auf die mobile Größe, das Visual kommt nach den Aktionen. Dichte Vorschauen werden mobil einfacher statt kleiner gezoomt, kein Text unter 11px.

Modus A:

- Echte App-Proportionen: Shell füllt den Viewport, Sidebar 240 bis 280, Inhalt fluid, gedeckelt um 1440 bis 1600. Nie eine App in eine schmale zentrierte Spalte drücken.
- Ein Hauptchart, klar das größte Element. Daneben anderes in anderer Art (Liste mit dünnen Balken, kurze Tabelle), nie ein zweiter gleich großer Chart.
- Raster mit Rhythmus: drei bis vier kompakte Stats über einem breiten Chart, oder breiter Chart neben schmaler Liste.

Modus L, Hero:

- Stärkster Hero ist eine **Szene**: ein generiertes Bild füllt den Hero randlos, das Motiv sitzt auf einer Seite, die Headline auf der ruhigen leeren Fläche desselben Bildes, die Produktansicht steigt von der Unterkante auf. Text sitzt im oberen Teil zwischen Navigation und Produktansicht, leicht über der optischen Mitte.
- Ohne Szene: asymmetrischer Split (Text auf einer Seite, Visual mindestens halbe Breite) oder Text über großer Produktansicht. Im Split den Textblock vertikal zum Visual zentrieren; ist das Visual viel höher, das Visual kürzen.
- Zentriert gestapelt nur bei `DESIGN_VARIANCE` bis 4 oder als kurzes Manifest ohne Visual.
- Höchstens vier Textelemente: Eyebrow oder Markenstreifen (null oder eins), Headline (höchstens zwei Zeilen), Subtext (höchstens 20 Wörter, höchstens vier Zeilen), CTAs (ein primärer, höchstens ein sekundärer). Trust-Streifen, Preis-Teaser, Feature-Bullets, Avatar-Reihe gehören in den Abschnitt darunter.
- Hero passt in den ersten Viewport, CTA ohne Scrollen sichtbar. Schriftgröße und Bildgröße zusammen planen: `text-4xl md:text-5xl lg:text-6xl` als Standard, `text-6xl md:text-7xl` nur bei drei bis fünf Wörtern. Eine vierzeilige Headline ist immer ein Größenfehler.
- Abstand Navigation zu Headline bzw. Hero-Padding oben höchstens 96px auf Desktop, mobil 48 bis 64. Kein toter Leerstreifen im ersten Screen; ist der Inhalt kürzer, die Produktansicht tief beginnen und über die Unterkante laufen lassen.
- `min-h-[100dvh]`, nie `h-screen`.
- Navigation ruhig: Logo, vorhandene Links, ein Button; Login als Textlink daneben. Eine Zeile auf Desktop, 64 bis 72px hoch, höchstens 80. Mobil ein Menübutton. Eine schwebende Pill-Navigation ist keine Pflicht.

Modus L, Seite:

- Jede Layoutfamilie (Drei-Karten-Reihe, Split Text/Bild, Vollbreiten-Zitat, Bento) höchstens einmal; bei acht Abschnitten mindestens vier Familien.
- Höchstens zwei Zickzack-Splits in Folge.
- Bento: so viele Zellen wie Inhalte, Rhythmus in den Zellgrößen, zwei bis drei Zellen mit echtem Inhalt als Variation (Bild, Produktdetail, Chart, Flächenstufe). Kein Hue-Verlauf als Abwechslung.
- Abschnittsheader: Headline und Text untereinander. Split-Header nur, wenn rechts ein Visual oder Interaktives steht.
- Eyebrows höchstens `ceil(Abschnitte / 3)`, in Satzschreibung, ohne Nummerierung.
- Karten nur, wenn Erhöhung echte Hierarchie zeigt, sonst Gruppieren über Abstand oder `divide-y`. Ab `VISUAL_DENSITY` 8 keine Kartenrahmen.
- Lange Listen (über fünf) in eine passendere Komponente: Gruppen, Karten, Tabs, Akkordeon, horizontale Pills. Höchstens ein Marquee pro Seite.
- Logo-Wand direkt unter dem Hero, nie darin, nur Logos.
- Zitate höchstens drei Zeilen, Name plus Rolle.

## 7. Details `[u+t]`

- Verschachtelte Radien: innen = außen minus Padding, nie unter 4. Controls 8 bis 10, Karten 12 bis 16, Panels 14 bis 20. Nicht alles ist Pill. Eine dokumentierte Radius-Regel, überall befolgt; alle Buttons teilen den Control-Radius.
- Zähler und Meta als ruhiger Text, oft Mono und gedämpft, statt leuchtender Pills. Tastenkürzel als kleine Keycaps.
- Charts: gedämpftes Raster, gedämpfte Mono-Labels, keine Regenbogenbalken in einer Serie, keine Versal-Tageslabels. Ein Akzent pro Chart auf dem, was zählt. Mehrere Farbtöne nur, wenn Serien wirklich unterschieden werden müssen, dann führt eine. Charttyp passend: Trend Linie, Vergleich Balken, Anteil ein gestapelter Balken oder Liste mit Balken, Ziel Fortschrittsbalken. Platzhalter-Rauschen durch Daten ersetzen, die etwas erzählen.
- Stat-Karten sind Zahlen: Label, große Zahl, Veränderung mit Bezug. Keine Sparklines oder Icons als Füllung. Ein echtes Objekt darf hinein, wenn es genau das ist, was die Zahl zählt.
- Aktiver Zustand: kleine Flächenstufe mit Haarlinien-Highlight, kein Verlauf mit Glow.
- Tabellenzustände unterscheidbar: Kopf, Wert, Auswahl, Tastaturfokus.
- Alle Zustände: Hover und Fokus in der Palette, sichtbarer Fokusring, Laden als Skeleton in Form des Inhalts, Leerzustand mit Hinweis, wie er sich füllt, Fehler inline bei Formularen. Formulare: Label über dem Feld, Fehler darunter, kein Placeholder als Label, alles mit 4,5:1 Kontrast.
- Logo: Produktname in der Hauptfamilie plus einfaches Zeichen, falls vorhanden. Ist das Logo selbst Slop (Emoji, Sparkle in Verlaufskachel), flach neu zeichnen: Wortmarke allein oder ein schlichtes Zeichen in einer Volltonfarbe. Nie Glanzkugel, Glow oder Verlaufskachel. Den Produktnamen nie ändern.
- Die Signatur aus der Richtung erscheint, wo sie hingehört, und nirgends sonst.
- Z-Index nur für Ebenensysteme (Sticky-Nav, Modal, Overlay), keine Streu-`z-50`.

## 8. Visuals

Vor diesem Durchgang `visuals.md` lesen.

## 9. Bewegung `[u+t]`

- Raus: Schleifen ohne Grund (`animate-pulse`, `animate-ping` auf Nicht-Live-Elementen, Shimmer auf Headlines, atmende Glows, schwebende Elemente, Parallax ohne Zweck), `transition-all`, federnde Springs, `hover:scale` auf Karten, alles, was sich bei Hover mehr als ein paar Pixel bewegt, eigene Mauszeiger.
- Jede Animation braucht einen Satz Begründung: Hierarchie, Erzählung, Rückmeldung oder Zustandswechsel. "Sah gut aus" zählt nicht.
- Bleibt: Hover als schneller Farb- oder Flächenwechsel, Press als kleines Skalieren (0.97 bis 0.98), Menü blendet ein und steigt wenige Pixel von seinem Ursprung, eine sich ändernde Zahl tweent.
- Nur `transform`, `opacity`, Farbe, Hintergrund, Rahmen animieren und benennen (`transition-colors`, `transition-[transform,opacity]`). Nie Breite, Höhe, `top`, `left`, Margins, große Blurs.
- Eine Easing-Kurve, wenige Dauern (`tokens.md`).
- Beim Laden höchstens ein Einstieg: kurzes Fade-and-Rise des Hauptinhalts mit kleinem Stagger.
- Was `MOTION_INTENSITY` darüber hinaus erlaubt (Scroll-Reveal ab 4, Choreografie ab 8), siehe `richtung.md`. Für Sticky-Stack und Horizontal-Pan: `start: "top top"`, `pin: true`, `scrub`; Code-Gerüste stehen im Original-taste-skill (Abschnitt 5.A und 5.B).
- Scroll-Logik nur über `useScroll`, ScrollTrigger, IntersectionObserver oder CSS `animation-timeline`, nie `window.addEventListener('scroll')` oder `scrollY` in React-State. Kontinuierliche Werte (Maus, Scroll) als Motion-Values, nie `useState`.
- Animierte Komponenten als isolierte Client-Blätter (`'use client'`), `useEffect` mit Cleanup. GSAP oder Three.js nie mit Motion im selben Baum.
- `prefers-reduced-motion` ohne Ausnahme: Schleifen, Parallax, Scroll-Hijack und Magnet-Effekte fallen auf statisch.
- Feinarbeit an Timing und Gesten: `emil-design-eng`, `motion-design`.

---

Teile übersetzt und angepasst aus unslop von Damir Sokolovsky ([@heydamir](https://x.com/heydamir)), CC BY 4.0, und aus taste-skill von Leonxlnx (MIT).
