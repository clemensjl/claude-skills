---
name: produkt-regelwerk
description: Use when building, changing or reviewing any user-facing product surface (app screens, forms, websites, landing pages, shops, checkouts, pricing pages, signup, onboarding, subscriptions, cancellation flows, push notifications, newsletters) in web, React, Next.js, Expo/React Native or Flutter; when asked to improve UX, conversion, retention or churn ("UX prüfen", "Conversion verbessern", "Churn senken", "Kündigungsflow", "Landing Page", "vor dem Launch prüfen", "UI fühlt sich falsch an"); when a request touches dark patterns, urgency timers, pre-checked boxes, harder cancellation, discounts/Streichpreise, newsletter consent or the Widerrufsbutton; and before declaring any UI task finished.
---

# Produkt-Regelwerk

Verbindliche Regeln für Bedienbarkeit, Webdesign, Conversion, Retention und Launch, branchenübergreifend für Apps, SaaS, Shops und Websites. Ersetzt `ux-regelwerk` und übernimmt alle seine Regeln. Gebündelt aus `ux-details-audit`, `emil-design-eng`, `apple-design`, `accessibility` (WCAG 2.2), Vercels Web Interface Guidelines, `signup`, `onboarding`, `review-animations`, `motion-design`, `break-ui`, `mobile-native`, 27 ausgewerteten Instagram-Reels (aus 460 gespeicherten Posts) und einer Recherche in Primärquellen (Baymard, NN/g, W3C, web.dev, Stripe, Duolingo, RIS, EUR-Lex; Rechtsstand AT/EU 15.11.2026, gegengeprüft).

**Kernprinzip 1: Eine Regel gilt erst als erfüllt, wenn sie im laufenden Produkt nachweisbar ist.** Geschriebener Code, ein importiertes Paket oder ein CSS-Property ist kein Beleg. Die meisten Fehler entstehen, weil ein Zustand (Laden, Leer, Fehler, Doppeltap, langer Name, Tastatur offen, Zahlung abgelehnt, Kündigung) beim Bauen nie angesehen wurde.

**Kernprinzip 2: Bindung und Umsatz entstehen durch Wert, Klarheit und Vertrauen, nie durch Hürden oder Täuschung.** Was in `references/verboten.md` steht, wird nicht gebaut, auch nicht auf ausdrücklichen Wunsch. Das Ziel des Auftrags (weniger Churn, mehr Käufe) wird mit den erlaubten Mitteln verfolgt.

## Modus wählen

| Auftrag | Modus |
|---|---|
| UI, Seite, Flow bauen oder ändern | **BAUEN** |
| "prüf", Audit, Review, "warum konvertiert das nicht", "vor dem Launch checken" | **PRÜFEN** |
| "verbessere UX/Conversion/Retention" | erst PRÜFEN (Bericht), dann BAUEN für die freigegebenen Befunde |

## Domänen wählen

Bedienbarkeit gilt immer. Die übrigen Domänen kommen dazu, sobald der Auftrag sie berührt; im Zweifel dazunehmen.

| Domäne | Gilt wenn | Referenz |
|---|---|---|
| Bedienbarkeit (Z, FO, T, N, L, E, A, M, X, Q) | jede UI | `references/regeln-bedienung.md` |
| Webdesign und Launch (WD, LA) | Website, Landing Page, Web-App im Browser, öffentlicher Livegang | `references/regeln-web.md` |
| Conversion (CV) | Kauf, Buchung, Warenkorb, Checkout, Pricing, Signup, Anfrageformular, Rabatt, Bewertungen | `references/regeln-conversion.md` |
| Retention (RT) | Konto, Onboarding, Abo, Kündigung, Push, Newsletter, E-Mail-Flows, Streaks, Win-back | `references/regeln-retention.md` |
| Verboten (D) | immer prüfen, sobald CV oder RT gilt | `references/verboten.md` |

## Kurzfassung (Mindestmenge, Schweregrad K kritisch, H hoch, M mittel, N niedrig)

**Feedback und Zustände**
- Z1 K: Jeder Tap zeigt in ≤ 100 ms einen Gedrückt-Zustand, ausgelöst wird beim Loslassen. Z10 H: Antwort ≤ 400 ms, sonst Fortschritt.
- Z2 K: Ab dem ersten Tap gesperrt bis zur Antwort ("Wird gespeichert…"); Doppeltap = ein Request; Geld oder Datensätze zusätzlich mit Idempotency Key.
- Z3 H: Jede Mutation hat Lade-, Erfolgs-, Fehlerzustand; kein leerer `catch`. Z9 H: Buttons mit allen sechs Zuständen, Laden im Button.
- Z5 H: Umkehrbares mit Undo, Unumkehrbares mit Dialog: Titel als konkrete Frage, ein Satz Folge, Buttons benennen beide Ausgänge.

