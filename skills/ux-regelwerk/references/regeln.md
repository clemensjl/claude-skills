# Regelkatalog

Jede Regel hat eine ID, eine prüfbare Bedingung und eine Quelle. "Prüfen" beschreibt, woran ein Befund festgemacht wird: eine Zahl, ein Selektor, ein Codemuster oder ein Testfall im laufenden Produkt. Stack-Umsetzung und Suchmuster für Web, React Native/Expo und Flutter stehen in `stacks.md`.

Quellenkürzel am Ende der Datei. Wo zwei Quellen sich widersprechen, gilt die hier formulierte Regel; die Begründung steht in `widersprueche.md` unter der genannten Nummer (W1 bis W15).

Schweregrad je Regel (für das Befundformat im PRÜFEN-Modus):
- **K** kritisch: Nutzer scheitert, verliert Daten, bucht doppelt oder ist ausgeschlossen (Tastatur, Screenreader).
- **H** hoch: Nutzer stolpert spürbar, Fehlbedienung wahrscheinlich.
- **M** mittel: wirkt unfertig, kostet Zeit.
- **N** niedrig: Politur.

---

## Z. Feedback und Zustände

**Z1 (K) Jeder Tap antwortet sichtbar in höchstens 100 ms.** Gedrückt-Zustand beim Aufsetzen des Fingers bzw. Maus-Down; die Aktion selbst löst erst beim Loslassen aus (W3).
Prüfen: Jedes klickbare Element hat einen Pressed-Stil (Web `:active`, RN `Pressable` mit `({pressed}) =>`-Style oder `android_ripple`, Flutter `InkWell`/`ButtonStyle.overlayColor`). Ein `TouchableWithoutFeedback`, `onClick` auf `div` ohne `:active` oder `GestureDetector` ohne visuelle Reaktion ist ein Befund.
Quelle: R06, APL §1, MN §5, EMIL.

**Z2 (K) Kein Doppel-Submit.** Ab dem ersten Tap ist die auslösende Aktion gesperrt, bis die Antwort da ist: Button zeigt Ladezustand und Verb im Verlauf ("Wird gespeichert…"), zweiter Tap tut nichts. Bei Bestellung, Zahlung, Anlegen von Datensätzen zusätzlich Idempotency Key pro Absicht.
Prüfen: Testfall Doppeltap bzw. Doppelklick schnell hintereinander bei gedrosseltem Netz: genau ein Request im Netzwerk-Log, genau ein Datensatz. Im Code ein Guard (`if (pending) return`) vor dem `await`, nicht nur `disabled={loading}` nach einem `setState`, das erst im nächsten Render greift.
Quelle: R06, UDA 19, WIG Forms.

**Z3 (H) Jede Aktion mit Wartezeit hat vier Zustände: Ruhe, läuft, Erfolg, Fehler.** Erfolg wird bestätigt (Toast, Inline-Haken, Navigation mit sichtbarem Ergebnis), Fehler mit Text und Weg zur Lösung, nie still verschluckt.
Prüfen: Für jede Mutation (`insert`, `update`, `delete`, `fetch` mit POST) gibt es einen sichtbaren Fehlerpfad. `catch {}` leer, `catch (e) { console.log(e) }` ohne UI oder fehlendes `try` um ein `await` ist ein Befund.
Quelle: APL §16 (vier Feedback-Arten), MD state-feedback.

**Z4 (H) Optimistic Update nur mit Rollback.** Umkehrbare, fast immer erfolgreiche Aktionen (Abhaken, Liken, Umbenennen) zeigen das Ergebnis sofort; schlägt der Request fehl, kehrt die UI zurück und meldet es. Nie für Zahlungen oder Löschen ohne Soft Delete.
Prüfen: Testfall Netz aus, Aktion auslösen: alter Zustand kommt zurück plus Meldung.
Quelle: UDA 2, R24.

