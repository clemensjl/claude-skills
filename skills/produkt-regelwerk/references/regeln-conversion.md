# Conversion, Checkout, Preise, Vertrauen (CV)

Für alles, wo Nutzer kaufen, buchen, sich registrieren oder ein Angebot anfragen: Produktseite, Warenkorb, Checkout, Pricing-Seite, Signup, Bestätigung. CV34 steht inhaltlich bei CV10 (vorvertragliche Infos), die Nummer ist später vergeben. Rechtsregeln gelten für B2C an Verbraucher in EU/AT (Stand 15.11.2026, Kernnormen am RIS gegengeprüft; vor Livegang über `legal-at` bestätigen). Der Digital Fairness Act (Verordnungsvorschlag COM(2026) 1100 vom 11.11.2026) ist noch kein geltendes Recht. Verbotene Taktiken stehen gesammelt in `verboten.md`, hier nur als Verweis.

Kernzahlen Baymard (US-Befragung, Anteil an Abbrüchen, Stand 10/2026): Zusatzkosten 40 %, Lieferung zu langsam 20 %, kein Vertrauen für Kartendaten 19 %, Kontozwang 18 %, Checkout zu lang 17 %, Fehler/Absturz 17 %, Rückgabe unklar 13 %, Gesamtkosten vorab nicht sichtbar 12 %, Karte abgelehnt 10 %, zu wenige Zahlarten 9 %. Durchschnittliche Warenkorb-Abbruchquote 70 %.

---

## CV-A. Rechtlich zwingend vor dem Kauf (EU/AT)

**CV1 (K) Bestell-Button eindeutig: "zahlungspflichtig bestellen"** oder gleichwertig eindeutig ("Kaufen", "Jetzt kaufen", "Kostenpflichtig abonnieren"). Nicht: "Weiter", "Bestellen", "Absenden", "Submit", "Anmelden", "Jetzt testen". Gilt für jeden Weg, der zahlungspflichtig bindet: Express-Wallet, Ein-Klick-Kauf, In-App-Upgrade, Testphase mit späterer Zahlung. Maßgeblich ist nur der Button-Text. Rechtsfolge eines falschen Texts: Der Verbraucher ist an die Bestellung nicht gebunden.
Prüfen: Text jedes Elements, das die Bestellung auslöst.
Quelle: Art. 8 Abs. 2 VRRL, § 8 Abs. 2 FAGG ("ausschließlich mit den Worten 'zahlungspflichtig bestellen' oder einer gleichartigen, eindeutigen Formulierung"), EuGH C-249/21.

**CV2 (K) Pflichtinfos unmittelbar über dem Bestell-Button, nicht nur verlinkt:** wesentliche Merkmale, Gesamtpreis inkl. USt und aller Versand- und Zusatzkosten; bei Abo zusätzlich Preis je Abrechnungszeitraum, Mindestlaufzeit, automatische Verlängerung, Kündigungsbedingungen, Zeitpunkt der ersten Belastung nach einer Testphase. Bei Waren mit Hersteller-Haltbarkeitsgarantie über 2 Jahre (Verträge ab 27.09.2026) auch die harmonisierte Garantie-Kennzeichnung.
Quelle: Art. 6 Abs. 1 und Art. 8 Abs. 2 VRRL, § 8 Abs. 1 FAGG iVm § 4 Abs. 1 Z 12a und Anhang III FAGG.

**CV3 (K) Verbraucherpreise sind Bruttopreise in Euro** und tragen den Hinweis "inkl. USt, zzgl. Versand" (mit Link auf die Versandkosten) bzw. "inkl. Versand". Netto nur zusätzlich und nur neben dem Bruttopreis; "zzgl. USt" nur auf erkennbar reinen B2B-Seiten.
Quelle: § 9 PrAG, § 5 Abs. 2 ECG.