**Formulare**
- FO1 K: Sichtbares Label über jedem Feld. FO2 H: Fehler erst beim Verlassen, dann live. FO3/FO4 H: Fehler am Feld mit Lösung, Submit springt nicht.
- FO5 K: Codes, PLZ, Telefon, Karten nie `type="number"`. FO7 H: richtige Tastatur und `autocomplete`. FO13 H: Eingaben überleben Fehler.

**Touch, Navigation, Laden, Extremfälle**
- T1 K: Trefferfläche 44 × 44 pt bzw. 48 dp (Untergrenze 24 × 24). T3/T4 H: Safe Areas, `dvh`/`svh` statt `100vh`.
- N1 H: Genau eine dominante Hauptaktion pro Screen. N8 M: gewohnte Muster vor eigenen.
- L1 H: Skeleton statt zentralem Spinner. E1/E2: Empty State und Fehlerzustand mit "Erneut versuchen" für jede Liste und jeden Abruf.

**Barrierefreiheit und Motion**
- A1 K: Fokus sichtbar. A2 K: alles per Tastatur, echte Buttons. A3 K: Icon-Buttons haben Namen. A4 K: Kontrast 4,5:1 bzw. 3:1.
- M2 H: UI < 300 ms, Modal bis 500 ms, Exit 20 bis 35 % kürzer. M3 H: nie `ease-in`. M7 H: Reduced Motion. M11 M: Was am Finger hängt, folgt 1:1.

**Webdesign und Launch**
- WD1/WD3 H: Zeilen 45 bis 90 Zeichen, Text ≥ 16 px in `rem`. WD9 M: weder reines Schwarz noch reines Weiß als Textfläche. WD10/11 H: Dark Mode als eigene Palette, ohne Flash.
- WD15 H: ein H1, lückenlose Überschriften, H1 sagt was und für wen. WD19/WD20 H: Hero beantwortet in 5 s was, für wen, welcher Nutzen; ein konkreter primärer CTA.
- WD22 H: Desktop-Navigation sichtbar. WD25 H: LCP ≤ 2,5 s, CLS ≤ 0,1, Seite < 1,5 MB. WD29 H: Platz für deutschen Text, Buttons stapeln statt kürzen. WD31 H: `39,99 €` über `Intl`.
- LA1 K: echte 404. LA2 bis LA5 H: Title, Description, OG-Bild, Favicon, robots/Sitemap. LA7 K: Impressum und Datenschutz im Footer (Inhalt über `legal-at`).

**Conversion**
- CV1 K: Bestell-Button "zahlungspflichtig bestellen" oder gleichartig eindeutig. CV2 K: Gesamtpreis und Abo-Bedingungen direkt darüber.
- CV3/CV4 K: Bruttopreise mit "inkl. USt", keine Kosten erst im letzten Schritt. CV5 K: Zusatzleistungen nie vorangekreuzt. CV6 K: kein Zahlart-Aufschlag.
- CV8 K: Rabatt vom 30-Tage-Tiefstpreis. CV9 K: Widerrufsfunktion "Vertrag widerrufen" (AT: Verträge ab 01.10.2026). Das ist keine Kündigungsfunktion für Abos, dafür RT1.
- CV15 H: Gast-Checkout. CV16 H: nur nötige Felder. CV17 H: am Kaufen-Button steht, was danach passiert. CV19 K: Eingaben überleben Fehler. CV21 K: eine Bestellung pro Absicht.

**Retention**
- RT1 K: Online abgeschlossen = online kündbar, nicht schwerer als der Abschluss. RT24 K: Kündigen nie an Umfrage, Angebot oder Gespräch gekoppelt. RT25 H: höchstens ein passendes Gegenangebot (Pause, Downgrade).
- RT2 H: definierte Aktivierungsaktion, Onboarding führt direkt hin. RT8 H: Push-Abfrage erst nach einem Wertmoment. RT10 H: jeder Push hat eigenen Wert.
- RT13/RT14 K: Werbung nur mit Einwilligung (§ 174 TKG) und Ein-Klick-Abmeldung. RT16 K: Einwilligungs-Checkboxen leer und getrennt. RT19/RT20 H: Erinnerung vor Testende und Verlängerung.

