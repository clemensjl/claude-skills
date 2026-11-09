# Aufgelöste Widersprüche

Die Quellen dieses Skills widersprechen sich an einigen Stellen. Hier steht jeweils, wer was sagt, was gilt und warum. Die Regel-IDs verweisen auf `regeln.md`.

---

**W1 Submit-Button deaktivieren, bis alles gültig ist?**
- Reel R22: Button grau lassen, bis alle Pflichtfelder stimmen, aber deutlich zeigen, was fehlt.
- Vercel WIG: Button bleibt aktiv, bis der Request startet; Fehler inline, Fokus aufs erste Fehlerfeld.
- **Gilt:** Button aktiv. Tap auf Submit zeigt alle Fehler, fokussiert das erste fehlerhafte Feld und bei langen Formularen eine Zusammenfassung oben. Deaktiviert wird nur während des Requests (Z2).
- **Warum:** Ein deaktivierter Button ist nicht fokussierbar, Screenreader überspringen ihn, und er erklärt nicht, was fehlt. R22 räumt das selbst ein ("grayed out with no explanation is even more frustrating"). Wer trotzdem deaktiviert (sehr kurze Formulare, ein bis zwei Felder), muss den Grund sichtbar daneben schreiben (Z7).

**W2 Bestätigungsdialog oder Undo?**
- WIG: "confirmation modal or undo window".
- `ux-details-audit` 5: Undo statt Bestätigung.
- `apple-design` §16: Bestätigung nur bei wirklich unumkehrbaren Aktionen, sparsam.
- **Gilt:** Umkehrbar → Undo (Toast mit Rückgängig, Löschung verzögert oder Soft Delete). Unumkehrbar (Konto löschen, Zahlung, Versand an Dritte) → Dialog, Button benennt die Aktion. Beides fehlt → Befund K.
- **Warum:** Dialoge werden aus Gewohnheit weggeklickt; Undo schützt tatsächlich. Kein Undo ohne echte Rücknahme.

**W3 Reaktion beim Aufsetzen oder beim Loslassen?**
- `apple-design` §1, `mobile-native` §5: "respond on pointer-down".
- WCAG 2.5.2 Pointer Cancellation: Aktion nicht beim Down-Event auslösen.
- **Gilt:** Visuelles Feedback beim Aufsetzen, Aktion beim Loslassen; Wegziehen bricht ab. Apple sagt das in §10 selbst so ("highlight on touch-down, commit on touch-up").

**W4 Easing beim Ausblenden.**
- `motion-design`: Exit = ease-in (bzw. MD3 Accelerate).
- `emil-design-eng`, `review-animations`: nie ease-in auf UI; Ein- und Ausblenden ease-out.
- **Gilt:** In Produkt-UI ease-out für beides (starke Kurve). ease-in nur in erklärenden oder Marketing-Animationen, wo niemand auf eine Reaktion wartet.
- **Warum:** ease-in verzögert genau den Moment, in dem der Nutzer hinsieht; ein Schließen wirkt dann träge.

**W5 Wie viel kürzer ist der Exit?**
- R10: etwa 20 % kürzer. `motion-design`: Exit 65 bis 75 % des Entry. `emil-design-eng`: Exit schneller als Enter.
- **Gilt:** Exit 20 bis 35 % kürzer als Enter.

**W6 Maximale Dauer.**
- `emil-design-eng`: UI unter 300 ms, Modale/Drawer 200 bis 500 ms.
- `motion-design`: Persönlichkeit "Premium" 350 bis 600 ms, Modal 300 bis 400 ms, Seitenwechsel 400 bis 600 ms.
- **Gilt:** Produkt-UI nach Emil (M2). Die längeren Werte von `motion-design` nur für Marketing, Onboarding-Momente und erklärende Animationen.
- **Warum:** Häufig gesehene UI muss sich beim hundertsten Mal schnell anfühlen; `motion-design` misst Wirkung, nicht Wiederholung.

