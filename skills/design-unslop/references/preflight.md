# Pre-Flight

Letzter Filter vor "fertig". Jeder Punkt ist mit Ja oder Nein beantwortbar. Ein Nein heißt: nicht fertig, beheben oder im Bericht begründen. `L` und `A` markieren Punkte, die nur in einem Modus gelten.

## 1. Maschinelle Checks

Auf die geänderten Dateien laufen lassen (`SRC` = Pfad oder Dateiliste des Screens). Jeder Treffer wird angesehen; erklärbare Treffer (Text auf Akzent in `#fff`, Skeleton-Shimmer beim echten Laden) stehen mit Grund im Bericht.

```bash
SRC=src   # anpassen
rg -nP "[\x{1F300}-\x{1FAFF}\x{2600}-\x{27BF}\x{2B50}]" $SRC                      # Emoji: 0
rg -n "—|–|&mdash;|&ndash;" $SRC                                                  # Gedankenstriche in UI-Text: 0
rg -n "bg-clip-text|text-transparent|background-clip:\s*text" $SRC                # Verlaufstext: 0
rg -n "from-(purple|violet|indigo|fuchsia|pink)|shadow-\[0_0_|drop-shadow" $SRC   # KI-Lila, Glow: 0
rg -n "font-(bold|extrabold|black)|font-weight:\s*(700|800|900)" $SRC             # Gewichte: 0
rg -n "transition-all|transition:\s*all" $SRC                                     # 0
rg -n "animate-(pulse|ping|bounce)|hover:scale-" $SRC                             # nur echte Live-Zustände
rg -n "h-screen|height:\s*100vh" $SRC                                             # L: 0
rg -n "addEventListener\(\s*['\"]scroll|cursor:\s*url|cursor-none" $SRC          # 0
rg -n -- "-\[\d+px\]" $SRC                                                        # Einzelwerte: jeder auf 4er-Raster
rg -ni "supercharge|seamless|unlock|unleash|elevate|revolutioni|game.?chang|next.?gen|nahtlos|mühelos|revolutionär|entfessel" $SRC   # 0
rg -n "John Doe|Jane Doe|Mustermann|Acme|Nexus|Lorem|123[,.]?456|\[X\]|99\.99" $SRC   # 0
rg -n "uppercase" $SRC                                                            # zählen, siehe Eyebrow-Regel
rg -n "prefers-reduced-motion|useReducedMotion|motion-reduce:" $SRC              # vorhanden, sobald etwas animiert
```

Zählungen:

- [ ] Eyebrows (kleine Versal- oder Mono-Labels über Abschnittsheadlines) höchstens `ceil(Abschnitte / 3)` `L`
- [ ] Unterschiedliche Textfarben: höchstens drei Rollen plus Akzent plus Semantik
- [ ] Unterschiedliche Schriftgrößen: höchstens sechs; Gewichte: höchstens drei, alle zwischen 400 und 600
- [ ] Icon-Bibliotheken im Import: genau eine
- [ ] Akzentfarbe: genau eine, auf allen Abschnitten dieselbe
- [ ] Easing-Kurven: genau eine
- [ ] Layoutfamilien bei acht Abschnitten: mindestens vier, keine doppelt; höchstens zwei Zickzack-Splits in Folge `L`
- [ ] Marquees: höchstens eins `L`

## 2. Kontrast

Mit dem Kontrastwert aus DevTools oder einem Rechner, nicht nach Augenmaß:

- [ ] Fließtext und Labels mindestens 4,5:1, große Schrift ab 18px mindestens 3:1
- [ ] Text auf jedem Button mindestens 4,5:1, auch Ghost-Buttons über Fotos
- [ ] Platzhalter, Hilfetexte, Fehlertexte und Fokusringe in Formularen mindestens 4,5:1 bzw. 3:1 für den Ring
- [ ] Beide Modi geprüft, falls die Seite hell und dunkel hat

## 3. Sichtprüfung mit agentfenster

Seite lokal starten und mit dem `browser`-Tool von agentfenster öffnen (unsichtbarer Desktop). Nicht Playwright. Screenshots:

1. Desktop 1440 breit, hell
2. Desktop 1440 breit, dunkel (falls vorhanden)
3. Mobil 390 breit
4. Hover und Fokus am primären CTA, ein Tab-Durchlauf über die Navigation
5. Bei Bewegung: einmal mit reduzierter Bewegung (Emulation oder Systemeinstellung)