**Verboten (nie bauen)**: Fake-Countdown, Fake-Knappheit, versteckte Kosten, vorangekreuzte Kosten oder Einwilligung, Fake-Bewertungen und -Siegel, Fake-Rabatt, mehrdeutiger Bestell-Button, Abofalle, Roach Motel, Confirmshaming, Nagging, Fake-Benachrichtigung, Werbung ohne Einwilligung, Datenverlust als Kündigungshebel. Details und Alternativen: `references/verboten.md`.

## Fehler, die Claude typischerweise macht (Pflicht-Gegenprüfung)

Vor jedem "fertig" und in jedem Audit jede Zeile aktiv gegen Code und laufendes Produkt prüfen. Diese Fehler tauchen in generiertem Code und in Reviews immer wieder auf, auch wenn die Regel bekannt ist.

| # | Fehler | Woran erkennen | Regel |
|---|---|---|---|
| C1 | Placeholder statt Label | Feld ohne sichtbaren Text darüber | FO1 |
| C2 | `type="number"` für Codes, PLZ, Karten, Komma-Werte | Suchmuster; Testfall "0123", "72,5" | FO5, FO6 |
| C3 | Icon-Button so groß wie das Icon | 14 bis 24 px Fläche ohne Padding/`hitSlop` | T1 |
| C4 | Kein Lade- und Sperrzustand am Submit, kein Idempotency Key bei Bestellung | `async`-Handler ohne Guard; Doppelklick = zwei Einträge | Z2, CV21 |
| C5 | Zentraler Spinner statt Skeleton | Spinner als Seiteninhalt | L1 |
| C6 | Kein Empty State, kein Fehlerzustand, Fehlertext "Error" | `catch` leer; Liste rendert bei 0 nichts | E1, E2, Z3, X2 |
| C7 | Hover nicht hinter `(hover: hover)`, Aktion nur per Hover oder Geste | `:hover` ohne Media Query; `group-hover:opacity-100` | Z8, T7 |
| C8 | Fokusring entfernt | `outline: none` ohne `:focus-visible` | A1 |
| C9 | Validierung beim ersten Zeichen oder erst nach Submit | `mode: "onChange"`, Fehler nur nach Submit | FO2 |
| C10 | Fehlermeldung schiebt den Submit-Button | bedingtes Fehler-Element ohne reservierte Höhe | FO4 |
| C11 | Mehrere gleich starke Buttons, keine Hauptaktion | 2 bis 5 gefüllte Buttons nebeneinander | N1, WD20 |
| C12 | `div`/`img onClick` statt Button, Icon ohne Namen | fehlende Rolle, kein `aria-label` | A2, A3 |
| C13 | Ausgegrauter Submit ohne Erklärung | `disabled={!valid}` ohne Hinweis | Z7, W1 |
| C14 | Layout nur mit Demo-Daten und englischer Textlänge angesehen | feste Button-Breiten; "1 Einträge"; Text abgeschnitten | E4, E5, WD29 |
| C15 | `100vh`, fehlender Viewport-Meta, fehlende Safe Areas | Suchmuster | T3, T4, WD18 |
| C16 | `transition: all`, `ease-in`, große `scale` beim Hover, UI-Dauer > 300 ms (Modal/Drawer > 500 ms) | Suchmuster | M2 bis M5 |
| C17 | Dialog "Bist du sicher?" mit "OK/Abbrechen" | `confirm(`, generische Buttons | Z5 |
| C18 | Reines `#000`/`#fff`, Gradient-Text ohne Fallback, Emoji als Icons, Floskel-Headline | Suchmuster; Hero-Text lesen | WD9, WD8, X7, WD19 |
| C19 | Preis `39.99`, ohne "€", ohne "inkl. USt", Versand erst am Ende | Preis-Strings im Code und im UI | WD31, CV3, CV4 |
| C20 | Bestell-Button "Submit"/"Weiter"/"Bestellen", Pflichtinfos nur verlinkt | Button-Text | CV1, CV2 |
| C21 | Vorangekreuzte Checkbox für Newsletter, Partner oder Zusatzleistung | `checked` als Default | CV5, RT16, D4 |
| C22 | Rechtsfakten aus dem Gedächtnis: Widerrufsbutton mit Kündigungsbutton verwechselt, falscher Stichtag, falsche Norm | Rechtsaussage ohne Paragraf aus diesem Skill | CV9, RT1 |
| C23 | Checkout ohne "was passiert danach", ohne Fortschritt zur Gratisversand-Schwelle (falls es eine gibt), ohne Danke-/Bestätigungsseite | Redirect auf `/` nach Erfolg | CV17, CV26, CV31 |
| C24 | Kündigungs- oder Push-Flow mit Hürden gebaut, weil der Auftrag "möglichst wenige Kündigungen" sagt | Schrittzahl, Pflichtfrage, Mehrfach-Angebote | RT1, RT24, D11 bis D14 |
| C25 | Launch ohne 404, OG, Favicon, Sitemap, Titel "Home" | `curl`, `<head>` lesen | LA1 bis LA5 |
| C26 | "Fertig" bzw. Bericht nur aus dem Code, ohne Sichtprüfung im Browser | kein Screenshot, kein Klickpfad im Bericht | Kernprinzip 1 |
| C27 | Sichtprüfung nur am Desktop, Tastatur und Doppelklick als "nicht geprüft" abgehakt, Fix nach der Prüfung ungemessen | Abschnitt "Nicht geprüft" ohne technischen Grund | Harte Regeln |

