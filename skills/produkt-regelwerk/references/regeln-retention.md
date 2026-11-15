# Retention, Onboarding, Benachrichtigungen, Abos (RT)

Für alles, was Nutzer zum Wiederkommen bringen soll: Aktivierung und Onboarding, Gewohnheit (Streaks), Push, E-Mail, Abo-Verwaltung, Kündigung, Zahlungsausfall, Win-back. Grundsatz: **Retention entsteht durch Wert, nicht durch Hürden.** Erschwerte Kündigung verschiebt Churn nur nach hinten und erzeugt Chargebacks, schlechte Bewertungen und Rechtsrisiko. Alles, was Nutzer gegen ihren Willen festhält, steht in `verboten.md` und wird nie gebaut, auch nicht auf ausdrücklichen Wunsch (dann Alternative aus dieser Datei anbieten).

Rechtsstand 15.11.2026 (EU/AT, Kernnormen am RIS gegengeprüft): Einen allgemeinen gesetzlichen Kündigungsbutton gibt es in AT nicht (DE: § 312k BGB). Erschwerte Kündigung beurteilt § 1a UWG (aggressive Geschäftspraktik; Kriterium Abs. 2 Z 4: "belastende oder unverhältnismäßige Hindernisse nichtvertraglicher Art", insbesondere beim Kündigen). DSA Art. 25 gilt nur für Online-Plattformen (nicht für Kleinst- und Kleinunternehmen, nicht wo UGP-RL oder DSGVO greifen). Der Digital Fairness Act (COM(2026) 1100 vom 11.11.2026: Kündigungsfunktion, Autoverlängerung, Probeabo-Fallen, Dark-Pattern-Liste) ist nur ein Vorschlag; seine Regeln stehen hier als Best Practice, weil sie absehbar Pflicht werden.

Zahlen aus Anbieter-Blogs (Recurly, Recharge, Churnkey) zeigen Größenordnungen, keine Kausalität; im eigenen Produkt per A/B-Test messen.

---

## RT-0. Grundregel

**RT1 (K) Wer online abschließen kann, kann online kündigen,** mit nicht mehr Schritten und keiner stärkeren Anmeldung als beim Abschluss. Pfad Konto > Abo > "Abo kündigen" höchstens 3 Klicks von jeder Abo-Ansicht, Button eindeutig beschriftet. Kein Zwang zu Telefon, Brief, Chat, Termin oder Retention-Gespräch.
Prüfen: Klicks zählen für Abschluss und Kündigung; Kündigen ohne Support-Kontakt möglich?
Quelle: § 1a Abs. 1 iVm Abs. 2 Z 4 UWG, DSA Art. 25 Abs. 3 lit. c (Plattformen), DFA-Vorschlag.

---

## RT-A. Aktivierung und Onboarding

**RT2 (H) Eine definierte Aktivierungsaktion (Aha-Moment) je Produkt,** und der kürzeste Weg dorthin wird gemessen (Zeit bis zur Aktion, Abbruchstelle). Das Onboarding führt direkt dorthin.
Quelle: Recurly/Hanover (66 % der Kündigungen im ersten Jahr, Herstellerumfrage), N7.

**RT3 (M) Onboarding kurz, überspringbar, wieder aufrufbar.** Erklärungen kontextuell beim ersten Bedarf statt Pflicht-Tutorial vor der Nutzung. Checkliste mit Fortschritt höchstens 3 bis 5 Schritte, die zur Aktivierungsaktion führen.
Quelle: NNG Onboarding Tutorials, N7 (Praxis für Checkliste).

**RT4 (M) Im Onboarding keine Werbung, keine Bewertungsbitte, keine Push-Abfrage vor dem ersten Wertmoment** (RT8).
Quelle: MAT3 Notifications.

**RT5 (M) Leere Zustände sind Onboarding:** jede leere Liste erklärt den Bereich und bietet die Aktion zum ersten Eintrag, optional mit Beispieldaten (E1).
Quelle: ON, E1.

---

## RT-B. Gewohnheit und Streaks

**RT6 (M) Streak zählt schon durch eine minimale Aktion,** getrennt vom Tagesziel.
Quelle: Duolingo A/B (+3,3 % Tag-14-Retention, Unternehmensdaten).

**RT7 (M) Streaks haben eine eingebaute Pause** (Freeze, Wochenend-Schutz), die der Nutzer vorab aktiviert; Erinnerung höchstens 1 pro Tag, abschaltbar, ohne Schuld- oder Angsttext ("Dein Streak stirbt!"). Gegenüber Kindern nie mit Kaufaufforderung verknüpfen (D20). Die Streak-Erinnerung zählt als vom Nutzer bestellte Erinnerung, nicht als Marketing-Push nach RT11.
Quelle: Duolingo (Weekend Amulet: +4 % Rückkehr), DFA-Vorschlag, UWG Anhang Z 28.