**CV4 (K) Keine Kosten, die erst im letzten Schritt auftauchen.** Versand-, Service-, Verpackungsgebühren spätestens im Warenkorb als Zahl oder berechenbare Regel. Nicht genannte Zusatzkosten muss der Verbraucher nicht zahlen, und sie sind der häufigste Abbruchgrund (40 %).
Quelle: Art. 6 Abs. 6 VRRL, Baymard.

**CV5 (K) Zusatzleistungen nur per aktivem Opt-in:** Versicherung, Express, Geschenkverpackung, Garantie, Spende standardmäßig aus, jeweils mit eigenem Preis. Eine nicht abgewählte Voreinstellung ist keine Zustimmung; der Betrag ist zurückzuzahlen. Gilt für alle Verbraucherverträge, nicht nur online. Siehe D4.
Quelle: Art. 22 VRRL, § 6c KSchG.

**CV6 (K) Kein Aufschlag für eine Zahlart** (Karte, PayPal, Rechnung, Wallet). Rabatt für eine Zahlart ist erlaubt.
Quelle: § 56 Abs. 3 ZaDiG 2018 (AT, strenger als Art. 19 VRRL).

**CV7 (H) Liefergebiete und akzeptierte Zahlarten spätestens zu Beginn des Bestellvorgangs** sichtbar, nicht erst beim Fehlschlag.
Quelle: Art. 8 Abs. 3 VRRL, § 8 Abs. 3 FAGG.

**CV8 (K) Rabatte auf Waren nennen den niedrigsten Preis der letzten 30 Tage.** Streichpreis und Prozentangabe werden aus dem 30-Tage-Tiefstpreis desselben Vertriebskanals gerechnet, nicht aus UVP oder letztem Listenpreis. Schrittweise steigende Ermäßigung: Bezug bleibt der Preis vor der ersten Ermäßigung. Ware kürzer als 30 Tage am Markt: Tiefstpreis seit Markteintritt. Gilt für Sachgüter, nicht für Dienstleistungen (bei Abos und SaaS trotzdem nie irreführend, D8). Technisch: Preishistorie je Artikel und Kanal speichern.
Quelle: Art. 6a RL 98/6/EG, § 9a PrAG, EuGH C-330/23 (Prozentangabe), Kommissionsleitlinie 2021/C 526/02.

**CV9 (K) Widerrufsfunktion bei online geschlossenen Fernabsatzverträgen mit Rücktrittsrecht** (AT: Verträge ab 01.10.2026; EU-Richtlinie seit 19.06.2026): während der gesamten Frist durchgehend verfügbare, hervorgehobene Funktion "Vertrag widerrufen" bzw. gleichartig eindeutig. Formular fragt nur Name, Angaben zur Identifizierung des Vertrags und den elektronischen Kanal für die Bestätigung ab (eingeloggt vorausgefüllt). Bestätigungsbutton ausschließlich "Widerruf bestätigen" bzw. gleichartig, kein Gegenangebot in diesem Schritt. Unverzüglich Eingangsbestätigung auf dauerhaftem Datenträger mit Inhalt, Datum und Uhrzeit; Absenden vor Fristende wahrt die Frist. Die vorvertragliche Information nennt, wo die Funktion zu finden ist. Gilt für alle über eine Online-Oberfläche geschlossenen Fernabsatzverträge, nicht nur Finanzdienste. **Das ist keine Kündigungsfunktion für Abos** (dafür RT1). Verstoß ist eine Verwaltungsübertretung.
Quelle: Art. 11a VRRL idF RL (EU) 2023/2673; § 13a, § 4 Abs. 1 Z 8, § 19 Abs. 1 Z 6a, § 20 Abs. 5 FAGG idF BGBl. I Nr. 59/2026.

**CV10 (H) Vertragsbestätigung auf dauerhaftem Datenträger** (E-Mail/PDF) mit allen Pflichtinfos, spätestens bei Lieferung; die Bestätigungsseite ersetzt sie nicht. Sofort startende digitale Leistungen: nicht vorangekreuzte Zustimmung zum vorzeitigen Beginn mit Hinweis auf Verlust des Widerrufsrechts, in der Bestätigung wiederholt.
Quelle: Art. 8 Abs. 7/8, Art. 16 lit. m VRRL.

