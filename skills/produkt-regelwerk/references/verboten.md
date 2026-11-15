# Verboten: Dark Patterns (D)

Diese Muster werden **nie gebaut, auch nicht auf ausdrücklichen Wunsch** des Auftraggebers und auch nicht "nur als Test". Verlangt ein Auftrag eines davon ("Kündigung erschweren", "Countdown für Dringlichkeit", "Newsletter vorankreuzen"), dann: das Muster beim Namen nennen, die Rechtsgrundlage in einem Satz, und die erlaubte Alternative aus `regeln-retention.md` bzw. `regeln-conversion.md` bauen. Im PRÜFEN-Modus ist jeder Fund Schweregrad **K**.

Status: **gilt** = geltendes Recht (AT/EU, Stand 15.11.2026); **Auslegung** = über Generalklauseln, Einzelfall; **DFA** = steht auf der Liste des Digital-Fairness-Act-Vorschlags (COM(2026) 1100), noch nicht anwendbar. Auch "Auslegung"- und "DFA"-Muster werden nicht gebaut: Sie schaden Vertrauen und Bewertungen, und Behörden gehen bereits dagegen vor (CPC-Sweep 2022: 37 % von 399 Shops potenziell rechtswidrig; Kommissionsstudie 2022: 97 % der populärsten Seiten mit mindestens einem Dark Pattern).