**Z5 (H) Umkehrbares Löschen: Undo statt Bestätigungsdialog. Unumkehrbares: Dialog mit benannter Aktion.** Undo-Toast mindestens 5 s, pausiert bei Hover/Fokus, Löschung wird bis Ablauf zurückgehalten oder als Soft Delete umgesetzt. Dialog-Button heißt wie die Aktion ("Konto löschen"), nicht "OK"/"Ja" (W2).
Prüfen: `confirm(`, `Alert.alert` oder `AlertDialog` vor umkehrbarer Aktion ist ein Befund; ebenso Löschen ganz ohne Schutz.
Quelle: UDA 5, APL §16 Agency, WIG Navigation.

**Z6 (M) Zustandsänderung ist nicht nur Farbe.** Ausgewählt, aktiv, fehlerhaft, deaktiviert werden zusätzlich über Form, Icon, Text oder Gewicht unterschieden.
Prüfen: Screenshot in Graustufen: Zustand noch erkennbar?
Quelle: A11Y 1.4.1.

**Z7 (M) Deaktivierte Elemente erklären sich.** Ein ausgegrauter Button ohne sichtbaren Grund ist ein Befund. Entweder Grund daneben ("Noch 2 Pflichtfelder") oder Button aktiv lassen und beim Tap erklären (W1).
Quelle: R22, WIG Forms.

**Z8 (N) Hover nur bei Geräten mit Hover.** Hover-Stile in `@media (hover: hover) and (pointer: fine)`; Touch bekommt Feedback über `:active`. Nichts Wichtiges ist nur per Hover erreichbar (Aktionen, Tooltips mit Pflichtinfo).
Prüfen: Touch-Testfall: Gibt es Aktionen, die erst bei Hover erscheinen (`opacity-0 group-hover:opacity-100`)? Dann Befund **H**.
Quelle: MN §1, EMIL, BU Environment.

---

## FO. Formulare und Eingabe

**FO1 (K) Sichtbares Label über jedem Feld, Placeholder nur als Beispiel.** Das Label verschwindet nie, auch nicht beim Tippen; Floating Label ist erlaubt, wenn es oben stehen bleibt. Placeholder zeigt ein Beispielformat und endet mit "…" oder ist ein Beispielwert ("z. B. 72,5").
Prüfen: Feld mit Text gefüllt: ist noch erkennbar, wofür es steht? Web: `<label for>` bzw. umschließendes `<label>`; RN/Flutter: sichtbarer `Text` über dem Feld plus `accessibilityLabel` bzw. `InputDecoration.labelText`.
Quelle: R09, SU Microcopy, WIG Forms, A11Y 3.3.2.

**FO2 (H) Validierung: beim Verlassen des Felds, nach dem ersten Fehler bei jedem Tastendruck.** Kein Rot beim ersten Zeichen; der Fehler verschwindet in dem Moment, in dem er behoben ist. Ausnahme: Passwort-Anforderungen als Checkliste live beim Tippen, positiv formuliert (W9).
Prüfen: Testfall: ungültige E-Mail tippen ohne das Feld zu verlassen: kein Fehler. Feld verlassen: Fehler. Zurück ins Feld, korrigieren: Fehler weg ohne erneutes Verlassen.
Quelle: R09, R22, APL §16, SU Error Handling.

**FO3 (H) Fehlertext direkt am Feld, mit Lösung.** "Bitte eine gültige E-Mail eingeben, z. B. name@beispiel.at" statt "Ungültig". Feld bekommt `aria-invalid="true"` und `aria-describedby` auf den Fehlertext; nicht nur roter Rahmen (Z6).
Quelle: WIG Content, A11Y 3.3.1/3.3.3.

**FO4 (H) Submit-Button springt nicht.** Platz für Fehlermeldungen unter jedem Feld ist reserviert (feste Mindesthöhe der Hilfezeile) oder Fehler erscheinen ohne Layout-Verschiebung. Nach Submit mit Fehlern: Fokus auf erstes fehlerhaftes Feld, bei langen Formularen zusätzlich Zusammenfassung oben mit Sprung zu jedem Feld.
Prüfen: Screenshot vor und nach Fehleranzeige: Submit-Button an gleicher Position?
Quelle: R09, WIG Forms, A11Y Error Handling.

