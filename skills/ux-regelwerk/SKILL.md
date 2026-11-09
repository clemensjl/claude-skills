---
name: ux-regelwerk
description: Use when building, changing or reviewing any user interface (screens, forms, buttons, lists, dialogs, sheets, navigation, loading, empty or error states) in web, React, Next.js, Expo/React Native or Flutter, and whenever asked to check, audit, improve or fix UX or usability ("UX prüfen", "UX verbessern", "fühlt sich falsch an", "Formular nervt", "auf dem Handy schlecht bedienbar"). Also use before declaring any UI task finished.
---

# UX-Regelwerk

Ein verbindliches Regelwerk für Bedienbarkeit, gebündelt aus `ux-details-audit`, `emil-design-eng`, `apple-design`, `accessibility` (WCAG 2.2), Vercels Web Interface Guidelines, `signup`, `onboarding`, `review-animations`, `motion-design`, `break-ui`, `mobile-native` und mehreren UX-Reels. Doppelte Regeln sind zusammengeführt, Widersprüche aufgelöst (`references/widersprueche.md`).

**Kernprinzip:** Eine Regel gilt erst als erfüllt, wenn sie im laufenden Produkt nachweisbar ist. Geschriebener Code, ein importiertes Paket oder ein CSS-Property ist kein Beleg. Die meisten UX-Fehler entstehen nicht aus Unwissen, sondern weil ein Zustand (Laden, Leer, Fehler, Doppeltap, langer Name, Tastatur offen) beim Bauen nie angesehen wurde.

## Modus wählen

| Auftrag | Modus |
|---|---|
| UI bauen, ändern, Komponente oder Screen anlegen | **BAUEN** |
| "prüf die UX", Audit, Review, "warum fühlt sich das falsch an" | **PRÜFEN** |
| "verbessere die UX" | erst PRÜFEN (Bericht), dann BAUEN für die freigegebenen Befunde |

## Abgrenzung

Dieser Skill ist der Oberbegriff. Für Tiefe in einem Teilgebiet den Spezialskill zusätzlich laden, falls installiert:
- `ux-details-audit`: die 20 Politur-Details (Command Menu, View Transitions, Squircles, Idempotency) als eigener Bericht.
- `accessibility`: Vollaudit WCAG 2.2 inklusive Screenreader.
- `review-animations` (nur per SKILL.md lesbar): Animationen im Diff mit Freigabeentscheidung.
- `break-ui`: Extremdaten-Toggle für eine einzelne Komponente.
- `mobile-native`: Web-App auf dem Handy, Plattformschicht.
- `web-quality-audit` / `core-web-vitals`: gemessene Ladezeit statt gefühlter.
- Visuelles Design (Farben, Typo-Wahl, Layout-Stil): `frontend-design` und die taste-Skills, nicht hier.

## Die Regeln

Vollständig mit Prüfung und Quelle in `references/regeln.md`, Umsetzung je Stack in `references/stacks.md`. Die Kurzfassung unten ist die Mindestmenge, die bei jeder UI-Arbeit gilt. Schweregrad: K kritisch, H hoch, M mittel, N niedrig.

**Feedback und Zustände (Z)**
- Z1 K: Jeder Tap zeigt in höchstens 100 ms einen Gedrückt-Zustand; ausgelöst wird beim Loslassen.
- Z2 K: Ab dem ersten Tap ist die Aktion gesperrt, bis die Antwort da ist; Button zeigt "Wird gespeichert…". Doppeltap erzeugt genau einen Request.
- Z3 H: Jede Mutation hat Lade-, Erfolgs- und Fehlerzustand; kein leerer `catch`.
- Z5 H: Umkehrbares Löschen mit Undo, Unumkehrbares mit Dialog, dessen Button die Aktion nennt.
- Z7 M: Kein ausgegrauter Button ohne sichtbaren Grund.
- Z8 N: Hover nur hinter `(hover: hover) and (pointer: fine)`; nichts Wichtiges nur per Hover.