---

## RT-C. Benachrichtigungen

**RT8 (H) System-Abfrage für Push nie beim ersten Start.** Auslöser ist ein Wertmoment (Bestellung aufgegeben, Eintrag gespeichert, Session beendet), davor ein eigener Hinweis, der konkret nennt, was kommt ("Wir melden uns, wenn deine Bestellung unterwegs ist"). Auf iOS ist eine Ablehnung nicht wiederholbar.
Quelle: NNG Push Notifications.

**RT9 (H) Einstellungen nach Kategorien in der App,** Ein/Aus in höchstens 2 Taps, nicht nur in den Systemeinstellungen.
Quelle: NNG, MAT3.

**RT10 (H) Jede Push-Nachricht hat eigenen Wert für den Nutzer:** keine "Wir vermissen dich", Geburtstagsgrüße, Bewertungsbitten oder Cross-Promotion als Push; keine erfundenen Anlässe ("Jemand hat dir geschrieben", D16).
Quelle: MAT1 Notifications Pattern, Play-Store-Regeln.

**RT11 (M) Frequenz begrenzt und gemessen:** Marketing-Push höchstens ca. 1 pro Woche, transaktionale nach Bedarf; Ruhezeiten (z. B. 21 bis 8 Uhr Ortszeit); mehr als 5 ausstehende bündeln; Opt-out-Rate je Versand messen, Alarm ab 1 bis 2 %.
Quelle: NNG, Airship (Korrelation), Praxis.

**RT12 (N) Texte:** Titel unter ca. 30 Zeichen, Wochentag statt "heute/morgen" (wird oft später gelesen).
Quelle: MAT3 Notifications.

---

## RT-D. E-Mail, Einwilligung (Recht)

**RT13 (K) Werbe-E-Mail und -SMS nur mit nachweisbarer Einwilligung** (Zeitpunkt, Text, Quelle, Double-Opt-in-Bestätigung gespeichert) oder bei Bestandskunden nur, wenn alle vier Bedingungen zugleich gelten: Kontakt aus Verkauf/Dienstleistung, nur eigene ähnliche Produkte, Ablehnung bei Erhebung und in jeder Nachricht kostenfrei möglich, Empfänger nicht in der ECG-Liste. Marketing-Push und In-App-Werbung wie Werbe-Mail behandeln (eigene Einwilligung; die System-Push-Erlaubnis ist keine Werbeeinwilligung).
Quelle: § 174 Abs. 3/4 TKG 2021, DSGVO Art. 7.

**RT14 (K) Jede Werbenachricht nennt den Absender und hat eine funktionierende Abmeldung mit einem Klick,** ohne Login, kostenfrei. Widerruf nie schwerer als die Erteilung.
Quelle: § 174 Abs. 5 TKG 2021, Art. 7 Abs. 3 DSGVO.

**RT15 (H) Service-Nachrichten ohne Werbung:** Bestell-, Zahlungs-, Sicherheits-, Kündigungs- und Vertragsmails enthalten keine Angebote; sonst werden sie zu Werbung und brauchen RT13.
Quelle: § 174 TKG (Auslegung).

**RT16 (K) Einwilligungs-Checkboxen sind leer, je Zweck getrennt, nicht an den Vertrag gekoppelt** und nicht in AGB gebündelt. "Newsletter und Angebote von Partnern" in einer vorangekreuzten Box ist doppelt unzulässig (D4).
Quelle: Art. 4 Nr. 11, Art. 7 DSGVO, EDPB 03/2022.

**RT17 (H) Getroffene Wahl wird respektiert:** Nach "Nicht jetzt" (Push, Newsletter, Upsell, Bewertung) dieselbe Frage nicht in derselben Sitzung und frühestens nach einer definierten Sperrfrist (Vorschlag 30 Tage) und nur bei neuem Anlass (D13).
Quelle: DSA Art. 25 Abs. 3 lit. b, EDPB "continuous prompting".

---

## RT-E. Abo-Gestaltung, Verlängerung, Zahlung

**RT18 (K) Abo-Bedingungen vor dem Abschluss im Sichtfeld** (CV2): Preis je Periode, Mindestlaufzeit, automatische Verlängerung, Kündigungsfrist und -weg, erste Belastung nach Testphase.
Quelle: Art. 8 Abs. 2 VRRL, § 8 FAGG.

**RT19 (H) Testphase mit Zahlungsmittel: Erinnerung 2 bis 3 Tage vor Ende** per E-Mail (und Push, falls erlaubt) mit Enddatum, Preis und Ein-Klick-Weg zum Beenden.
Quelle: DFA-Vorschlag, UCPD-Leitlinie 2.9.6 (Abofallen).

