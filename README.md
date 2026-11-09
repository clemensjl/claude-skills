# Claude Skills

Agent Skills von [Clemens Jele](https://github.com/clemensjl). Für Claude Code, Cursor, Codex und jeden Agenten, der das [Agent-Skills-Format](https://agentskills.io/specification) liest.

Der Schwerpunkt liegt auf Dingen, bei denen es auf die Rechtsordnung, den Standort oder die konkrete Norm ankommt — also dort, wo generische Vorlagen aus dem englischsprachigen Raum nicht nur ungenau, sondern falsch sind.

## Installation

```bash
npx skills@latest add clemensjl/claude-skills
```

Einzelnen Skill installieren:

```bash
npx skills@latest add clemensjl/claude-skills --skill legal-at
```

Verfügbare Skills auflisten, ohne zu installieren:

```bash
npx skills@latest add clemensjl/claude-skills --list
```

Global statt projektweit, nur für Claude Code:

```bash
npx skills@latest add clemensjl/claude-skills -a claude-code -g -s '*' -y
```

Alternativ das gewünschte Verzeichnis unter `skills/` direkt nach `~/.claude/skills/` kopieren.

## Skills

### Rechtstexte nach Rechtsordnung

Pflichttexte für Websites, Webshops, Apps und Newsletter. `legal-at` ist auf Deutsch verfasst, alle übrigen auf Englisch, mit Normbezeichnungen in der Originalsprache und Textvorlagen in der Sprache, in der sie veröffentlicht werden müssen.

| Skill | Rechtsordnung | Kern |
|---|---|---|
| [legal-at](./skills/legal-at/SKILL.md) | Österreich | Impressumspflicht aus drei Gesetzen parallel, Einwilligungsalter 14, FAGG statt BGB |
| [legal-de](./skills/legal-de/SKILL.md) | Deutschland | § 5 TMG existiert nicht mehr, DDG und TDDDG seit 14.05.2024, drei verschiedene Buttons mit drei Paragrafen |
| [legal-ch](./skills/legal-ch/SKILL.md) | Schweiz | Impressumspflicht im UWG, kein allgemeines Widerrufsrecht, DSG-Strafen gegen natürliche Personen |
| [legal-fr](./skills/legal-fr/SKILL.md) | Frankreich | Mentions légales in article 1-1 LCEN, Pflicht-Médiateur, CNIL-Cookie-Doktrin |
| [legal-it](./skills/legal-it/SKILL.md) | Italien | Partita IVA auf der Seite, PEC-Pflicht, Einwilligungsalter 14, Garante-Cookie-Leitlinien |
| [legal-uk](./skills/legal-uk/SKILL.md) | Vereinigtes Königreich | UK GDPR nach dem Data (Use and Access) Act 2025, ICO-Gebühr, DMCC-Regime |
| [legal-us](./skills/legal-us/SKILL.md) | USA | Kein Bundesdatenschutzgesetz, Schwellenwertanalyse über gut zwanzig Staatengesetze, FTC Act § 5 |
| [legal-au](./skills/legal-au/SKILL.md) | Australien | Nicht abdingbare Consumer Guarantees, kein Rücktrittsrecht, keine Cookie-Einwilligung |
| [legal-eu](./skills/legal-eu/SKILL.md) | Unionsebene | Gemeinsame Basis für die EU-Länder: DSGVO, ePrivacy, DSA, CRD, EAA, AI Act, GPSR |

`legal-eu` deckt die Unionsebene ab, die nationalen Skills die Ebene darüber. Jeder Skill funktioniert allein; sind beide installiert, verweist der nationale auf den europäischen.

### Compliance in der Umsetzung

Diese Skills schreiben keine Rechtstexte, sondern entscheiden, ob die Implementierung hält, was der Text verspricht.

| Skill | Zweck |
|---|---|
| [cookie-consent-impl](./skills/cookie-consent-impl/SKILL.md) | Consent technisch korrekt verdrahten: Blocken auf Ladeebene, Consent Mode v2, Server-Side-Tagging, Nachweis, Audit-Script |
| [privacy-vendor-review](./skills/privacy-vendor-review/SKILL.md) | Drittanbieter vor dem Einbau prüfen: Rolle, AVV, Transfermechanismus, Consent-Kategorie, Verarbeitungsverzeichnis-Eintrag |
| [data-retention](./skills/data-retention/SKILL.md) | Löschfristen als Engineering-Problem: gesetzliches Minimum gegen Speicherbegrenzung, Backups, Löschjobs, Kopien-Inventar |
| [ai-act-compliance](./skills/ai-act-compliance/SKILL.md) | Rolle und Risikoklasse nach Verordnung (EU) 2024/1689 bestimmen, Art-50-Transparenzpflichten operativ umsetzen |

### Rechnungen, Steuern, Lokalisierung

| Skill | Zweck |
|---|---|
| [einvoicing-eu](./skills/einvoicing-eu/SKILL.md) | Strukturierte E-Rechnung in Europa: EN 16931, UBL und CII, nationale CIUS, Peppol, ViDA-Zeitplan, Validierungsfehler |
| [steuer-at](./skills/steuer-at/SKILL.md) | Österreichische Rechnungs-, Beleg- und Registrierkassenpflichten, Kleinunternehmer, Leistungsort, RKSV |
| [i18n-locale-correctness](./skills/i18n-locale-correctness/SKILL.md) | Namen, Adressen, Telefonnummern, Datum, Zahlen, Sortierung, Prüfsummen — ohne US-Annahmen |

### Produktqualität

| Skill | Zweck |
|---|---|
| [ux-regelwerk](./skills/ux-regelwerk/SKILL.md) | Ein verbindliches UX-Regelwerk mit Modus Bauen und Prüfen: prüfbare Regeln für Zustände, Formulare, Touch, Navigation, Laden, Leer- und Fehlerzustände, Barrierefreiheit, Motion und Texte, Gegenprüfung typischer KI-Fehler und Pflicht-Sichtprüfung, für Web, Expo/React Native und Flutter |
| [ux-details-audit](./skills/ux-details-audit/SKILL.md) | App oder Website auf 20 unsichtbare UX-Details prüfen (Skeletons, Optimistic Updates, Command Menu, Undo-Toasts, Safe Areas, Idempotency Keys und weitere) und die fehlenden priorisiert umsetzen, für Web, React/Next.js, Flutter und Electron |
| [design-unslop](./skills/design-unslop/SKILL.md) | KI-generierte Landing Pages, Dashboards und App-Screens entslopen: Merkmal-Katalog mit Suchmustern, Richtung und Dials, neun Durchgänge, Pre-Flight. Bearbeitung von [unslop](https://github.com/heydamir/unslop) (Damir Sokolovsky) und [taste-skill](https://github.com/Leonxlnx/taste-skill), daher CC BY 4.0 |

## Warum das nicht aus dem Modellgedächtnis kommt

Die Skills wurden gegen Primärquellen geschrieben, nicht gegen Erinnerung. Beim Bau hat sich in jeder einzelnen Rechtsordnung mindestens eine verbreitete Zitierung als veraltet erwiesen. Eine Auswahl:

- **§ 5 TMG gibt es nicht mehr.** Das Telemediengesetz wurde am 14.05.2024 durch das DDG ersetzt, das TTDSG in TDDDG umbenannt. Jeder Generator, jedes Plugin und jedes Sprachmodell liefert weiterhin § 5 TMG.
- **Die mentions légales stehen in article 1-1 LCEN**, nicht mehr in article 6-III — verschoben durch die loi SREN vom 23.05.2024.
- **Die EU-ODR-Plattform ist seit 20.07.2025 abgeschaltet** (Verordnung (EU) 2024/3228). Der Link, den unzählige Muster weiterhin ausliefern, führt ins Leere.
- **Die High-Risk-Termine des AI Act sind verschoben** — auf 02.12.2027 und 02.08.2028 durch Verordnung (EU) 2026/1744. Die überall zitierten Daten 02.08.2026 und 02.08.2027 sind überholt.
- **Deutsche Buchungsbelege sind acht Jahre aufzubewahren, nicht zehn** (§ 147 Abs 3 AO seit 01.01.2025), österreichische durchgehend sieben.
- **Die österreichische Kalte-Hände-Regelung liegt bei 45.000 €**, nicht bei 30.000 € — praktisch alle Sekundärquellen sagen weiterhin 30.000.
- **ZUGFeRD-Profile MINIMUM und BASIC WL sind keine Rechnungen** im Sinn des UStG. FeRD schreibt das selbst.
- **Das Einwilligungsalter ist nicht überall 16.** Österreich und Italien 14, Frankreich und Dänemark 15, Deutschland und Irland 16.

## Kein Rechtsrat

Die `legal-*`-Skills sowie `ai-act-compliance`, `data-retention`, `privacy-vendor-review` und `steuer-at` erzeugen Entwürfe und Prüfergebnisse. Das ist keine Rechts- oder Steuerberatung und ersetzt sie nicht. Erzeugte Texte tragen einen sichtbaren Entwurfs-Marker, bis eine fachliche Freigabe vorliegt. Bei Webshop, Abo, Zahlungsabwicklung, Kinderdaten, Gesundheitsdaten oder Plattformbetrieb ist diese Freigabe nicht optional.

Rechtslage ändert sich. Der in den Dateien angegebene Stand ist der Tag der letzten Prüfung, keine Zusage für die Zukunft.

## Umgang mit Unsicherheit

Wo eine Angabe nicht gegen eine Primärquelle verifiziert werden konnte, steht sie nicht als Tatsache im Text, sondern als `[[UNVERIFIED: … ]]` mit dem Hinweis, was zu prüfen ist und wo. Harte Regeln enthalten grundsätzlich keine solchen Marker — was dort steht, ist belegt.

Die Marker sind ungleich verteilt, und zwar nach Erreichbarkeit der Quelle, nicht nach Sorgfalt: `legal-uk` und `legal-ch` hatten offene Gesetzesportale, `legal-au` und `legal-us` nicht, weil mehrere Behördenseiten automatisierte Abrufe abweisen. Das steht sichtbar im Text statt kaschiert zu werden.

Fehlende Angaben zum Projekt selbst — Firmenbuchnummer, UID, Aufsichtsbehörde, Anschrift — werden nie plausibel ausgefüllt, sondern als `[[FEHLT: …]]` beziehungsweise `[[MISSING: …]]` ausgewiesen.

## Aufbau

```
skills/
  <skill-name>/
    SKILL.md          # Router: wann greift der Skill, harte Regeln, Verweise
    references/       # Detailwissen, erst bei Bedarf gelesen
      *.md
```

`SKILL.md` beginnt mit YAML-Frontmatter aus `name` und `description`. Die Beschreibung nennt ausschließlich die Auslösebedingungen, nie den Ablauf des Skills — sonst folgen Agenten der Zusammenfassung statt dem Skill.

Jede Referenzdatei enthält die Rechts- oder Normgrundlage mit Stand, die Pflichtinhalte, eine Vorlage mit Platzhaltern und eine Prüfliste. Jeder Skill hat einen Fragenkatalog für den Sachverhalt und eine Pre-Launch-Prüfliste.

Neuen Skill anlegen:

```bash
mkdir -p skills/mein-skill/references
$EDITOR skills/mein-skill/SKILL.md
npx skills@latest add . --list          # Erkennung prüfen
```

## Beitragen

Korrekturen am Rechtsstand und neue Skills sind willkommen, Hinweise in [CONTRIBUTING.md](./CONTRIBUTING.md).

## Lizenz

MIT, siehe [LICENSE](./LICENSE).