**Formulare (FO)**
- FO1 K: Sichtbares Label über jedem Feld; Placeholder nur als Beispiel.
- FO2 H: Fehler erst beim Verlassen des Felds, danach Revalidierung bei jedem Tastendruck.
- FO3/FO4 H: Fehlertext am Feld mit Lösung; Platz reserviert, Submit springt nicht; nach Submit Fokus aufs erste Fehlerfeld.
- FO5 K: Codes, PLZ, Telefon nie `type="number"`; `inputmode="numeric"` bzw. `number-pad`, Wert bleibt Text.
- FO6 H: Dezimalfelder akzeptieren "72,5".
- FO7 H: Passende Tastatur, `autocomplete`/`autoComplete`/`autofillHints`, keine Autokorrektur bei Kennungen, Return springt weiter.
- FO8 K: Einfügen nie blockieren. FO13 H: Eingaben überleben Fehler und Zurück. FO14 H: Feld bleibt über der Tastatur.

**Touch und Mobile (T)**
- T1 K: Trefferfläche 44 × 44 pt bzw. 48 dp, Untergrenze WCAG 24 × 24; Icon klein, Fläche groß (Padding, `hitSlop`).
- T3 H: Safe Areas an fixen Leisten, Sheets, Toasts. T7 H: Jede Geste hat eine Tap- und Tastatur-Alternative.
- T10 H: Systemschriftgröße und 200 % Zoom brechen nichts.

**Navigation und Entscheidungen (N)**
- N1 H: Genau eine visuell dominante Hauptaktion pro Screen; nie zwei gleich starke Buttons nebeneinander.
- N2 M: Fortgeschrittenes versteckt bis gebraucht. N3 M: Jeder Screen sagt, wo man ist und wie man zurückkommt.

**Laden (L)**
- L1 H: Inhalt lädt als Skeleton in Inhaltsform, Spinner nur in Buttons. L2 M: Unter 200 ms nichts zeigen.
- L3 H: Bekannte Daten sofort, Aktualisierung im Hintergrund.

**Leer, Fehler, Extrem (E)**
- E1 H: Jede Liste hat einen Empty State mit Erklärung und Hauptaktion.
- E2 K: Jeder Datenabruf hat einen Fehlerzustand mit "Erneut versuchen"; nie rohe Fehlermeldungen.
- E4 H: Lange Namen, E-Mails, Übersetzungen sprengen kein Layout. E5 M: Plural und Zahlenformat korrekt, nie `NaN`/`undefined` sichtbar.

**Barrierefreiheit (A)**
- A1 K: Fokus immer sichtbar; nie `outline: none` ohne Ersatz. A2 K: Alles per Tastatur, Esc schließt, Fokus kehrt zurück.
- A3 K: Icon-Buttons haben einen Namen. A4 K: Kontrast 4,5:1 bzw. 3:1. A5 H: Statusmeldungen werden angesagt.

**Motion (M)**
- M1 H: Kein Animieren bei Tastatur- und Hochfrequenz-Aktionen. M2 H: UI unter 300 ms, Modal/Drawer bis 500 ms, Exit 20 bis 35 % kürzer.
- M3 H: Nie `ease-in` auf UI. M4 M: Nie aus `scale(0)`. M6 H: Unterbrechbar. M7 H: Reduced Motion: Bewegung weg, Überblendung bleibt.

**Texte (X)**
- X2 H: Fehlertext sagt, was passiert ist und was jetzt zu tun ist. X3 M: Eine Anrede, eine Sprache, keine englischen Reste.

## Fehler, die Claude typischerweise macht (Pflicht-Gegenprüfung)

Vor jedem "fertig" und in jedem Audit jede Zeile aktiv gegen den Code und das laufende Produkt prüfen. Diese Liste existiert, weil genau diese Fehler in generiertem UI-Code immer wieder auftauchen, auch wenn die Regel bekannt ist.