**CV34 (H) Neue Pflichtinfos für Verträge ab 27.09.2026 (Waren, digitale Leistungen):** hervorgehobene harmonisierte Mitteilung zur gesetzlichen Gewährleistung (Muster Anhang II FAGG), ggf. Haltbarkeitsgarantie-Kennzeichnung (Anhang III, auch direkt vor dem Button, CV2), Mindestzeitraum für Software-Updates, Reparierbarkeitswert bzw. Ersatzteilinfo, umweltfreundliche Liefermöglichkeiten, sofern vorhanden. Wortlaut und Gestaltung über `legal-at`.
Quelle: RL (EU) 2024/825; § 4 Abs. 1 Z 7, 12 bis 12d, 20, 21 FAGG, § 20 Abs. 6 FAGG, § 5a Abs. 1 KSchG.

**CV11 (K) Bewertungen nur als "Kundenbewertungen" ausweisen, wenn sie geprüft sind,** und neben den Bewertungen sagen, ob und wie geprüft wird. Keine selbst geschriebenen, gekauften oder gefilterten Bewertungen (D6).
Quelle: UWG Anhang Z 23b/23c (UCPD Anhang I Nr. 23b/23c), Art. 7 Abs. 6 UCPD.

**CV12 (K) Knappheit und Fristen nur, wenn wahr und technisch gedeckt** (echter Lagerbestand, echtes serverseitiges Ende, kein Reset bei Reload, keine Zufallszahlen). Siehe D1, D2.
Prüfen: `Math.random` in Countdown-, Lager- oder "x schauen gerade"-Komponenten; Timer nach Reload.
Quelle: UWG Anhang Z 7 (UCPD Anhang I Nr. 7), Art. 6 UCPD.

**CV13 (H) Ablehnen ist gleich sichtbar wie Annehmen** bei Upsell, Abo, Zusatzprodukt, Versandart: gleiche Größe und Lesbarkeit, neutrales Label, keine Schuldformulierung, keine erneute Aufforderung nach Ablehnung (D12, D13).
Quelle: Art. 5 bis 9 UCPD, CPC-Sweep 2022 (54 von 399 Shops mit falscher Hierarchie).

**CV14 (H) Siegel und Social Proof nur echt:** Gütezeichen real vergeben und belegbar; Nachhaltigkeitssiegel und allgemeine Umweltaussagen ("klimaneutral", "umweltfreundlich") nur mit Zertifizierung bzw. Nachweis (UWG Anhang Z 2a, 4a bis 4c, seit 27.09.2026); Kundenzahlen und Sterne aus einer Abfrage mit Stand; Logos und Zitate mit Einwilligung der Genannten; "Beliebt"/"Empfohlen"-Badge nur mit Datenbasis.
Quelle: UCPD Anhang I Nr. 2/4, Art. 6 UCPD.

---

## CV-B. Checkout-Ablauf (Baymard, Stripe)

**CV15 (H) Gast-Checkout für jeden, prominent:** Button "Als Gast bestellen" oben auf dem Konto-Schritt, nicht als Textlink unter dem Login. Kontoanlage optional auf der Bestätigungsseite mit vorausgefüllten Daten (nur Passwort fehlt).
Quelle: Baymard (18 % Abbruch wegen Kontozwang; 62 % der Shops machen Gast nicht prominent).

**CV16 (H) Nur Felder, ohne die der nächste Schritt nicht geht.** Ziel 12 bis 14 Formularelemente im Checkout (Durchschnitt 23). Geburtsdatum, Firma, "Wie hast du uns gefunden?", Telefon nur wenn wirklich nötig, sonst weglassen oder nach dem Kauf optional. Ein Feld "Vollständiger Name" statt Vor- und Nachname, Adresse mit Autovervollständigung. Signup (SaaS/App): E-Mail plus Passwort oder Passkey/Social, Zahlungsdaten nicht vor dem ersten Nutzen außer transparent bei Testphase.
Quelle: Baymard Checkout UX, FO10.