**FO5 (K) Ziffernfelder ohne `type="number"`.** PLZ, Codes, Telefonnummern, Kartennummern, IDs: `inputmode="numeric"` (Web) bzw. `keyboardType="number-pad"` (RN) bzw. `TextInputType.number` mit `FilteringTextInputFormatter.digitsOnly` (Flutter), Wert bleibt Text. `type="number"` nur für echte Mengen, und selbst dort wegen Scroll-Änderung, "e"-Eingabe und Spinner meist besser `inputmode="decimal"`.
Prüfen: Suchmuster `type="number"`, `keyboardType="numeric"` bei Codes, führende Nullen gehen verloren.
Quelle: R09, UDA 15, MN §4.

**FO6 (H) Dezimalzahlen akzeptieren Komma.** Deutschsprachige Nutzer tippen "72,5". Eingabe tolerant parsen (Komma und Punkt), Anzeige mit `Intl.NumberFormat` in der Nutzer-Locale. Tastatur: `inputmode="decimal"` bzw. `keyboardType="decimal-pad"`.
Prüfen: Testfall "72,5" eingeben: wird 72.5 gespeichert, nicht 72, 725 oder NaN?
Quelle: WIG Locale, R22 (formatierungstolerant), BU Numbers.

**FO7 (H) Richtige Tastatur, Autofill, keine Korrektur bei Kennungen.** E-Mail: `type="email"`, `autocomplete="email"`, `autocapitalize="none"`, `spellcheck=false`; Passwort: `autocomplete="current-password"`/`"new-password"`; Code: `autocomplete="one-time-code"`; Name: `autocomplete="name"`. Return-Taste benennt die Aktion (`enterkeyhint`, RN `returnKeyType`) und springt ins nächste Feld.
Prüfen: Jedes Auth- und Kontaktfeld hat `autocomplete`/`autoComplete`/`textContentType`/`autofillHints`. Fehlt es, Befund.
Quelle: WIG Forms, MN §4, UDA 15, A11Y 1.3.5.

**FO8 (K) Einfügen nie blockieren.** Kein `onPaste` mit `preventDefault`, kein `contextMenuHidden` auf Passwortfeldern. Passwort-Sichtbarkeitsschalter vorhanden.
Quelle: WIG, SU Password, A11Y 3.3.8.

**FO9 (M) Autofill-Zustand gestaltet.** Auf dunklen oder farbigen Flächen den Autofill-Hintergrund überschreiben (`input:-webkit-autofill { box-shadow: 0 0 0 1000px var(--surface) inset; -webkit-text-fill-color: var(--text); }`), Text bleibt lesbar.
Prüfen: Browser-Autofill auslösen, Screenshot im Dark Mode.
Quelle: R09.

**FO10 (M) Pflichtfelder markiert, Optionales gekennzeichnet.** Konsistent eine Konvention: entweder Pflicht mit "*" plus Legende oder Optionales mit "(optional)". Felder, die man nicht braucht, gar nicht abfragen.
Quelle: R22, SU Minimize Fields.

**FO11 (M) Längenlimit sichtbar.** Feld mit `maxLength` zeigt den Zähler beim Tippen ("38/50"), spätestens ab 80 % des Limits. Frontend-Limit = Backend-Limit.
Quelle: R22, BU Phase 1.

**FO12 (M) Vorbefüllen, was bekannt ist.** Eingeloggt: E-Mail, Name, letzte Werte nicht erneut abfragen. Sinnvolle Defaults (heutiges Datum, letzte Einheit).
Quelle: R22, A11Y 3.3.7, SU.

**FO13 (H) Eingaben überleben Fehler und Navigation.** Formular wird bei Fehler nicht geleert; Verlassen mit ungespeicherten Änderungen fragt nach oder speichert als Entwurf (Web `beforeunload`/Router-Guard, RN `usePreventRemove`/`beforeRemove`, Flutter `PopScope`).
Quelle: SU Error Handling, WIG Forms, UDA 12.

