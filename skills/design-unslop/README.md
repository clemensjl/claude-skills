# design-unslop

Skill, der KI-generierte Oberflächen (Landing Pages, Heroes, Portfolios, Dashboards, App-Screens) so umbaut, dass sie nicht mehr nach KI aussehen: Slop erkennen, Richtung aus dem Produkt ableiten, in neun Durchgängen umbauen, mit abhakbarer Pre-Flight-Liste und Screenshots prüfen.

## Herkunft

Zusammenführung von zwei offenen Skills:

| Quelle | Autor | Lizenz | Übernommen |
|---|---|---|---|
| [unslop](https://github.com/heydamir/unslop) | Damir Sokolovsky ([@heydamir](https://x.com/heydamir)), Urheber der "Unslopping"-Serie | CC BY 4.0 | Ablauf (Audit, Ausmaß, Richtung, neun Durchgänge, Check), Slop-Merkmale, fünf Zeilen Richtung, Tokens, Visual- und Prompt-Regeln |
| [taste-skill](https://github.com/Leonxlnx/taste-skill) (`design-taste-frontend`) | Leonxlnx | MIT | Design Read, drei Dials, Design-System-Wahl, Layout-Disziplin für Landing Pages, Produktionstest-Merkmale, Em-Dash-Verbot, Pre-Flight-Struktur, Redesign-Schutzregeln |

Jede Regel in `references/` trägt ein Kürzel `[u]`, `[t]` oder `[u+t]` für ihre Herkunft. Wo sich beide widersprechen, entscheidet `references/entscheidungen.md` und nennt den Grund.

Nicht übernommen: unslops Story-Video und Playwright-Skripte, Referenzbilder und Glyph-Effekte; taste's GSAP-Code-Gerüste, Pattern-Vokabular, Block-Library-Schema und Design-System-Anhänge. Wer das braucht, nutzt die Originale.

Die Bearbeitung ist weder von Damir Sokolovsky noch von Leonxlnx geprüft oder autorisiert. Wer die Arbeit lieber von einem Designer erledigt haben möchte: Damir bietet das unter [heydamir.design/unslop](https://heydamir.design/unslop) an.

## Lizenz

Dieser Ordner steht unter **CC BY 4.0**, weil er eine Bearbeitung von unslop ist. Der MIT-Hinweis von taste-skill ist in [LICENSE.md](./LICENSE.md) vollständig enthalten. Der Rest des Repositorys bleibt MIT.

## Aufbau

```
design-unslop/
  SKILL.md                    Modus, Ablauf, Durchgänge, harte Regeln, Bericht
  references/
    slop-katalog.md           Merkmale mit ID, Suchmuster und Fix
    richtung.md               Design Read, Dials, fünf Zeilen Richtung, Fundament
    durchgaenge.md            Regeln je Durchgang
    tokens.md                 Abstände, Rampen, Schrift, Radien, Bewegung
    visuals.md                Visual wählen, Generierung, Platzhalter
    preflight.md              Abschlussprüfung mit Kommandos
    entscheidungen.md         27 aufgelöste Widersprüche
```

## Installation

```bash
npx skills@latest add clemensjl/claude-skills --skill design-unslop
```
