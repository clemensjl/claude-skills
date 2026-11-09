# Beitragen

Beiträge sind willkommen, vor allem Korrekturen am Rechtsstand. Die Skills gelten nur, solange ihre Normbezüge stimmen.

## Fehler melden

Ein Fehler im Inhalt ist eine falsche, veraltete oder fehlende Norm, Frist, Summe oder Behördenangabe. Bitte als Issue melden, mit:

- Skill und Datei (`skills/<name>/references/<datei>.md`)
- was dort steht und was stimmt
- Primärquelle (Gesetzestext, Amtsblatt, Behördenseite), nicht Sekundärliteratur

Ohne Primärquelle lässt sich eine Korrektur nicht prüfen.

## Änderung vorschlagen

1. Repository forken und einen Branch anlegen.
2. Änderung vornehmen. Der Aufbau steht im [README](./README.md#aufbau): `SKILL.md` als Router, Detailwissen in `references/`.
3. Erkennung prüfen:

   ```bash
   npx skills@latest add . --list
   ```

   Der geänderte Skill muss mit seiner `description` in der Liste erscheinen.
4. Pull Request gegen `main` öffnen und die Primärquelle der Änderung nennen.

## Regeln für Inhalte

- Die `description` im Frontmatter nennt nur die Auslösebedingungen, nie den Ablauf des Skills.
- Angaben, die sich nicht gegen eine Primärquelle belegen lassen, stehen als `[[UNVERIFIED: … ]]` mit dem Hinweis, was zu prüfen ist und wo. Nie als Tatsache.
- Fehlende Angaben zum Projekt (Firmenbuchnummer, UID, Anschrift) nie plausibel ausfüllen, sondern als `[[FEHLT: …]]` beziehungsweise `[[MISSING: …]]` ausweisen.
- Bei jeder geprüften Angabe den Stand (Datum der Prüfung) mitführen.
- Der Entwurfs-Marker in erzeugten Rechtstexten bleibt, bis eine fachliche Freigabe vorliegt.
- Sprache wie im jeweiligen Skill (vor dem Schreiben in dessen `SKILL.md` nachsehen), Normbezeichnungen in der Originalsprache.

Mit dem Pull Request stimmst du zu, dass dein Beitrag unter der [MIT-Lizenz](./LICENSE) steht.