**RT20 (H) Erinnerung vor automatischer Verlängerung** von Verträgen ab 6 Monaten Laufzeit (Jahresabo): 14 bis 30 Tage vorher, mit Betrag, Datum und Kündigungslink. Preiserhöhungen nur mit Vorab-Mitteilung und Hinweis auf die Kündigungsmöglichkeit.
Quelle: DFA-Vorschlag (Best Practice), EPRS (62 % erlebten Verlängerung ohne Erinnerung).

**RT21 (H) Zahlungsausfall (Dunning):** automatische Wiederholversuche, Service-Mail mit direktem Link zum Aktualisieren der Zahlungsart, Erinnerungen nach ca. 3 und 7 Tagen, Kulanzzeit vor Sperre, im Produkt ein Banner statt sofortiger Sperre. Keine Werbung in diesen Mails (RT15).
Quelle: Stripe Smart Retries, Recurly (Praxis; unfreiwilliger Churn ist ein großer vermeidbarer Anteil).

**RT22 (N) Jahresplan als Option neben dem Monatsplan,** mit ehrlich gerechneter Ersparnis ("79 € statt 119,88 €"), nie vorausgewählt.
Quelle: Praxis, CV29.

**RT23 (M) Treue belohnen statt Austritt bestrafen,** z. B. Preis sinkt mit Abo-Dauer, Bonusinhalte ab Monat X, eingefrorener Bestandskundenpreis. Die Regeln stehen vor dem Abschluss transparent da, und eine Kündigung kostet nichts außer dem künftigen Vorteil (kein Datenverlust, keine Strafgebühr).
Quelle: R42 (Idee, keine Daten), Verlustaversion; als Hypothese per A/B-Test prüfen.

---

## RT-F. Kündigung, Pause, Win-back

**RT24 (K) Kündigen ist nie von einer Umfrage, einem Angebot oder einem Gespräch abhängig.** Jede Zwischenstufe hat einen gleich großen, gleich kontrastreichen Weg "Trotzdem kündigen" bzw. "Kündigung bestätigen". Höchstens eine Frage (Multiple Choice mit 4 bis 6 Gründen plus "Sonstiges", überspringbar), Freitext optional.
Quelle: § 1a UWG, DSA Erw. 67, Praxis (Churnkey).

**RT25 (H) Höchstens ein Gegenangebot pro Kündigungsversuch, passend zum Grund:** "zu teuer" → Downgrade oder Jahresplan; "gerade keine Zeit" → Pause 1 bis 3 Monate; "fehlt etwas" → Feedback-Kontakt. Rabatt höchstens einmal pro Kunde, sonst kündigen Nutzer gezielt für den Rabatt.
Quelle: Recurly, Recharge (Save-Raten 10 bis 25 %, Herstellerdaten).

**RT26 (H) Pause verwandelt sich nur mit Vorab-Erinnerung zurück in ein zahlungspflichtiges Abo** (3 bis 7 Tage vorher, mit Ein-Klick-Kündigung). Ohne Erinnerung: D15.
Quelle: UCPD Art. 7, DFA-Vorschlag.

**RT27 (H) Kündigungsbestätigung sofort per E-Mail** mit Enddatum, Zugang bis Periodenende, "keine weitere Abbuchung", Ein-Klick-Link "Kündigung zurücknehmen". Im Produkt bleibt der Zugang bis zum Ende; Datenexport bleibt verfügbar; Daten werden nach einer genannten Frist gelöscht.
Quelle: DFA-Vorschlag, Art. 20 DSGVO, Praxis.

**RT28 (M) Win-back höchstens 3 Nachrichten in 90 Tagen** (z. B. Tag 30 Neuigkeiten, Tag 60 Angebot, Tag 90 letzte), nur mit Rechtsgrundlage nach RT13, jede mit Abmeldung. Danach Ruhe.
Quelle: ChartMogul (45 % der Rückkehrer binnen 30 Tagen), Praxis.

**RT29 (M) Retention messen, nicht vermuten:** Aktivierungsrate, Tag-1/7/30-Retention, Kündigungsgründe als Trend, Save-, Pause- und Rückkehrrate, Chargeback-Quote. Steigende Chargebacks nach einer Flow-Änderung sind ein Warnsignal für ein Dark Pattern.
Quelle: Praxis.

**RT30 (K) App-Store-Abos:** Abos über Apple oder Google lassen sich nur dort verwalten; die Abo-Seite erkennt die Quelle und verlinkt direkt in die Abo-Verwaltung des Stores, statt einen toten Kündigen-Button zu zeigen.
Quelle: Apple/Google Plattformregeln, RT1.