| # | Fehler | Woran erkennen | Regel |
|---|---|---|---|
| C1 | Placeholder statt Label | Feld ohne sichtbaren Text darüber | FO1 |
| C2 | `type="number"` bzw. `keyboardType="numeric"` für Codes, PLZ, Gewicht mit Komma | Suchmuster, Testfall "0123" und "72,5" | FO5, FO6 |
| C3 | Icon-Button so groß wie das Icon | 16 bis 24 px Fläche, kein Padding, kein `hitSlop` | T1 |
| C4 | Kein Lade- und Sperrzustand am Submit | `onPress={async…}` ohne Guard; Doppeltap erzeugt zwei Einträge | Z2 |
| C5 | Zentraler Spinner statt Skeleton | `ActivityIndicator`/`CircularProgressIndicator`/`<Spinner/>` als Seiteninhalt | L1 |
| C6 | Kein Empty State, kein Fehlerzustand | Liste rendert bei 0 Einträgen nichts; `catch` leer oder nur `console` | E1, E2, Z3 |
| C7 | Aktion nur per Hover oder nur per Geste erreichbar | `group-hover:opacity-100`, Swipe ohne Button | Z8, T7 |
| C8 | Fokusring entfernt | `outline-none`, `outlineStyle: "none"` ohne Ersatz | A1 |
| C9 | Validierung beim ersten Zeichen oder nur beim Absenden | `mode: "onChange"`, `onUserInteraction`, Fehler erst nach Submit | FO2 |
| C10 | Fehlermeldung schiebt den Submit-Button | bedingt gerendertes Fehler-Element ohne reservierte Höhe | FO4 |
| C11 | Zwei gleich starke Buttons, keine klare Hauptaktion | zwei gefüllte Buttons in einer Gruppe | N1 |
| C12 | `div onClick` / `onPress` auf `View` statt echtem Button | fehlende Rolle, kein Tastaturzugang | A2, A3 |
| C13 | Icon-Button ohne `aria-label`/`accessibilityLabel`/`tooltip` | Suchmuster | A3 |
| C14 | Ausgegrauter Submit ohne Erklärung | `disabled={!valid}` ohne Hinweistext | Z7, W1 |
| C15 | Layout nur mit Demo-Daten angesehen | kein `min-w-0`/`flexShrink`, Text ohne `numberOfLines`; "1 Einträge" | E4, E5 |
| C16 | `100vh`, fehlende Safe Areas, Feld unter der Tastatur | Suchmuster, Gerätetest | T3, T4, FO14 |
| C17 | Animation mit `ease-in`, `transition: all`, aus `scale(0)`, ohne Reduced Motion | Suchmuster | M3 bis M7 |
| C18 | Roher Fehlertext oder englische Reste | `error.message` direkt angezeigt; "Loading…", "Submit" in deutscher UI | X2, X3, E2 |
| C19 | Bestätigungsdialog für umkehrbare Aktionen, Löschen ohne Undo | `confirm(`, `Alert.alert` vor Löschen | Z5 |
| C20 | "Fertig" ohne Sichtprüfung | kein Screenshot, kein Tastatur-Durchlauf im Bericht | Kernprinzip |

## BAUEN

1. **Stack erkennen** (`references/stacks.md`, oben) und die Spalte "Richtig" dieses Stacks als Vorlage nehmen.
2. **Vor dem Code: Zustandsliste je Screen** schreiben, kurz und im Kopf oder als Kommentar im Plan:
   - Hauptaktion (genau eine) und Nebenaktionen.
   - Datenzustände: Laden, Leer, Fehler, Offline, Erfolg; wie sieht jeder aus?
   - Eingaben: Label, Tastatur, Autofill, Validierungszeitpunkt, Pflicht/optional, Limit.
   - Mutationen: Sperre gegen Doppeltap, Undo oder Dialog, Rollback.
   - Extremwerte: längster realistischer Text, 0/1/viele Einträge, große Schrift.