**W7 Mindestgröße für Tap-Ziele.**
- WCAG 2.2 SC 2.5.8 (AA), R11: 24 × 24 CSS-px oder ausreichender Abstand.
- `ux-details-audit` 13, `signup`, Apple HIG: 44 pt. Material: 48 dp. WCAG 2.5.5 (AAA): 44 px.
- **Gilt:** 44 pt (iOS, Web) bzw. 48 dp (Android) als Standard dieses Skills; 24 px ist die rechtliche Untergrenze und reicht nur bei dichten Desktop-Oberflächen mit Maus. Gemessen wird die Trefferfläche, nicht das Icon (R20).

**W8 Animation aus `scale(0)`.**
- `motion-design` (Confirmation Badge): "scales from 0".
- `emil-design-eng`, `review-animations`, R10: nie aus 0, Start bei 0,9 bis 0,97.
- **Gilt:** nie aus 0.

**W9 Validierung beim Tippen oder beim Verlassen?**
- R09: beim Verlassen, nach dem ersten Fehler bei jedem Tastendruck.
- R22: Passwort-Anforderungen live beim Tippen abhaken; E-Mail beim Verlassen.
- `apple-design`: inline, nicht erst beim Absenden.
- **Gilt:** FO2. Kein Widerspruch im Kern: Fehler erst nach Blur; positive Fortschrittsanzeigen (Passwort-Checkliste, Zeichenzähler) dürfen live laufen, weil sie nicht bestrafen.
- **Hinweis Flutter:** `AutovalidateMode.onUserInteraction` validiert ab dem ersten Tastendruck und erfüllt FO2 damit nicht; Blur-Validierung über `FocusNode`-Listener.

**W10 Bounce bei Springs.**
- `emil-design-eng`: Bounce 0,1 bis 0,3, "avoid in most UI".
- `apple-design`: Dämpfung 1,0 als Standard, Bounce nur nach Schwung.
- R10: kein Spring-Bounce für alltägliche UI-Übergänge.
- **Gilt:** M8, Bounce 0 als Standard; nur nach Gesten mit Geschwindigkeit bis ca. 0,2.

**W11 Wo Feedback-Dauer und Latenz-Grenzen liegen.**
- R06: Antwort innerhalb einer Zehntelsekunde.
- `motion-design`: Press/Tap unter 150 ms. `emil-design-eng`: Press-Feedback 100 bis 160 ms.
- **Gilt:** Das Feedback beginnt innerhalb von 100 ms (Z1); die Animation des Feedbacks selbst darf 100 bis 160 ms dauern. Das eine ist Latenz, das andere Dauer.

**W12 Reduced Motion: alles aus oder sanfter?**
- `accessibility`: globaler Schalter, alle Animationen und Transitions auf 0,01 ms.
- `emil-design-eng`, `apple-design`: weniger und sanfter, nicht null; Überblendungen behalten.
- **Gilt:** Bewegung (Verschieben, Skalieren, Parallax, Springs) entfällt, kurze Überblendungen bleiben, wo sie einen Zustandswechsel lesbar machen. Der globale 0,01-ms-Schalter ist als Notnagel zulässig, wenn keine Überblendung Information trägt.

**W13 `overscroll-behavior` auf der Seite.**
- `mobile-native`: `overscroll-behavior: none` auf `html, body` in der Baseline.
- WIG: nur innerhalb `@media (pointer: fine)`, auf Touch Pull-to-Refresh erhalten.
- **Gilt:** App-Shell mit eigenen Scroll-Containern (PWA, Expo Web als App): `none` auf der Seite, `contain` in Sheets. Dokumentartige Seite: Standard lassen, `contain` nur in Sheets und Modalen. `mobile-native` nennt diese Ausnahme selbst am Ende der Baseline.

**W14 Was ist "großer Text" für den Kontrast?**
- `accessibility` (SKILL.md): "≥ 18px / ≥ 14px bold".
- WCAG 2.2 Definition: 18 pt bzw. 14 pt fett, also 24 px bzw. ca. 18,66 px fett.
- **Gilt:** WCAG. Die px-Angabe in `accessibility` verwechselt pt und px und würde 18-px-Text fälschlich mit 3:1 durchwinken.

**W15 Title Case für Buttons.**
- WIG: Title Case nach Chicago.
- **Gilt:** nur für englische UI. Deutsche UI schreibt Buttons im Satzbau ("Mahlzeit speichern").