## BAUEN

1. **Stack erkennen** (`references/stacks.md`) und dessen Spalte "Richtig" als Vorlage nehmen. **Domänen wählen** (Tabelle oben).
2. **Vor dem Code eine Zustandsliste je Screen bzw. Flow:**
   - Hauptaktion (genau eine) und Nebenaktionen; bei Kauf oder Abo der Button-Text nach CV1.
   - Datenzustände: Laden, Leer, Fehler, Offline, Erfolg.
   - Eingaben: Label, Tastatur, Autofill, Validierungszeitpunkt, Pflicht/optional; jedes Feld begründet (CV16).
   - Mutationen: Sperre, Idempotenz, Undo oder Dialog, Rollback.
   - Geld und Recht (bei CV/RT): Preise brutto im Locale-Format, Kosten ab Warenkorb, Pflichtinfos am Button, Einwilligungen leer, Kündigungsweg.
   - Extremwerte: längster deutscher Text, 0/1/viele Einträge, große Schrift, abgelehnte Zahlung.
3. **Bauen** nach den Referenzen der gewählten Domänen. Kein Zustand bleibt "später". Verlangt der Auftrag ein Muster aus `verboten.md`: nicht bauen, im Antworttext benennen, erlaubte Alternative bauen (W21).
4. **Gegenprüfung:** Tabelle C1 bis C27 Zeile für Zeile, Suchmuster aus `stacks.md` (inklusive Abschnitt "Stackübergreifend") über die geänderten Dateien.
5. **Verifikation** nach `references/verifikation.md`: starten, Desktop-Breite im agentfenster-Browser ansehen, 390 px per chrome-devtools-Emulation (Messwerte plus Screenshot), alle Zustände der Zustandsliste auslösen, Tastatur-Durchlauf, Extremdaten, Domänen-Prüfungen (Abschnitt 4a). Befunde beheben, erneut prüfen.
6. **Abschlusszeile:** welche Screens bei welchen Breiten und Zuständen geprüft wurden, was ein echtes Gerät oder ein Jurist (`legal-at`) noch braucht.

## PRÜFEN

1. **Umfang klären:** Screen, Flow oder Produkt; Stack und Domänen erkennen.
2. **Code lesen**, Suchmuster aus `stacks.md` laufen lassen. Jeder Treffer ist ein Kandidat, kein Befund.
3. **Live bestätigen** nach `verifikation.md`, inklusive Abschnitt 4a. Nicht live Prüfbares als "aus Code gefolgert" kennzeichnen. Eine reine Code-Lektüre ist kein Audit; geht kein Start, die Datei bzw. URL im agentfenster-Browser öffnen.
4. **Alle Bereiche der gewählten Domänen** durchgehen, auch wenn die Suchmuster nichts finden; die Pflicht-Gegenprüfung C1 bis C27 vollständig; `verboten.md` vollständig, sobald CV oder RT gilt.
5. **Bericht** im Format unten. Nichts ändern, solange der Auftrag nur Prüfen lautet.

### Befundformat

Eine Tabelle, sortiert nach Schweregrad, dann nach Aufwand:

| # | Schwere | Regel | Ort | Befund | Fix | Beleg |
|---|---|---|---|---|---|---|
| 1 | K | CV21 | `checkout.js:73` | Bestellen ohne Sperre und ohne Idempotency Key, Doppelklick legt zwei Bestellungen an | Guard vor `await`, Button "Wird bestellt…", Key je Checkout-Sitzung | live: Doppelklick bei Slow 3G, zwei POST `/api/order` |