3. **Bauen** nach `regeln.md`. Kein Zustand bleibt "später".
4. **Gegenprüfung:** Tabelle "Fehler, die Claude typischerweise macht" Zeile für Zeile durchgehen, Suchmuster aus `stacks.md` über die geänderten Dateien laufen lassen.
5. **Verifikation** nach `references/verifikation.md`: starten, mit agentfenster bei 390 px und Desktop-Breite ansehen, alle Zustände der Zustandsliste auslösen, Tastatur-Durchlauf, Extremdaten. Befund aus der Verifikation beheben und erneut prüfen.
6. **Abschlusszeile** im Antworttext: welche Screens bei welchen Breiten und Zuständen geprüft wurden, was ein echtes Gerät braucht.

## PRÜFEN

1. **Umfang klären:** Screen, Flow oder ganzes Produkt; Stack erkennen.
2. **Code lesen** und die Suchmuster aus `stacks.md` laufen lassen. Jeder Treffer ist ein Kandidat, kein Befund.
3. **Live bestätigen** nach `verifikation.md`. Kandidaten, die im laufenden Produkt nicht auftreten, verwerfen; nicht live prüfbare als "aus Code gefolgert" kennzeichnen.
4. **Alle Bereiche Z, FO, T, N, L, E, A, M, X** durchgehen, auch wenn die Suchmuster nichts finden; die Pflicht-Gegenprüfung C1 bis C20 vollständig.
5. **Bericht** im Format unten. Nichts ändern, solange der Auftrag nur Prüfen lautet.

### Befundformat

Eine Tabelle, sortiert nach Schweregrad, dann nach Aufwand:

| # | Schwere | Regel | Ort | Befund | Fix | Beleg |
|---|---|---|---|---|---|---|
| 1 | K | Z2 | `app/food/new.tsx:88` | Speichern ohne Sperre, Doppeltap legt zwei Lebensmittel an | `useRef`-Guard vor `await`, Button `disabled` + "Wird gespeichert…" | live: Doppelklick, zwei Einträge in Liste |

- **Ort:** `Datei:Zeile`; bei rein visuellen Befunden Screen und Breite.
- **Fix:** konkret und im Stil des Projekts, mit Wert oder Codeform; nicht "verbessern".
- **Beleg:** `live` mit Beobachtung oder `Code` (aus dem Code gefolgert, nicht live gesehen).
- Schweregrad nie über der nachgewiesenen Auswirkung.

Unter der Tabelle: **Hält** (was bereits stimmt, damit es niemand anfasst), **Nicht geprüft** (mit Grund, z. B. "Gerät nötig: Safe Area"), **Entscheidungen** (Befunde mit mehr als einer richtigen Lösung, je eine Empfehlung).

## Harte Regeln

- **Kein "fertig" ohne Sichtprüfung.** Fehlen die agentfenster-Werkzeuge, das sofort melden statt den Punkt still zu überspringen.
- **Keine erfundenen Befunde und keine erfundenen Bestätigungen.** Jede Zeile hat Ort und Beleg.
- **Nichts ungefragt umbauen** im PRÜFEN-Modus; im BAUEN-Modus nur, was zum Auftrag gehört. Fremde Befunde außerhalb des Auftrags als "Separat" melden.
- **Projektkonventionen vor Regelwerk-Werten,** solange sie keine K- oder H-Regel verletzen (bestehende Tokens, Komponenten, Wortwahl).
- **Lieber fünf verifizierte Befunde als zwanzig vermutete.**

## Referenzen

- `references/regeln.md`: alle Regeln mit Prüfung, Schweregrad und Quelle
- `references/stacks.md`: Stack-Erkennung, richtige Umsetzung und Suchmuster für Web, React Native/Expo, Flutter
- `references/verifikation.md`: Start je Stack, agentfenster-Ablauf, Mess-Skripte, Extremdatensatz, Gerätegrenzen
- `references/widersprueche.md`: W1 bis W15, welche Quelle wo nachgibt und warum
