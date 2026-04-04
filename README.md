# Learning Skill v2.0

> Verwandelt Codebases in interaktive Lernkurse UND Knowledge Graphs — optimiert für Claude.

![Version](https://img.shields.io/badge/version-2.0-blue) ![Skill](https://img.shields.io/badge/Claude_Code-Skill-orange) ![License](https://img.shields.io/badge/license-MIT-green)

## Was ist das?

Dieses Skill-Paket erweitert Claude Code um drei leistungsstarke Analyse-Modi. **Kurs** generiert mehrstufige HTML-Lernkurse (L0–L3), die eine Codebase didaktisch aufbereiten. **Verstehen** erzeugt einen maschinenlesbaren Knowledge Graph samt interaktivem React-Dashboard. **Kombiniert** vereint beide Ansätze und nutzt den Knowledge Graph zur Qualitätsbewertung der Kursinhalte.

## Drei Modi

| Modus | Was es macht | Output | Typischer Befehl |
|---|---|---|---|
| **Kurs** | Multi-Level HTML-Kurse L0–L3 | Verlinktes HTML-Set | `Erstelle einen Kurs aus diesem Repo` |
| **Verstehen** | Knowledge Graph + Dashboard | `knowledge-graph.json` + React Dashboard | `Analysiere diese Codebase` |
| **Kombiniert** | Beides — KG-gestütztes Scoring | HTML-Kurse + Knowledge Graph | `Erstelle alles für dieses Projekt` |

## Features

- **4 Tiefenebenen (L0–L3)** mit autonomem Helpfulness-Scoring
- **3 Zielgruppen** (👤 Anwender / 🔧 Entwickler / 📊 Entscheider) mit eigenen Pipelines
- **Bilingual DE/EN** — automatisch beide Versionen
- **Energiekonzern-Design** (Tiefenblau / Impuls-Orange / Warmgrau)
- **Multi-Agent Knowledge Graph Pipeline** (8 spezialisierte Agenten)
- **23 Programmiersprachen + 10 Frameworks** unterstützt
- **Interaktives Dashboard** mit Force-Directed Graph
- **Domain-Analyse, Diff-Impact, Onboarding-Guides**
- **Parallelisierung** über Claude's Agent-Tool

## Projektstruktur

```
├── skill.md              <- Haupt-Skill (3.008 Zeilen)
├── agents/               <- 8 KI-Agenten
│   ├── project-scanner.md
│   ├── file-analyzer.md
│   ├── architecture-analyzer.md
│   ├── tour-builder.md
│   ├── domain-analyzer.md
│   ├── assemble-reviewer.md
│   ├── graph-reviewer.md
│   └── knowledge-graph-guide.md
├── languages/            <- 23 Sprachguides
│   ├── python.md, typescript.md, rust.md, go.md ...
└── frameworks/           <- 10 Framework-Guides
    ├── react.md, django.md, spring.md ...
```

## Installation

**Option A — Global Skill:**

```bash
cp -r Learning-Skill ~/.claude/skills/
```

**Option B — Projekt-Referenz:**

In der Datei `.claude/settings.json` des Projekts:

```json
{
  "skills": ["~/.claude/skills/Learning-Skill/skill.md"]
}
```

Nach der Installation steht der Skill in jeder Claude-Code-Session zur Verfügung.

## Schnellstart

**Kurs erstellen:**
```
> Erstelle einen Lernkurs aus diesem Repository für Entwickler.
```

**Knowledge Graph generieren:**
```
> Analysiere diese Codebase und erstelle einen Knowledge Graph.
```

**Kombinierter Modus:**
```
> Erstelle einen vollständigen Kurs mit Knowledge Graph für dieses Projekt.
```

## Das Level-System

```
L0  Kurzreferenz        ──  1–2 Seiten, schneller Einstieg
 │
L1  Grundlagen-Kurs     ──  Konzepte, Architektur, erste Schritte
 │
L2  Vertiefung           ──  Interna, Patterns, fortgeschrittene Nutzung
 │
L3  Experten-Deep-Dive  ──  Vollständige Analyse, Edge Cases, Performance
```

**Tiefenprofile nach Zielgruppe:**

| Zielgruppe | L0 | L1 | L2 | L3 |
|---|---|---|---|---|
| 👤 Anwender | Voll | Voll | Teilweise | — |
| 🔧 Entwickler | Voll | Voll | Voll | Voll |
| 📊 Entscheider | Voll | Voll | Teilweise | — |

## Die Agent-Pipeline

```
Scanner ─→ Analyzer ─→ Architect ─→ Tour Builder ─→ Reviewer
  │            │            │             │              │
  │  Dateien   │  Analyse   │  Struktur   │   Inhalte    │  Qualität
  │  erfassen  │  pro File  │  erkennen   │   erstellen  │  prüfen
```

Die Agenten arbeiten parallel, wo möglich. Der **Reviewer** bewertet jeden Abschnitt mit einem Helpfulness-Score und triggert bei Bedarf eine Nachbesserung.

## Zusätzliche Befehle

| Befehl | Beschreibung |
|---|---|
| `understand diff` | Analysiert Git-Diff und zeigt Impact auf den Knowledge Graph |
| `understand domain` | Extrahiert Fachdomänen-Konzepte und Ubiquitous Language |
| `understand onboarding` | Generiert rollenspezifische Onboarding-Guides |
| `understand query <Frage>` | Beantwortet Fragen anhand des Knowledge Graphs |
| `understand export` | Exportiert den Graph in verschiedene Formate |
| `understand dashboard` | Startet das interaktive React-Dashboard |

## Lizenz

MIT License. Siehe [LICENSE](LICENSE) für Details.