**CV17 (H) Vorhersehbarkeit am Kaufen-Button:** In unmittelbarer Nähe steht, was nach dem Kauf passiert: Bestätigungsmail, Lieferzeitraum als Datum ("Zustellung Di 18.11. bis Do 20.11."), Sendungsverfolgung, Rückgabe (Frist, wer zahlt), Support-Kontakt. Offene Fragen in den letzten Sekunden kippen den Kauf.
Quelle: R25 (Praxis), Baymard (20 % Lieferzeit, 13 % Rückgabe, 19 % Vertrauen).

**CV18 (H) Review-Schritt zeigt nur Bekanntes,** jede Zeile mit "Ändern" ohne Browser-Zurück; keine neue Gebühr hier. Der Button vor der Prüfung heißt "Weiter zur Prüfung", nicht "Weiter". Bestellübersicht mit Gesamtpreis auf allen Schritten sichtbar.
Quelle: Baymard.

**CV19 (K) Eingaben überleben jeden Fehler,** auch Kartendaten, Warenkorb nach 3-D-Secure-Rückkehr, Reload und Zurück (FO13).
Quelle: Baymard (34 % der Shops leeren nach Fehler).

**CV20 (H) Fehlertexte spezifisch, am Feld, mit Korrektur** (FO3, X2); bei Zahlungsfehler bleibt der Nutzer im Zahlungsschritt, sieht "Karte abgelehnt, andere Karte oder Zahlart wählen" und kann sofort eine andere Zahlart nehmen. Betrugsgründe (`fraudulent`, `lost_card`, `stolen_card`) wie ein generischer Decline anzeigen, behebbare (`incorrect_cvc`, `expired_card`, `insufficient_funds`) konkret.
Quelle: Baymard (98 % generische Fehlertexte), Stripe Decline Codes.

**CV21 (K) Genau eine Bestellung pro Absicht:** Button sperrt ab dem ersten Klick (Z2), serverseitiger Idempotency Key je Warenkorb/Checkout-Sitzung, PaymentIntent bei Unterbrechung wiederverwenden, Bestellung per Webhook bestätigen statt nur per Redirect. Reload der Bestätigungsseite erzeugt keine zweite Bestellung.
Prüfen: zwei schnelle Klicks bei gedrosseltem Netz ergeben eine Bestellung und eine Belastung.
Quelle: Stripe Idempotent Requests, R06.

**CV22 (H) Kartenformular:** gehostete Felder des Zahlungsanbieters (Stripe Elements, Mollie Components) statt eigener Inputs für Kartennummer und CVC (PCI). Sonst: Kartentyp automatisch erkannt, Nummer in Blöcken formatiert, Luhn-Prüfung vor Absenden, Ablauf MM/JJ, Hinweis zum CVC-Ort, `autocomplete="cc-number|cc-exp|cc-csc"`, `inputmode="numeric"`. 3-D Secure (`requires_action`) wird im Ablauf behandelt und führt zurück zur Bestellung.
Quelle: Baymard Payment UX, Stripe SCA.

**CV23 (M) Zahlarten passend zum Markt,** mindestens eine Express-Wallet (Apple Pay, Google Pay, PayPal); in AT zusätzlich eps bzw. Sofortüberweisung/Klarna üblich. CV1 und CV2 gelten auch für Wallet-Buttons.
Quelle: Baymard (9 % zu wenige Zahlarten, Praxis).

**CV24 (M) Vertrauen am Zahlungsfeld:** Kartenfelder optisch abgesetzt, 1 bis 2 Sicherheits- oder echte Siegelsymbole daneben, Rückgabe aus dem Checkout erreichbar.
Quelle: Baymard Perceived Security.

