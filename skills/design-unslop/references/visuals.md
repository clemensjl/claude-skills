# Visuals

Deko-Füllstoff durch ein Visual ersetzen, das zu diesem Produkt gehört.

## Braucht der Screen eins? `[u+t]`

- **Dashboards, Einstellungen, die meisten App-Screens:** nein. Ihre Momente kommen aus dem Produkt: ein sorgfältiger Chart, schön gesetzte Zahlen, echte Inhalte (Produktfotos, Avatare), ein Status, der lebendig wirkt. Ein physischer Gegenstand des Produkts (Bankkarte in einer Finanz-App) wird meist besser im Code gebaut: weicher Verlauf innerhalb eines Tons, Chip, Nummer. Bilder für Apps nur für Leerzustände, Onboarding, Marketing oder auf Wunsch.
- **Landing-Hero:** ja, immer. Text plus Verlaufsblob ist kein Hero, sondern ein Platzhalter.
- **Weitere Abschnitte einer Landing Page:** dort, wo ein Bild Inhalt trägt (Produktdetail, Anwendung, Team). Ein Visual auf jedem Abschnitt ist Slop; eine reine Textseite ohne ein einziges Bild ist unfertig. Richtwert: Hero plus ein bis zwei tragende Bilder.

## Was das Visual ist

1. **Szene aus der Welt** (mit Bildgenerierung): Hintergrund des ganzen Heros, Motiv auf einer Seite, ruhige Fläche für die Headline auf der anderen. Darunter steigt die Produktansicht auf. Stärkster Hero.
2. **Das Produkt zeigen:** unter der Szene oder als Visual ohne Generierung. Eine Vorschau dessen, was die Seite schon verspricht, aus den echten Komponenten des Projekts oder sorgfältigem HTML in der neuen Palette, mit plausiblen Daten. Den einen Moment zeigen, der die Headline beweist, nicht die ganze App: ein Planungstool zeigt eine Woche mit gebuchtem Slot, ein Code-Review-Tool einen Diff mit Kommentar. Was die Copy behauptet, zu zeigen, ist kein Erfinden eines Features.
   - Erlaubt: echte Mini-Komponente, echter Screenshot, generiertes Bild.
   - Verboten: Div-Rechtecke als Fake-Screenshot, Fake-Terminal, Fake-Versionsfooter (`v0.6.2-rc.1`, `last sync 4s ago`).
   - Die Vorschau trägt einen Moment: ein gerendertes Objekt darin (Bankkarte auf einer Zahl), ein reicher Chart, ein Gegenstand aus der Welt.
3. **Redaktionelle Fotografie** statt Produktvorschau, wenn das Produkt nichts zu zeigen hat.

Das Motiv als **einen Satz** schreiben, bevor generiert wird. Geht es nicht in einem Satz, ist es noch nicht klar. Form, nicht zum Kopieren:

- Backup-Schutz: ein kleiner Leuchtturm an dunkler Felsküste, der Strahl reicht in den Nebel
- Meditations-App: eine dampfende Tasse Tee auf einem Fensterbrett im ersten Licht
- Logistik-API: ein Containerschiff von oben auf ruhiger grauer See

Keine KI-Defaults, außer das Produkt handelt wörtlich davon: glänzende Blobs, Orbs, Nebel, Liquid Chrome, schwebende Würfel, Neon-Leiterbahnen, Hologramme, leuchtende Gehirne, Roboter, Raketen, Kristalle.

## Stile, die funktionieren `[u]`

Einen wählen, der zum Charakter passt, und für die ganze Seite halten.

- **Gemalte Hintergrundkunst:** ruhiger Himmel oder Landschaft mit einem Motiv, offener Himmel für Text. Warm, hoffnungsvoll, menschlich.
- **Filmisches Foto eines Objekts:** ein echtes Ding in schlichtem dramatischem Licht. Ruhig, seriös, vertrauenswürdig.
- **Weiches stilisiertes 3D:** eine kleine Szene mit matten Materialien. Verspielt, freundlich.
- **Produktobjekt-Render:** Bankkarte, Telefon, Paket, studiobeleuchtet, als Moment im Interface.
- **Licht und Optik:** ein physikalisches Phänomen auf dunklem Feld. Technisch, datenlastig.
- **Stich oder Druck:** einfarbig auf getönter Seite, nur wenn die ganze Marke darin lebt.

Scheitert meist: Prompts mit Film- oder Papierkorn (Modelle backen Schachbrettmuster ein; Textur im Code ergänzen), Druckstil auf einem Bild in sonst moderner Oberfläche, mehrere Motive oder Collagen, violett-blaue Glanzabstraktion.