**FO14 (H) Eingabefelder bleiben über der Tastatur sichtbar.** Fokussiertes Feld und Submit-Button werden nicht von der Software-Tastatur verdeckt (RN `KeyboardAvoidingView`/`keyboard-controller`, Flutter `Scaffold.resizeToAvoidBottomInset`, Web `interactive-widget=resizes-content` plus `dvh`).
Prüfen: Auf Gerät/Emulator unterstes Feld fokussieren.
Quelle: MN Baseline, UDA 14.

**FO15 (H) Schrift in Web-Inputs mindestens 16 px.** Sonst zoomt iOS Safari beim Fokus. Nie per `maximum-scale=1` oder `user-scalable=no` lösen.
Quelle: MN §4, WIG Anti-patterns.

**FO16 (N) Formatierung tolerant.** Telefonnummer mit oder ohne Leerzeichen, Bindestrich, Klammern; E-Mail mit Leerzeichen am Ende; Tippfehler-Hinweis bei bekannten Domains ("gmial.com").
Quelle: R22, SU Email.

---

## T. Touch und Mobile

**T1 (K) Trefferfläche mindestens 44 × 44 pt (iOS/Web) bzw. 48 × 48 dp (Android/Material).** Untergrenze nach WCAG 2.2 AA: 24 × 24 CSS-px oder ein 24-px-Kreis ohne Überlappung mit dem Nachbarn. Das sichtbare Icon darf kleiner sein; die Fläche wächst über Padding, `hitSlop` oder ein Pseudo-Element (W7). Ausgenommen: Links im Fließtext.
Prüfen: Fläche messen (`getBoundingClientRect`, `onLayout`, Flutter Inspector) inklusive `hitSlop`. Icon-Button mit `width: 24` ohne Padding/hitSlop ist ein Befund. Schließen-X direkt neben anderem Button ohne Abstand: Befund K.
Quelle: R11, R20, UDA 13, A11Y 2.5.8, SU Mobile.

**T2 (H) Trefferflächen überlappen nicht und haben mindestens 8 px Abstand.**
Quelle: UDA 13.

**T3 (H) Safe Areas.** Fixierte Header, Tab-Bars, Sheets, Toasts halten Abstand zu Notch, Dynamic Island, Home-Indikator. Web: `viewport-fit=cover` plus `env(safe-area-inset-*)`; RN: `useSafeAreaInsets`; Flutter: `SafeArea`.
Prüfen: Gerät/Emulator mit Notch und Gestennavigation, auch Querformat.
Quelle: UDA 14, MN §7, WIG.

**T4 (H) `dvh`/`svh` statt `100vh`** für App-Shells und unten fixierte Elemente.
Quelle: MN §3, UDA 14.

**T5 (M) Kein Tap-Highlight-Blitz, kein 300-ms-Delay, kein Textmarkieren auf Buttons.** `-webkit-tap-highlight-color: transparent` (nur zusammen mit eigenem `:active`), `touch-action: manipulation`, `user-select: none` nur auf Controls, nie auf `body`.
Quelle: MN §2, §5, §8, WIG Touch.

**T6 (M) Scroll-Verkettung in Sheets und Modalen gestoppt** (`overscroll-behavior: contain`). Seitenweites `overscroll-behavior: none` nur bei App-Shells mit eigenen Scroll-Containern (W13).
Quelle: MN §6, WIG Touch.

**T7 (H) Jede Geste hat eine Tap- und Tastatur-Alternative.** Swipe-to-delete, Drag-to-reorder, Pull-to-dismiss: zusätzlich Button oder Menüeintrag.
Quelle: A11Y 2.5.7, WIG Touch, UDA 10.

**T8 (M) Sheets lassen sich wegwischen und haben einen Schließen-Button.** Wischen folgt dem Finger 1:1, entscheidet nach Distanz oder Geschwindigkeit (> ca. 0,11 px/ms).
Quelle: UDA 10, EMIL Gestures, APL §2.