Am Screenshot abhaken:

- [ ] Jeder Audit-Befund aus Schritt 2 ist sichtbar behoben oder steht begründet im Bericht
- [ ] Die Richtung (Charakter, Welt) ist erkennbar, die Signatur sitzt dort, wo sie hingehört
- [ ] Icons, Labels und Zahlen stehen je in einer Fluchtlinie; gleiche Dinge gleich groß
- [ ] Verschachtelte Radien gehen auf; alle Buttons teilen den Control-Radius
- [ ] Keine Hue-Verläufe, Glows, Farbschatten, Farbblobs auf Flächen
- [ ] Ein Theme pro Seite, kein Abschnitt kippt
- [ ] Hero `L`: Headline höchstens zwei Zeilen, Subtext höchstens 20 Wörter, höchstens vier Textelemente, ein primärer und höchstens ein sekundärer CTA, CTA ohne Scrollen sichtbar, Padding oben höchstens 96px, kein toter Leerstreifen
- [ ] Hero `L` nicht zentriert gestapelt bei `DESIGN_VARIANCE` über 4 (außer Manifest)
- [ ] Navigation eine Zeile, höchstens 80px hoch, Login als Textlink
- [ ] Kein CTA-Label bricht auf Desktop um, kein Label über drei Wörter, eine Formulierung je Absicht
- [ ] Hero hat ein echtes Visual oder eine Produktvorschau mit Moment; kein Div-Fake, kein beschrifteter Platzhalter, kein Text im Bild
- [ ] Bildränder verschmelzen mit der Seite
- [ ] Charts: ein Akzent, gedämpftes Raster, Hauptchart klar am größten `A`
- [ ] Stat-Karten ohne Sparklines oder Füll-Icons `A`
- [ ] App-Proportionen: Sidebar 240 bis 280, Inhalt fluid, keine schmale zentrierte Spalte `A`
- [ ] Mobil: alles in Lesereihenfolge gestapelt, kein horizontales Scrollen, kein Text unter 11px
- [ ] Hover und Fokus vorhanden und in der Palette, Fokusring sichtbar
- [ ] Laden, Leer und Fehler existieren, wo Daten asynchron kommen
- [ ] Bewegung: höchstens ein Einstieg beim Laden, keine Schleife auf Nicht-Live-Elementen, mit reduzierter Bewegung statisch
- [ ] Bewegung, falls `MOTION_INTENSITY` über 4: die Seite bewegt sich wirklich, nichts ruckelt oder bricht ab `L`

## 4. Inhalt

- [ ] Copy-Selbstprüfung: jeder sichtbare String gelesen (Headlines, Buttons, Alt-Texte, Footer, Fehler), kein schiefer oder KI-poetischer Satz
- [ ] Keine Ausrufezeichen, keine Schlusspunkte an kurzen Strings, keine Begrüßungs-Headline
- [ ] Unprüfbare Behauptungen erfragt und entweder bestätigt oder entfernt; Liste im Bericht
- [ ] Keine erfundenen Features, Kennzahlen, Logos, Zitate
- [ ] Zahlen in einem Format mit `tabular-nums`
- [ ] Zitate höchstens drei Zeilen, Name plus Rolle `L`
- [ ] Unverändert: URLs, Nav-Labels, Formularfeldnamen, Produktname, Rechts- und Consent-Texte (außer ausdrücklich beauftragt)

## 5. Template-Test

- [ ] Produktnamen gedanklich gegen den eines anderen Produkts tauschen. Passt der Screen noch, Richtung in Copy, Visual und Signatur härter durchziehen und erneut prüfen.
- [ ] Der Screen sieht nicht aus wie das letzte Projekt (Palettenfamilie, Schrift, Layout).

## 6. Technik

- [ ] Build läuft, keine neuen Konsolenfehler
- [ ] Jede neue Abhängigkeit steht in `package.json`, Installationsbefehl genannt
- [ ] Ein Design-System, nicht zwei gemischt
- [ ] Animierte Komponenten sind Client-Blätter mit Cleanup
- [ ] Hero-Bild mit Priorität und festen Maßen, LCP plausibel unter 2,5 s, CLS unter 0,1

---

Teile übersetzt und angepasst aus unslop von Damir Sokolovsky ([@heydamir](https://x.com/heydamir)), CC BY 4.0, und aus taste-skill von Leonxlnx (MIT).