## Bildquelle in dieser Reihenfolge `[u+t]`

1. **Bildgenerierung, falls ein Tool verfügbar ist** (MCP für fal, Replicate, OpenAI Images, Higgsfield o. ä.). Vorher Prompt, Modell und Größe zeigen und fragen, weil Generierung Geld kostet. Einmal laufen lassen, Ergebnis gegen den einen Satz und die Palette prüfen, beim nächsten Versuch den Prompt ändern statt neu würfeln. Ergebnis in die Projekt-Assets speichern, keine temporäre URL. Mit dem Bild starten, sobald die Richtung bestätigt ist, und parallel die ersten Durchgänge machen.
2. **Echte Bilder:** vom Nutzer, von der Marke, offen lizenziert und erlaubt.
3. **Nichts davon:** vor dem Visual-Durchgang sagen, dass ein Bild fehlt, und anbieten, ein Bildtool anzubinden. Überspringt der Nutzer das, bleibt ein leerer Slot: eine schlichte Flächenstufe in exakter Größe mit dem Radius des Layouts, **ohne Text darin**, damit nichts Unfertiges versehentlich live geht. Prompt, Größe und Dateiname in den Bericht, nicht auf die Seite.

`picsum.photos` nur für lokale Entwürfe zum Proportionen-Prüfen, nie im ausgelieferten Stand.

## Prompt-Rezept `[u]`

In dieser Reihenfolge:

- **Motiv:** der eine Satz, konkret und physisch.
- **Umgebung:** schlicht.
- **Licht und Palette:** zur Seite passend, Seitenhintergrundfarbe nennen, damit die Ränder verschmelzen; Lichtrichtung.
- **Stil:** eine klare Richtung passend zum Charakter.
- **Komposition:** wo das Motiv sitzt, damit Platz für Text bleibt ("Motiv rechte Hälfte, links ruhige leere Fläche"). Szene hinter dem ganzen Hero: 16:9 oder breiter, unteres Fünftel ruhig halten, weil die Produktansicht darüber steigt.
- **Ausschlüsse:** kein Text, keine Buchstaben, keine Logos, keine UI, kein Wasserzeichen.
- **Format:** Seitenverhältnis des Slots in doppelter Anzeigegröße.

## Objekte für Momente `[u]`

- Ein Objekt, studiobeleuchtet, auf schlichtem Hintergrund in exakter Seitenfarbe, weicher Kontaktschatten, sonst nichts im Bild. Benötigten Winkel nennen.
- Freistellen, wenn das Tool es kann, sonst mit Maske in die Seitenfarbe blenden. Freistellung löscht dunkle Bereiche nahe der Hintergrundfarbe (schwarzer Bildschirm): Bildschirm in kontrastierender Flachfarbe anfordern.
- Leicht gedreht über die Kante einer Karte gelegt, mit weichem Schatten in der dunkelsten Rampenfarbe.
- Echte UI auf einem generierten Gerät: Gerät frontal generieren, Bildschirmrechteck messen, HTML darüberlegen, beides zusammen drehen.
- Alles in einem Visual erzählt dieselbe Geschichte: zeigt die Liste Rechnung INV-0142, zeigt das Telefon denselben Kunden und Betrag.

## Einbauen `[u+t]`

- WebP oder AVIF in doppelter Anzeigegröße, echter `alt`-Text, der sagt, was zu sehen ist.
- Bildränder an den Seitenhintergrund angleichen, sonst Maske (`mask-image: radial-gradient(closest-side, #000 70%, transparent)`) oder Verlauf in Seitenfarbe. Harte Rechteckkante auf andersfarbiger Seite ist Slop.
- Statisch oder eine langsame, dezente Bewegung, die zum Motiv passt. Keine Parallax.
- Eine Code-Behandlung (Duotone in die Seitenpalette, Bild aus Glyphen) nur, wenn sie zum Charakter passt, nur am Haupt-Visual, nie als neue Deko.
- Hero-Bild mit hoher Priorität laden (`priority`, `fetchpriority="high"`) und feste Maße geben, damit nichts springt (CLS unter 0,1, LCP unter 2,5 s).
- Kein Text, keine Pills, keine Tags über Fotos; Bildunterschrift nur funktional und darunter.

---

Teile übersetzt und angepasst aus unslop von Damir Sokolovsky ([@heydamir](https://x.com/heydamir)), CC BY 4.0, und aus taste-skill von Leonxlnx (MIT).