- **Ort:** `Datei:Zeile`; bei rein visuellen Befunden Screen und Breite.
- **Fix:** konkret, mit Wert oder Codeform, im Stil des Projekts.
- **Beleg:** `live` mit Beobachtung oder `Code` (gefolgert, nicht gesehen).
- Schweregrad nie über der nachgewiesenen Auswirkung. Erfüllt ein Befund ein D-Muster aus `verboten.md`, ist er K, auch wenn die zugehörige CV- oder RT-Regel H trägt; ohne erfülltes D-Muster gilt der Grad der Regel.

Unter der Tabelle: **Hält** (was stimmt), **Nicht geprüft** (mit Grund, z. B. "Gerät nötig", "Rechtstext: `legal-at`"), **Entscheidungen** (mehr als eine richtige Lösung, je eine Empfehlung).

## Harte Regeln

- **Kein "fertig" und kein Audit ohne Sichtprüfung.** Fehlen die agentfenster-Werkzeuge, das sofort melden.
- **Pflichtumfang der Sichtprüfung:** Desktop-Breite (agentfenster) und 390 px (chrome-devtools-Emulation, weil agentfenster keine Fenstergröße setzt), Tastatur-Durchlauf mit echten Tab-Tasten, die Testfälle des Flows (Doppelklick, Fehlerpfad, Leer- und Ladezustand). "Nicht geprüft" ist nur mit technischem Grund zulässig (Werkzeug fehlt, Backend fehlt, echtes Gerät nötig), nie wegen Zeit oder weil der Auftraggeber es eilig hat. Jeder Fix, der nach der Verifikation noch gemacht wird, wird erneut gemessen, nicht nur per Grep bestätigt.
- **Lokale HTML-Dateien** über `python -m http.server <port> --bind 127.0.0.1` bereitstellen (der agentfenster-Browser öffnet kein `file://`), den Server nach der Prüfung selbst beenden.
- **Rechtsaussagen nur mit Norm aus diesem Skill;** was hier nicht steht oder sich seit dem Rechtsstand geändert haben kann, an `legal-at` geben statt aus dem Gedächtnis zu ergänzen. Rechtstexte (Impressum, AGB, Datenschutz, Widerrufsbelehrung) schreibt `legal-at`.
- **`verboten.md` geht vor jedem Auftrag.**
- **Keine erfundenen Befunde, Zahlen oder Bestätigungen.** Reel- und Herstellerzahlen nie als Beleg ausgeben (`mythen.md`).
- **Nichts ungefragt umbauen** im PRÜFEN-Modus; im BAUEN-Modus nur, was zum Auftrag gehört. Fremdes als "Separat".
- **Projektkonventionen vor Regelwerk-Werten,** solange sie keine K- oder H-Regel verletzen.
- **Lieber fünf verifizierte Befunde als zwanzig vermutete.**

## Abgrenzung

Für Tiefe in einem Teilgebiet zusätzlich laden, falls installiert: `ux-details-audit` (20 Politur-Details als eigener Bericht), `accessibility` (WCAG-Vollaudit), `review-animations` (Animationen im Diff), `break-ui` (Extremdaten-Toggle), `mobile-native` (Web am Handy), `web-quality-audit`/`core-web-vitals` (gemessene Ladezeit), `legal-at` (Rechtstexte, Freigabe). Visuelle Richtung (Stil, Schriftwahl, Markenfarben) liefern `frontend-design`, die taste-Skills und `design-unslop`; dieses Regelwerk setzt nur die messbaren Grenzen.

## Referenzen

- `references/regeln-bedienung.md`: Z, FO, T, N, L, E, A, M, X, Q mit Prüfung und Quelle
- `references/regeln-web.md`: WD (Typografie, Farbe, Layout, Landing, Navigation, Bilder, Lokalisierung), LA (Launch)
- `references/regeln-conversion.md`: CV (Recht vor dem Kauf, Checkout, Warenkorb, Pricing, nach dem Kauf)
- `references/regeln-retention.md`: RT (Onboarding, Streaks, Push, E-Mail-Recht, Abo, Kündigung, Win-back)
- `references/verboten.md`: D1 bis D23 mit Erkennung, Alternative, Rechtsgrundlage, Rationalisierungen
- `references/stacks.md`: Stack-Erkennung, richtige Umsetzung, Suchmuster
- `references/verifikation.md`: Start, agentfenster-Ablauf, Mess-Skripte, Extremdaten, Domänen-Prüfungen
- `references/widersprueche.md`: W1 bis W21, welche Quelle wo nachgibt
- `references/mythen.md`: Y1 bis Y17, Behauptungen, die nicht als Regel gelten
- `references/quellen.md`: Skill-Kürzel, Reels R01 bis R42 mit Post-Code, Primärquellen
