# Pflicht-Verifikation

Code lesen ist kein Beleg. Ein Befund im PRÜFEN-Modus und ein "fertig" im BAUEN-Modus stützen sich auf das laufende Produkt. Was nicht live geprüft werden konnte, steht im Bericht unter "nicht geprüft", mit Grund.

## 1. Produkt starten

| Stack | Start | Prüfziel |
|---|---|---|
| Next.js / Vite | `npm run dev`, Port aus der Ausgabe | `http://localhost:<port>` |
| Expo / React Native | `npx expo start --web` für den Web-Build; nativ: Android-Emulator (`npx expo start --android`) oder Expo Go am Gerät | Web: `http://localhost:8081`; nativ: Emulatorfenster |
| Flutter | `flutter run -d chrome` oder `-d windows`; mobil: Emulator | Browser bzw. App-Fenster |
| Einzelne HTML-Datei | `python -m http.server 8765 --bind 127.0.0.1` im Ordner der Datei, danach selbst beenden | `http://127.0.0.1:8765/<datei>.html` |
| Live-Deploy | — | URL; Login über Clemens' Sitzung im agentfenster-Browser |

Dev-Server im Hintergrund starten und nur die eigenen Prozesse wieder beenden. Im PRÜFEN-Modus nichts am Projekt ändern; ist kein Start möglich (fehlende `.env`, Backend), die Live-URL nehmen oder den Punkt als "nicht geprüft" führen.

## 2. Sichtprüfung mit agentfenster

Werkzeug: `mcp__agentfenster__browser` (unsichtbarer Desktop, angemeldete Sitzung). Für Desktop-, Electron- und Emulatorfenster `open_app`, `read_desktop`, `click`.

Ablauf je Screen:
1. `open` mit der URL, dann `screenshot` und `read` (Elementbaum mit Rollen und Namen).
2. **Breiten:** 390 px (Mobile), 768 px, 1280 px oder breiter. Der agentfenster-Browser hat derzeit keine Aktion für die Fenstergröße. Für die Mobile-Breite ausnahmsweise chrome-devtools `new_page` (mit `isolatedContext`) plus `emulate` mit `viewport: "390x844x3,mobile,touch"` nutzen, dort die Mess-Skripte aus Abschnitt 3 laufen lassen und das im Bericht nennen. Hängt dort `take_screenshot`, reichen die Messwerte; die Sichtbeurteilung bleibt beim agentfenster-Screenshot.
3. **Zustände auslösen:** Ruhe, Laden (Netz drosseln oder langsamen Request abwarten), Leer, Fehler (Netz aus, ungültige Eingabe), Erfolg. Jeder Zustand ein Screenshot.
4. **Tastatur-Durchlauf (Web und Expo Web):** `press` mit `tab` durch den ganzen Screen. Echte Tastendrücke verwenden: ein per Skript gesetztes `element.focus()` löst `:focus-visible` an Buttons nicht aus und täuscht einen fehlenden Fokusring vor. Prüfen mit `document.activeElement.matches(':focus-visible')` plus Screenshot. Je Schritt: Ist der Fokus sichtbar (A1)? Stimmt die Reihenfolge mit der Optik (A2)? Lassen sich alle Aktionen mit `enter`/`space` auslösen? Schließt `escape` Dialoge und Sheets? Kommt der Fokus danach zum Auslöser zurück?
5. **Formular-Testfälle** (FO2, FO4, Z2): ungültig tippen ohne Verlassen, Feld verlassen, korrigieren, leer absenden, Doppelklick auf Submit. Position des Submit-Buttons vor und nach der Fehleranzeige vergleichen.
6. **Extremdaten** (Abschnitt 4) einspielen, wo das ohne Änderung am Projekt geht (Testkonto, Eingabe in Formulare, lokaler Mock). Sonst aus dem Code begründen und als "aus Code gefolgert" markieren.
7. **Reduced Motion und Dark Mode**, wenn das Produkt Bewegung bzw. ein dunkles Theme hat.

## 3. Messen statt schätzen (per `eval`, falls Skripte erlaubt)

Zu kleine Trefferflächen (T1). Achtung: In Expo Web greift `hitSlop` nicht in `getBoundingClientRect`; RN-`hitSlop` aus dem Code dazurechnen und auf Gerät prüfen.
```js
[...document.querySelectorAll('button,a[href],[role=button],[role=tab],[role=checkbox],input,select,textarea')]
  .map(e => [e, e.getBoundingClientRect()])
  .filter(([e, r]) => r.width && r.height && (r.width < 44 || r.height < 44))
  .map(([e, r]) => `${Math.round(r.width)}x${Math.round(r.height)} ${(e.getAttribute('aria-label') || e.innerText || e.tagName).trim().slice(0, 40)}`)
```

Bedienelemente ohne Namen (A3):
```js
[...document.querySelectorAll('button,a[href],[role=button]')]
  .filter(e => !(e.innerText.trim() || e.getAttribute('aria-label') || e.getAttribute('aria-labelledby') || e.title))
  .map(e => e.outerHTML.slice(0, 120))
```

Felder ohne Label (FO1):
```js
[...document.querySelectorAll('input:not([type=hidden]),textarea,select')]
  .filter(e => !(e.labels?.length || e.getAttribute('aria-label') || e.getAttribute('aria-labelledby')))
  .map(e => e.outerHTML.slice(0, 120))
```

Horizontales Scrollen bei 320 bis 390 px (A7): `document.documentElement.scrollWidth > innerWidth`.