| ID | Muster | Woran erkennen (Code/UI) | Erlaubte Alternative | Rechtsgrundlage | Status |
|---|---|---|---|---|---|
| D1 | **Fake-Countdown / falsche Befristung** | Timer ohne serverseitiges Ende, Reset bei Reload oder per Cookie, "nur heute" ohne echte Frist | echte Aktion mit festem Enddatum, das danach wirklich endet | UWG Anhang Z 7, Art. 6 UCPD | gilt |
| D2 | **Fake-Knappheit / Fake-Nachfrage** | `Math.random()` oder Konstante bei "nur noch 3", "12 sehen das gerade", "fast ausverkauft" | echter Lagerbestand aus der DB, sonst nichts | Art. 6 Abs. 1 lit. b UCPD, UWG Anhang Z 5/6 | gilt |
| D3 | **Drip Pricing / versteckte Kosten** | Versand-, Service-, Zahlungsgebühr erst im letzten Schritt | Gesamtpreis ab Warenkorb (CV4) | Art. 6 Abs. 6 VRRL, Art. 7 UCPD, § 9 PrAG | gilt |
| D4 | **Vorangekreuzt** (Zusatzkosten, Einwilligung) | `checked` als Default bei Versicherung, Spende, Express, Newsletter, Partnerweitergabe | leere Checkbox, je Zweck getrennt | § 6c KSchG (Art. 22 VRRL), Art. 4 Nr. 11 und Erw. 32 DSGVO | gilt |
| D5 | **Sneak into Basket** | Artikel landet ungefragt im Warenkorb | Vorschlag mit eigenem "Hinzufügen"-Button | § 6c KSchG, UCPD | gilt |
| D6 | **Fake-Bewertungen und Fake-Social-Proof** | hartkodierte Testimonials, gefilterte Negativbewertungen, erfundene Kundenzahlen, Logos ohne Einwilligung | echte, geprüfte Bewertungen mit Hinweis zur Prüfung (CV11) | UWG Anhang Z 23b/23c | gilt |
| D7 | **Fake-Siegel und Greenwashing** | selbstgebautes "geprüfte Qualität"-Badge, "klimaneutral" ohne Nachweis | echtes Siegel oder keins | UWG Anhang Z 2, 2a, 4a bis 4c | gilt |
| D8 | **Fake-Rabatt** | Streichpreis über dem 30-Tage-Tiefstpreis, Preis kurz vor "Sale" angehoben, Prozent auf UVP | Rabatt vom 30-Tage-Tiefstpreis (CV8) | § 9a PrAG, Art. 6a RL 98/6/EG, EuGH C-330/23 | gilt |
| D9 | **Mehrdeutiger Bestell-Button** | "Weiter", "Jetzt testen", "Submit" beim zahlungspflichtigen Schritt | "zahlungspflichtig bestellen" (CV1) | § 8 Abs. 2 FAGG, EuGH C-249/21 | gilt (keine Bindung) |
| D10 | **Abo- und Testphasen-Falle** | Preis, Laufzeit, Verlängerung nicht vor dem Button; Test wird ohne Erinnerung kostenpflichtig | CV2, RT18, RT19 | Art. 6/8 VRRL, Art. 7 UCPD, UCPD-Leitlinie 2.9.6 | gilt; Erinnerung DFA |
| D11 | **Roach Motel: Kündigung schwerer als Abschluss** | Kündigen nur per Telefon, Brief, Chat, Termin; mehr Schritte als der Abschluss; versteckt in Hilfe-Center | RT1 | § 1a UWG (Kriterium Abs. 2 Z 4), DSA Art. 25 (Plattformen), DE § 312k BGB | gilt (Auslegung); DFA |
| D12 | **Confirmshaming und falsche Hierarchie** | "Nein, ich will nicht sparen"; Ablehnen als grauer Mini-Link neben großem grünem Button; Doppelverneinung | neutral, gleich groß (CV13) | Art. 5 bis 9 UCPD, DSA Erw. 67 | Auslegung; DFA |
| D13 | **Nagging** | Modal (Push, Newsletter, Upsell, Bewertung) kommt nach "Nein" bei jedem Start wieder | Sperrfrist und neuer Anlass (RT17) | DSA Art. 25 Abs. 3 lit. b, EDPB 03/2022, § 1a UWG | gilt teils; DFA |
| D14 | **Kündigung an Umfrage, Gespräch oder Angebot gekoppelt** | kein "Trotzdem kündigen" auf einer Zwischenseite; Pflicht-Freitext | RT24 | § 1a UWG (Kriterium Abs. 2 Z 4) | Auslegung |
| D15 | **Stille Rückverwandlung** | Pause oder Gratis-Monat wird ohne Vorab-Mail kostenpflichtig | RT26 | Art. 7 UCPD | Auslegung; DFA |
| D16 | **Fake-Benachrichtigung** | Push "Jemand hat dir geschrieben" ohne realen Auslöser | nur echte Ereignisse (RT10) | Art. 6 UCPD | gilt; DFA |
| D17 | **Werbung ohne Einwilligung** | Newsletter an alle Registrierten, kein Consent-Log, Abmeldung nur nach Login | RT13, RT14 | § 174 TKG 2021, Art. 7 DSGVO | gilt |
| D18 | **Widerruf/Abmeldung schwerer als Zustimmung** | Opt-in mit 1 Klick, Opt-out über 4 Ebenen | gleich viele Schritte | Art. 7 Abs. 3 DSGVO | gilt |
| D19 | **Datenverlust als Kündigungshebel** | Konto bei Kündigung sofort gelöscht, Export gesperrt | Zugang bis Periodenende, Export (RT27) | § 1a UWG, Art. 20 DSGVO | Auslegung |
| D20 | **Druck auf Kinder** | "Dein Streak stirbt, kauf jetzt" an Minderjährige | RT7 ohne Kaufbezug | UWG Anhang Z 28 | gilt |
| D21 | **"Gratis" mit versteckten Kosten** | Gratis-Badge, Folgekosten im Kleingedruckten | Kosten neben "gratis" | UWG Anhang Z 20 | gilt |
| D22 | **Zahlart-Aufschlag** | Gebühr für Karte oder PayPal | Rabatt für die günstige Zahlart | § 56 Abs. 3 ZaDiG 2018 | gilt |
| D23 | **Widerrufsfunktion mit Hürden** | Gegenangebot oder Zusatztext im "Widerruf bestätigen"-Schritt, Funktion nur im Kleingedruckten | CV9 | § 13a FAGG | gilt (Verträge ab 01.10.2026) |

## Rationalisierungen, die nicht gelten

| Aussage | Antwort |
|---|---|
| "Der Kunde will es ausdrücklich so." | Der Auftrag ändert das Gesetz nicht. Muster benennen, Alternative bauen; das Ziel (weniger Churn, mehr Umsatz) bleibt erreichbar. |
| "Nur als A/B-Test." | Ein Test mit echten Nutzern ist eine echte Geschäftspraktik. |
| "Machen alle so." | 37 % der geprüften Shops wurden genau dafür beanstandet. |
| "Wir sind keine Plattform, DSA gilt nicht." | Dann greifen UWG, UCPD, VRRL, DSGVO; die Spalte Rechtsgrundlage nennt sie. |
| "Ist ja nur ein Countdown für Dringlichkeit." | Ohne echtes Ende ist er per se irreführend (Anhang Z 7). |
| "Die Pause ist kundenfreundlich, die Erinnerung nervt." | Ohne Vorab-Erinnerung ist die Pause eine Abo-Falle (D15). |
