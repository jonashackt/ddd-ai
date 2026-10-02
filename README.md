# ddd-ai

## Ressourcen

### Miro Board

Arbeitsboard für dieses Projekt (alle Inputs aus dem Workshop vom 2026-10-02):
https://miro.com/app/board/uXjVHriCZAI=/

Das Miro Board ist die primäre Wissensquelle: Domain Stories, Diagramme und alle
Workshop-Ergebnisse wurden dort erarbeitet und dienen als Ausgangsmaterial für
die Analysen in diesem Projekt (z.B. `domainstory/` und `DomainStoryAuswertung.md`).

---

## Installierter Skill: domain-story-interpreter

### Quelle

GitHub-Repository von Annegret Junker:
https://github.com/Grinseteddy/SamplesDddMeetAi/tree/main/Chapter06/Skills/DomainStorytellingSkill

### Installation

Der Skill wurde manuell per `gh api` aus dem Repository gezogen und lokal abgelegt:

```
.claude/skills/domain-story-interpreter/
├── SKILL.md
└── references/
    ├── pictographic-language.md
    └── worked-examples.md
```

Konkret wurden die drei Dateien mit folgendem Muster heruntergeladen:

```bash
gh api repos/Grinseteddy/SamplesDddMeetAi/contents/Chapter06/Skills/DomainStorytellingSkill/SKILL.md \
  --jq '.content' | base64 -d > .claude/skills/domain-story-interpreter/SKILL.md

gh api repos/Grinseteddy/SamplesDddMeetAi/contents/Chapter06/Skills/DomainStorytellingSkill/references/pictographic-language.md \
  --jq '.content' | base64 -d > .claude/skills/domain-story-interpreter/references/pictographic-language.md

gh api repos/Grinseteddy/SamplesDddMeetAi/contents/Chapter06/Skills/DomainStorytellingSkill/references/worked-examples.md \
  --jq '.content' | base64 -d > .claude/skills/domain-story-interpreter/references/worked-examples.md
```

### Verwendung

```
/domain-story-interpreter
```

Der Skill liest Domain Story Diagramme (Hofer & Schwentner Notation, z.B. aus egon.io) und
erzeugt daraus einen strukturierten Prototype Brief mit Domänenmodell, State Machines,
Use Cases und Screen-Vorschlägen.

**Beispiel-Anwendung in diesem Projekt:**

```
# Screenshot unter domainstory/ ablegen, dann:
/domain-story-interpreter
# → Claude liest das Bild, transkribiert es und erzeugt DomainStoryAuswertung.md
```

Ergebnis: `DomainStoryAuswertung.md`

---

## Installierter Skill: visual-glossary

### Quelle

GitHub-Repository von Annegret Junker:
https://github.com/Grinseteddy/SamplesDddMeetAi/tree/main/Chapter07/Skills/VisualGlossarySkill

### Installation

```bash
gh api repos/Grinseteddy/SamplesDddMeetAi/contents/Chapter07/Skills/VisualGlossarySkill/SKILL.md \
  --jq '.content' | base64 -d > .claude/skills/visual-glossary/SKILL.md

gh api repos/Grinseteddy/SamplesDddMeetAi/contents/Chapter07/Skills/VisualGlossarySkill/references/notation.md \
  --jq '.content' | base64 -d > .claude/skills/visual-glossary/references/notation.md

gh api repos/Grinseteddy/SamplesDddMeetAi/contents/Chapter07/Skills/VisualGlossarySkill/references/companion-techniques.md \
  --jq '.content' | base64 -d > .claude/skills/visual-glossary/references/companion-techniques.md

gh api repos/Grinseteddy/SamplesDddMeetAi/contents/Chapter07/Skills/VisualGlossarySkill/references/worked-example.md \
  --jq '.content' | base64 -d > .claude/skills/visual-glossary/references/worked-example.md
```

Abgelegt unter:

```
.claude/skills/visual-glossary/
├── SKILL.md
└── references/
    ├── notation.md
    ├── companion-techniques.md
    └── worked-example.md
```

### Verwendung

```
/visual-glossary
```

Der Skill liest Visual Glossary Diagramme (Begriffe als Stickies, verbunden durch
beschriftete Kanten mit Kardinalitäten) und erzeugt daraus einen Glossary Brief
mit Term-Katalog, Beziehungstabelle, abgeleitetem Domänenmodell und offenen Fragen.