Input-Schriftgröße unter 16 px (FO15):
```js
[...document.querySelectorAll('input,textarea,select')].filter(e => parseFloat(getComputedStyle(e).fontSize) < 16).length
```

Kontrast: Farben aus `getComputedStyle` gegen die Formel prüfen oder Lighthouse/axe als Messreihe laufen lassen; das Urteil bleibt beim Screenshot.

## 4. Extremdatensatz (Kurzform von `break-ui`)

Plausibel, nie Zufallsmüll. Mehrere Fälle auf die ersten sichtbaren Zeilen verteilen.

| Feld | Werte |
|---|---|
| Name | `Aleksandra Wiśniewska-Kowalczyk`, `Jo`, `Đặng Thị Ngọc Hân`, `王秀英`, `🦊 Fox`, fehlend |
| E-Mail | `bartholomew.fitzgerald@northwind-industries-holdings.example.com`, `a@b.co` |
| Label aus Daten | `Benachrichtigungseinstellungen`, 2.000 Zeichen Beschreibung, Zeilenumbruch im einzeiligen Feld |
| Zahl | `0`, `1` (Plural), `1284`, `12345678,9`, `-42,5`, `142 %`, `null` |
| Liste | 0, 1, Seitengröße + 1, 1.000 Einträge |
| Zeit | jetzt, 23:59 und 00:01 (Tagesgrenze), vor 12 Tagen, Zukunft |
| Bild | 404, fehlend, 4000 × 200 |
| Umgebung | 320 px Breite, 200 % Zoom bzw. größte Systemschrift, Dark Mode, Netz aus |

## 4a. Domänen-Prüfungen (Web, Conversion, Retention)

Nur die Domänen, die der Auftrag berührt (Tabelle "Domänen" in `SKILL.md`).

**Web und Launch (WD, LA)**, per `eval` bzw. Shell:
```js
({
  title: document.title,
  h1: document.querySelectorAll('h1').length,
  viewport: document.querySelector('meta[name=viewport]')?.content ?? null,
  description: document.querySelector('meta[name=description]')?.content?.length ?? 0,
  og: ['og:title','og:description','og:image','og:url'].filter(k => !document.querySelector(`meta[property="${k}"]`)),
  lang: document.documentElement.lang,
  imgOhneMasse: [...document.images].filter(i => !(i.getAttribute('width') || getComputedStyle(i).aspectRatio !== 'auto')).length,
  imgOhneAlt: [...document.images].filter(i => !i.hasAttribute('alt')).length,
  lcpLazy: [...document.images].filter(i => i.loading === 'lazy' && i.getBoundingClientRect().top < innerHeight).length,
  reinSchwarz: getComputedStyle(document.body).backgroundColor,
})
```
Shell: `curl -sI https://<domain>/gibt-es-nicht` (404 erwartet), `curl -sIL http://<domain>` (ein 301 auf HTTPS), `curl -s https://<domain>/robots.txt`, `/sitemap.xml`, `/favicon.ico`. Lighthouse Mobile als Messreihe.

**Conversion (CV)**, im laufenden Checkout mit Testdaten bzw. Test-Modus des Zahlungsanbieters:
- Text des Bestell-Buttons wörtlich notieren (CV1); was steht im selben Sichtbereich darüber (CV2)?
- Preisformat an Karte, Warenkorb, Summe (`39,99 €`, inkl. USt, Versandhinweis; CV3, WD31).
- Gebühren je Schritt notieren: taucht im letzten Schritt etwas Neues auf (CV4)?
- Alle Checkboxen im Ausgangszustand: keine vorangekreuzt (CV5, RT16).
- Fehlerpfad: ungültige Karte bzw. Testkarte "declined", danach sind alle Eingaben noch da (CV19, CV20).
- Doppelklick auf Bestellen bei gedrosseltem Netz: eine Bestellung (CV21).
- Reload der Bestätigungsseite: keine zweite Bestellung, Bestellnummer sichtbar (CV31).
- Countdown oder Knappheitsanzeige: Seite neu laden, Wert springt zurück oder ändert sich zufällig? Dann D1/D2.

**Retention (RT)**:
- Klicks zählen: Abschluss bis Bezahlung vs. Konto bis Kündigung bestätigt (RT1). Jede Zwischenseite hat "Kündigung bestätigen" ohne Pflichtantwort (RT24)?
- Kündigungsbestätigung und Zugang bis Periodenende sichtbar (RT27).
- Erster App-Start: erscheint eine System-Push-Abfrage, bevor der Nutzer etwas getan hat (RT8)?
- Newsletter- und Marketing-Checkboxen leer, Abmeldelink im Mail-Template vorhanden (RT13, RT14).
- Nach "Nicht jetzt" denselben Screen erneut öffnen: kommt die Frage wieder (RT17, D13)?

## 5. Was nur am echten Gerät geht

Emulation und Desktop-Browser zeigen nicht: klebende Hover-Zustände, Tap-Highlight, Tap-Verzögerung, Input-Zoom auf iOS, Safe Areas mit Notch, Software-Tastatur über Feldern, Rubber-Banding, Haptik, Gestengefühl. Diese Punkte im Bericht als "Gerät nötig" führen, nicht als bestanden.

## 6. Beleg im Bericht

Je geprüftem Screen: URL bzw. Fenster, Breiten, ausgelöste Zustände, Tastatur-Durchlauf ja/nein, Screenshot-Pfade oder Beobachtung in einem Satz. Ohne diese Zeile gilt der Screen als nicht geprüft.