**CV25 (M) Keine Ablenkung im Checkout:** keine Newsletter-Popups, Werbebanner, Cross-Sell-Zwischenseiten nach "Bestellen". Zusatzangebote höchstens dezent im Warenkorb.
Quelle: Baymard.

---

## CV-C. Warenkorb, Preise, Pricing-Seite

**CV26 (M) Gratisversand-Schwelle als Fortschritt im Warenkorb,** wenn es eine echte Schwelle gibt: "Noch 16,00 € bis zum kostenlosen Versand" mit Balken; darunter ein kleiner passender Artikel zum Auffüllen. Balken nur zeigen, wenn die Schwelle erreichbar wirkt (Faustregel: Restbetrag höchstens ca. 30 bis 40 % des Warenkorbs); bei weitem Abstand stattdessen nur die Versandkosten nennen.
Quelle: R38, Baymard (Gratisversand-Info in die Warenkorbsumme), Schwellenwert Praxis.

**CV27 (H) Warenkorb ist bearbeitbar:** Bild, Name, Variante, Menge (+/−), Entfernen mit Undo (Z5), Einzel- und Gesamtpreis im Locale-Format (WD31), Versand und voraussichtliche Lieferung schon hier.
Quelle: Baymard (Praxis), CV4.

**CV28 (H) Pricing-Seite zeigt Preise,** mindestens "ab"-Preise oder Preise für typische Szenarien. Reiner "Kontakt aufnehmen"-Plan nur für wirklich individuelle Leistung, dann mit Startpreis. Kein Rechner als einzige Preisquelle.
Quelle: NNG Show Price.

**CV29 (M) Planvergleich als Tabelle mit höchstens 5 Plänen,** jede Zeile in jedem Plan ausgefüllt, Spaltenköpfe beim Scrollen sichtbar. Jahrespreis nennt den Jahresgesamtbetrag und "jährliche Abrechnung"; Einrichtungs- und Zusatzgebühren stehen beim Plan; Jahresplan nie vorausgewählt (RT22).
Quelle: NNG Comparison Tables, CV2.

**CV30 (M) IKEA-Effekt nutzen, wo das Produkt konfigurierbar ist:** Nutzer stellen ihr Angebot selbst zusammen (Konfigurator mit Maßen, Material, Farbe, Live-Preis), statt ein fertiges Angebot zu bekommen. Der Effekt wirkt nur, wenn der Nutzer fertig wird: wenige Schritte, Zwischenstand gespeichert, Preis jederzeit sichtbar.
Quelle: Norton, Mochon, Ariely 2012 (Bereitschaft zu zahlen +63 % bei selbst aufgebauter IKEA-Box), R27.

---

## CV-D. Nach dem Kauf

**CV31 (H) Bestätigungsseite:** Bestellnummer, Zusammenfassung mit Gesamtpreis, Liefer- bzw. Zugangserwartung als Datum, Hinweis auf die Bestätigungsmail, Kontakt, optionales Konto (CV15). Kein Upsell-Schirm davor. Bei Anfrageformularen: Danke-Seite mit Antwortzeit und nächstem Schritt statt Redirect auf die Startseite.
Quelle: Baymard, Art. 8 Abs. 7 VRRL, R36, R37.

**CV32 (M) Bestell- und Retourenstatus mit Meilensteinen** (bestätigt, versandt mit Tracking-Link, zugestellt; Retoure eingegangen, Erstattung ausgelöst), jeweils mit Datum, im Konto und per Service-Mail ohne Werbung (RT15).
Quelle: Baymard.

**CV33 (M) Rückgabeseite in einfacher Sprache:** Kurzliste, Frist, wer die Rücksendung zahlt, Link zum Rücksendeprozess; verlinkt von Produktseite und Checkout.
Quelle: Baymard (13 % Abbruch wegen Rückgabe).