**T9 (M) Primäraktion im Daumenbereich.** Auf Mobile liegt die Hauptaktion unten oder ist als fixe Leiste erreichbar; eine fixe Leiste verdeckt nie den fokussierten Inhalt (A11Y 2.4.11).
Quelle: SU Mobile (Sticky CTA), A11Y 2.4.11.

**T10 (H) Systemschriftgröße wird respektiert.** Web: Zoom bis 200 % ohne Verlust; RN: kein globales `allowFontScaling={false}`, höchstens `maxFontSizeMultiplier` an engen Stellen; Flutter: kein fixer `TextScaler.noScaling`. Layout wächst mit (keine festen Höhen um Text).
Prüfen: Größte Systemschrift bzw. 200 % Zoom: abgeschnittener Text, überlappende Elemente?
Quelle: APL §15, A11Y 1.4.4, BU Environment.

---

## N. Navigation und Entscheidungen

**N1 (H) Eine Hauptaktion pro Screen.** Sie ist visuell am stärksten (Füllung, Farbe, Größe); keine zwei Buttons gleich gewichtet nebeneinander. Sekundäres als Outline/Text-Button.
Prüfen: Screenshot: Lässt sich in 1 s sagen, was die Hauptaktion ist? Zwei gefüllte Buttons in derselben Gruppe: Befund.
Quelle: R17 (Hick's Law), APL §16 Simplicity, ON One Goal.

**N2 (M) Erweiterte Optionen versteckt, bis sie gebraucht werden** (Progressive Disclosure). Nicht relevante Optionen gar nicht zeigen statt deaktiviert.
Quelle: R17, APL §16, SU Use Case.

**N3 (M) Wegfindung.** Jeder Screen beantwortet: Wo bin ich (Titel, aktiver Tab), wohin kann ich, wie komme ich zurück. Kein Screen ohne Zurück oder Schließen.
Quelle: APL §16 Wayfinding, A11Y 2.4.2/2.4.8.

**N4 (M) Konkrete Labels.** Buttons nennen die Aktion ("Mahlzeit speichern", nicht "Weiter"/"OK"); Navigation nennt Inhalte.
Quelle: WIG Content, APL §16.

**N5 (M) Web: Zustand in der URL.** Filter, Tabs, Paginierung, offene Detailansicht per URL teilbar und mit Zurück-Taste erreichbar. Navigation über `<a>`/`<Link>`, nie `onClick` mit `router.push` auf einem `div`.
Quelle: WIG Navigation.

**N6 (M) Konsistenz.** Gleiche Aktion, gleiches Label, gleicher Ort, gleiches Verhalten auf allen Screens.
Quelle: APL §16 Familiarity, A11Y 3.2.3/3.2.4.

**N7 (M) Onboarding: erster Erfolg ohne Umweg.** Kein Pflicht-Tutorial vor dem Kern; Touren höchstens 3 bis 5 Schritte, jederzeit überspringbar, nicht wiederholt.
Quelle: ON.

---

## L. Laden und gefühlte Geschwindigkeit

**L1 (H) Inhalt lädt mit Skeleton in Inhaltsform, nicht mit zentralem Spinner.** Skeleton hat die Maße des echten Inhalts (kein Layout Shift). Spinner nur für Aktionen (im Button) und unbestimmte Kurzvorgänge.
Prüfen: Netz drosseln, Screen öffnen: Spinner mitten im Inhalt (`ActivityIndicator`, `CircularProgressIndicator`, `<Spinner/>`) als einziger Ladezustand ist ein Befund. Layout-Sprung beim Eintreffen der Daten: Befund.
Quelle: R01 (Skeleton), UDA 1, R24, BU States.

**L2 (M) Unter ca. 200 ms nichts zeigen.** Ladeindikator erst nach Verzögerung oder mit Mindestdauer, damit nichts flackert.
Quelle: UDA 1.

**L3 (H) Bekanntes sofort zeigen (Stale-while-revalidate).** Zurücknavigieren zeigt die letzten Daten sofort und aktualisiert im Hintergrund; kein Ladezustand bei jedem Tab-Wechsel.
Quelle: UDA 6.

**L4 (M) Suche entprellt (ca. 250 bis 300 ms), gleiche Requests nicht doppelt,** unabhängige Requests parallel, lange Listen paginiert oder virtualisiert (ab ca. 50 Einträgen), KI-Antworten gestreamt.
Quelle: R24, WIG Performance.

**L5 (M) Bilder mit festen Maßen bzw. `aspect-ratio` und Platzhalter;** below the fold lazy, LCP-Bild priorisiert.
Quelle: UDA 8, WIG Images.

**L6 (M) Pull-to-Refresh oder Aktualisieren-Weg** auf Listen mit Serverdaten (Mobile).
Quelle: Plattformkonvention; MN §6 (nicht kaputtmachen).

---

## E. Leer-, Fehler- und Extremzustände

**E1 (H) Jede Liste hat einen Empty State:** erklärt den Bereich, zeigt eine Hauptaktion zum ersten Eintrag. Leere Suche hat einen eigenen Text ("Nichts gefunden für …") mit Ausweg.
Prüfen: Testfall 0 Einträge. RN `FlatList` ohne `ListEmptyComponent`, `.map()` ohne Leerzweig: Befund.
Quelle: ON Empty States, WIG Content, BU Collections.

**E2 (K) Fehlerzustand für jeden Datenabruf** mit verständlichem Text und "Erneut versuchen". Nie rohe Fehlermeldungen (`TypeError…`, Postgres-Codes) zeigen.
Prüfen: Testfall Netz aus bzw. Server-Fehler.
Quelle: BU States, WIG Content.

**E3 (H) Offline erkennbar.** Ohne Netz sagt die App das, statt endlos zu laden; Eingaben gehen nicht verloren.
Quelle: R24 (schlechtes Netz testen).

**E4 (H) Lange Texte brechen nichts.** `min-width: 0` an Flex-Kindern mit Text, `overflow-wrap: anywhere` bei E-Mails/URLs, `flex-shrink: 0` an Icons/Avataren/Aktionen. RN: `numberOfLines` plus `flexShrink: 1`; Flutter: `Expanded`/`Flexible` plus `overflow: TextOverflow.ellipsis`. Entscheidung je Feld: umbrechen, Ende kürzen, Mitte kürzen, klemmen; Zahlen und Beträge nie kürzen.
Prüfen: Extremdatensatz aus `verifikation.md` laden.
Quelle: BU, WIG Content.

**E5 (M) Zahlen und Plural korrekt.** "1 Eintrag"/"2 Einträge" über `Intl.PluralRules` oder getrennte Strings; Tausendertrennzeichen und Dezimalkomma über `Intl.NumberFormat('de-AT')`; nie `NaN`, `undefined`, `null`, `0.30000000000000004` sichtbar.
Quelle: BU Numbers, WIG Locale.

**E6 (N) Wechselnde Zahlen mit Tabellenziffern** (`tabular-nums`, RN `fontVariant: ['tabular-nums']`, Flutter `FontFeature.tabularFigures()`).
Quelle: UDA 16, WIG Typography.

**E7 (M) Fehlende Optionalfelder hinterlassen keine Lücken** (kein verwaistes "—" oder leere Zeile), fehlende Bilder haben Fallback (Initialen, Icon).
Quelle: BU.

**E8 (M) Zeit korrekt.** Relative Zeit über `Intl.RelativeTimeFormat`, ab ca. einer Woche absolutes Datum; Tagesgrenzen in der Zeitzone des Nutzers (Mitternacht!).
Quelle: BU Time, WIG Locale.

---

## A. Barrierefreiheit (Pflichtteil; Vollaudit über `accessibility`)

**A1 (K) Sichtbarer Fokus.** Nie `outline: none`/`outline-none` ohne `:focus-visible`-Ersatz mit mindestens 3:1 Kontrast. Fokus wird nicht von Sticky-Elementen verdeckt.
Prüfen: Tastatur-Durchlauf (Tab) über den ganzen Screen: Fokus jederzeit sichtbar?
Quelle: A11Y 2.4.7/2.4.11, WIG Focus.

**A2 (K) Alles per Tastatur bedienbar, logische Reihenfolge, keine Falle.** Echte `<button>`/`<a>` statt `div onClick`; Modale halten den Fokus und geben ihn beim Schließen an den Auslöser zurück; Esc schließt.
Quelle: A11Y 2.1.1/2.1.2/2.4.3, WIG.

**A3 (K) Jedes Bedienelement hat einen Namen und eine Rolle.** Icon-Buttons: `aria-label` bzw. `accessibilityLabel`/`role="button"` bzw. Flutter `Semantics(label:)`/`tooltip:`. Dekorative Icons versteckt (`aria-hidden`, `accessible={false}`, `ExcludeSemantics`). Sichtbarer Text ist im Namen enthalten (2.5.3).
Quelle: A11Y 4.1.2, WIG.

**A4 (K) Kontrast:** Text 4,5:1, großer Text (ab 24 px bzw. 18,66 px fett, W14) 3:1, UI-Elemente (Feldrahmen bzw. Feldfläche gegen den Hintergrund, Checkbox-Rand, Icon-Buttons) und Fokusring 3:1. Auch Placeholder, deaktivierte Labels mit Inhalt, Text auf Bildern und Glas-Flächen.
Quelle: A11Y 1.4.3/1.4.11, APL §12.

**A5 (H) Statusmeldungen werden angesagt.** Toasts, Inline-Fehler, "Gespeichert": `role="status"`/`aria-live="polite"`, Fehler `role="alert"`; RN `accessibilityLiveRegion` (Android) bzw. `AccessibilityInfo.announceForAccessibility`; Flutter `SemanticsService.announce`.
Quelle: A11Y 4.1.3, WIG.

**A6 (H) Zustände sind programmatisch gesetzt:** `aria-pressed`, `aria-expanded`, `aria-selected`, `aria-busy`, `disabled`; RN `accessibilityState={{ selected, disabled, busy, checked }}`.
Quelle: A11Y 4.1.2.

**A7 (H) Zoom nicht gesperrt, Reflow bei 320 px ohne horizontales Scrollen.**
Quelle: A11Y 1.4.4/1.4.10, MN Hard Rule 4.

**A8 (M) Bilder mit Inhalt haben Alternativtext, Seiten einen Titel und `lang`.**
Quelle: A11Y 1.1.1/2.4.2/3.1.1.

---

## M. Motion (Vollreview über `review-animations`)

**M1 (H) Bewegung hat einen Zweck** (Orientierung, Zustand, Feedback, Erklärung); Aktionen, die 100-mal am Tag oder per Tastatur passieren, animieren nicht.
Quelle: EMIL, RA 1/2.

**M2 (H) Dauer:** Press-Feedback 100 bis 160 ms, Tooltip 125 bis 200 ms, Dropdown 150 bis 250 ms, Modal/Drawer 200 bis 500 ms, sonstige UI unter 300 ms. Exit 20 bis 35 % kürzer als Enter (W5, W6).
Quelle: EMIL, R10, MD timing.

**M3 (H) Easing:** Ein- und Ausblenden `ease-out` mit starker Kurve (`cubic-bezier(0.23, 1, 0.32, 1)`), Bewegung auf dem Screen `ease-in-out` (`cubic-bezier(0.77, 0, 0.175, 1)`), nie `ease-in` auf UI (W4).
Quelle: EMIL, RA 3, R10.

**M4 (M) Nie aus `scale(0)`.** Start bei 0,9 bis 0,97 plus Opacity; Popover bei 0,95 aus dem Auslöser (`transform-origin` am Trigger), Modale zentriert. Press-Feedback `scale(0.97)` (W8).
Quelle: EMIL, R10, RA 5.

**M5 (M) Nur `transform` und `opacity` animieren;** nie `transition: all`.
Quelle: EMIL, WIG Animation, RA 7.

**M6 (H) Unterbrechbar:** Zustandswechsel per Transition oder Spring vom aktuellen Wert, nicht per Keyframe von vorn; Eingaben während einer Animation werden nie blockiert.
Quelle: APL §3, EMIL, UDA 11.

**M7 (H) `prefers-reduced-motion` respektiert:** Bewegung entfällt, Überblendungen bleiben (W12). RN: `AccessibilityInfo.isReduceMotionEnabled` bzw. Reanimated `useReducedMotion`/`ReduceMotion.System`; Flutter `MediaQuery.disableAnimationsOf`.
Quelle: A11Y 2.3, APL §14, EMIL, UDA.

**M8 (M) Springs ohne Bounce als Standard;** Bounce (bis ca. 0,2) nur nach Gesten mit Schwung (Flick, Drag-Release) (W10).
Quelle: APL §4, R10, EMIL.

**M9 (N) Listen-Stagger 30 bis 80 ms pro Eintrag, Gesamtdauer unter 500 ms,** blockiert keine Interaktion.
Quelle: EMIL, R10 (30 ms), MD.

**M10 (H) Endlos- oder Autoplay-Bewegung über 5 s pausierbar,** nichts blinkt öfter als 3-mal pro Sekunde.
Quelle: A11Y 2.2.2/2.3.1, WIG.

---

## X. Texte und Mikrocopy

**X1 (M) Ladetexte mit Verb und Auslassungszeichen:** "Wird gespeichert…", "Lädt…" (echtes "…", nicht "...").
Quelle: WIG Typography.

**X2 (H) Fehlertexte sagen, was passiert ist und was jetzt zu tun ist,** ohne Schuldzuweisung und ohne Fachjargon. "Keine Verbindung. Deine Eingabe ist gespeichert, wir senden sie, sobald du online bist." statt "Network Error".
Quelle: WIG Content, SU.

**X3 (M) Eine Anrede, eine Sprache, ein Ton** im ganzen Produkt (du oder Sie, nicht gemischt); keine englischen Reste in deutscher UI ("Loading…", "Submit").
Quelle: APL §16 Familiarity, A11Y 3.2.4.

**X4 (M) Buttons und Links benennen das Ergebnis** (N4); keine "Hier klicken"-Links.
Quelle: WIG Content, A11Y 2.4.4.

**X5 (N) Typografie:** typografische Anführungszeichen („…“), geschützte Leerzeichen zwischen Zahl und Einheit (`72&nbsp;kg`), Überschriften `text-wrap: balance`, Absätze `text-wrap: pretty`.
Quelle: WIG Typography, UDA 17.

**X6 (N) Keine Platzhalter-Reste:** kein "Lorem ipsum", kein "Vite + React" im Tab-Titel, kein Standard-Favicon, eigene 404-Seite.
Quelle: Reel-Auswertung gruppe2 #30.

---

## Quellen

| Kürzel | Quelle |
|---|---|
| UDA | `ux-details-audit` (Clemens), Nummer = Detail 1 bis 20 |
| EMIL | `emil-design-eng` |
| APL | `apple-design`, Paragrafennummer |
| A11Y | `accessibility` und WCAG 2.2, Nummer = Erfolgskriterium |
| WIG | Vercel Web Interface Guidelines (über `web-design-guidelines`), Abschnitt |
| SU | `signup` |
| ON | `onboarding` |
| RA | `review-animations` (Standards 1 bis 10), `improve-animations` |
| MD | `motion-design` (patterns/state-feedback, reference/timing-easing-tables) |
| BU | `break-ui` und dessen `CATALOG.md` |
| MN | `mobile-native`, Paragrafennummer |
| R01 | Reel @mhmdnabdev: Skeleton statt Spinner |
| R06 | Reel "10 UX Rules #1": jeden Tap sofort beantworten, Doppelbestellung |
| R09 | Reel "5 Signup-Fehler": Label, Blur-Validierung, Submit springt, Autofill, inputmode |
| R10 | Reel Animations-Timings |
| R11 | Reel WCAG 2.2 Target Size (@Redcheck) |
| R17 | Reel Hick's Law |
| R20 | Reel Hit-Slop |
| R22 | Reel "6 Formular-Regeln" |
| R24 | Reel Speed-Checkliste |