**Beispiel-Anwendung in diesem Projekt:**

```
# Screenshot unter visualglossary/ ablegen, dann:
/visual-glossary
# → Claude liest das Bild, transkribiert alle Begriffe und Beziehungen,
#   leitet Entitäten, Value Objects und Aggregate ab
```

Ergebnis: `VisualGlossaryAuswertung.md`

---

## Installierter Skill: webapp-style-extractor

### Quelle

GitHub-Repository von Annegret Junker:
https://github.com/Grinseteddy/SamplesDddMeetAi/blob/main/Chapter06/Skills/WebappStyleExtractorSkill/SKILL.md

### Installation

```bash
gh api repos/Grinseteddy/SamplesDddMeetAi/contents/Chapter06/Skills/WebappStyleExtractorSkill/SKILL.md \
  --jq '.content' | base64 -d > .claude/skills/webapp-style-extractor/SKILL.md

gh api repos/Grinseteddy/SamplesDddMeetAi/contents/Chapter06/Skills/WebappStyleExtractorSkill/references/schema.md \
  --jq '.content' | base64 -d > .claude/skills/webapp-style-extractor/references/schema.md

gh api repos/Grinseteddy/SamplesDddMeetAi/contents/Chapter06/Skills/WebappStyleExtractorSkill/scripts/probe.py \
  --jq '.content' | base64 -d > .claude/skills/webapp-style-extractor/scripts/probe.py
```

Abgelegt unter:

```
.claude/skills/webapp-style-extractor/
├── SKILL.md
├── references/
│   └── schema.md
└── scripts/
    └── probe.py
```

### Verwendung

```
/webapp-style-extractor
```

Der Skill analysiert eine bestehende Web-App und extrahiert daraus ein Style-Profil
(Farben, Typografie, Abstände, Komponenten-Muster) — als Grundlage für die
Generierung neuer UI-Komponenten im selben visuellen Stil.

---

## Installierter Skill: prototype-with-glossary

### Quelle

GitHub-Repository von Annegret Junker:
https://github.com/Grinseteddy/SamplesDddMeetAi/blob/main/Chapter07/Skills/ProtypeSkillWithVisualGlossary/SKILL.md

### Installation

```bash
gh api repos/Grinseteddy/SamplesDddMeetAi/contents/Chapter07/Skills/ProtypeSkillWithVisualGlossary/SKILL.md \
  --jq '.content' | base64 -d > .claude/skills/prototype-with-glossary/SKILL.md

gh api repos/Grinseteddy/SamplesDddMeetAi/contents/Chapter07/Skills/ProtypeSkillWithVisualGlossary/references/glossary-to-ui.md \
  --jq '.content' | base64 -d > .claude/skills/prototype-with-glossary/references/glossary-to-ui.md
```

Abgelegt unter:

```
.claude/skills/prototype-with-glossary/
├── SKILL.md
└── references/
    └── glossary-to-ui.md
```

### Verwendung

```
/prototype-with-glossary
```

Der Skill baut aus dem Glossary Brief (`/visual-glossary`) und optional dem
Domain Story Brief (`/domain-story-interpreter`) sowie einem Style-Profil
(`/webapp-style-extractor`) einen klickbaren HTML/CSS-Prototypen. Er übersetzt
Entitäten in Datenmodelle, State Machines in UI-Zustände und Use Cases in Screens.

---

## Zusammenspiel der Skills

| Skill | Perspektive | Liefert |
|-------|-------------|---------|
| `domain-story-interpreter` | Dynamisch — Prozess, Ablauf, Akteure | Use Cases, Screens, State Machines |
| `visual-glossary` | Statisch — Begriffe, Struktur, Kardinalitäten | Domänenmodell, Ubiquitous Language |
| `webapp-style-extractor` | Visuell — UI-Stil einer bestehenden App | Style-Profil für konsistente UI-Generierung |
| `prototype-with-glossary` | Synthetisierend — baut den Prototypen | HTML/CSS-Prototype aus allen Vorstufen |

**Empfohlene Reihenfolge:**
1. `/domain-story-interpreter` → versteht den Prozess und die Rollen
2. `/visual-glossary` → versteht die Datenstruktur dahinter
3. `/webapp-style-extractor` → extrahiert den Stil einer Referenz-App
4. `/prototype-with-glossary` → baut den Prototypen aus allen drei Inputs
