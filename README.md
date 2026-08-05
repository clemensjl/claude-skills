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

Alternativ das Verzeichnis `skills/legal-at` direkt nach `~/.claude/skills/` kopieren.

## Skills

| Skill | Zweck |
|---|---|
| [legal-at](./skills/legal-at/SKILL.md) | Pflichttexte für österreichische Websites, Webshops, Apps und Newsletter — Impressum und Offenlegung, Datenschutzerklärung, Cookie-Consent, AGB, Rücktrittsrecht, Gewährleistung, Marketing, Barrierefreiheit, DSA-Plattformpflichten. |

### legal-at

Österreichisches Recht weicht an Stellen von deutschem ab, an denen Vorlagen und Sprachmodelle gern das deutsche Muster übernehmen. Drei Beispiele, die der Skill abfängt:

- Die Impressumspflicht folgt aus **drei** Gesetzen parallel — § 5 ECG, §§ 24 und 25 MedienG sowie § 14 UGB und § 63 GewO. Ein aus § 5 TMG übersetztes Impressum ist unvollständig, nicht bloß anders formuliert.
- Das datenschutzrechtliche **Einwilligungsalter liegt bei 14**, nicht bei 16. Österreich hat die Öffnungsklausel des Art 8 DSGVO über § 4 Abs 4 DSG genutzt.
- Die **EU-ODR-Plattform ist seit 20.07.2025 abgeschaltet** (Verordnung (EU) 2024/3228). Der Link, den unzählige Muster und Shop-Systeme weiterhin ausliefern, führt ins Leere und ist potenziell eine irreführende Geschäftspraxis.

Abgedeckte Rechtsquellen: DSGVO, DSG, ECG, MedienG, UGB, GewO, FAGG, KSchG, VGG, TKG 2021, UWG, PrAG, BaFG, DSA.

Der Skill besteht aus einem Router mit Pflicht-Matrix und harten Regeln sowie 13 Referenzdateien mit Normtext, Textvorlagen und Prüflisten. Die Paragrafenzitate wurden gegen den Rechtsinformationsdienst des Bundes geprüft, Stand 05.08.2026.

Getestet nach dem RED-GREEN-REFACTOR-Verfahren aus [obra/superpowers](https://github.com/obra/superpowers): fünf Szenarien, jeweils mit und ohne Skill, unter Zeit-, Autoritäts- und Sunk-Cost-Druck. Ohne Skill scheiterten Agenten reproduzierbar an übernommenen ODR-Links, erfundenen Gewerbedaten, verwechselten FAGG-Paragrafen und einer für Österreich frei erfundenen Kündigungsbutton-Pflicht nach deutschem § 312k BGB.

## Kein Rechtsrat

`legal-at` erzeugt Entwürfe und Prüfergebnisse. Das ist keine Rechtsberatung und ersetzt sie nicht. Erzeugte Texte tragen den Marker `<!-- ENTWURF – juristisch nicht freigegeben -->`, bis eine anwaltliche Freigabe vorliegt. Bei Webshop, Abo, Zahlungsabwicklung, Kinderdaten, Gesundheitsdaten oder Plattformbetrieb ist diese Freigabe nicht optional.

Rechtslage ändert sich. Der angegebene Stand ist der Tag der letzten Prüfung, keine Zusage für die Zukunft.

## Aufbau

```
skills/
  <skill-name>/
    SKILL.md          # Router: wann greift der Skill, harte Regeln, Verweise
    references/       # Detailwissen, erst bei Bedarf gelesen
      *.md
```

`SKILL.md` beginnt mit YAML-Frontmatter aus `name` und `description`. Die Beschreibung nennt ausschließlich die Auslösebedingungen, nie den Ablauf des Skills — sonst folgen Agenten der Zusammenfassung statt dem Skill.

Neuen Skill anlegen:

```bash
mkdir -p skills/mein-skill/references
$EDITOR skills/mein-skill/SKILL.md
npx skills@latest add . --list          # Erkennung prüfen
```

## Lizenz

MIT, siehe [LICENSE](./LICENSE).
