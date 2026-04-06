---
name: learning-skill
description: Kombiniert zwei Superkraefte: (1) Verwandelt Codebases in interaktive Multi-Level-HTML-Kurse (L0-L3) mit Zielgruppen-Segmentierung und Energiekonzern-Design, UND (2) erzeugt interaktive Knowledge Graphs mit Dashboard zur Code-Exploration. DREI MODI: "Kurs" für HTML-Kurse, "Verstehen" für Knowledge Graphs, "Kombiniert" für beides. Optimiert für Claude.
---

# Learning Skill v2.0

---

## 🛑 IDENTITÄTS-REGEL — KEINE EXTERNEN PROJEKTNAMEN (HARD BLOCK)

**Dieser Skill heißt "Learning Skill". Das ist der EINZIGE Name der in jeglichem Output verwendet wird.**

**VERBOTEN — in JEGLICHEM generierten Output (HTML, JSON, Markdown, Kommentare, Tooltips, Logs, Commit-Messages, Dateinamen, Variablennamen, Beschreibungen, Reports, README, Tiefenkarten):**

| ❌ VERBOTEN | Warum |
|---|---|
| "Understand Anything" | Externer Projektname — darf NIEMALS erscheinen |
| "Understand-Anything" | Externer Projektname — darf NIEMALS erscheinen |
| "Understanding Skill" | Falscher Name — der Skill heißt NUR "Learning Skill" |
| "Claude Learning & Understanding Skill" | Falscher Name — der Skill heißt NUR "Learning Skill" |
| "claude-learning-understanding" | Falscher Slug — korrekt ist "learning-skill" |
| ".understand-anything/" | Falscher Ordnername — korrekt ist ".claude-learning/" |
| Jeder Verweis auf die Herkunft der Verstehen-Pipeline | Die Pipeline ist TEIL dieses Skills, kein externes Projekt |

**KORREKTE Bezeichnungen:**

| Kontext | Korrekter Name |
|---|---|
| Skill-Name | "Learning Skill" oder "Learning Skill v2.0" |
| Skill-Slug (YAML, Ordner, Referenzen) | "learning-skill" |
| Output-Ordner für Knowledge Graphs | ".claude-learning/" |
| Modus-Bezeichnungen | "Kurs-Modus", "Verstehen-Modus", "Kombiniert-Modus" |
| Agenten-Referenzen | "project-scanner", "file-analyzer" etc. — OHNE Projektpräfix |

**Selbst-Check vor JEDEM Output:**
```
□ Enthält der Output den String "Understand Anything"? → ENTFERNEN
□ Enthält der Output den String "Understanding"? → Nur OK wenn generisches englisches Wort in einem Satz (z.B. "for understanding the code"), NICHT OK als Namensbestandteil
□ Enthält der Output ".understand-anything/"? → ERSETZEN durch ".claude-learning/"
□ Enthält eine Commit-Message einen Hinweis auf externe Projekte? → ENTFERNEN
□ Enthält der Output "aus Understand-Anything" oder "(aus ...)"? → ENTFERNEN
```

**Diese Regel gilt IMMER — auch bei Tests, Selbstanwendung, Debug-Output, Logs und internen Zwischenergebnissen.**

---

Dieser Skill vereint zwei leistungsstarke Analyse-Pipelines in einem einzigen, Claude-optimierten Werkzeug:

1. **Kurs-Modus** -- Verwandelt beliebige Codebases in interaktive **Multi-Level-HTML-Kurse** mit 4 Tiefenebenen (L0-L3), Zielgruppen-Segmentierung (Anwender/Entwickler/Entscheider), bilingual DE/EN, und Energiekonzern-Design (Tiefenblau #000099, Impuls-Orange #FE8F11, Warmgrau #E4DAD4).

2. **Verstehen-Modus** -- Erzeugt einen interaktiven **Knowledge Graph** (`knowledge-graph.json`) mit Multi-Agent-Pipeline (project-scanner, file-analyzer, architecture-analyzer, tour-builder, graph-reviewer) und interaktivem React Dashboard zur Code-Exploration.

3. **Kombiniert-Modus** (BEST OF BOTH) -- Führt zuerst die Verstehen-Pipeline aus, erzeugt den Knowledge Graph, und nutzt dessen Daten dann um BESSERE HTML-Kurse zu generieren. Der KG verbessert Phase 1 (Analyse) und das Helpfulness-Scoring.

---

## MODUS-ERKENNUNG -- Automatische Weichenstellung

Wenn der User den Skill aufruft, wird der Modus anhand von Schlüsselwörtern bestimmt:

| Modus | Schlüsselwörter | Was passiert |
|---|---|---|
| **Kurs-Modus** | "Kurs", "Tutorial", "Walkthrough", "interaktiv", "course", "teach", "lernen", "erklären", "HTML", "Kursseiten" | Nur die Kurs-Pipeline (Phasen 0-6) |
| **Verstehen-Modus** | "verstehen", "understand", "knowledge graph", "dashboard", "explore", "graph", "analyse", "analyze" | Nur die KG-Pipeline (Phasen 0-7) |
| **Kombiniert-Modus** | "beides", "komplett", "full", "alles", "combined", "kurs + graph", "everything" | Erst KG-Pipeline, dann KG-gestuetzte Kurs-Pipeline |
| **Unklar** | Keines der obigen | User fragen: "Welchen Modus möchtest du? (1) Kurs-Modus -- HTML-Kurse, (2) Verstehen-Modus -- Knowledge Graph + Dashboard, (3) Kombiniert-Modus -- beides" |

---

## UNUMGEHBARE VORBEDINGUNG -- VOR ALLEM ANDEREN LESEN

> **Gilt für: Kurs-Modus und Kombiniert-Modus (Phase B)**
> Für Verstehen-Modus allein: Nur der Quellpfad wird benötigt.

**BEVOR auch nur eine einzige Zeile Code, HTML oder Analyse erzeugt wird, MUSS der User zwei Fragen beantwortet haben:**

1. **Zielgruppen** -- Für wen ALLES? (Anwender, Entwickler, Entscheider, Custom)
2. **Integrationsmodus** -- Standalone oder Eingebettet? (Bei eingebettet: GitHub-URL? Impressum? Datenschutz? Copyright?)

**Es gibt KEINE Ausnahme von dieser Regel. Auch nicht bei:**
- "Verprobe den Skill" / "Teste den Skill" / "Wende den Skill auf sich selbst an"
- "Mach einfach" / "Leg los" / "Ich brauch das schnell"
- "Nur für mich" / "Ist nur ein Test" / "Egal, Hauptsache es funktioniert"
- Impliziten Annahmen aus dem Kontext ("ist ja ein Dev-Repo, also wohl für Entwickler")
- Wenn der User eine Zielgruppe nennt aber den Integrationsmodus nicht ("für Entwickler" -- Integration ist TROTZDEM unklar!)
- Wenn der User den Integrationsmodus nennt aber die Zielgruppen nicht ("standalone" -- Zielgruppen sind TROTZDEM unklar!)

**Was passiert wenn die Fragen nicht gestellt werden:**
- Der gesamte Output ist FALSCH -- falsche Dateibenennung, falscher Tonfall, falscher Inhalt, fehlende/überflüssige Footer und Header-Links
- Jede Datei die ohne diese Antworten erzeugt wird, muss komplett neu geschrieben werden
- Der User verliert Vertrauen in den Skill

**Die EINZIGE korrekte Reaktion wenn Zielgruppen ODER Integrationsmodus unklar sind:**
- Die Rückfrage stellen (siehe Phase 0: "Die Rückfrage")
- WARTEN bis der User antwortet
- ERST DANN mit Phase 1 beginnen

**Selbst-Check vor Phase 1:**
```
[ ] Hat der User EXPLIZIT gesagt für welche Zielgruppen? -> Wenn nein: FRAGEN
[ ] Hat der User EXPLIZIT gesagt ob Standalone oder Eingebettet? -> Wenn nein: FRAGEN
[ ] Wenn Eingebettet: Hat der User GitHub-URL, Impressum, Datenschutz, Copyright angegeben? -> Wenn nein: NACHFRAGEN
[ ] Alle drei Checks bestanden? -> Erst jetzt Phase 1 starten
```

---

## LEVEL-SYSTEM -- Die 4 Tiefenebenen

```
+---------------------------------------------------------------------------+
|  L0: UEBERBLICK (index_*.html)                                             |
|  +- 5-8 Module als Scroll-Seite                                           |
|  +- Jedes Modul = 1 Thema mit max 3 Sätzen + Visualisierung              |
|  +- Jedes Modul verlinkt auf seine L1-Seite                                |
|      |                                                                     |
|  L1: THEMENDETAIL (l1/thema-slug_*.html) -- max 10 pro L0                  |
|  +- Ein Thema aus L0 wird vertieft erklärt                                |
|  +- 4-8 Abschnitte mit je eigener Visualisierung                          |
|  +- Jeder Abschnitt kann auf L2-Seite verlinken                           |
|  +- Breadcrumb: L0 > L1                                                   |
|      |                                                                     |
|  L2: SUB-THEMEN (l2/sub-thema-slug_*.html) -- max 10 pro L1                |
|  +- Ein Abschnitt aus L1 wird zum eigenstaendigen Lernmodul                |
|  +- Tiefe Erklärungen, vollstaendige Code-Walkthroughs                    |
|  +- Kann auf L3-Seiten verlinken für ultimatives Detail                   |
|  +- Breadcrumb: L0 > L1 > L2                                              |
|      |                                                                     |
|  L3: TIEFENDETAIL (l3/detail-slug_*.html) -- max 10 pro L2                 |
|  +- Maximale Tiefe: Zeile-für-Zeile, Edge-Cases, Internals               |
|  +- Für Entwickler: Jede Zeile erklärt + Alternativen                    |
|  +- Für Anwender: Jedes UI-Detail + Fehlerbehebung                       |
|  +- Für Entscheider: Jede Zahl belegt + Szenarien                        |
|  +- Breadcrumb: L0 > L1 > L2 > L3                                         |
|                                                                            |
|  === TIEFERE EBENEN GIBT ES NICHT ===                                      |
|  L3 ist das Maximum. Dort steht ALLES.                                     |
+---------------------------------------------------------------------------+
```

### Level-Charakter-Tabelle

| Level | Zweck | Inhalt pro Seite | Interaktivitaet | Laenge |
|-------|-------|------------------|-----------------|--------|
| **L0** | Vogelperspektive -- "Was gibt es hier?" | 5-8 Module, je 2-3 Sätze + 1 Visual | Quiz, Scroll-Nav | 1 Scroll-Seite |
| **L1** | Themenvertiefung -- "Wie funktioniert das?" | 4-8 Abschnitte, je 1 Absatz + Visual | Quiz, Code<->Klartext, Flow-Diagramme | 1 Scroll-Seite |
| **L2** | Detailwissen -- "Zeig mir die Mechanik" | 3-6 tiefe Abschnitte mit vollstaendigen Erklärungen | Interaktive Diagramme, Drag&Drop, Chat-Simulationen | 1 Scroll-Seite |
| **L3** | Expertenwissen -- "Zeig mir ALLES" | 2-5 ultra-detaillierte Sektionen | Zeile-für-Zeile-Walkthroughs, Edge-Case-Szenarien, Debugging-Challenges | 1 Scroll-Seite |

### Zielgruppen-Tiefenprofile -- Bedarfsgerechte Level-Erzeugung

**KERNPRINZIP:** Nicht jede Zielgruppe braucht 4 Ebenen. Das Tiefenprofil bestimmt PRO ZIELGRUPPE, welche Level überhaupt erzeugt werden. Das spart Dateien, fokussiert Inhalte und verhindert kuenstlich aufgeblaehte Kurse.

**Vordefinierte Tiefenprofile:**

| Zielgruppe | Default Max-Level | Typische Tiefe | HS-Schwelle eigene Seite | HS-Schwelle "noch tiefer" | Begründung |
|---|---|---|---|---|---|
| **Anwender** | **L2** | L0->L1, selten L2 | HS >= 7 (strenger) | HS >= 9 | Anwender wollen NUTZEN, nicht VERSTEHEN. Tiefe nur bei komplexen Workflows oder Troubleshooting |
| **Entwickler** | **L3** | L0->L1->L2->L3 | HS >= 6 (Standard) | HS >= 8 | Entwickler brauchen maximale Tiefe: Code, Edge-Cases, Internals |
| **Entscheider** | **L1** | L0->L1, selten L2 | HS >= 8 (am strengsten) | HS >= 10 (praktisch nie) | Entscheider brauchen Überblick + Kerndetails. Mehr Tiefe = Zeitverschwendung |
| **Custom** | **L2** (anpassbar) | Vom User definiert | HS >= 7 | HS >= 9 | User kann Max-Level bei der Weichenstellung überschreiben |

**Tiefenprofil-Logik:**

```
FUER JEDE Zielgruppe Z:
  max_level = Tiefenprofil[Z].default_max_level
  hs_schwelle = Tiefenprofil[Z].hs_schwelle_eigene_seite
  hs_tiefer = Tiefenprofil[Z].hs_schwelle_noch_tiefer

  FUER JEDES Thema T auf Level L:
    WENN L >= max_level -> STOPP (kein tieferes Level für diese Zielgruppe)
    WENN HS(T, Z) < hs_schwelle -> Inhalt bleibt auf Eltern-Seite
    WENN HS(T, Z) >= hs_schwelle UND HS(T, Z) < hs_tiefer -> Eigene Seite, aber KEIN noch tieferes Level
    WENN HS(T, Z) >= hs_tiefer UND L < max_level -> Eigene Seite + prüfe nächstes Level
```

**Beispiel-Ergebnis für 3 Zielgruppen, Thema "Authentifizierung":**

```
                        Anwender       Entwickler       Entscheider
L0 (Überblick)         Modul          Modul            Modul
L1 (Themendetail)       HS=7           HS=9             HS=8
L2 (Sub-Themen)         HS=5 <7        HS=9             === MAX L1 ===
L3 (Tiefendetail)       === MAX L2 === HS=8             === MAX L1 ===

-> Anwender:    3 Dateien (L0-Modul + L1 DE/EN)
-> Entwickler:  7 Dateien (L0-Modul + L1 + L2 + L3, je DE/EN)
-> Entscheider: 3 Dateien (L0-Modul + L1 DE/EN)
```

**Tiefenprofil-Überschreibung durch User:**

Der User kann bei der Weichenstellung das Tiefenprofil überschreiben:
- "Für Entscheider, aber mit voller Tiefe" -> Max-Level wird auf L3 hochgesetzt
- "Für Entwickler, nur Überblick" -> Max-Level wird auf L1 runtergesetzt
- "Für Anwender bis L3" -> Max-Level wird auf L3 hochgesetzt

Die Überschreibung wird in der Tiefenkarte dokumentiert.

### Dateistruktur & Naming-Konvention

```
output-verzeichnis/
+-- index_de.html                     <- L0 Überblick (Anwender oder allgemeinste Zielgruppe)
+-- index_en.html
+-- index_dev_de.html                 <- L0 Überblick (Entwickler)
+-- index_dev_en.html
+-- l1/
|   +-- authentifizierung_de.html     <- L1 Themendetail
|   +-- authentication_en.html
|   +-- authentifizierung_dev_de.html
|   +-- authentication_dev_en.html
|   +-- datenfluss_de.html
|   +-- dataflow_en.html
|   +-- ... (max 10 Themen x Zielgruppen x 2 Sprachen)
+-- l2/
|   +-- oauth-flow_de.html            <- L2 Sub-Thema
|   +-- oauth-flow_en.html
|   +-- oauth-flow_dev_de.html
|   +-- oauth-flow_dev_en.html
|   +-- ... (max 10 pro L1 x Zielgruppen x 2 Sprachen)
+-- l3/
    +-- token-refresh-mechanik_de.html <- L3 Tiefendetail
    +-- token-refresh-mechanics_en.html
    +-- ... (max 10 pro L2 x Zielgruppen x 2 Sprachen)
```

**Naming-Regeln:**

| Sprache | Slug-Sprache | Beispiel |
|---------|-------------|----------|
| DE-Datei | Deutscher Slug | `authentifizierung_de.html` |
| EN-Datei | Englischer Slug | `authentication_en.html` |
| Zielgruppen-Suffix | Vor Sprach-Suffix | `authentication_dev_en.html` |

**Slug-Generierung:**
- Lowercase, keine Umlaute (ae->ae, oe->oe, ue->ue, ss->ss)
- Bindestriche statt Leerzeichen
- Max 40 Zeichen
- Keine Stoppwörter (der, die, das, the, a, an)

---

## HELPFULNESS-SCORING -- Autonome Tiefenentscheidung

**KERNPRINZIP:** Nicht jedes Thema verdient 3 weitere Ebenen. Der Skill bewertet AUTONOM, ob eine tiefere Seite dem Lernenden WIRKLICH hilft.

### Helpfulness-Score (HS) -- Skala 1-10

Für JEDES potenzielle Unter-Thema wird ein Score berechnet:

```
HS = Komplexitaet(0-3) + Relevanz(0-3) + Lernwert(0-2) + Eigenstaendigkeit(0-2)
```

| Dimension | 0 | 1 | 2 | 3 |
|-----------|---|---|---|---|
| **Komplexitaet** | Trivial, in 1 Satz erklärt | Braucht 1 Absatz | Braucht mehrere Abschnitte | Braucht eigene Seite mit Visuals |
| **Relevanz** | Nischen-Detail | Nice-to-know | Wichtig für Verständnis | Kern-Konzept, ohne das nichts geht |
| **Lernwert** | Nur Fakten-Auflistung | Erklärt ein "Warum" | Ermöglicht eigenes Handeln | Veraendert das Gesamtverständnis |
| **Eigenstaendigkeit** | Wiederholung von Eltern-Seite | 50% neue Information | 80% neue Information | Komplett eigenstaendiges Thema |

### Schwellenwerte -- Zielgruppenspezifisch

Die Schwellenwerte sind NICHT für alle Zielgruppen gleich. Jede Zielgruppe hat eigene Schwellen aus ihrem Tiefenprofil:

| Score-Bereich | Anwender (streng) | Entwickler (Standard) | Entscheider (am strengsten) |
|---|---|---|---|
| **1-4** | Absatz auf Eltern-Seite | Absatz auf Eltern-Seite | Absatz auf Eltern-Seite |
| **5-6** | Erweiterter Absatz / Aufklapp | Eigene Seite | Erweiterter Absatz / Aufklapp |
| **7-8** | Eigene Seite (kein tieferes Level) | Eigene Seite + prüfe L+1 | Eigene Seite (kein tieferes Level) |
| **9-10** | Eigene Seite + prüfe L+1 (bis Max-Level) | Eigene Seite + L+1 empfohlen | Eigene Seite + prüfe L+1 (bis Max-Level) |

**Zusaetzlicher Hard-Stop:** Unabhängig vom HS wird KEIN Level jenseits des Max-Levels der Zielgruppe erzeugt.

```
Entscheidungsbaum pro Thema T, Zielgruppe Z, Level L:

  1. L >= max_level[Z]?           -> STOPP. Kein tieferes Level.
  2. HS(T,Z) < hs_schwelle[Z]?    -> Kein eigene Seite. Absatz/Aufklapp auf Eltern.
  3. HS(T,Z) >= hs_schwelle[Z]?   -> Eigene Seite erstellen.
  4. HS(T,Z) >= hs_tiefer[Z]      -> Prüfe ob L+1 < max_level[Z]. Wenn ja: L+1 planen.
     UND L+1 < max_level[Z]?
```

### Zielgruppen-Gewichtung

Der HS wird PRO ZIELGRUPPE berechnet -- ein Thema kann für Entwickler HS=9 haben und für Entscheider HS=2:

| Thema-Typ | Anwender HS-Tendenz | Entwickler HS-Tendenz | Entscheider HS-Tendenz |
|-----------|---------------------|----------------------|------------------------|
| Implementierungsdetail | 1-3 (irrelevant) | 7-10 (Kern!) | 1-3 (irrelevant) |
| UI-Workflow | 7-10 (Kern!) | 3-5 (nice-to-know) | 2-4 (nice-to-know) |
| Kosten/ROI | 2-4 (nice-to-know) | 1-3 (irrelevant) | 8-10 (Kern!) |
| Fehlerbehandlung | 6-8 (Troubleshooting!) | 8-10 (Kern!) | 3-5 (Risiko-relevant) |
| Architektur-Entscheidung | 1-3 (irrelevant) | 7-9 (wichtig) | 6-8 (strategisch!) |
| Sicherheit/Compliance | 3-5 (was muss ich tun?) | 7-9 (wie umgesetzt?) | 8-10 (Pflicht!) |

### Transparenz-Regel

Am Ende jeder Generierung wird eine **Tiefenkarte** als Markdown-Tabelle ausgegeben, die zeigt:
- Das **Tiefenprofil** jeder Zielgruppe (Max-Level + HS-Schwellen)
- Welche Themen welchen HS bekommen haben
- Welche Seiten erstellt wurden und welche nicht
- Warum ein Thema NICHT tief genug für eine eigene Seite war
- Ob der Hard-Stop (Max-Level) oder der HS-Score die Grenze war

```markdown
## Tiefenkarte -- Generierte Dateien

### Aktive Tiefenprofile
| Zielgruppe | Max-Level | HS-Schwelle (eigene Seite) | HS-Schwelle (noch tiefer) | Überschrieben? |
|---|---|---|---|---|
| Entwickler | L3 | >= 6 | >= 8 | Nein (Default) |
| Anwender | L2 | >= 7 | >= 9 | Nein (Default) |
| Entscheider | L1 | >= 8 | >= 10 | Nein (Default) |

### Detail-Tabelle
| Thema | Zielgruppe | HS | Level | Datei | Stopp-Grund |
|-------|------------|-----|-------|-------|-------------|
| Authentifizierung | Dev | 9 | L1->L2->L3 | 3 Dateien | L3 = Max-Level erreicht |
| Authentifizierung | User | 7 | L1 nur | 1 Datei | HS=7 < 9 (Schwelle "noch tiefer") |
| Authentifizierung | Exec | 8 | L1 nur | 1 Datei | L1 = Max-Level erreicht |
| Logging | Dev | 4 | -- | Absatz auf L1 | HS=4 < 6 (unter Schwelle) |
| UI-Theme | User | 9 | L1->L2 | 2 Dateien | L2 = Max-Level erreicht |
| UI-Theme | Exec | 3 | -- | Absatz auf L0 | HS=3 < 8 (unter Schwelle) |
```

### Knowledge-Graph-gestuetztes Scoring (Kombiniert-Modus)

**Wenn ein Knowledge Graph aus dem Verstehen-Modus existiert, wird das HS-Scoring mit KG-Daten angereichert:**

| HS-Dimension | KG-Datenanreicherung | Auswirkung |
|---|---|---|
| **Komplexitaet** | Node `complexity` Rating aus dem KG (`simple`/`moderate`/`complex`) | `complex` Nodes -> Komplexitaet +1 Bonus, `simple` Nodes -> -1 |
| **Relevanz** | Fan-in/Fan-out Daten (Anzahl eingehender/ausgehender Edges) | Nodes mit >5 Fan-in -> Relevanz +1 (hochvernetzte Kern-Komponenten) |
| **Lernwert** | Layer-Zuordnung aus dem KG | Core-Layer Nodes -> Lernwert +1 gegenüber Utility-Layer Nodes |
| **Eigenstaendigkeit** | Edge-Dichte (Anzahl Cross-Referenzen zu anderen Nodes) | Nodes mit vielen ausgehenden Edges für Entwickler -> hoehere Eigenstaendigkeit |

**KG-gestuetztes Scoring-Verfahren:**

```
FUER JEDES Thema T, basierend auf KG-Node N:
  base_HS = Komplexitaet(0-3) + Relevanz(0-3) + Lernwert(0-2) + Eigenstaendigkeit(0-2)
  
  kg_bonus = 0
  WENN N.complexity == "complex": kg_bonus += 1
  WENN fan_in(N) > 5: kg_bonus += 1
  WENN N in core_layer: kg_bonus += 1
  WENN edge_count(N) > 8 UND Zielgruppe == Entwickler: kg_bonus += 1
  
  final_HS = min(10, base_HS + kg_bonus)
```

**Vorteile des KG-gestuetzten Scorings:**
- Objektivere Bewertung: Basiert auf tatsaechlichen Code-Metriken statt nur auf Heuristiken
- Bessere Vernetzungs-Erkennung: Fan-in/Fan-out zeigt echte Abhängigkeiten
- Konsistentere Ergebnisse: KG-Daten sind reproduzierbar

---

## ORCHESTRATOR -- Modi-übergreifende Phasensteuerung

### Kurs-Modus (Learning-Skill Pipeline)

```
Phase 0: BOOTSTRAP -> Weichen klaeren
Phase 1: ANALYSE -> Codebase verstehen
Phase 2: CURRICULUM -> Modulstruktur + Tiefenkarte
Phase 3: FOUNDATION -> CSS/JS Design-System
Phase 4: BUILD -> Zielgruppen-Pipelines (parallel)
Phase 5: POLISH -> Cross-Level-Navigation
Phase 6: TIEFENKARTE -> Transparenz-Report
```

### Verstehen-Modus (Verstehen-Pipeline)

```
Phase 0: PRE-FLIGHT -> Git-Status, Config
Phase 1: SCAN -> Projekt-Dateien entdecken (project-scanner Agent)
Phase 2: ANALYZE -> Strukturdaten extrahieren (file-analyzer Agents, 5 parallel)
Phase 3: ASSEMBLE REVIEW -> Graph zusammenbauen + validieren
Phase 4: ARCHITECTURE -> Layer-Analyse (architecture-analyzer Agent)
Phase 5: TOUR -> Lernpfade erstellen (tour-builder Agent)
Phase 6: REVIEW -> Graph validieren
Phase 7: SAVE -> knowledge-graph.json speichern
-> Auto-Launch Dashboard
```

### Kombiniert-Modus (BEST OF BOTH)

```
=== PHASE A: VERSTEHEN ===
Phase A0-A7: Vollstaendige Verstehen-Pipeline
-> Erzeugt knowledge-graph.json + Dashboard

=== PHASE B: LEHREN ===
Phase B0: BOOTSTRAP (Weichen klaeren -- Zielgruppen + Integration)
Phase B1: KG-GESTUETZTE ANALYSE (nutzt Knowledge Graph statt roher Code-Analyse)
Phase B2: KG-GESTUETZTES CURRICULUM (HS-Scoring nutzt KG-Daten)
Phase B3-B6: Identisch mit Kurs-Modus
-> Erzeugt HTML-Kurs-Dateien
```

### Orchestrator-Regeln

0. **WEICHEN KLAEREN vor Phase 1 -- HARD BLOCK** -- Zielgruppen (wer ALLE?) UND Integrationsmodus (Standalone/Eingebettet) muessen VOM USER EXPLIZIT BEANTWORTET sein. NICHT aus dem Kontext ableiten. NICHT stillschweigend annehmen. NICHT "für einen Test" überspringen. KEINE AUSNAHME. Wenn der User sagt "leg los" ohne die Fragen beantwortet zu haben -> Rückfrage stellen, NICHT losbauen. Siehe: "UNUMGEHBARE VORBEDINGUNG" am Anfang des Skills.
1. **Kein Curriculum-Review durch den User** -- Direkt bauen.
2. **Ausführungsmodus -- Sequenziell ODER Parallel:**
   - **Sequenziell (Default / Chat-Kontext):** Eine Zielgruppe nach der anderen, jeweils L0->L1->...->max_level.
   - **Parallel (Claude Code mit Agent-Tool):** Jede Zielgruppe bekommt eine **eigene Pipeline** als Subagent. Alle Pipelines laufen gleichzeitig. Siehe Abschnitt "PARALLELISIERUNGS-STRATEGIE".
   - In beiden Modi gilt: Qualitaetsgates pro Seite einhalten, Helpfulness-Score VOR dem Bauen.
3. **Zielgruppen-Pipelines sind unabhängig** -- Die Pipeline von Anwender wartet NICHT auf die Pipeline von Entwickler. Jede Zielgruppe hat ihren eigenen Tiefenpfad. Die EINZIGE Cross-Zielgruppen-Abhängigkeit ist der Zielgruppen-Switch auf L0 -- dieser wird in Phase 5 (Polish) nachtraeglich verlinkt.
4. **Level-Reihenfolge INNERHALB einer Pipeline** -- Pro Zielgruppe gilt: L0 -> L1 -> L2 -> L3. Nie L2 bauen bevor L1 dieser Zielgruppe fertig ist. Aber: Dev-L2 darf parallel zu User-L1 gebaut werden, da verschiedene Pipelines.
5. **Bedarfsgerechte Tiefe -- Pipeline endet am Max-Level** -- Jede Pipeline baut NUR die Levels die laut Tiefenprofil noetig sind:
   - Entscheider-Pipeline: L0 -> L1 -> **STOPP** (Max-Level L1)
   - Anwender-Pipeline: L0 -> L1 -> L2 -> **STOPP** (Max-Level L2)
   - Entwickler-Pipeline: L0 -> L1 -> L2 -> L3 -> **STOPP** (Max-Level L3)
   - Es werden KEINE leeren Levels erzeugt. Wenn eine ZG kein L2 braucht, wird kein L2-Ordner für sie angelegt.
6. **Tiefenprofil-Check VOR dem Bauen** -- Vor JEDER Seite zwei Prüfungen:
   - (a) Liegt das Level innerhalb des max_level der Zielgruppe? Wenn nein -> Pipeline-STOPP für dieses Level.
   - (b) Ist der HS >= der zielgruppenspezifischen Schwelle? Wenn nein -> Absatz/Aufklapp auf Eltern-Seite.
7. **Max 10 Themen pro Ebene** -- Wenn mehr als 10 Kandidaten existieren: nach HS sortieren, Top 10 nehmen, Rest als Absatz auf Eltern-Seite einarbeiten.
8. **Deep-Dive-Links nur wenn Ziel existiert** -- Ein Deep-Dive-Link auf L+1 wird NUR eingefügt, wenn das Tiefenprofil der Zielgruppe L+1 erlaubt UND der HS des Ziel-Themas die Schwelle erreicht. Kein "Deep Dive ->" ins Nichts.
9. **Qualitaetsgates pro Seite (alle Level):**
   - Mindestens 1 interaktives Element
   - Maximal 2-3 Sätze pro Textblock
   - Mindestens 50% visuelle Elemente pro Screen
   - Alle Fachbegriffe mit Tooltip versehen
   - Entwickler: Mindestens 1 Code<->Klartext-Übersetzungsblock pro Seite
   - Anwender: Mindestens 1 Workflow-Flow oder UI-Walkthrough pro Seite
   - Entscheider: Mindestens 1 KPI/Impact-Darstellung pro Seite
   - **Zielgruppen-Switch:** Auf ALLEN L0-Seiten vorhanden (wenn >1 Zielgruppe), verlinkt korrekt auf gleiche Sprache
   - **Navigation:** Breadcrumbs korrekt, Deep-Dive-Links funktional, Zurück-Links vorhanden
   - **L1-L3 Hero:** Page-Overview mit Abschnittsliste vorhanden (NICHT nur Titel + Zurück-Link!)
   - **L1-L3 Module:** Jede Sektion hat grosse gefadete Modulnummer (01, 02, ...) -- KEINE nackten `<section>`-Tags
   - **L1-L3 Struktur:** Identische CSS-Klassen wie L0 (`.module`, `.module-content`, `.module-header`, `.module-number`, `.module-title`, `.module-body`, `.screen`)
   - **min-height:** ALLE Module auf ALLEN Levels haben `min-height: 100dvh`
10. **Fehler-Checkliste vor Abschluss:**
   - [ ] **Pipeline-Vollstaendigkeit** -- Jede ZG-Pipeline hat ALLE geplanten Levels erzeugt (und NUR diese)
   - [ ] **Bedarfsgerechte Tiefe** -- Entscheider hat KEIN L2/L3, Anwender hat KEIN L3, Entwickler hat volle Tiefe bis L3
   - [ ] **Zielgruppen-Trennung** -- Jede Zielgruppe hat eigene Dateien, kein Mischmasch
   - [ ] **Zielgruppen-Switch auf L0** -- Erst in Phase 5 verlinkt, zeigt auf ALLE anderen ZG-L0-Seiten (gleiche Sprache)
   - [ ] **Keine Cross-ZG-Abhängigkeiten im Build** -- Keine Pipeline wartet auf eine andere Pipeline
   - [ ] **Integrationsmodus korrekt** -- Standalone: kein Footer. Eingebettet: alle Links vorhanden
   - [ ] **Beide Sprachversionen** -- DE + EN für JEDE Zielgruppe UND JEDES erzeugte Level
   - [ ] **Cross-Level-Links** -- Alle Deep-Dive-Links zeigen auf existierende Dateien DIESER Zielgruppe
   - [ ] **Breadcrumbs korrekt** -- Jede Seite hat vollstaendigen Pfad zurück zu L0 DIESER Zielgruppe
   - [ ] **Max 10 pro Ebene** -- Keine Ebene hat mehr als 10 Kinder
   - [ ] **HS-Schwelle zielgruppenspezifisch** -- Für jede ZG die EIGENE Schwelle geprüft (Anwender>=7, Entwickler>=6, Entscheider>=8), NICHT pauschal >=6
   - [ ] **Keine toten Deep-Dive-Links** -- Kein Deep-Dive-Link zeigt auf ein Level das für diese ZG nicht existiert
   - [ ] **Tiefenkarte generiert** -- User sieht Tiefenprofile + was pro Pipeline erstellt wurde und warum
   - [ ] Tooltip-Clipping geprüft (position: fixed, body-append)
   - [ ] Genug Tooltips (jeder Fachbegriff)
   - [ ] Keine Textwaende (max 3 Sätze am Stueck)
   - [ ] Keine recycelten Metaphern
   - [ ] Code unveraendert aus der echten Codebase
   - [ ] Quiz testet Anwendung, nicht Auswendiglernen
   - [ ] scroll-snap-type: y proximity (NICHT mandatory)
   - [ ] Jede Seite hat interaktive Elemente
   - [ ] **Farbraum korrekt** -- Tiefenblau/Impuls-Orange/Warmgrau durchgaengig
   - [ ] **Ordnerstruktur korrekt** -- l1/, l2/, l3/ Ordner existieren (nur wenn mindestens 1 ZG dieses Level hat)
   - [ ] **L1-L3 Hero nicht leer** -- Jeder Hero auf L1-L3 enthält Page-Overview mit klickbaren Abschnittslinks
   - [ ] **L1-L3 Modulnummern** -- Jede Inhaltssektion hat grosse gefadete Modulnummer (01, 02, ...)
   - [ ] **L1-L3 CSS-Klassen** -- Identisch zu L0: `.module`, `.module-content`, `.module-header`, `.module-number`
   - [ ] **L1-L3 min-height** -- Alle Module haben `min-height: 100dvh` für konsistentes Scroll-Snap

---

## PARALLELISIERUNGS-STRATEGIE -- Zielgruppen-Pipeline-Architektur

**Wann aktivieren:** Wenn Claude Code verwendet wird UND das Agent-Tool verfügbar ist. Im normalen Chat-Kontext (kein Agent-Tool) wird sequenziell gearbeitet (eine ZG nach der anderen).

**Kernprinzip:** Jede Zielgruppe ist eine unabhängige Pipeline. Pipelines laufen parallel. Innerhalb einer Pipeline: Levels sequenziell, Themen+Sprachen parallel.

### Architektur-Übersicht

```
Phase 0-3: SEQUENZIELL (alle ZG gemeinsam)
  Bootstrap -> Analyse -> Curriculum -> Foundation
  |
Phase 4: ZIELGRUPPEN-PIPELINES (PARALLEL)
  +----------------------------------------------------------+
  |                                                          |
  |  Pipeline Anwender --> L0 --> L1(HS>=7) --> L2(HS>=9) --> DONE |
  |       ||                                                 |
  |  Pipeline Entwickler --> L0 --> L1(HS>=6) --> L2(HS>=8) --> L3 --> DONE |
  |       ||                                                 |
  |  Pipeline Entscheider --> L0 --> L1(HS>=8) --> DONE       |
  |                                                          |
  +----------------------------------------------------------+
  | (Alle Pipelines fertig)
Phase 5-6: SEQUENZIELL (Cross-ZG-Verlinkung + Tiefenkarte)
```

### Was parallelisiert werden KANN

| Ebene | Parallelisierbar | Warum |
|-------|-----------------|-------|
| Phase 0-3 (gemeinsam) | NEIN | Sequenziell -- jede Phase braucht das Ergebnis der vorherigen |
| **Zielgruppen-Pipelines untereinander** | JA | Anwender-Pipeline und Entwickler-Pipeline sind KOMPLETT unabhängig -- verschiedene Inhalte, Tiefen, Dateien |
| Levels INNERHALB einer Pipeline | NEIN | L1 braucht fertiges L0 (für Deep-Dive-Link-Ziele, Breadcrumbs) |
| Themen INNERHALB eines Levels einer Pipeline | JA | `l1/auth_dev_de.html` und `l1/datenfluss_dev_de.html` sind unabhängig |
| DE + EN des gleichen Themas | JA | `l1/auth_dev_de.html` und `l1/authentication_dev_en.html` können parallel entstehen |
| Phase 5-6 (Polish + Tiefenkarte) | NEIN | Braucht ALLE Pipelines fertig um Cross-ZG-Links zu setzen |

### Was NICHT parallelisiert werden darf

- **Levels innerhalb einer Pipeline:** L1 der Entwickler-Pipeline darf NICHT parallel zu L0 der Entwickler-Pipeline gebaut werden. L0 muss fertig sein bevor L1 startet -- sonst fehlen Deep-Dive-Link-Ziele und Breadcrumbs.
- **Phase 3 -> Phase 4:** Das CSS/JS-Foundation MUSS abgeschlossen sein bevor die erste Pipeline startet.
- **Phase 5 (Polish):** Erst wenn ALLE Pipelines komplett sind -- hier werden die Zielgruppen-Switches auf L0 verlinkt.
- **ABER: Pipelines UNTEREINANDER sind frei!** Dev-L2 darf parallel zu User-L0 gebaut werden, da verschiedene Pipelines.

### Zwei-Ebenen-Subagent-Architektur

**Ebene 1: Pipeline-Agents (1 pro Zielgruppe)**

Jede Zielgruppe bekommt einen **Pipeline-Agent**, der den kompletten Tiefenpfad dieser Zielgruppe steuert. Der Pipeline-Agent:
- Kennt das Tiefenprofil seiner ZG (Max-Level, HS-Schwellen)
- Baut Level für Level sequenziell: L0 -> L1 -> ... -> Max-Level
- Startet pro Level Unter-Agents für einzelne Dateien (Ebene 2)
- Stoppt automatisch am Max-Level seiner ZG
- Gibt am Ende eine Pipeline-Zusammenfassung zurück

**Ebene 2: Datei-Agents (N pro Level)**

Innerhalb eines Levels kann der Pipeline-Agent **Datei-Agents** parallel starten:
- Jeder Datei-Agent erstellt EINE HTML-Datei (1 Thema x 1 Sprache)
- Alle Datei-Agents eines Levels laufen parallel
- Der Pipeline-Agent WARTET bis alle Datei-Agents eines Levels fertig sind, bevor das nächste Level beginnt

**Pipeline-Agent-Prompt-Template:**

```
Du bist der Pipeline-Agent für die Zielgruppe [EMOJI + NAME].

Tiefenprofil:
- Max-Level: [L1/L2/L3]
- HS-Schwelle eigene Seite: [>=6/>=7/>=8]
- HS-Schwelle noch tiefer: [>=8/>=9/>=10]

Integrationsmodus: [Standalone/Eingebettet]
Output-Verzeichnis: [PFAD]

Curriculum für deine Zielgruppe:
[THEMEN-BAUM MIT HS-SCORES NUR FUER DIESE ZG]

CSS/JS-Foundation: [REFERENZ AUF PHASE-3-OUTPUT]

Naming-Konvention:
- L0: index[_SUFFIX]_[de|en].html
- L1: l1/[slug][_SUFFIX]_[de|en].html
- L2: l2/[slug][_SUFFIX]_[de|en].html
- L3: l3/[slug][_SUFFIX]_[de|en].html

Deine Aufgabe:
1. Baue L0 (DE + EN parallel als Datei-Agents)
2. WARTE bis L0 fertig
3. Baue L1 -- NUR Themen mit HS >= [SCHWELLE] (alle Themen x DE+EN parallel)
4. WARTE bis L1 fertig
5. [Wenn Max-Level >= L2:] Baue L2 -- NUR Themen mit HS >= [SCHWELLE_TIEFER]
6. WARTE bis L2 fertig
7. [Wenn Max-Level = L3:] Baue L3 -- NUR Themen mit HS >= [SCHWELLE_TIEFER]
8. Gib Pipeline-Zusammenfassung zurück: erzeugte Dateien, übersprungene Themen, Stopp-Gründe

WICHTIG: Zielgruppen-Switch-Links auf L0 LEER lassen (werden in Phase 5 gesetzt).
Qualitaetsgates: [ALLE RELEVANTEN GATES FUER DIESE ZG]
```

**Datei-Agent-Prompt-Template:**

```
Erstelle die HTML-Datei [DATEINAME] im Verzeichnis [PFAD].

Kontext:
- Zielgruppe: [EMOJI + NAME]
- Sprache: [DE/EN]
- Level: [L0/L1/L2/L3]
- Thema: [THEMA]
- Integrationsmodus: [Standalone/Eingebettet]
- Helpfulness-Score: [SCORE]

Inhalt: [INHALTSBESCHREIBUNG AUS CURRICULUM]

CSS/JS: Verwende exakt das folgende Foundation: [FOUNDATION EINFUEGEN ODER REFERENZ]

Verlinkung:
- Breadcrumb-Pfad: [PFAD]
- Deep-Dive-Links: [LISTE DER ZIEL-DATEIEN DIESER ZG]
- Sibling-Seiten: [LISTE INNERHALB DIESER ZG]
- Sprach-Pendant: [DATEINAME]
- Zielgruppen-Switch (nur L0): PLATZHALTER (wird in Phase 5 befuellt)

Qualitaetsgates: [ALLE RELEVANTEN GATES]
```

### Empfohlene Ausführungsreihenfolge

**PRAXIS-MODUS (EMPFOHLEN -- zuverlaessig):**

Die Dateierzeugung erfolgt **sequenziell**, eine Datei nach der anderen. Das ist langsamer aber zuverlaessig. Die Pipeline-Logik bestimmt trotzdem die REIHENFOLGE und TIEFE:

```
Schritt 1: Phase 0-3 sequenziell (Bootstrap -> Analyse -> Curriculum -> Foundation)
           -> Ergebnis: 1 Curriculum pro ZG + 1 Shared Foundation

Schritt 2: Kuerzeste Pipeline ZUERST abarbeiten
           Entscheider-Pipeline: L0(DE) -> L0(EN) -> L1(DE) -> L1(EN) -> DONE
           Anwender-Pipeline: L0(DE) -> L0(EN) -> L1(DE,EN...) -> L2(DE,EN...) -> DONE
           Entwickler-Pipeline: L0(DE) -> L0(EN) -> L1(DE,EN...) -> L2(DE,EN...) -> L3(DE,EN...) -> DONE

Schritt 3: Phase 5 -- Polish (alle Dateien fertig)
           -> Zielgruppen-Switch auf L0-Seiten verlinken
           -> Cross-Links verifizieren

Schritt 4: Phase 6 -- Tiefenkarte ausgeben
```

**PARALLEL-MODUS (OPTIONAL -- nur wenn Agent-Tool zuverlaessig):**

Wenn Subagents gewuenscht sind, maximal **2 parallele Agents** gleichzeitig (nicht mehr!). Bevorzugt: DE + EN des gleichen Themas parallel. NICHT ganze Pipelines parallel starten -- das überfordert das System.

```
Parallelisierung nur auf Datei-Ebene:
  Agent A: auth_dev_de.html  ||  Agent B: authentication_dev_en.html
  -> Warten -> nächstes Paar
```

**Effizienz durch bedarfsgerechte Tiefe (unabhängig vom Modus):**

```
Dateizahl-Vergleich:
  Pauschal L0-L3 für alle: ~100+ Dateien
  Bedarfsgerecht:
    Entscheider: ~8 Dateien (nur L0+L1)
    Anwender: ~12 Dateien (L0+L1+L2)
    Entwickler: ~32 Dateien (L0+L1+L2+L3)
  = ~52 Dateien total -> ~48% weniger
```

### Fehlerbehandlung

- **Datei-Erzeugung schlägt fehl:** NUR diese Datei neu generieren.
- **Cross-ZG-Links:** Werden erst in Phase 5 gesetzt -- funktioniert unabhängig von der Erzeugungsreihenfolge.
- **Bei Problemen:** Auf rein sequenziellen Modus zurückfallen (1 Datei nach der anderen, kein Agent-Tool).

---

## Phase 0: BOOTSTRAP (MODUS-ABHAENGIG)

### Kurs-Modus & Kombiniert-Modus (Phase B0)

#### Begruessung (wenn keine Codebase angegeben)

> **Ich kann jede Codebase in einen interaktiven Multi-Level-Kurs verwandeln -- von der Vogelperspektive bis zum tiefsten Detail.**
>
> Zeig mir einfach ein Projekt:
> * **Lokaler Ordner** -- z.B. "mach einen Kurs aus ./mein-projekt"
> * **GitHub-Link** -- z.B. "erstelle einen Kurs aus https://github.com/user/repo"
> * **Das aktuelle Projekt** -- sag einfach "mach daraus einen Kurs"
>
> Ich erzeuge automatisch:
> * **Das Wichtigste auf einen Blick** -- Was gibt es hier?
> * **Vertiefungsseiten** -- Wie funktioniert das im Detail?
> * **Detailseiten** -- Zeig mir die Mechanik
> * **Alles Schritt für Schritt** -- Für maximale Tiefe
>
> Jede Ebene als eigene HTML-Datei, sauber verlinkt, in DE + EN.

#### Quell-Erkennung

- **GitHub-Link** -> `git clone <url> /tmp/<repo-name>` ausführen
- **Lokaler Ordner** -> Pfad direkt verwenden
- **"Dieses Projekt"** -> Aktuelles Working Directory verwenden

#### Weichenstellungen VOR Phase 1

**STOPP-REGEL (HARD BLOCK -- keine Ausnahme, auch nicht bei Tests!):** Bevor Phase 1 (Analyse) beginnt, MUESSEN zwei Dinge VOM USER EXPLIZIT BEANTWORTET sein: Zielgruppen und Integrationsmodus. Sprache ist KEINE Frage -- es werden IMMER beide Versionen generiert. Auch wenn der User sagt "teste den Skill", "verprobe das mal", "mach einfach" oder "ist nur ein Prototyp" -- die Fragen werden gestellt. KEIN EINZIGES Byte HTML wird geschrieben bevor beide Antworten vorliegen.

**Die Weichen im Überblick:**

| Weiche | Typ | Default wenn unklar |
|---|---|---|
| **Zielgruppen** | Multi-Select: für WEN ALLES? | KEIN Default -- MUSS gefragt werden |
| **Integrationsmodus** | Standalone / Eingebettet | KEIN Default -- MUSS gefragt werden |
| **Sprache** | DE + EN IMMER BEIDES | Automatisch -- KEINE Frage |

---

#### Weiche 1: Zielgruppen (Multi-Select)

**Nicht "für wen" sondern "für wen ALLES"** -- der Skill generiert für JEDE genannte Zielgruppe einen eigenen Kurs (x2 wegen DE+EN, x4 Level). Deshalb muss der User ALLE Zielgruppen auf einmal nennen.

**Vordefinierte Zielgruppen:**

| Kuerzel | Emoji | Wer | Kernfrage |
|---|---|---|---|
| (kein Suffix) | Anwender | **Anwender** -- Nutzer, Kunden, Fachabteilung | "Was kann ich damit tun?" |
| `_dev` | Entwickler | **Entwickler** -- Devs, QA, neue Teammitglieder | "Wie ist das gebaut?" |
| `_exec` | Entscheider | **Entscheider** -- Manager, Stakeholder, C-Level | "Was muss ich wissen?" |
| Custom | Custom | Beliebig -- User kann eigene Zielgruppen definieren | User definiert die Kernfrage |

**Dateibenennung:**

Die allgemeinste / erste Zielgruppe bekommt `index_de.html` / `index_en.html` (ohne Suffix). Weitere Zielgruppen bekommen den Kuerzel als Suffix:

```
Beispiel: User sagt "für Anwender und Entwickler"
-> Anwender = allgemeinste -> index_de.html / index_en.html
-> Entwickler              -> index_dev_de.html / index_dev_en.html

-> L1-Dateien:
  l1/authentifizierung_de.html        (Anwender)
  l1/authentication_en.html           (Anwender)
  l1/authentifizierung_dev_de.html    (Entwickler)
  l1/authentication_dev_en.html       (Entwickler)
```

**Allgemeinste Zielgruppe bestimmen:** Anwender > Entscheider > Entwickler > Custom. Wenn nur eine Zielgruppe -> die bekommt `index_*`. Wenn User die Reihenfolge explizit nennt -> seine Reihenfolge respektieren.

---

#### Weiche 2: Integrationsmodus

| | **STANDALONE** | **EINGEBETTET** |
|---|---|---|
| **Was** | Dateien komplett eigenstaendig | Teil einer Website / Dokumentation |
| **Typisch** | Per E-Mail/Slack geteilt, lokal geoeffnet | Auf GitHub Pages, Firmen-Wiki, Doku-Site |
| **Header** | Kurstitel + Nav-Dots + Flaggen-Link + Level-Nav | + Externe Links (GitHub, Doku, Home) + Buttons |
| **Footer** | Keiner noetig | Impressum, Datenschutz, Copyright |

---

#### KEIN Weiche: Sprache -- IMMER BEIDES

**ES WIRD NICHT GEFRAGT.** Jeder Kurs wird IMMER in Deutsch UND Englisch generiert.

**Sprachversions-Verlinkung:**

Jede Datei enthält in der Nav-Bar einen Flaggen-Link zur jeweils anderen Sprachversion:

```html
<!-- In der DE-Version (l1/authentifizierung_de.html): -->
<a href="authentication_en.html" class="nav-lang" title="English version">🇬🇧</a>

<!-- In der EN-Version (l1/authentication_en.html): -->
<a href="authentifizierung_de.html" class="nav-lang" title="Deutsche Version">🇩🇪</a>
```

**WICHTIG:** Sprachlinks verweisen immer auf die Datei IM GLEICHEN Ordner (relatives Linking innerhalb l1/, l2/, l3/).

---

#### Die Rückfrage (IMMER -- es sei denn der User hat BEIDES bereits explizit beantwortet)

**Die Rückfrage ist der DEFAULT. Sie wird IMMER gestellt, es sei denn der User hat in seiner Nachricht BEIDE Weichen EXPLIZIT beantwortet.** "Nicht eindeutig" ist der Normalfall -- nicht die Ausnahme. Sprache wird NIE gefragt.

**Wann ist "explizit beantwortet"?**
- "Für Entwickler und Anwender, standalone" -> Beides klar, KEINE Rückfrage noetig
- "Für Devs, eingebettet auf unserer GitHub Page, Impressum: example.com/impressum" -> Beides klar
- "Mach einen Kurs aus diesem Repo" -> BEIDES unklar -> Rückfrage!
- "Für Entwickler" -> Zielgruppe klar, Integration UNKLAR -> Rückfrage!
- "Standalone bitte" -> Integration klar, Zielgruppe UNKLAR -> Rückfrage!
- "Verprobe den Skill an sich selbst" -> BEIDES unklar -> Rückfrage!
- "Teste das mal" -> BEIDES unklar -> Rückfrage!

> **Bevor ich loslege, zwei Fragen:**
>
> **1. Für wen ALLES soll der Kurs sein?** (Mehrfachauswahl -- jede Gruppe bekommt einen eigenen Kurs mit bedarfsgerechter Tiefe, jeweils DE + EN)
> * **Anwender** -- Leute die die App/das Produkt BENUTZEN wollen *(Default: bis L2, Fokus auf Workflows)*
> * **Entwickler** -- Leute die den Code VERSTEHEN und AENDERN wollen *(Default: bis L3, volle Tiefe)*
> * **Entscheider** -- Management, Stakeholder *(Default: bis L1, kompakt + KPIs)*
> * **Andere** -- eigene Zielgruppe definieren *(Default: bis L2, anpassbar)*
>
> *Die Tiefe pro Zielgruppe wird automatisch bedarfsgerecht gesteuert. Falls du für eine Gruppe mehr oder weniger Tiefe willst, sag z.B. "Entscheider bis L2" oder "Anwender nur L0+L1".*
>
> **2. Wie werden die Kurse genutzt?**
> * **Standalone** -- Dateien zum Teilen/Offline-Nutzen
> * **Eingebettet** -- Teil einer Website (dann brauche ich: GitHub-Link? Impressum-URL? Copyright?)
>
> *(Sprache muss nicht gewählt werden -- es entstehen automatisch immer DE + EN Versionen.)*

---

### Verstehen-Modus: Phase 0 -- Pre-flight

Determine whether to run a full analysis or incremental update.

1. Set `PROJECT_ROOT` to the current working directory.
2. Get the current git commit hash:
   ```bash
   git rev-parse HEAD
   ```
3. Create the intermediate and temp output directories:
   ```bash
   mkdir -p $PROJECT_ROOT/.claude-learning/intermediate
   mkdir -p $PROJECT_ROOT/.claude-learning/tmp
   ```
3.5. **Auto-update configuration:**
   - If `--auto-update` is in `$ARGUMENTS`: write `{"autoUpdate": true}` to `$PROJECT_ROOT/.claude-learning/config.json`
   - If `--no-auto-update` is in `$ARGUMENTS`: write `{"autoUpdate": false}` to `$PROJECT_ROOT/.claude-learning/config.json`
   - These flags only set the config -- analysis proceeds normally regardless.

4. **Check for subdomain knowledge graphs to merge:**
   List all `*knowledge-graph*.json` files in `$PROJECT_ROOT/.claude-learning/` **excluding** `knowledge-graph.json` itself (e.g. `frontend-knowledge-graph.json`, `backend-knowledge-graph.json`). If any subdomain graphs exist, run the merge script bundled with this skill:
   ```bash
   python <SKILL_DIR>/merge-subdomain-graphs.py $PROJECT_ROOT
   ```
   The script discovers subdomain graphs, loads the existing `knowledge-graph.json` as a base (if present), and merges everything into `knowledge-graph.json` (deduplicating nodes and edges). Report the merge summary to the user, then continue with the merged graph.

5. Check if `$PROJECT_ROOT/.claude-learning/knowledge-graph.json` exists. If it does, read it.
6. Check if `$PROJECT_ROOT/.claude-learning/meta.json` exists. If it does, read it to get `gitCommitHash`.
7. **Decision logic:**

   | Condition | Action |
   |---|---|
   | `--full` flag in `$ARGUMENTS` | Full analysis (all phases) |
   | No existing graph or meta | Full analysis (all phases) |
   | `--review` flag + existing graph + unchanged commit hash | Skip to Phase 6 (review-only -- reuse existing assembled graph) |
   | Existing graph + unchanged commit hash | Ask the user: "The graph is up to date at this commit. Would you like to: **(a)** run a full rebuild (`--full`), **(b)** run the LLM graph reviewer (`--review`), or **(c)** do nothing?" Then follow their choice. If they pick (c), STOP. |
   | Existing graph + changed files | Incremental update (re-analyze changed files only) |

   **Review-only path:** Copy the existing `knowledge-graph.json` to `$PROJECT_ROOT/.claude-learning/intermediate/assembled-graph.json`, then jump directly to Phase 6 step 3.

   For incremental updates, get the changed file list:
   ```bash
   git diff <lastCommitHash>..HEAD --name-only
   ```
   If this returns no files, report "Graph is up to date" and STOP.

8. **Collect project context for subagent injection:**
   - Read `README.md` (or `README.rst`, `readme.md`) from `$PROJECT_ROOT` if it exists. Store as `$README_CONTENT` (first 3000 characters).
   - Read the primary package manifest (`package.json`, `pyproject.toml`, `Cargo.toml`, `go.mod`, `pom.xml`) if it exists. Store as `$MANIFEST_CONTENT`.
   - Capture the top-level directory tree:
     ```bash
     find $PROJECT_ROOT -maxdepth 2 -type f -not -path '*/node_modules/*' -not -path '*/.git/*' -not -path '*/dist/*' | head -100
     ```
     Store as `$DIR_TREE`.
   - Detect the project entry point by checking for common patterns (in order): `src/index.ts`, `src/main.ts`, `src/App.tsx`, `index.js`, `main.py`, `manage.py`, `app.py`, `wsgi.py`, `asgi.py`, `run.py`, `__main__.py`, `main.go`, `cmd/*/main.go`, `src/main.rs`, `src/lib.rs`, `src/main/java/**/Application.java`, `Program.cs`, `config.ru`, `index.php`. Store first match as `$ENTRY_POINT`.

---

## VERSTEHEN-MODUS PHASEN (Knowledge Graph Pipeline)

### Phase 1 -- SCAN (Full analysis only)

Dispatch a subagent using the `project-scanner` agent definition (at `agents/project-scanner.md`). Append the following additional context:

> **Additional context from main session:**
>
> Project README (first 3000 chars):
> ```
> $README_CONTENT
> ```
>
> Package manifest:
> ```
> $MANIFEST_CONTENT
> ```
>
> Use this context to produce more accurate project name, description, and framework detection. The README and manifest are authoritative -- prefer their information over heuristics.

Pass these parameters in the dispatch prompt:

> Scan this project directory to discover all project files (including non-code files like configs, docs, infrastructure), detect languages and frameworks.
> Project root: `$PROJECT_ROOT`
> Write output to: `$PROJECT_ROOT/.claude-learning/intermediate/scan-result.json`

After the subagent completes, read `$PROJECT_ROOT/.claude-learning/intermediate/scan-result.json` to get:
- Project name, description
- Languages, frameworks
- File list with line counts and `fileCategory` per file (`code`, `config`, `docs`, `infra`, `data`, `script`, `markup`)
- Complexity estimate
- Import map (`importMap`): pre-resolved project-internal imports per file (non-code files have empty arrays)

Store `importMap` in memory as `$IMPORT_MAP` for use in Phase 2 batch construction.
Store the file list as `$FILE_LIST` with `fileCategory` metadata for use in Phase 2 batch construction.

**Gate check:** If >100 files, inform the user and suggest scoping with a subdirectory argument. Proceed only if user confirms or add guidance that this may take a while.

---

### Phase 2 -- ANALYZE

#### Full analysis path

Batch the file list from Phase 1 into groups of **20-30 files each** (aim for ~25 files per batch for balanced sizes).

**Batching strategy for non-code files:**
- Group related non-code files together in the same batch when possible:
  - Dockerfile + docker-compose.yml + .dockerignore -> same batch
  - SQL migration files -> same batch (ordered by filename)
  - CI/CD config files (.github/workflows/*) -> same batch
  - Documentation files (docs/*.md) -> same batch
- This allows the file-analyzer to create cross-file edges (e.g., docker-compose `depends_on` Dockerfile)
- Non-code files can be mixed with code files in the same batch if batch sizes are small
- Each file's `fileCategory` from Phase 1 must be included in the batch file list

For each batch, dispatch a subagent using the `file-analyzer` agent definition (at `agents/file-analyzer.md`). Run up to **5 subagents concurrently** using parallel dispatch. Append the following additional context:

> **Additional context from main session:**
>
> Project: `<projectName>` -- `<projectDescription>`
> Languages: `<languages from Phase 1>`

Before dispatching each batch, construct `batchImportData` from `$IMPORT_MAP`:
```json
batchImportData = {}
for each file in this batch:
  batchImportData[file.path] = $IMPORT_MAP[file.path] ?? []
```

Fill in batch-specific parameters below and dispatch:

> Analyze these files and produce GraphNode and GraphEdge objects.
> Project root: `$PROJECT_ROOT`
> Project: `<projectName>`
> Languages: `<languages>`
> Batch index: `<batchIndex>`
> Write output to: `$PROJECT_ROOT/.claude-learning/intermediate/batch-<batchIndex>.json`
>
> Pre-resolved import data for this batch (use this for all import edge creation -- do NOT re-resolve imports from source):
> ```json
> <batchImportData JSON>
> ```
>
> Files to analyze in this batch:
> 1. `<path>` (<sizeLines> lines, fileCategory: `<fileCategory>`)
> 2. `<path>` (<sizeLines> lines, fileCategory: `<fileCategory>`)
> ...

After ALL batches complete, run the merge-and-normalize script bundled with this skill:
```bash
python <SKILL_DIR>/merge-batch-graphs.py $PROJECT_ROOT
```

This script reads all `batch-*.json` files from `$PROJECT_ROOT/.claude-learning/intermediate/`, then in one pass:
- Combines all nodes and edges across batches
- Normalizes node IDs (strips double prefixes, project-name prefixes, adds missing prefixes)
- Normalizes complexity values (`low`->`simple`, `medium`->`moderate`, `high`->`complex`, etc.)
- Rewrites edge references to match corrected node IDs
- Deduplicates nodes by ID (keeps last occurrence) and edges by `(source, target, type)`
- Drops dangling edges referencing missing nodes
- Logs all corrections and dropped items to stderr

Output: `$PROJECT_ROOT/.claude-learning/intermediate/assembled-graph.json`

Include the script's warnings in `$PHASE_WARNINGS` for the reviewer.

#### Incremental update path

Use the changed files list from Phase 0. Batch and dispatch file-analyzer subagents using the same process as above (20-30 files per batch, up to 5 concurrent, with batchImportData constructed from $IMPORT_MAP), but only for changed files.

After batches complete:
1. Remove old nodes whose `filePath` matches any changed file from the existing graph
2. Remove old edges whose `source` or `target` references a removed node
3. Write the pruned existing nodes/edges as `batch-existing.json` in the intermediate directory
4. Run the same merge script -- it will combine `batch-existing.json` with the fresh `batch-*.json` files:
   ```bash
   python <SKILL_DIR>/merge-batch-graphs.py $PROJECT_ROOT
   ```

---

### Phase 3 -- ASSEMBLE REVIEW

Dispatch a subagent using the `assemble-reviewer` agent definition (at `agents/assemble-reviewer.md`).

Pass these parameters in the dispatch prompt:

> Review the assembled graph at `$PROJECT_ROOT/.claude-learning/intermediate/assembled-graph.json`.
> Project root: `$PROJECT_ROOT`
> Batch files are at: `$PROJECT_ROOT/.claude-learning/intermediate/batch-*.json`
> Write review output to: `$PROJECT_ROOT/.claude-learning/intermediate/assemble-review.json`
>
> **Merge script report:**
> ```
> <paste the full stderr output from merge-batch-graphs.py>
> ```
>
> **Import map for cross-batch edge verification:**
> ```json
> $IMPORT_MAP
> ```

After the subagent completes, read `$PROJECT_ROOT/.claude-learning/intermediate/assemble-review.json` and add any notes to `$PHASE_WARNINGS`.

---

### Phase 4 -- ARCHITECTURE

**Build the combined prompt template:**
1. Use the `architecture-analyzer` agent definition (at `agents/architecture-analyzer.md`).
2. **Language context injection:** For each language detected in Phase 1 (e.g., `python`, `markdown`, `dockerfile`, `yaml`, `sql`, `terraform`, `graphql`, `protobuf`, `shell`, `html`, `css`), read the file at `./languages/<language-id>.md` (e.g., `./languages/python.md`, `./languages/dockerfile.md`) and append its content after the base template under a `## Language Context` header. If the file does not exist for a detected language, skip it silently and continue. These files are in the `languages/` subdirectory next to this SKILL.md file. **Include non-code language snippets** -- they provide edge patterns and summary styles for non-code files.
3. **Framework addendum injection:** For each framework detected in Phase 1 (e.g., `Django`), read the file at `./frameworks/<framework-id-lowercase>.md` (e.g., `./frameworks/django.md`) and append its full content after the language context. If the file does not exist for a detected framework, skip it silently and continue. These files are in the `frameworks/` subdirectory next to this SKILL.md file.

Append the language/framework context and the following additional context to the agent's prompt:

> **Additional context from main session:**
>
> Frameworks detected: `<frameworks from Phase 1>`
>
> Directory tree (top 2 levels):
> ```
> $DIR_TREE
> ```
>
> Use the directory tree, language context, and framework addendums (appended above) to inform layer assignments. Directory structure is strong evidence for layer boundaries. Non-code files (config, docs, infrastructure, data) should be assigned to appropriate layers -- see the prompt template for guidance.

Pass these parameters in the dispatch prompt:

> Analyze this codebase's structure to identify architectural layers.
> Project root: `$PROJECT_ROOT`
> Write output to: `$PROJECT_ROOT/.claude-learning/intermediate/layers.json`
> Project: `<projectName>` -- `<projectDescription>`
>
> File nodes (all node types -- includes code files, config, document, service, pipeline, table, schema, resource, endpoint):
> ```json
> [list of {id, type, name, filePath, summary, tags} for ALL file-level nodes -- omit complexity, languageNotes]
> ```
>
> Import edges:
> ```json
> [list of edges with type "imports"]
> ```
>
> All edges (for cross-category analysis -- includes configures, documents, deploys, triggers, etc.):
> ```json
> [list of ALL edges -- include all edge types]
> ```

After the subagent completes, read `$PROJECT_ROOT/.claude-learning/intermediate/layers.json` and normalize it into a final `layers` array. Apply these steps **in order**:

1. **Unwrap envelope:** If the file contains `{ "layers": [...] }` instead of a plain array, extract the inner array.
2. **Rename legacy fields:** If any layer object has a `nodes` field instead of `nodeIds`, rename `nodes` -> `nodeIds`. If `nodes` entries are objects with an `id` field rather than plain strings, extract just the `id` values into `nodeIds`.
3. **Synthesize missing IDs:** If any layer is missing an `id`, generate one as `layer:<kebab-case-name>`.
4. **Convert file paths:** If `nodeIds` entries are raw file paths without a known prefix (`file:`, `config:`, `document:`, `service:`, `pipeline:`, `table:`, `schema:`, `resource:`, `endpoint:`), convert them to `file:<relative-path>`.
5. **Drop dangling refs:** Remove any `nodeIds` entries that do not exist in the merged node set.

Each element of the final `layers` array MUST have this shape:

```json
[
  {
    "id": "layer:<kebab-case-name>",
    "name": "<layer name>",
    "description": "<what belongs in this layer>",
    "nodeIds": ["file:src/App.tsx", "config:tsconfig.json", "document:README.md"]
  }
]
```

All four fields (`id`, `name`, `description`, `nodeIds`) are required.

**For incremental updates:** Always re-run architecture analysis on the full merged node set, since layer assignments may shift when files change.

**Context for incremental updates:** When re-running architecture analysis, also inject the previous layer definitions:

> Previous layer definitions (for naming consistency):
> ```json
> [previous layers from existing graph]
> ```
>
> Maintain the same layer names and IDs where possible. Only add/remove layers if the file structure has materially changed.

---

### Phase 5 -- TOUR

Dispatch a subagent using the `tour-builder` agent definition (at `agents/tour-builder.md`). Append the following additional context:

> **Additional context from main session:**
>
> Project README (first 3000 chars):
> ```
> $README_CONTENT
> ```
>
> Project entry point: `$ENTRY_POINT`
>
> Use the README to align the tour narrative with the project's own documentation. Start the tour from the entry point if one was detected. The tour should tell the same story the README tells, but through the lens of actual code structure.

Pass these parameters in the dispatch prompt:

> Create a guided learning tour for this codebase.
> Project root: `$PROJECT_ROOT`
> Write output to: `$PROJECT_ROOT/.claude-learning/intermediate/tour.json`
> Project: `<projectName>` -- `<projectDescription>`
> Languages: `<languages>`
>
> Nodes (all file-level nodes -- includes code files, config, document, service, pipeline, table, schema, resource, endpoint):
> ```json
> [list of {id, name, filePath, summary, type} for ALL file-level nodes -- do NOT include function or class nodes]
> ```
>
> Layers:
> ```json
> [list of {id, name, description} for each layer -- omit nodeIds]
> ```
>
> Edges (all types -- includes imports, calls, configures, documents, deploys, triggers, etc.):
> ```json
> [list of ALL edges -- include all edge types for complete graph topology analysis]
> ```

After the subagent completes, read `$PROJECT_ROOT/.claude-learning/intermediate/tour.json` and normalize it into a final `tour` array. Apply these steps **in order**:

1. **Unwrap envelope:** If the file contains `{ "steps": [...] }` instead of a plain array, extract the inner array.
2. **Rename legacy fields:** If any step has `nodesToInspect` instead of `nodeIds`, rename it -> `nodeIds`. If any step has `whyItMatters` instead of `description`, rename it -> `description`.
3. **Convert file paths:** If `nodeIds` entries are raw file paths without a known prefix (`file:`, `config:`, `document:`, `service:`, `pipeline:`, `table:`, `schema:`, `resource:`, `endpoint:`), convert them to `file:<relative-path>`.
4. **Drop dangling refs:** Remove any `nodeIds` entries that do not exist in the merged node set.
5. **Sort** by `order` before saving.

Each element of the final `tour` array MUST have this shape:

```json
[
  {
    "order": 1,
    "title": "Project Overview",
    "description": "Start with the README to understand the project's purpose and architecture.",
    "nodeIds": ["document:README.md"]
  },
  {
    "order": 2,
    "title": "Application Entry Point",
    "description": "This step explains how the frontend boots and mounts.",
    "nodeIds": ["file:src/main.tsx", "file:src/App.tsx"]
  }
]
```

Required fields: `order`, `title`, `description`, `nodeIds`. Preserve optional `languageLesson` when present.

---

### Phase 6 -- REVIEW

Assemble the full KnowledgeGraph JSON object:

```json
{
  "version": "1.0.0",
  "project": {
    "name": "<projectName>",
    "languages": ["<languages>"],
    "frameworks": ["<frameworks>"],
    "description": "<projectDescription>",
    "analyzedAt": "<ISO 8601 timestamp>",
    "gitCommitHash": "<commit hash from Phase 0>"
  },
  "nodes": [<all nodes from assembled-graph.json after Phase 3 review>],
  "edges": [<all edges from assembled-graph.json after Phase 3 review>],
  "layers": [<layers from Phase 4>],
  "tour": [<steps from Phase 5>]
}
```

1. Before writing the assembled graph, validate that:
   - `layers` is an array of objects with these required fields: `id`, `name`, `description`, `nodeIds`
   - `tour` is an array of objects with these required fields: `order`, `title`, `description`, `nodeIds`
   - `tour[*].languageLesson` is allowed as an optional string field
   - Every `layers[*].nodeIds` entry exists in the merged node set
   - Every `tour[*].nodeIds` entry exists in the merged node set

   If validation fails, automatically normalize and rewrite the graph into this shape before saving. If the graph still fails final validation after the normalization pass, save it with warnings but mark dashboard auto-launch as skipped.

2. Write the assembled graph to `$PROJECT_ROOT/.claude-learning/intermediate/assembled-graph.json`.

3. **Check `$ARGUMENTS` for `--review` flag.** Then run the appropriate validation path:

---

#### Default path (no `--review`): inline deterministic validation

Write the following Node.js script to `$PROJECT_ROOT/.claude-learning/tmp/ua-inline-validate.cjs`:

```javascript
#!/usr/bin/env node
const fs = require('fs');
const graphPath = process.argv[2];
const outputPath = process.argv[3];
try {
  const graph = JSON.parse(fs.readFileSync(graphPath, 'utf8'));
  const issues = [], warnings = [];
  if (!Array.isArray(graph.nodes)) { issues.push('graph.nodes is missing or not an array'); graph.nodes = []; }
  if (!Array.isArray(graph.edges)) { issues.push('graph.edges is missing or not an array'); graph.edges = []; }
  const nodeIds = new Set();
  const seen = new Map();
  graph.nodes.forEach((n, i) => {
    if (!n.id) { issues.push(`Node[${i}] missing id`); return; }
    if (!n.type) issues.push(`Node[${i}] '${n.id}' missing type`);
    if (!n.name) issues.push(`Node[${i}] '${n.id}' missing name`);
    if (!n.summary) issues.push(`Node[${i}] '${n.id}' missing summary`);
    if (!n.tags || !n.tags.length) issues.push(`Node[${i}] '${n.id}' missing tags`);
    if (seen.has(n.id)) issues.push(`Duplicate node ID '${n.id}' at indices ${seen.get(n.id)} and ${i}`);
    else seen.set(n.id, i);
    nodeIds.add(n.id);
  });
  graph.edges.forEach((e, i) => {
    if (!nodeIds.has(e.source)) issues.push(`Edge[${i}] source '${e.source}' not found`);
    if (!nodeIds.has(e.target)) issues.push(`Edge[${i}] target '${e.target}' not found`);
  });
  const fileLevelTypes = new Set(['file', 'config', 'document', 'service', 'pipeline', 'table', 'schema', 'resource', 'endpoint']);
  const fileNodes = graph.nodes.filter(n => fileLevelTypes.has(n.type)).map(n => n.id);
  const assigned = new Map();
  if (!Array.isArray(graph.layers)) { if (graph.layers) warnings.push('graph.layers is not an array'); graph.layers = []; }
  if (!Array.isArray(graph.tour)) { if (graph.tour) warnings.push('graph.tour is not an array'); graph.tour = []; }
  graph.layers.forEach(layer => {
    (layer.nodeIds || []).forEach(id => {
      if (!nodeIds.has(id)) issues.push(`Layer '${layer.id}' refs missing node '${id}'`);
      if (assigned.has(id)) issues.push(`Node '${id}' appears in multiple layers`);
      assigned.set(id, layer.id);
    });
  });
  fileNodes.forEach(id => {
    if (!assigned.has(id)) issues.push(`File node '${id}' not in any layer`);
  });
  graph.tour.forEach((step, i) => {
    (step.nodeIds || []).forEach(id => {
      if (!nodeIds.has(id)) issues.push(`Tour step[${i}] refs missing node '${id}'`);
    });
  });
  const withEdges = new Set([
    ...graph.edges.map(e => e.source),
    ...graph.edges.map(e => e.target)
  ]);
  graph.nodes.forEach(n => {
    if (!withEdges.has(n.id)) warnings.push(`Node '${n.id}' has no edges (orphan)`);
  });
  const stats = {
    totalNodes: graph.nodes.length,
    totalEdges: graph.edges.length,
    totalLayers: graph.layers.length,
    tourSteps: graph.tour.length,
    nodeTypes: graph.nodes.reduce((a, n) => { a[n.type] = (a[n.type]||0)+1; return a; }, {}),
    edgeTypes: graph.edges.reduce((a, e) => { a[e.type] = (a[e.type]||0)+1; return a; }, {})
  };
  fs.writeFileSync(outputPath, JSON.stringify({ issues, warnings, stats }, null, 2));
  process.exit(0);
} catch (err) { process.stderr.write(err.message + '\n'); process.exit(1); }
```

Execute it:
```bash
node $PROJECT_ROOT/.claude-learning/tmp/ua-inline-validate.cjs \
  "$PROJECT_ROOT/.claude-learning/intermediate/assembled-graph.json" \
  "$PROJECT_ROOT/.claude-learning/intermediate/review.json"
```

If the script exits non-zero, read stderr, fix the script, and retry once.

---

#### `--review` path: full LLM reviewer

If `--review` IS in `$ARGUMENTS`, dispatch the LLM graph-reviewer subagent as follows:

Dispatch a subagent using the `graph-reviewer` agent definition (at `agents/graph-reviewer.md`). Append the following additional context:

> **Additional context from main session:**
>
> Phase 1 scan results (file inventory):
> ```json
> [list of {path, sizeLines} from scan-result.json]
> ```
>
> Phase warnings/errors accumulated during analysis:
> - [list any batch failures, skipped files, or warnings from Phases 2-5]
>
> Cross-validate: every file in the scan inventory should have a corresponding node in the graph (node types may vary: `file:`, `config:`, `document:`, `service:`, `pipeline:`, `table:`, `schema:`, `resource:`, `endpoint:`). Flag any missing files. Also flag any graph nodes whose `filePath` doesn't appear in the scan inventory.

Pass these parameters in the dispatch prompt:

> Validate the knowledge graph at `$PROJECT_ROOT/.claude-learning/intermediate/assembled-graph.json`.
> Project root: `$PROJECT_ROOT`
> Read the file and validate it for completeness and correctness.
> Write output to: `$PROJECT_ROOT/.claude-learning/intermediate/review.json`

---

4. Read `$PROJECT_ROOT/.claude-learning/intermediate/review.json`.

5. **If `issues` array is non-empty:**
   - Review the `issues` list
   - Apply automated fixes where possible:
     - Remove edges with dangling references
     - Fill missing required fields with sensible defaults (e.g., empty `tags` -> `["untagged"]`, empty `summary` -> `"No summary available"`)
     - Remove nodes with invalid types
   - Re-run the final graph validation after automated fixes
   - If critical issues remain after one fix attempt, save the graph anyway but include the warnings in the final report and mark dashboard auto-launch as skipped

6. **If `issues` array is empty:** Proceed to Phase 7.

---

### Phase 7 -- SAVE

1. Write the final knowledge graph to `$PROJECT_ROOT/.claude-learning/knowledge-graph.json`.

2. Write metadata to `$PROJECT_ROOT/.claude-learning/meta.json`:
   ```json
   {
     "lastAnalyzedAt": "<ISO 8601 timestamp>",
     "gitCommitHash": "<commit hash>",
     "version": "1.0.0",
     "analyzedFiles": <number of files analyzed>
   }
   ```

2.5. **Generate structural fingerprints** for all analyzed files and save to `$PROJECT_ROOT/.claude-learning/fingerprints.json`.

3. Clean up intermediate files:
   ```bash
   rm -rf $PROJECT_ROOT/.claude-learning/intermediate
   rm -rf $PROJECT_ROOT/.claude-learning/tmp
   ```

4. Report a summary to the user containing:
   - Project name and description
   - Files analyzed / total files (with breakdown by fileCategory: code, config, docs, infra, data, script, markup)
   - Nodes created (broken down by type: file, function, class, config, document, service, table, endpoint, pipeline, schema, resource)
   - Edges created (broken down by type)
   - Layers identified (with names)
   - Tour steps generated (count)
   - Any warnings from the reviewer
   - Path to the output file: `$PROJECT_ROOT/.claude-learning/knowledge-graph.json`

5. Only automatically launch the dashboard if final graph validation passed after normalization/review fixes.
   If final validation did not pass, report that the graph was saved with warnings and dashboard launch was skipped.

---

## Reference: KnowledgeGraph Schema

### Node Types (13 total)
| Type | Description | ID Convention |
|---|---|---|
| `file` | Source code file | `file:<relative-path>` |
| `function` | Function or method | `function:<relative-path>:<name>` |
| `class` | Class, interface, or type | `class:<relative-path>:<name>` |
| `module` | Logical module or package | `module:<name>` |
| `concept` | Abstract concept or pattern | `concept:<name>` |
| `config` | Configuration file (YAML, JSON, TOML, env) | `config:<relative-path>` |
| `document` | Documentation file (Markdown, RST, TXT) | `document:<relative-path>` |
| `service` | Deployable service definition (Dockerfile, K8s) | `service:<relative-path>` |
| `table` | Database table or migration | `table:<relative-path>:<table-name>` |
| `endpoint` | API endpoint or route definition | `endpoint:<relative-path>:<endpoint-name>` |
| `pipeline` | CI/CD pipeline configuration | `pipeline:<relative-path>` |
| `schema` | Schema definition (GraphQL, Protobuf, Prisma) | `schema:<relative-path>` |
| `resource` | Infrastructure resource (Terraform, CloudFormation) | `resource:<relative-path>` |

### Edge Types (26 total)
| Category | Types |
|---|---|
| Structural | `imports`, `exports`, `contains`, `inherits`, `implements` |
| Behavioral | `calls`, `subscribes`, `publishes`, `middleware` |
| Data flow | `reads_from`, `writes_to`, `transforms`, `validates` |
| Dependencies | `depends_on`, `tested_by`, `configures` |
| Semantic | `related`, `similar_to` |
| Infrastructure | `deploys`, `serves`, `provisions`, `triggers` |
| Schema/Data | `migrates`, `documents`, `routes`, `defines_schema` |

### Edge Weight Conventions
| Edge Type | Weight |
|---|---|
| `contains` | 1.0 |
| `inherits`, `implements` | 0.9 |
| `calls`, `exports`, `defines_schema` | 0.8 |
| `imports`, `deploys`, `migrates` | 0.7 |
| `depends_on`, `configures`, `triggers` | 0.6 |
| `tested_by`, `documents`, `provisions`, `serves`, `routes` | 0.5 |
| All others | 0.5 (default) |

---

## KURS-MODUS PHASEN (HTML-Kurs-Pipeline)

### Phase 1: ANALYSE

Codebase tiefgehend verstehen. Alle Schlüsseldateien lesen, Datenfluesse nachvollziehen, "Hauptfiguren" identifizieren.

**Zu extrahieren:** Hauptakteure, primaere User-Journey, APIs/Datenfluesse, Engineering-Patterns, Tech-Stack.

**Selbst herausfinden was die App tut** -- README + Einstiegspunkte lesen. Modul 1 startet immer mit konkreter User-Aktion.

#### Tiefenanalyse für Level-System -- PRO ZIELGRUPPE

Zusaetzlich zur Basis-Analyse für L0 werden jetzt **pro Zielgruppe getrennt** Tiefenkandidaten identifiziert. Die Analyse geht NUR so tief wie das Tiefenprofil der jeweiligen ZG erlaubt:

| Zielgruppe | Analysierte Tiefe | Was wird analysiert? |
|---|---|---|
| **Entscheider** (Max L1) | Themen für L1 | Welche L0-Module brauchen Vertiefung? (KPI-Relevanz, Strategie-Impact) |
| **Anwender** (Max L2) | Themen für L1 + L2 | Welche Workflows brauchen Detailseiten? Welche L1-Abschnitte brauchen L2? |
| **Entwickler** (Max L3) | Themen für L1 + L2 + L3 | Volle Tiefe: Sub-Aspekte, Mechaniken, Edge-Cases, Debugging-Szenarien |

**KERNREGEL:** Für Entscheider werden KEINE L2/L3-Kandidaten analysiert oder geplant. Das spart Analyse-Aufwand und verhindert Phantom-Themen die nie gebaut werden.

**Analyse-Output** (intern, nicht an User) -- **GETRENNTE Themen-Baeume pro ZG:**

```markdown
## Themen-Baum Entwickler (Max-Level: L3, HS-Schwelle: >=6/>=8)

1. Authentifizierung [HS=9 -> L1]
   1.1. OAuth-Flow [HS=9 -> L2]
      1.1.1. Token-Refresh [HS=7 -> L3 <8]
      1.1.2. Error-Handling bei OAuth [HS=8 -> L3]
   1.2. Session-Management [HS=7 -> L2 <8, erweiterter Absatz]
   1.3. Berechtigungen (RBAC) [HS=8 -> L2]
2. Datenbank [HS=8 -> L1]
   2.1. Schema-Design [HS=8 -> L2]
   2.2. Migrations [HS=4 -> bleibt auf L1]

## Themen-Baum Anwender (Max-Level: L2, HS-Schwelle: >=7/>=9)

1. Erste Schritte [HS=8 -> L1]
   1.1. Anmeldung einrichten [HS=9 -> L2]
   1.2. Profil anpassen [HS=5 -> bleibt auf L1]
2. Hauptfunktionen [HS=9 -> L1]
   2.1. Dashboard nutzen [HS=9 -> L2]
3. Fehlerbehebung [HS=7 -> L1]
   (Keine L2-Kandidaten mit HS>=9)

## Themen-Baum Entscheider (Max-Level: L1, HS-Schwelle: >=8)

1. Executive Summary [HS=9 -> L1]
2. Architektur-Überblick [HS=8 -> L1]
3. Kosten & Ressourcen [HS=8 -> L1]
4. Risiken [HS=6 -> <8, bleibt auf L0]
(KEINE L2/L3-Planung -- Max-Level ist L1!)
```

---

### Phase 2: CURRICULUM + TIEFENPLANUNG

#### L0-Curriculum (identisch zur Basisversion)

5-8 Module pro Zielgruppe. Der Bogen beginnt bei dem was der Lernende kennt -> was er nicht kennt.

#### Entwickler-Curriculum (L0)

| Modul | Zweck |
|-------|-------|
| 1 | App + Kernaktion tracen |
| 2 | Akteure kennenlernen (Komponenten) |
| 3 | Kommunikation der Teile |
| 4 | Aussenwelt (APIs, DB, externe Dienste) |
| 5 | Clevere Tricks (Patterns) |
| 6 | Wenn etwas kaputt geht (Debugging) |
| 7 | Das grosse Ganze |

#### Anwender-Curriculum (L0)

| Modul | Zweck |
|-------|-------|
| 1 | Was ist das? Erster Eindruck |
| 2 | Die Hauptbereiche |
| 3 | Kern-Feature im Detail |
| 4 | Tipps, Tricks, Einstellungen |
| 5 | Haeufige Fragen & Problembehebung |

#### Entscheider-Curriculum (L0)

| Modul | Zweck |
|-------|-------|
| 1 | Executive Summary |
| 2 | Architektur-Überblick (vereinfacht) |
| 3 | Kosten & Ressourcen |
| 4 | Risiken & Abhängigkeiten |
| 5 | Nächste Schritte / Roadmap |

#### L1-L3 Curriculum-Ableitung -- Bedarfsgerecht pro Zielgruppe

**KERNPRINZIP:** Jede Zielgruppe bekommt ihren EIGENEN Curriculum-Baum. Es werden NUR Levels geplant die das Tiefenprofil der ZG vorsieht. Kein Planungs-Overhead für Levels die nie gebaut werden.

**L1-Themen** werden pro ZG aus den L0-Modulen dieser ZG abgeleitet. HS-Schwelle ist zielgruppenspezifisch (Entwickler>=6, Anwender>=7, Entscheider>=8).

**L2-Sub-Themen** werden NUR für ZG mit max_level >= L2 geplant (Entwickler, Anwender). Für Entscheider wird KEIN L2-Curriculum erstellt. HS-Schwelle für "noch tiefer": Entwickler>=8, Anwender>=9.

**L3-Details** werden NUR für ZG mit max_level = L3 geplant (typischerweise nur Entwickler). Für Anwender und Entscheider wird KEIN L3-Curriculum erstellt.

#### Pipeline-Tiefenkarten erstellen (Phase 2 Output)

Vor dem Bauen wird **pro Zielgruppe eine Pipeline-Tiefenkarte** erstellt -- als Planungsdokument für den jeweiligen Pipeline-Agent:

```
=== Pipeline-Tiefenkarte Entwickler (Max: L3, Schwelle: >=6/>=8) ===
L0: Überblick (7 Module)
+-- Modul 1: App + Kernaktion tracen [HS=8 -> L1]
|   +-- L1: Erster Request-Lifecycle [HS=9 -> L2]
|   |   +-- L2: HTTP-Handler im Detail [HS=8 -> L3]
|   |   +-- L2: Middleware-Chain [HS=8 -> L3]
|   +-- L1: Einstiegspunkte [HS=5 -> <6, Absatz auf L0]
+-- Modul 2: Akteure [HS=9 -> L1]
|   +-- L1: Frontend-Komponenten [HS=8 -> L2]
|   |   +-- L2: State-Management [HS=8 -> L3]
|   +-- L1: Backend-Services [HS=8 -> L2]
...
-> Geplante Dateien: 2 (L0) + 10 (L1) + 12 (L2) + 8 (L3) = 32

=== Pipeline-Tiefenkarte Anwender (Max: L2, Schwelle: >=7/>=9) ===
L0: Überblick (5 Module)
+-- Modul 1: Erste Schritte [HS=8 -> L1]
|   +-- L1: Anmeldung einrichten [HS=9 -> L2]
+-- Modul 2: Hauptfunktionen [HS=9 -> L1]
|   +-- L1: Dashboard nutzen [HS=9 -> L2]
+-- Modul 3: Fehlerbehebung [HS=7 -> L1]
|   (Keine L2-Kandidaten mit HS>=9)
...
-> Geplante Dateien: 2 (L0) + 6 (L1) + 4 (L2) = 12
-> KEIN L3 (Max-Level ist L2!)

=== Pipeline-Tiefenkarte Entscheider (Max: L1, Schwelle: >=8) ===
L0: Überblick (5 Module)
+-- Modul 1: Executive Summary [HS=9 -> L1]
+-- Modul 2: Architektur-Überblick [HS=8 -> L1]
+-- Modul 3: Kosten [HS=8 -> L1]
+-- Modul 4: Risiken [HS=6 -> <8, Absatz auf L0]
...
-> Geplante Dateien: 2 (L0) + 6 (L1) = 8
-> KEIN L2/L3 (Max-Level ist L1!)
```

---

### Phase 3: FOUNDATION -- Design-System

#### Shared CSS & JS

**ALLE Level-Seiten** teilen das identische Design-System. Es gibt KEINE separate CSS-Datei -- alles ist inline in jeder HTML-Datei (Self-Contained-Prinzip).

**Aber:** Um Konsistenz zu gewährleisten, wird das CSS einmal definiert und dann in jede Datei kopiert.

#### Google Fonts (in `<head>`)

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Bricolage+Grotesque:opsz,wght@12..96,400;12..96,600;12..96,700;12..96,800&family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;0,9..40,600;0,9..40,700;1,9..40,400;1,9..40,500&family=JetBrains+Mono:wght@400;500;600&display=swap" rel="stylesheet">
```

#### FARBRAUM -- Energiekonzern-Palette (KRITISCH)

```css
:root {
  /* === PRIMAERE BRAND-FARBEN === */
  --color-deep-blue:      #000099;
  --color-impulse-orange:  #FE8F11;
  --color-warm-gray:       #E4DAD4;

  /* === HINTERGRUENDE === */
  --color-bg:              #FFFFFF;
  --color-bg-warm:         #F3EFEB;
  --color-bg-code:         #000066;

  /* === TEXT === */
  --color-text:            #1A1A2E;
  --color-text-secondary:  #6B6560;  /* warm getönt statt kalt-violett #5C5A6B */
  --color-text-muted:      #7A7570;  /* warm getönt statt kalt-violett #6B6778, WCAG AA: 4.6:1 auf Weiss */

  /* === BORDERS & SURFACES === */
  --color-border:          #E4DAD4;
  --color-border-light:    #EDE8E4;
  --color-surface:         #FFFFFF;
  --color-surface-warm:    #F8F5F2;

  /* === AKZENT = Impuls-Orange === */
  --color-accent:          #FE8F11;
  --color-accent-hover:    #E57D00;
  --color-accent-light:    #FFF3E5;
  --color-accent-muted:    #FEB85C;

  /* === SEMANTISCHE FARBEN === */
  --color-success:         #84C041;
  --color-success-light:   #EFF7E5;
  --color-error:           #CC0000;
  --color-error-light:     #FFE5E5;
  --color-info:            #1195EB;
  --color-info-light:      #E5F2FC;
  --color-warning:         #FDC83A;
  --color-warning-light:   #FFF9E5;

  /* === AKTEUR-FARBEN === */
  --color-actor-1:         #000099;
  --color-actor-2:         #FE8F11;
  --color-actor-3:         #84C041;
  --color-actor-4:         #1195EB;
  --color-actor-5:         #5BE3D6;
  --color-actor-6:         #FDC83A;

  /* === DIAGRAMM-PALETTE === */
  --color-chart-1:         #000099;
  --color-chart-2:         #FE8F11;
  --color-chart-3:         #84C041;
  --color-chart-4:         #1195EB;
  --color-chart-5:         #FDC83A;
  --color-chart-6:         #E2C39A;

  /* === FONTS === */
  --font-display:  'Bricolage Grotesque', Georgia, serif;
  --font-body:     'DM Sans', -apple-system, sans-serif;
  --font-mono:     'JetBrains Mono', 'Fira Code', 'Consolas', monospace;

  /* === TYPOGRAFIE === */
  --text-xs:.75rem; --text-sm:.875rem; --text-base:1rem; --text-lg:1.125rem;
  --text-xl:1.25rem; --text-2xl:1.5rem; --text-3xl:1.875rem; --text-4xl:2.25rem;
  --text-5xl:3rem; --text-6xl:3.75rem;
  --leading-tight:1.15; --leading-snug:1.3; --leading-normal:1.6; --leading-loose:1.8;

  /* === ABSTAENDE === */
  --space-1:.25rem; --space-2:.5rem; --space-3:.75rem; --space-4:1rem;
  --space-5:1.25rem; --space-6:1.5rem; --space-8:2rem; --space-10:2.5rem;
  --space-12:3rem; --space-16:4rem; --space-20:5rem; --space-24:6rem;

  /* === LAYOUT === */
  --content-width:820px; --content-width-wide:1000px; --nav-height:50px;
  --radius-sm:8px; --radius-md:12px; --radius-lg:16px; --radius-full:9999px;

  /* === SCHATTEN === */
  --shadow-sm:  0 1px 2px rgba(0,0,60,.05);
  --shadow-md:  0 4px 12px rgba(0,0,60,.08);
  --shadow-lg:  0 8px 24px rgba(0,0,60,.10);
  --shadow-xl:  0 16px 48px rgba(0,0,60,.12);

  /* === ANIMATIONEN === */
  --ease-out:cubic-bezier(.16,1,.3,1); --ease-out-quart:cubic-bezier(.25,1,.5,1); --ease-in-out:cubic-bezier(.65,0,.35,1);
  --duration-fast:150ms; --duration-normal:300ms; --duration-slow:500ms; --stagger-delay:120ms;
}

/* === TRANSITIONS: ease-out-quart als Standard (NICHT generisches 'ease') === */
/* Verwende in allen transition-Deklarationen:
   transition: property Xms var(--ease-out-quart);
   NIEMALS: transition: property Xms ease;
   Das generische 'ease' ist ein Kompromiss der selten optimal ist.
   ease-out-quart (cubic-bezier(.25,1,.5,1)) erzeugt natuerliche Verzoegerung. */
```

#### Syntax-Highlighting (auf #000066)

```css
.code-keyword  { color: #FEB85C; }
.code-string   { color: #84C041; }
.code-function { color: #5BE3D6; }
.code-comment  { color: #7B7BA0; }
.code-number   { color: #FDC83A; }
.code-property { color: #E2C39A; }
.code-operator { color: #1195EB; }
.code-tag      { color: #FE8F11; }
.code-attr     { color: #E2C39A; }
.code-value    { color: #84C041; }
```

#### Design-Regeln (NICHT VERHANDELBAR)

| Regel | Detail |
|-------|--------|
| **Primaerfarbe** | Tiefenblau (#000099) für: Nav-Bar-Akzente, Modulnummern (15% Opacity), Hero-Sektionen |
| **Akzentfarbe** | Impuls-Orange (#FE8F11) für: Buttons, Links, Fortschrittsbalken, Deep-Dive-Links |
| **Warmgrau** | #E4DAD4 für: Borders, Hintergrund-Alternation, Bullet-Farben |
| **Hintergründe** | Gerade Module: Weiss. Ungerade: Warmgrau. Hero: Tiefenblau |
| **Code-Bloecke** | Auf #000066. NICHT Charcoal/Schwarz |
| **Typografie** | Bricolage Grotesque Headings. DM Sans Body. JetBrains Mono Code |
| **Kein Logo** | Keine Logos, keine Firmennamen |
| **Kein Purple** | KEINE Purple-Gradienten |
| **Kein Glassmorphism** | KEIN backdrop-filter:blur() -- ist ein AI-Slop-Tell. Solides rgba() verwenden |
| **Easing** | KEIN generisches `ease` in Transitions. IMMER `var(--ease-out-quart)` oder `cubic-bezier(.25,1,.5,1)` |
| **Transitions** | NUR transform und opacity animieren. NIEMALS width, height, padding, margin |

#### BARRIEREFREIHEIT -- PFLICHT-BLOECKE (in JEDE HTML-Datei)

**Diese beiden CSS-Blöcke MUESSEN in JEDER erzeugten HTML-Datei enthalten sein, direkt vor `</style>`:**

```css
/* === A11Y: Reduced Motion === */
@media(prefers-reduced-motion:reduce){
  *,*::before,*::after{
    animation-duration:0.01ms !important;
    animation-iteration-count:1 !important;
    transition-duration:0.01ms !important;
    scroll-behavior:auto !important;
  }
  html{scroll-snap-type:none !important;scroll-behavior:auto !important}
}

/* === A11Y: Focus Visible === */
*:focus-visible{
  outline:2px solid var(--color-impulse-orange,#FE8F11);
  outline-offset:2px;
  border-radius:4px;
}
button:focus:not(:focus-visible),
a:focus:not(:focus-visible){outline:none}
```

**Warum:**
- **Reduced Motion**: ~35% der Erwachsenen ueber 40 haben vestibulaere Stoerungen. Scroll-Snap, Entrance-Animationen und Canvas-Animationen muessen deaktivierbar sein. WCAG-Verstoß ohne diesen Block.
- **Focus Visible**: Keyboard-User muessen sehen wo sie sind. Impuls-Orange als Fokusring ist CI/CD-konform und gut sichtbar. `:focus:not(:focus-visible)` verhindert den Ring bei Mausklick.

#### KONTRAST-REGELN (KRITISCH -- WCAG AA PFLICHT)

**JEDE Text-Hintergrund-Kombination muss mindestens WCAG AA erfuellen (4.5:1 Kontrast für Normaltext, 3:1 für grossen Text >=18px bold).**

**VERBOTENE Kombinationen:**

| VERBOTEN | Warum | STATTDESSEN |
|---|---|---|
| Weiss (#FFF) auf Warmgrau (#F3EFEB) | Kontrast 1.04:1 -- unlesbar | #1A1A2E (Textfarbe) auf Warmgrau |
| Weiss (#FFF) auf Hellgrau (#E4DAD4) | Kontrast 1.3:1 -- unlesbar | #1A1A2E auf Hellgrau |
| `rgba(255,255,255,.5)` auf Tiefenblau | Kontrast ~3:1 -- zu schwach | `rgba(255,255,255,.85)` oder #FFFFFF |
| `rgba(255,255,255,.4)` auf Tiefenblau | Kontrast ~2.5:1 -- unlesbar | `rgba(255,255,255,.75)` minimum |
| `#9995A0` (text-muted) auf Weiss | Kontrast 3.2:1 -- grenzwertig | `#7A7570` (warm getönt, Kontrast 4.6:1) |
| `#9995A0` (text-muted) auf Warmgrau (#F3EFEB) | Kontrast 2.6:1 -- unlesbar | `#6B6560` (warm getönt, text-secondary) |
| Helle Schrift auf hellen Buttons/Badges | Generell unlesbar | Dunkle Schrift oder dunkler Hintergrund |

**Korrigierte CSS-Werte:**

```css
/* ALT (zu schwach) -> NEU (kontrastreich, warm getönt) */
--color-text-muted:      #7A7570;  /* war #9995A0 -> #6B6778 -> jetzt warm getönt */
--color-text-secondary:  #6B6560;  /* war #5C5A6B -> jetzt warm getönt, harmoniert mit Warmgrau */

/* Auf dunklem Hintergrund (#000099 / #000066): */
/* MINIMUM opacity für weissen Text: .85 */
/* Labels/Subtitles: rgba(255,255,255,.85) statt .5 oder .7 */
/* Separatoren/Trenner: rgba(255,255,255,.6) statt .4 */
```

**Selbst-Check VOR jeder Datei:**
```
[ ] Kein weisser/heller Text auf Warmgrau (#F3EFEB) oder Hellgrau (#E4DAD4)?
[ ] Kein rgba(255,255,255,.5) oder niedriger auf dunklem BG?
[ ] Kein #9995A0 oder #6B6778 oder #5C5A6B (kalt getönt) auf hellem Hintergrund? -> Stattdessen #7A7570 / #6B6560 (warm)
[ ] Hero-Subtitle lesbar? (mindestens rgba(255,255,255,.85) auf #000099)
[ ] Badge-Text lesbar? (dunkle Schrift auf hellem Badge ODER helle auf dunklem)
[ ] Footer-Text lesbar? (mind. #6B6560 auf hellem BG)
[ ] Kein generisches 'ease' in Transitions? -> Stattdessen var(--ease-out-quart) oder cubic-bezier(.25,1,.5,1)
[ ] prefers-reduced-motion Block vorhanden?
[ ] :focus-visible Block vorhanden?
[ ] Kein backdrop-filter:blur() in der Navigation? -> Stattdessen solides rgba(0,0,153,.97)
```

#### UEBERSCHRIFTEN-REGELN (KRITISCH -- KEINE TECHNISCHEN LEVEL-BEZEICHNUNGEN)

**Level-Bezeichnungen (L0, L1, L2, L3) sind INTERNE Technik. Sie gehören NICHT in sichtbare Überschriften, Badges, Titel oder Buttons.**

**VERBOTEN in sichtbarer UI:**

| VERBOTEN | STATTDESSEN |
|---|---|
| "L0 Überblick" | "Das Wichtigste auf einen Blick" |
| "L1 Themendetail" | "Tiefer eintauchen" / konkreter Themenname |
| "L2 Sub-Thema" | "Im Detail erklärt" / konkreter Themenname |
| "L3 Tiefendetail" | "Alles Schritt für Schritt" / konkreter Themenname |
| "Deep Dive L1" | "Mehr erfahren" / "Details ansehen" |
| "+ X Deep-Dive-Seiten" | "+ X Vertiefungsseiten verfügbar" |

**WO Level-Bezeichnungen ERLAUBT sind:**
- Dateinamen (intern): `l1/auth_dev_de.html`
- Tiefenkarte (Entwickler-Report): "L0->L1->L2"
- Breadcrumb-Level-Badges (klein, dezent): `<span class="breadcrumb-level">L1</span>` (nur als Orientierung, nicht als Titel)
- Level-Indicator-Dots (title-Attribute): mit beschreibenden Namen ("Überblick", "Vertiefung", "Im Detail", "Alles erklärt")

**WO Level-Bezeichnungen VERBOTEN sind:**
- Hero-Badges und -Titel
- Modul-Überschriften
- Deep-Dive-Link-Labels
- Nav-Bar-Titel
- Button-Texte
- Alles was der Endnutzer prominent sieht

**Regel für Deep-Dive-Links:**

```html
<!-- FALSCH -->
<span class="deep-dive-label">Deep Dive L1</span>
<span class="deep-dive-title">Authentifizierung im Detail -></span>

<!-- RICHTIG -->
<span class="deep-dive-label">Mehr erfahren</span>
<span class="deep-dive-title">Authentifizierung im Detail -></span>
```

**Regel für Hero-Badges:**

```html
<!-- FALSCH -->
<span class="level-badge">L0 Überblick</span>

<!-- RICHTIG -->
<span class="level-badge">Das Wichtigste auf einen Blick</span>
```

---

### Phase 3 (Fortsetzung): CROSS-LEVEL-NAVIGATION -- Das Herzstueck

#### Breadcrumb-Komponente (L1, L2, L3)

```html
<!-- Beispiel für L2-Seite -->
<nav class="breadcrumb" aria-label="Navigationspfad">
  <a href="../index_dev_de.html" class="breadcrumb-link">
    <span class="breadcrumb-level">L0</span> Überblick
  </a>
  <span class="breadcrumb-sep">></span>
  <a href="authentifizierung_dev_de.html" class="breadcrumb-link">
    <span class="breadcrumb-level">L1</span> Authentifizierung
  </a>
  <span class="breadcrumb-sep">></span>
  <span class="breadcrumb-current">
    <span class="breadcrumb-level">L2</span> OAuth-Flow
  </span>
</nav>
```

```css
.breadcrumb {
  display: flex;
  align-items: center;
  gap: var(--space-2);
  padding: var(--space-3) 0;
  font-family: var(--font-body);
  font-size: var(--text-sm);
  flex-wrap: wrap;
}
.breadcrumb-link {
  color: var(--color-text-secondary);
  text-decoration: none;
  transition: color var(--duration-fast);
}
.breadcrumb-link:hover { color: var(--color-impulse-orange); }
.breadcrumb-sep { color: var(--color-text-muted); }
.breadcrumb-current { color: var(--color-text); font-weight: 500; }
.breadcrumb-level {
  display: inline-block;
  background: var(--color-accent-light);
  color: var(--color-impulse-orange);
  font-family: var(--font-mono);
  font-size: var(--text-xs);
  font-weight: 600;
  padding: 1px 6px;
  border-radius: var(--radius-sm);
  margin-right: 4px;
}
```

#### Deep-Dive-Link-Komponente (auf L0, L1, L2)

Der Link der von einer Ebene zur nächsten tieferen Ebene fuehrt:

```html
<!-- Auf L0-Seite, am Ende eines Moduls -->
<a href="l1/authentifizierung_dev_de.html" class="deep-dive-link animate-in">
  <div class="deep-dive-content">
    <span class="deep-dive-label">Mehr erfahren</span>
    <span class="deep-dive-title">Authentifizierung im Detail -></span>
    <span class="deep-dive-desc">OAuth-Flow, Session-Management, RBAC -- alles Schritt für Schritt</span>
  </div>
  <span class="deep-dive-level">L1</span>
</a>

<!-- Auf L1-Seite, verlinkt auf L2 -->
<a href="../l2/oauth-flow_dev_de.html" class="deep-dive-link animate-in">
  <div class="deep-dive-content">
    <span class="deep-dive-label">Im Detail</span>
    <span class="deep-dive-title">OAuth-Flow: Jeder Schritt erklärt -></span>
    <span class="deep-dive-desc">Token-Austausch, Redirect-Chain, Error-Handling</span>
  </div>
  <span class="deep-dive-level">L2</span>
</a>

<!-- Auf L2-Seite, verlinkt auf L3 -->
<a href="../l3/token-refresh-mechanik_dev_de.html" class="deep-dive-link animate-in">
  <div class="deep-dive-content">
    <span class="deep-dive-label">Alles Schritt für Schritt</span>
    <span class="deep-dive-title">Token-Refresh: Zeile für Zeile -></span>
    <span class="deep-dive-desc">Jede Codezeile erklärt, Edge-Cases, Debugging</span>
  </div>
  <span class="deep-dive-level">L3</span>
</a>
```

```css
.deep-dive-link {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: var(--space-5) var(--space-6);
  margin: var(--space-8) 0;
  background: var(--color-surface-warm);
  border: 1px solid var(--color-border);
  border-left: 4px solid var(--color-impulse-orange);
  border-radius: var(--radius-md);
  text-decoration: none;
  color: var(--color-text);
  transition: all var(--duration-normal) var(--ease-out);
}
.deep-dive-link:hover {
  border-left-color: var(--color-deep-blue);
  background: var(--color-accent-light);
  transform: translateX(4px);
  box-shadow: var(--shadow-md);
}
.deep-dive-content { display: flex; flex-direction: column; gap: var(--space-1); }
.deep-dive-label {
  font-family: var(--font-mono);
  font-size: var(--text-xs);
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: var(--color-impulse-orange);
  font-weight: 600;
}
.deep-dive-title {
  font-family: var(--font-display);
  font-size: var(--text-lg);
  font-weight: 600;
  color: var(--color-text);
}
.deep-dive-desc {
  font-size: var(--text-sm);
  color: var(--color-text-secondary);
}
.deep-dive-level {
  font-family: var(--font-mono);
  font-size: var(--text-xl);
  font-weight: 700;
  color: var(--color-impulse-orange);
  background: var(--color-accent-light);
  padding: var(--space-2) var(--space-4);
  border-radius: var(--radius-sm);
  flex-shrink: 0;
}
```

#### Sibling-Navigation (auf L1, L2, L3)

Am Ende jeder Tiefenseite: Links zu den Nachbar-Seiten auf gleicher Ebene:

```html
<nav class="sibling-nav" aria-label="Weitere Themen auf dieser Ebene">
  <div class="sibling-nav-title">Weitere Themen auf Level 1:</div>
  <div class="sibling-nav-items">
    <a href="datenfluss_dev_de.html" class="sibling-nav-link">
      <span class="sibling-nav-num">02</span>
      <span class="sibling-nav-text">Datenfluss</span>
    </a>
    <span class="sibling-nav-link sibling-nav-current" aria-current="page">
      <span class="sibling-nav-num">03</span>
      <span class="sibling-nav-text">Authentifizierung</span>
    </span>
    <a href="api-design_dev_de.html" class="sibling-nav-link">
      <span class="sibling-nav-num">04</span>
      <span class="sibling-nav-text">API-Design</span>
    </a>
  </div>
</nav>
```

```css
.sibling-nav {
  margin-top: var(--space-16);
  padding-top: var(--space-8);
  border-top: 2px solid var(--color-border);
}
.sibling-nav-title {
  font-family: var(--font-mono);
  font-size: var(--text-xs);
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: var(--color-text-muted);
  margin-bottom: var(--space-4);
}
.sibling-nav-items {
  display: flex;
  flex-wrap: wrap;
  gap: var(--space-3);
}
.sibling-nav-link {
  display: flex;
  align-items: center;
  gap: var(--space-2);
  padding: var(--space-2) var(--space-4);
  border-radius: var(--radius-full);
  border: 1px solid var(--color-border);
  font-size: var(--text-sm);
  text-decoration: none;
  color: var(--color-text-secondary);
  transition: all var(--duration-fast);
}
.sibling-nav-link:hover:not(.sibling-nav-current) {
  border-color: var(--color-impulse-orange);
  color: var(--color-impulse-orange);
  background: var(--color-accent-light);
}
.sibling-nav-current {
  border-color: var(--color-impulse-orange);
  background: var(--color-impulse-orange);
  color: #FFFFFF;
}
.sibling-nav-num {
  font-family: var(--font-mono);
  font-size: var(--text-xs);
  font-weight: 600;
}
```

#### Back-to-Parent-Button (auf L1, L2, L3)

Oben links, neben den Breadcrumbs, ein deutlicher Zurück-Button:

```html
<a href="../index_dev_de.html" class="back-button" title="Zurück zum Überblick">
  <svg width="16" height="16" viewBox="0 0 16 16" fill="currentColor">
    <path d="M7.78 12.53a.75.75 0 01-1.06 0L2.47 8.28a.75.75 0 010-1.06l4.25-4.25a.75.75 0 011.06 1.06L4.81 7h7.44a.75.75 0 010 1.5H4.81l2.97 2.97a.75.75 0 010 1.06z"/>
  </svg>
  <span>Überblick</span>
</a>
```

```css
.back-button {
  display: inline-flex;
  align-items: center;
  gap: var(--space-2);
  padding: var(--space-2) var(--space-4);
  border-radius: var(--radius-full);
  background: var(--color-surface-warm);
  border: 1px solid var(--color-border);
  color: var(--color-text-secondary);
  font-size: var(--text-sm);
  font-family: var(--font-body);
  text-decoration: none;
  transition: all var(--duration-fast);
  margin-bottom: var(--space-4);
}
.back-button:hover {
  border-color: var(--color-impulse-orange);
  color: var(--color-impulse-orange);
  background: var(--color-accent-light);
}
```

#### Level-Indikator (auf jeder Seite)

Ein subtiles Badge das anzeigt auf welchem Level man sich befindet:

```html
<div class="level-indicator" aria-label="Level 2 von 3">
  <span class="level-dot level-dot-done" title="Überblick"></span>
  <span class="level-dot level-dot-done" title="Vertiefung"></span>
  <span class="level-dot level-dot-active" title="Im Detail"></span>
  <span class="level-dot" title="Alles erklärt"></span>
</div>
```

```css
.level-indicator {
  display: flex;
  gap: 6px;
  align-items: center;
  margin-bottom: var(--space-2);
}
.level-dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  border: 2px solid var(--color-border);
  background: transparent;
  transition: all var(--duration-fast);
}
.level-dot-done {
  background: var(--color-impulse-orange);
  border-color: var(--color-impulse-orange);
}
.level-dot-active {
  background: var(--color-deep-blue);
  border-color: var(--color-deep-blue);
  width: 10px;
  height: 10px;
}
```

---

#### Nav-Bar (angepasst für Multi-Level)

Die Nav-Bar zeigt auf L0 die gewohnten Modul-Dots. Auf L1-L3 zeigt sie Breadcrumbs + Zurück-Button.

#### Zielgruppen-Switch (nur auf L0)

Wenn mehrere Zielgruppen generiert werden, enthält jede L0-Seite einen **Zielgruppen-Switch** direkt unter der Nav-Bar (oder als Teil der Nav-Bar). Dieser verlinkt auf die L0-Seiten aller anderen Zielgruppen in der gleichen Sprache.

```html
<!-- Beispiel: Auf index_dev_de.html (Entwickler-Version, DE) -->
<nav class="audience-switch" aria-label="Perspektive wechseln">
  <span class="audience-switch-label">Perspektive:</span>
  <a href="index_de.html" class="audience-switch-link">
    <span class="audience-switch-icon">Anwender</span>
  </a>
  <span class="audience-switch-link audience-switch-current" aria-current="page">
    <span class="audience-switch-icon">Entwickler</span>
  </span>
  <a href="index_exec_de.html" class="audience-switch-link">
    <span class="audience-switch-icon">Entscheider</span>
  </a>
</nav>
```

```css
/* Zielgruppen-Switch */
.audience-switch {
  display: flex; align-items: center; gap: var(--space-3);
  padding: var(--space-2) var(--space-6);
  background: rgba(0,0,153,.85); border-bottom: 1px solid rgba(255,255,255,.1);
  font-size: .85rem;
}
.audience-switch-label { color: rgba(255,255,255,.85); font-weight: 500; }
.audience-switch-link {
  color: rgba(255,255,255,.85); text-decoration: none;
  padding: var(--space-1) var(--space-3); border-radius: 4px;
  transition: all .2s;
}
.audience-switch-link:hover:not(.audience-switch-current) {
  color: #FFFFFF; background: rgba(254,143,17,.2);
}
.audience-switch-current {
  color: #FFFFFF; background: rgba(254,143,17,.25);
  border: 1px solid var(--color-impulse-orange);
}
.audience-switch-icon { margin-right: 4px; }

@media (max-width: 600px) {
  .audience-switch { flex-wrap: wrap; gap: var(--space-2); padding: var(--space-2) var(--space-3); }
  .audience-switch-label { width: 100%; font-size: .75rem; }
}
```

**Regeln für den Zielgruppen-Switch:**
- **NUR auf L0-Seiten** -- L1, L2, L3 haben KEINEN Zielgruppen-Switch
- Verlinkt immer auf die **gleiche Sprache** (DE->DE, EN->EN)
- Die aktuelle Zielgruppe ist visuell markiert (nicht klickbar)
- Wenn nur EINE Zielgruppe generiert wird: kein Switch anzeigen
- Reihenfolge: Anwender -> Entwickler -> Entscheider -> Custom

---

```css
/* L0: Standard-Nav mit Dots */
.nav { background: rgba(0,0,153,.97); border-bottom: 2px solid var(--color-impulse-orange); }
/* KEIN backdrop-filter:blur() — ist Glassmorphism und ein AI-Slop-Tell. Solides rgba genuegt. */
.nav-title { color: #FFFFFF; }
.progress-bar { background: var(--color-impulse-orange); }
.nav-dot { border-color: rgba(255,255,255,.6); }
.nav-dot.active { border-color: var(--color-impulse-orange); background: var(--color-impulse-orange); }
.nav-dot.visited { background: var(--color-impulse-orange); border-color: var(--color-impulse-orange); }

/* L1-L3: Kompakte Nav mit Breadcrumb */
.nav-deep {
  background: rgba(0,0,153,.97);
  /* KEIN backdrop-filter:blur() */
  border-bottom: 2px solid var(--color-impulse-orange);
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 9999;
  height: var(--nav-height);
  display: flex;
  align-items: center;
  padding: 0 var(--space-6);
}
.nav-deep .breadcrumb { margin: 0; padding: 0; }
.nav-deep .breadcrumb-link { color: rgba(255,255,255,.85); }
.nav-deep .breadcrumb-link:hover { color: var(--color-impulse-orange); }
.nav-deep .breadcrumb-sep { color: rgba(255,255,255,.6); }
.nav-deep .breadcrumb-current { color: #FFFFFF; }
.nav-deep .breadcrumb-level { background: rgba(254,143,17,.2); color: var(--color-impulse-orange); }
.nav-deep .nav-lang { color: #FFFFFF; margin-left: auto; }
```

#### Scroll & Layout (identisch für alle Level)

```css
html { scroll-snap-type: y proximity; scroll-behavior: smooth; }
.module { min-height: 100dvh; scroll-snap-align: start;
  padding: var(--space-16) var(--space-6); padding-top: calc(var(--nav-height) + var(--space-12)); }
.module-content { max-width: var(--content-width); margin: 0 auto; }

body {
  background: var(--color-bg);
  background-image: radial-gradient(ellipse at 20% 50%, rgba(0,0,153,.02) 0%, transparent 50%);
}

pre, code { white-space: pre-wrap; word-break: break-word; overflow-x: hidden; }
::-webkit-scrollbar { width: 6px; }
::-webkit-scrollbar-track { background: transparent; }
::-webkit-scrollbar-thumb { background: var(--color-warm-gray); border-radius: var(--radius-full); }
```

#### Responsive Breakpoints

```css
@media (max-width: 768px) {
  :root { --text-4xl: 1.875rem; --text-5xl: 2.25rem; --text-6xl: 3rem; }
  .translation-block { grid-template-columns: 1fr; }
  .sibling-nav-items { flex-direction: column; }
  .nav-links { gap: var(--space-2); }
  .nav-link span:not(.nav-link-icon) { display: none; }
}
@media (max-width: 480px) {
  :root { --text-4xl: 1.5rem; --text-5xl: 1.875rem; --text-6xl: 2.25rem; }
  .module { padding: var(--space-8) var(--space-4); }
  .flow-steps { flex-direction: column; }
  .deep-dive-link { flex-direction: column; text-align: center; }
  .deep-dive-level { margin-top: var(--space-2); }
  .nav-link-text { display: none; }
  .nav-links { gap: var(--space-1); }
  .footer-inner { flex-direction: column; text-align: center; }
}
```

#### Animationen

```css
.animate-in { opacity: 0; transform: translateY(20px);
  transition: opacity var(--duration-slow) var(--ease-out), transform var(--duration-slow) var(--ease-out); }
.animate-in.visible { opacity: 1; transform: translateY(0); }
.stagger-children > .animate-in { transition-delay: calc(var(--stagger-index, 0) * var(--stagger-delay)); }
```

#### JS-Basis (IIFE) -- Erweitert für Multi-Level

```javascript
(function() {
  // Animate-in Observer
  const obs = new IntersectionObserver(entries => {
    entries.forEach(e => { if (e.isIntersecting) { e.target.classList.add('visible'); obs.unobserve(e.target); } });
  }, { rootMargin: '0px 0px -10% 0px', threshold: 0.1 });
  document.querySelectorAll('.animate-in').forEach(el => obs.observe(el));

  // Stagger-Delay
  document.querySelectorAll('.stagger-children').forEach(p =>
    Array.from(p.children).forEach((c, i) => c.style.setProperty('--stagger-index', i)));

  // Progress Bar + Nav Dots (nur auf L0-Seiten)
  const pb = document.querySelector('.progress-bar');
  const dots = document.querySelectorAll('.nav-dot');
  const mods = document.querySelectorAll('.module');
  const navH = 60;

  function activeIndex() {
    let idx = 0;
    mods.forEach((m, i) => { if (m.getBoundingClientRect().top <= navH + 20) idx = i; });
    return idx;
  }

  function updateDots() {
    if (!dots.length) return; // L1-L3 haben keine Dots
    const ai = activeIndex();
    dots.forEach((d, i) => {
      d.classList.toggle('active', i === ai);
      if (i <= ai) d.classList.add('visited');
    });
  }

  window.addEventListener('scroll', () => requestAnimationFrame(() => {
    if (pb) pb.style.width = (window.scrollY / (document.documentElement.scrollHeight - window.innerHeight) * 100) + '%';
    updateDots();
  }), { passive: true });

  updateDots();

  // Dot-Klick (nur L0)
  dots.forEach(d => d.addEventListener('click', () => {
    const target = document.getElementById(d.dataset.target);
    if (!target) return;
    const top = target.getBoundingClientRect().top + window.scrollY - navH;
    window.scrollTo({ top: Math.max(0, top), behavior: 'smooth' });
  }));

  // Keyboard-Navigation
  function scrollToModule(i) {
    if (!mods[i]) return;
    const top = mods[i].getBoundingClientRect().top + window.scrollY - navH;
    window.scrollTo({ top: Math.max(0, top), behavior: 'smooth' });
  }
  function nextModule() { scrollToModule(Math.min(activeIndex() + 1, mods.length - 1)); }
  function prevModule() { scrollToModule(Math.max(activeIndex() - 1, 0)); }
  window.nextModule = nextModule;
  window.prevModule = prevModule;

  document.addEventListener('keydown', e => {
    if (['INPUT','TEXTAREA'].includes(e.target.tagName)) return;
    if (e.key === 'ArrowDown' || e.key === 'ArrowRight') { nextModule(); e.preventDefault(); }
    if (e.key === 'ArrowUp' || e.key === 'ArrowLeft') { prevModule(); e.preventDefault(); }
  });
})();
```

---

### Phase 4: BUILD -- Zielgruppen-Pipelines

**Jede Zielgruppe durchläuft ihre eigene Build-Pipeline.** Bei Claude Code mit Agent-Tool laufen alle Pipelines parallel. Im Chat-Modus werden Zielgruppen sequenziell abgearbeitet (schnellste/kompakteste zuerst: Entscheider -> Anwender -> Entwickler).

#### Pipeline-Schritt L0: BUILD Überblicks-Seite

Jede Pipeline beginnt mit der L0-Seite ihrer Zielgruppe. Jedes Modul endet mit einem **Deep-Dive-Link** auf die zugehörige L1-Seite -- aber NUR wenn der HS für diese Zielgruppe die Schwelle erreicht (Entwickler>=6, Anwender>=7, Entscheider>=8). Der **Zielgruppen-Switch** wird als Platzhalter angelegt und erst in Phase 5 verlinkt.

**Template L0-Modul mit Deep-Dive:**

```html
<section class="module" id="module-3" style="background:var(--color-bg-warm)">
  <div class="module-content">
    <header class="module-header animate-in">
      <span class="module-number" style="color:var(--color-deep-blue);opacity:.15">03</span>
      <h1 class="module-title">Authentifizierung</h1>
    </header>
    <div class="module-body">
      <section class="screen animate-in">
        <!-- 2-3 Sätze + Visualisierung -->
        <p>Die App verwendet OAuth 2.0 mit PKCE für sichere Anmeldung. Drei Provider werden unterstützt: Google, GitHub und E-Mail/Passwort.</p>
        <!-- Visualisierung hier -->
      </section>

      <!-- Deep-Dive-Link (nur wenn HS >= 6) -->
      <a href="l1/authentifizierung_dev_de.html" class="deep-dive-link animate-in">
        <div class="deep-dive-content">
          <span class="deep-dive-label">Mehr erfahren</span>
          <span class="deep-dive-title">Authentifizierung im Detail -></span>
          <span class="deep-dive-desc">OAuth-Flow, Session-Management, RBAC -- alles Schritt für Schritt</span>
        </div>
        <span class="deep-dive-level">L1</span>
      </a>
    </div>
  </div>
</section>
```

#### Pipeline-Schritt L1: BUILD Themendetail-Seiten (NUR wenn max_level >= L1)

**Wird ausgeführt von:** Allen Pipelines (Entscheider, Anwender, Entwickler) -- aber mit unterschiedlichen HS-Schwellen und unterschiedlichem Inhaltscharakter.

**Pipeline-spezifisch:**
- Entscheider: Nur Themen mit HS>=8. Kompakte, KPI-fokussierte Seiten. **Dies ist das LETZTE Level der Entscheider-Pipeline.**
- Anwender: Nur Themen mit HS>=7. Workflow-orientierte Seiten.
- Entwickler: Themen mit HS>=6. Code-fokussierte Seiten.

Jede L1-Seite ist eine eigenstaendige Scroll-Seite zu EINEM Thema aus L0. Deep-Dive-Links auf L2 werden NUR eingefügt wenn die Pipeline noch weiter geht (Entscheider: NIE, Anwender: nur HS>=9, Entwickler: HS>=8).

**L1-Seiten-Struktur:**

```html
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Authentifizierung -- [Kursname]</title>
  <!-- Google Fonts + CSS (identisch) -->
</head>
<body>
  <!-- Nav-Bar (Deep-Level-Variante) -->
  <nav class="nav-deep">
    <nav class="breadcrumb">
      <a href="../index_dev_de.html" class="breadcrumb-link">
        <span class="breadcrumb-level">L0</span> Überblick
      </a>
      <span class="breadcrumb-sep">></span>
      <span class="breadcrumb-current">
        <span class="breadcrumb-level">L1</span> Authentifizierung
      </span>
    </nav>
    <a href="authentication_dev_en.html" class="nav-lang" title="English version">EN</a>
  </nav>

  <!-- Hero-Sektion -->
  <section class="module module-hero" id="module-0">
    <div class="module-content" style="text-align:center">
      <div class="level-indicator">
        <span class="level-dot level-dot-done"></span>
        <span class="level-dot level-dot-active"></span>
        <span class="level-dot"></span>
        <span class="level-dot"></span>
      </div>
      <h1 style="color:#FFFFFF">Authentifizierung</h1>
      <p style="color:rgba(255,255,255,.85)">Wie die App Benutzer sicher erkennt und berechtigt</p>
    </div>
  </section>

  <!-- 4-8 Abschnitte als Module -->
  <section class="module" id="module-1">
    <div class="module-content">
      <header class="module-header animate-in">
        <span class="module-number" style="color:var(--color-deep-blue);opacity:.15">01</span>
        <h1 class="module-title">Der OAuth-Flow</h1>
      </header>
      <div class="module-body">
        <!-- Detaillierte Erklärung + Visuals -->

        <!-- Deep-Dive auf L2 (wenn HS >= Schwelle) -->
        <a href="../l2/oauth-flow_dev_de.html" class="deep-dive-link animate-in">
          <div class="deep-dive-content">
            <span class="deep-dive-label">Im Detail</span>
            <span class="deep-dive-title">OAuth-Flow: Jeder Schritt erklärt -></span>
            <span class="deep-dive-desc">Token-Austausch, Redirect-Chain, Error-Handling</span>
          </div>
          <span class="deep-dive-level">L2</span>
        </a>
      </div>
    </div>
  </section>

  <!-- ... weitere Abschnitte ... -->

  <!-- Sibling-Navigation -->
  <section class="module" style="min-height:auto; padding-bottom: var(--space-16)">
    <div class="module-content">
      <nav class="sibling-nav">
        <div class="sibling-nav-title">Weitere Themen auf Level 1:</div>
        <div class="sibling-nav-items">
          <a href="datenfluss_dev_de.html" class="sibling-nav-link">
            <span class="sibling-nav-num">01</span>
            <span class="sibling-nav-text">Datenfluss</span>
          </a>
          <span class="sibling-nav-link sibling-nav-current">
            <span class="sibling-nav-num">02</span>
            <span class="sibling-nav-text">Authentifizierung</span>
          </span>
          <!-- ... -->
        </div>
      </nav>
    </div>
  </section>

  <!-- JS (identisch) -->
</body>
</html>
```

#### Pipeline-Schritt L2: BUILD Sub-Themen-Seiten (NUR wenn max_level >= L2)

**Wird ausgeführt von:** Anwender-Pipeline und Entwickler-Pipeline. **Entscheider-Pipeline ist bereits fertig und hat diesen Schritt NICHT.**

**Pipeline-spezifisch:**
- Anwender: Nur Themen mit HS>=9 (strengste Schwelle). Workflow-Detail-Seiten. **Dies ist das LETZTE Level der Anwender-Pipeline.** Keine Deep-Dive-Links auf L3.
- Entwickler: Themen mit HS>=8. Code-Walkthrough-Seiten. Deep-Dive-Links auf L3 wenn HS>=8.

Identische Struktur wie L1, aber:
- Breadcrumb hat 3 Stufen (L0 > L1 > L2)
- Level-Indicator zeigt 3. Dot aktiv
- Inhalt ist DEUTLICH detaillierter: vollstaendige Code-Walkthroughs, Schritt-für-Schritt
- **Entwickler:** Zeile-für-Zeile-Erklärungen beginnen hier
- **Anwender:** Jeder Klick, jede Einstellung erklärt

#### Pipeline-Schritt L3: BUILD Tiefendetail-Seiten (NUR wenn max_level = L3)

**Wird ausgeführt von:** Typischerweise NUR Entwickler-Pipeline. **Anwender und Entscheider Pipelines sind bereits fertig.**

Maximale Tiefe. Kein Deep-Dive-Link mehr (L3 ist das Maximum). Dies ist der LETZTE Schritt der Entwickler-Pipeline.

**L3-Inhalts-Charakter (primaer Entwickler):**

| | Entwickler (Standard) | Anwender (nur bei Override auf L3) |
|---|---|---|
| **Fokus** | Jede Codezeile, jeder Edge-Case | Jedes UI-Detail, jede Fehlermeldung |
| **Typische Elemente** | Zeile-für-Zeile mit Erklärung, Alternative Implementierungen, Debugging-Challenges | Screenshot-Annotationen, Fehlerbehebungs-Flows |
| **Interaktivitaet** | Code-Challenges, Bug-Hunts | "Was passiert wenn..." Simulationen |
| **Tiefe** | Edge-Cases, Race-Conditions, Performance-Implikationen | Jeder Fehlerzustand dokumentiert |

**Hinweis:** Entscheider haben standardmaessig KEIN L3. Wenn der User per Override "Entscheider bis L3" anfordert, wird der Inhaltscharakter angepasst: ROI-Berechnungen, Risiko-Matrizen, Best/Worst/Expected-Case Szenarien.

---

### Phase 4 (alle Pipelines): BUILD -- Interaktive Elemente

#### Level-spezifische Element-Dichte (beachte: nicht jede ZG hat alle Levels!)

| Element | L0 (alle ZG) | L1 (alle ZG) | L2 (Anwender/Entwickler) | L3 (nur Entwickler) |
|---------|----|----|----|----|
| Code<->Klartext (Entwickler) | 0-1 | 1-3 | 3-6 | 5-10 |
| Visualisierungen | 1 pro Modul | 2 pro Abschnitt | 2-3 pro Abschnitt | 1-2 pro Abschnitt |
| Quiz | 1 pro Modul | 1-2 pro Seite | 2-3 pro Seite | 1-2 (anspruchsvoller) |
| Workflow-Flows (Anwender) | 1 pro Modul | 2-3 pro Seite | 3-5 pro Seite | -- (Anwender hat kein L3) |
| KPI-Dashboards (Entscheider) | 1 pro Modul | 1-2 pro Seite | -- (Entscheider hat kein L2) | -- (Entscheider hat kein L3) |
| Tooltips | Kern-Begriffe | Alle Fachbegriffe | Alle + Referenzen | Alle + Alternativ-Erklärungen |
| Deep-Dive-Links | Ja (->L1, wenn ZG L1 hat) | Ja (->L2, wenn ZG L2 hat) | Ja (->L3, NUR Entwickler) | **NEIN** (Maximum) |

#### Farbzuweisung (identisch für alle Level)

| Element | Primaerfarbe | Akzent |
|---------|-------------|--------|
| Step-Nummern | -- | Impuls-Orange BG, weisse Zahl |
| Callout-Border | -- | Impuls-Orange (accent), Hellblau (info), Rot (warning) |
| Card-Top-Border | -- | Akteur-Farben rotierend |
| Quiz-Option selected | -- | Impuls-Orange Border |
| Deep-Dive-Links | -- | Impuls-Orange Left-Border |
| Level-Dot active | Tiefenblau | -- |
| Level-Dot done | -- | Impuls-Orange |
| Breadcrumb-Level-Badge | -- | Impuls-Orange auf hellem BG |
| Code-Block BG | #000066 | -- |
| Translation-Border | -- | Impuls-Orange 3px links |

#### E1: Code <-> Klartext-Übersetzung (alle Level, Entwickler)

```css
.translation-code { background: var(--color-bg-code); color: #D0D0E8; }
.translation-english { background: var(--color-surface-warm); border-left: 3px solid var(--color-impulse-orange); }
```

**Level-Anpassung:**
- **L0:** Ganzer Funktionskoerper -> 1 Klartext-Satz
- **L1:** Funktion in 3-5 Bloecke -> je 1 Klartext-Absatz
- **L2:** Jeder logische Block -> Detaillierte Erklärung + Warum
- **L3:** Jede einzelne Zeile -> Erklärung + Alternative + Edge-Case

#### E13: Glossar-Tooltips (alle Level)

```css
.term { border-bottom: 1.5px dashed var(--color-accent-muted); cursor: pointer; }
.term:hover { border-bottom-color: var(--color-impulse-orange); color: var(--color-impulse-orange); }
.term-tooltip { position: fixed; background: var(--color-bg-code); color: #D0D0E8; z-index: 10000; }
```

**Level-Anpassung:**
- **L0:** Tooltip = 1 Satz Definition
- **L1:** Tooltip = Definition + "Warum wichtig"
- **L2:** Tooltip = Definition + Kontext + "Wo im Code"
- **L3:** Tooltip = Definition + Kontext + Implementierungsdetail + Alternatives

---

### Phase 5: POLISH -- Cross-Level-Konsistenz

#### Prüfliste (erweitert)

1. **Farb-Konsistenz:** Tiefenblau/Impuls-Orange/Warmgrau auf ALLEN Level-Seiten identisch.
2. **Cross-Level-Links:** JEDER Deep-Dive-Link zeigt auf eine existierende Datei.
3. **Breadcrumbs:** Korrekte Hierarchie, alle Links funktional, relative Pfade korrekt (../ für Ordnerwechsel).
4. **Sibling-Navigation:** Alle Geschwister-Seiten korrekt verlinkt, aktuelle Seite markiert.
5. **Level-Indicator:** Korrekte Anzahl Dots, richtiger aktiver/done-Status.
6. **Sprach-Links:** Jede DE-Datei verlinkt auf EN-Pendant und umgekehrt. INNERHALB des gleichen Ordners.
7. **Zielgruppen-Verlinkung auf L0:** Jede L0-Seite (index_*.html) enthält einen **Zielgruppen-Switch** im Header, der auf die L0-Seiten der anderen Zielgruppen verlinkt. Ab L1 abwaerts verlinken Dateien verschiedener Zielgruppen NICHT aufeinander.
8. **Ordnerstruktur:** l1/, l2/, l3/ korrekt angelegt.
9. **Relative Pfade korrekt:**
   - L0 -> L1: `href="l1/slug_de.html"` (kein ../)
   - L1 -> L2: `href="../l2/slug_de.html"` (eine Ebene hoch, dann in l2/)
   - L2 -> L3: `href="../l3/slug_de.html"` (eine Ebene hoch, dann in l3/)
   - L1 -> L0: `href="../index_de.html"`
   - L2 -> L0: `href="../index_de.html"`
   - L2 -> L1: `href="../l1/slug_de.html"`
   - L3 -> L0: `href="../index_de.html"`
   - L3 -> L1: `href="../l1/slug_de.html"`
   - L3 -> L2: `href="../l2/slug_de.html"`
10. **Mobile:** Deep-Dive-Links stacken vertikal. Sibling-Nav wird Column-Layout.
11. **ARIA:** Breadcrumbs mit aria-label, Level-Indicator mit aria-label.
12. **Sprache IMMER DE + EN:**
    - `<html lang="de">` bzw. `<html lang="en">` korrekt
    - Flaggen-Link zeigt auf korrekte Gegenstueck-Datei
    - Keine Sprachwechsel im Fliesstext

#### Relative-Pfad-Referenz

```
Dateisystem:
+-- index_de.html          (L0)
+-- l1/
|   +-- auth_de.html       (L1)
+-- l2/
|   +-- oauth_de.html      (L2)
+-- l3/
    +-- token_de.html      (L3)

Pfade VON -> NACH:
L0 -> L1: "l1/auth_de.html"
L0 -> L2: "l2/oauth_de.html"         (selten, meist über L1)
L1 -> L0: "../index_de.html"
L1 -> L1: "other_de.html"            (gleicher Ordner)
L1 -> L2: "../l2/oauth_de.html"
L2 -> L0: "../index_de.html"
L2 -> L1: "../l1/auth_de.html"
L2 -> L2: "other_de.html"            (gleicher Ordner)
L2 -> L3: "../l3/token_de.html"
L3 -> L0: "../index_de.html"
L3 -> L1: "../l1/auth_de.html"
L3 -> L2: "../l2/oauth_de.html"
L3 -> L3: "other_de.html"            (gleicher Ordner)
```

---

### Phase 6: TIEFENKARTE -- Transparenz-Report

Nach Abschluss aller Dateien wird dem User eine Tiefenkarte ausgegeben:

```markdown
## Tiefenkarte -- Generierte Dateien

### Statistik
- **Zielgruppen:** Entwickler, Anwender
- **Sprachen:** Deutsch, Englisch
- **Dateien gesamt:** 42
  - L0: 4 (2 Zielgruppen x 2 Sprachen)
  - L1: 16 (4 Themen x 2 Zielgruppen x 2 Sprachen)
  - L2: 14 (diverse, HS-gefiltert)
  - L3: 8 (nur hohe Komplexitaet)
- **Nicht erstellt (HS < 6):** 12 Themen -> als Absätze eingearbeitet

### Detail-Tabelle

| Thema | ZG | HS | Level | Dateien | Entscheidung |
|-------|----|----|-------|---------|-------------|
| Authentifizierung | Dev | 9 | L0->L1->L2->L3 | 8 | Kern-Konzept, maximale Tiefe |
| Authentifizierung | User | 6 | L0->L1 | 4 | Anwender brauchen nur Überblick + Login-Guide |
| Datenfluss | Dev | 8 | L0->L1->L2 | 6 | Wichtig, aber L3 waere Wiederholung |
| Datenfluss | User | 3 | L0 nur | 0 extra | Für Anwender nicht relevant, Absatz auf L0 |
| UI-Themes | User | 7 | L0->L1->L2 | 6 | Workflow-relevant für Anwender |
| UI-Themes | Dev | 2 | -- | 0 | Triviale CSS-Config, nicht lehrreich |
| Logging | Dev | 4 | L0 nur | 0 extra | Erweiterter Absatz auf L0 reicht |
| Deployment | Dev | 7 | L0->L1 | 4 | Eigenes Thema, aber L2 waere Config-Auflistung |
| ...  | ... | ... | ... | ... | ... |

### Ordnerstruktur

kursname/
+-- index_de.html               <- Anwender L0 Überblick
+-- index_en.html
+-- index_dev_de.html           <- Entwickler L0 Überblick
+-- index_dev_en.html
+-- l1/
|   +-- anmeldung_de.html       <- Anwender Login-Guide
|   +-- login-guide_en.html
|   +-- authentifizierung_dev_de.html  <- Entwickler Auth-Detail
|   +-- authentication_dev_en.html
|   +-- ... (12 weitere)
+-- l2/
|   +-- oauth-flow_dev_de.html
|   +-- oauth-flow_dev_en.html
|   +-- ... (12 weitere)
+-- l3/
    +-- token-refresh_dev_de.html
    +-- token-refresh_dev_en.html
    +-- ... (6 weitere)
```

---

## KOMBINIERT-MODUS SPEZIFIK -- KG-gestuetzte Kursoptimierung

Der Kombiniert-Modus fuehrt zuerst die vollstaendige Verstehen-Pipeline (Phase A0-A7) aus und nutzt dann die resultierenden KG-Daten um bessere Kurse zu generieren.

### Phase B1: KG-GESTUETZTE ANALYSE

**Anstatt alle Code-Dateien manuell zu lesen (wie im reinen Kurs-Modus), nutzt Phase B1 den Knowledge Graph:**

1. **Node-Summaries statt Code-Lesen:** Jeder Node im KG hat ein `summary` Feld. Diese Summaries geben einen schnellen Überblick über jede Datei/Funktion/Klasse -- ohne dass jede Datei nochmal gelesen werden muss.

2. **Complexity Ratings:** Der KG klassifiziert Nodes als `simple`, `moderate` oder `complex`. Das ist direkter Input für die HS-Dimension "Komplexitaet".

3. **Architektur-Layer:** Der KG hat Layer-Zuordnungen (z.B. "Frontend", "Backend", "Database", "Infrastructure"). Diese helfen bei der logischen Strukturierung der L0-Module.

4. **Edge-Analyse für Vernetzung:** Fan-in/Fan-out jedes Nodes zeigt, wie zentral eine Komponente ist. Hochvernetzte Nodes sind fast immer relevant (hoher HS).

5. **Tour-Daten als Lernpfad-Hinweis:** Die Tour aus dem KG zeigt bereits eine sinnvolle Reihenfolge für das Kennenlernen der Codebase. Das kann die Modul-Reihenfolge auf L0 informieren.

### Phase B2: KG-GESTUETZTES CURRICULUM

**Das HS-Scoring im Kombiniert-Modus nutzt KG-Daten für objektivere Bewertungen:**

| HS-Dimension | Datenquelle im reinen Kurs-Modus | Datenquelle im Kombiniert-Modus |
|---|---|---|
| **Komplexitaet** | Heuristik basierend auf Code-Laenge und Verschachtelung | KG `complexity` Rating (`simple`=0, `moderate`=1, `complex`=3) |
| **Relevanz** | Einschaetzung basierend auf README und Imports | KG Fan-in Count (>5 Imports = Relevanz 3) |
| **Lernwert** | Einschaetzung basierend auf Code-Kommentaren | KG Layer-Zuordnung (Core-Layer = Lernwert +1) |
| **Eigenstaendigkeit** | Einschaetzung basierend auf Datei-Größe | KG Edge-Count (viele ausgehende Edges = eigenstaendig) |

**Layer-basierte L0-Modul-Strukturierung:**

Im Kombiniert-Modus können die KG-Layer direkt in die L0-Modul-Struktur einfliessen:

```
KG-Layer "Frontend"       -> L0-Modul "Die Benutzeroberflaeche"
KG-Layer "API"            -> L0-Modul "Kommunikation zwischen Frontend und Backend"
KG-Layer "Business Logic" -> L0-Modul "Die Kern-Logik"
KG-Layer "Database"       -> L0-Modul "Datenhaltung"
KG-Layer "Infrastructure" -> L0-Modul "Deployment & Betrieb"
```

**Tour-gestuetzte Lernpfad-Optimierung:**

Die Tour aus dem KG schlägt bereits eine sinnvolle Reihenfolge vor. Im Kombiniert-Modus kann diese Reihenfolge die Modul-Reihenfolge auf L0 und die Themen-Reihenfolge auf L1 beeinflussen:

```
KG Tour Step 1: "Project Overview" (README)
  -> L0 Modul 1: "Was ist [Projektname]?"
KG Tour Step 2: "Entry Point" (main.ts)
  -> L0 Modul 2: "Die App startet -- was passiert?"
KG Tour Step 3: "Core Components" (src/components/)
  -> L0 Modul 3: "Die Hauptakteure"
```

---

## Inhalts-Regeln (alle Level)

| Regel | L0 | L1 | L2 | L3 |
|-------|----|----|----|----|
| **Visuell** | >=50% pro Screen | >=50% | >=40% | >=30% (mehr Text OK bei Code) |
| **Max Sätze** | 2-3 | 3-4 | 4-5 | 5-7 (Tiefenerklärungen erlaubt) |
| **Code original** | Snippets 3-5 Zeilen | Snippets 5-15 Zeilen | Vollstaendige Funktionen | Ganze Dateien mit Annotations |
| **Metaphern** | Je 1 pro Modul, einzigartig | Darf L0-Metapher vertiefen | Kann technischer werden | Keine noetig, Klartext |
| **1 Konzept/Screen** | Ja | Ja | Ja, aber breiter | Ja, aber tiefer |
| **Quiz** | Anwendung | Verständnis | Analyse | Synthese/Debugging |

### Zielgruppen-spezifische Regeln (gelten auf ALLEN Levels)

| | Anwender | Entwickler | Entscheider |
|---|---|---|---|
| **Tonalitaet** | Freundlich ("Probier mal...") | Sachlich ("Das System...") | Kompakt ("Das bedeutet...") |
| **Code** | Minimal | Kern-Element | Nie |
| **Jargon** | Null ohne Tooltip | Tech-Jargon OK | Business-Jargon OK |
| **Workflows** | Hauptelement | Sekundaer | Vereinfacht |
| **Architektur** | 3-4 Boxen | Detailliert | Vereinfacht, business-nah |
| **KPIs** | Nein | Selten | Hauptelement |

---

## Modul-Templates

### Hero (L0 -- identisch zur Basisversion)

```html
<section class="module module-hero" id="module-0">
  <div class="module-content" style="text-align:center">
    <h1 style="color:#FFFFFF">Kurstitel</h1>
    <p style="color:rgba(255,255,255,.85)">Perspektivabhängiger Untertitel</p>
    <div style="margin-top:var(--space-6);display:flex;gap:var(--space-3);justify-content:center;flex-wrap:wrap">
      <span class="level-badge">Das Wichtigste auf einen Blick</span>
      <span class="level-badge-count">+ X Vertiefungsseiten verfügbar</span>
    </div>
  </div>
</section>
```

```css
.level-badge {
  font-family: var(--font-mono);
  font-size: var(--text-xs);
  padding: var(--space-1) var(--space-4);
  border-radius: var(--radius-full);
  background: rgba(254,143,17,.2);
  color: var(--color-impulse-orange);
  font-weight: 600;
}
.level-badge-count {
  font-family: var(--font-body);
  font-size: var(--text-sm);
  color: rgba(255,255,255,.85);
  display: flex;
  align-items: center;
}
```

### Hero (L1-L3) -- KRITISCH: Nicht leer lassen!

**REGEL:** Der Hero auf L1-L3-Seiten darf NICHT nur Titel + Zurück-Link zeigen. Er MUSS auch eine **Page-Overview** enthalten, die dem User sofort zeigt, welche Abschnitte auf dieser Seite kommen. Ohne Page-Overview wirkt der obere Seitenbereich leer und orientierungslos.

```html
<section class="module module-hero" id="module-0">
  <div class="module-content" style="text-align:center">
    <div class="level-indicator" style="justify-content:center">
      <!-- Dots je nach Level:
           L1: done, active, empty, empty
           L2: done, done, active, empty
           L3: done, done, done, active -->
    </div>
    <a href="../index_dev_de.html" class="back-button" style="color:rgba(255,255,255,.85);border-color:rgba(255,255,255,.2);background:rgba(255,255,255,.05)">
      <svg width="16" height="16" viewBox="0 0 16 16" fill="currentColor"><path d="M7.78 12.53a.75.75 0 01-1.06 0L2.47 8.28a.75.75 0 010-1.06l4.25-4.25a.75.75 0 011.06 1.06L4.81 7h7.44a.75.75 0 010 1.5H4.81l2.97 2.97a.75.75 0 010 1.06z"/></svg>
      <span>Zurück zum Überblick</span>
    </a>
    <h1 style="color:#FFFFFF;margin-top:var(--space-4)">Thementitel</h1>
    <p style="color:rgba(255,255,255,.85)">Kontextbeschreibung</p>

    <!-- === PAGE-OVERVIEW (PFLICHT auf L1-L3!) === -->
    <div class="page-overview">
      <div class="page-overview-title">Auf dieser Seite:</div>
      <div class="page-overview-items">
        <a href="#module-1" class="page-overview-item">
          <span class="page-overview-num">01</span>
          <span class="page-overview-text">Abschnitt-Titel</span>
        </a>
        <a href="#module-2" class="page-overview-item">
          <span class="page-overview-num">02</span>
          <span class="page-overview-text">Abschnitt-Titel</span>
        </a>
        <!-- ... für jeden Abschnitt der Seite -->
      </div>
    </div>
  </div>
</section>
```

**CSS für Page-Overview:**

```css
.page-overview {
  margin-top: var(--space-8);
  text-align: left;
  max-width: 600px;
  margin-left: auto;
  margin-right: auto;
}
.page-overview-title {
  font-family: var(--font-mono);
  font-size: var(--text-xs);
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: rgba(255,255,255,.85);
  margin-bottom: var(--space-4);
}
.page-overview-items {
  display: flex;
  flex-direction: column;
  gap: var(--space-2);
}
.page-overview-item {
  display: flex;
  align-items: center;
  gap: var(--space-3);
  padding: var(--space-2) var(--space-4);
  border-radius: var(--radius-sm);
  border: 1px solid rgba(255,255,255,.12);
  background: rgba(255,255,255,.05);
  color: rgba(255,255,255,.8);
  text-decoration: none;
  font-family: var(--font-body);
  font-size: var(--text-sm);
  transition: all var(--duration-fast);
}
.page-overview-item:hover {
  background: rgba(254,143,17,.15);
  border-color: var(--color-impulse-orange);
  color: #FFFFFF;
}
.page-overview-num {
  font-family: var(--font-mono);
  font-size: var(--text-xs);
  font-weight: 700;
  color: var(--color-impulse-orange);
  min-width: 24px;
}
.page-overview-text {
  font-weight: 500;
}
```

### Inhalts-Module auf L1-L3 (PFLICHT: Modulnummern!)

**KRITISCH:** L1-L3-Seiten verwenden die IDENTISCHE Modul-Struktur wie L0. Jede Sektion MUSS eine grosse, gefadete Modulnummer haben. KEINE nackten `<section>`-Tags ohne Modulnummer-Pattern!

```html
<!-- RICHTIG -- L1/L2/L3 Inhalts-Modul: -->
<section class="module" id="module-1" style="background:var(--color-bg)">
  <div class="module-content">
    <header class="module-header animate-in">
      <span class="module-number" style="color:var(--color-deep-blue);opacity:.15">01</span>
      <h1 class="module-title">Abschnitt-Titel</h1>
    </header>
    <div class="module-body">
      <section class="screen animate-in">
        <!-- Inhalt: Text + Visualisierung -->
      </section>
      <!-- Optional: Deep-Dive-Link auf nächstes Level -->
    </div>
  </div>
</section>

<!-- FALSCH -- Nackte Sektion ohne Modulnummer: -->
<section id="thema">
  <div class="section-inner">
    <h2>Thema</h2>
    <!-- Keine Modulnummer! Wirkt leer und strukturlos -->
  </div>
</section>
```

**Haeufige Fehler bei L1-L3 Modul-Struktur:**

| Fehler | Problem | Loesung |
|--------|---------|--------|
| Nackte `<section>` ohne Modulnummer | Wirkt leer, keine visuelle Verankerung | IMMER `.module-number` mit grosser, gefadeter Zahl |
| Hero ohne Page-Overview | Oberer Seitenbereich wirkt leer | IMMER `.page-overview` mit Abschnittsliste im Hero |
| Sections ohne `min-height` | Content kann zu kurz sein, Scroll-Snap fuehlt sich kaputt an | `min-height: 100dvh` auf ALLEN Modulen (auch L1-L3) |
| CSS-Klassen weichen von L0 ab | Inkonsistentes Design | IDENTISCHE Klassen: `.module`, `.module-content`, `.module-header`, `.module-number`, `.module-title`, `.module-body`, `.screen` |
| Kein alternierender Hintergrund | Monotone Seite | Gerade Module: `--color-bg`. Ungerade: `--color-bg-warm` |

### Typografie-Zuordnung (alle Level)

| Element | Stil |
|---------|------|
| Modulnummern | --text-6xl, font-display, weight 800, Tiefenblau 15% Opacity |
| Modultitel | --text-4xl, font-display, weight 700 |
| Screen-Headings | --text-2xl, font-display, weight 600 |
| Fliesstext | --text-base/lg, font-body, --leading-normal |
| Code | --text-sm, font-mono, auf #000066 |
| Labels/Badges | --text-xs, font-mono, uppercase |
| Breadcrumbs | --text-sm, font-body |
| Level-Badges | --text-xs, font-mono, uppercase |

---

## Integrationsmodus (Standalone/Eingebettet) -- Auswirkung auf ALLE Level

**Standalone-Modus:**
- Alle Dateien funktionieren offline (relative Links)
- Kein Footer, keine externen Links
- Ideal zum Zippen und Teilen

**Eingebettet-Modus:**
- Header-Links (GitHub, Home, etc.) auf ALLEN Level-Seiten identisch
- Footer auf ALLEN Level-Seiten identisch
- Links oeffnen in `target="_blank"` mit `rel="noopener"`

**Nav-Links für Eingebettet (auf L1-L3):**

```html
<nav class="nav-deep">
  <nav class="breadcrumb"><!-- ... --></nav>
  <div class="nav-links">
    <a href="https://github.com/..." class="nav-link" target="_blank" rel="noopener">
      <svg class="nav-link-icon" viewBox="0 0 16 16" width="14" height="14" fill="currentColor">
        <path d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"/>
      </svg>
    </a>
  </div>
  <a href="authentication_dev_en.html" class="nav-lang" title="English version">EN</a>
</nav>
```

---

## Farb-Schnellreferenz

```
PRIMAER:    #000099  Tiefenblau      -- Vertrauen, Autoritaet, Hintergründe
AKZENT:     #FE8F11  Impuls-Orange   -- Energie, CTAs, Deep-Dive-Links, Fortschritt
WARM:       #E4DAD4  Warmgrau        -- Borders, Alternation, Ruhe

SEKUNDAER:  #84C041  Grün           -- Erfolg, Positiv
            #CC0000  Rot             -- Fehler, Negativ
            #1195EB  Hellblau        -- Info, Links
            #5BE3D6  Tuerkis         -- Tertiaer, Diagramme
            #FDC83A  Gelb            -- Warnung
            #E2C39A  Beige           -- Dezent

CODE-BG:    #000066  Tiefes Dunkelblau
TEXT:        #1A1A2E  Fast-Schwarz (Blau-Unterton)

LEVEL-SPEZIFISCH:
  L-Dot done:    #FE8F11 (Impuls-Orange)
  L-Dot active:  #000099 (Tiefenblau)
  Deep-Dive-BG:  #F8F5F2 (Surface-Warm)
  Breadcrumb-Badge: #FFF3E5 BG + #FE8F11 Text
```

---

## Zusaetzliche Verstehen-Befehle (nach Knowledge Graph Erstellung)

Sobald ein Knowledge Graph existiert (`knowledge-graph.json`), stehen folgende Zusatz-Befehle zur Verfuegung:

### `/understand-dashboard`
Startet das interaktive React Dashboard zur Visualisierung des Knowledge Graphs. Zeigt Nodes, Edges, Layer und Tour in einer graph-basierten Ansicht. Dark Luxury Theme mit DM Serif Display Typografie und Gold/Amber Akzenten.

### `/understand-explain <file>`
Tiefgehende Erklärung einer spezifischen Datei, Funktion oder eines Moduls. Nutzt den Knowledge Graph um Kontext, Abhängigkeiten und Auswirkungen zu zeigen. Liest die tatsaechliche Datei und korreliert mit KG-Nodes.

### `/understand-diff`
Analysiert die aktuellen Code-Änderungen (git diff) gegen den Knowledge Graph. Zeigt:
- Welche KG-Nodes betroffen sind
- Welche Abhängigkeiten sich ändern koennten
- Risikobewertung der Änderungen
- Welche Tests möglicherweise betroffen sind

### `/understand-onboard`
Generiert einen umfassenden Onboarding-Guide für neue Teammitglieder basierend auf dem Knowledge Graph. Beinhaltet Architektur-Überblick, wichtigste Dateien, Lernpfad und haeufige Aufgaben.

### `/understand-domain`
Extrahiert Business-Domain-Wissen aus der Codebase. Identifiziert Business-Domains, Geschaeftsprozesse und Process-Steps. Erzeugt einen interaktiven horizontalen Flow-Graphen im Dashboard. Funktioniert standalone (leichtgewichtiger Scan) oder leitet aus einem existierenden Knowledge Graph ab.

### `/understand-chat`
Interaktive Q&A-Session über die Codebase. Beantwortet Fragen wie "Wie funktioniert die Authentifizierung?", "Welche Dateien sind am komplexesten?", "Was haengt von der Datenbank ab?" basierend auf dem Knowledge Graph.

---

## Zusammenfassung -- Was der Skill erzeugt

### Kurs-Modus Output

```
Input:  1 Codebase + Zielgruppen + Integrationsmodus
Output: Verlinktes HTML-Datei-Set (bedarfsgerechte Tiefe pro Zielgruppe)

Jede Zielgruppe durchläuft eine EIGENE Pipeline mit EIGENEM Tiefenprofil:

Entscheider-Pipeline (Max: L1):
  L0: 2 Dateien (DE + EN)
  L1: 4-8 Dateien (2-4 Themen x 2 Sprachen, nur HS>=8)
  = ~6-10 Dateien

Anwender-Pipeline (Max: L2):
  L0: 2 Dateien (DE + EN)
  L1: 6-10 Dateien (3-5 Themen x 2 Sprachen, nur HS>=7)
  L2: 2-8 Dateien (1-4 Sub-Themen x 2 Sprachen, nur HS>=9)
  = ~10-20 Dateien

Entwickler-Pipeline (Max: L3):
  L0: 2 Dateien (DE + EN)
  L1: 8-12 Dateien (4-6 Themen x 2 Sprachen, HS>=6)
  L2: 6-16 Dateien (3-8 Sub-Themen x 2 Sprachen, HS>=8)
  L3: 4-10 Dateien (2-5 Details x 2 Sprachen, HS>=8)
  = ~20-40 Dateien

+ 1x Tiefenkarte (Markdown-Report mit Pipeline-Zusammenfassungen und HS-Entscheidungen)

Typischer Output für 3 Zielgruppen (Entscheider + Anwender + Entwickler):
  Entscheider: ~8 Dateien    (fertig nach 2 Pipeline-Zyklen)
  Anwender: ~15 Dateien      (fertig nach 3 Pipeline-Zyklen)
  Entwickler: ~30 Dateien    (fertig nach 4 Pipeline-Zyklen)
  = ~53 Dateien total (statt ~100+ bei pauschalem L0-L3 für alle)
  = ~45% weniger Dateien durch bedarfsgerechte Tiefe

Parallelisierung: Alle 3 Pipelines laufen gleichzeitig.
Entscheider ist fertig während Entwickler noch bei L2 ist.
```

### Verstehen-Modus Output

```
Input:  1 Codebase (git repository)
Output: .claude-learning/knowledge-graph.json + Interactive Dashboard

Knowledge Graph enthält:
  - Nodes: Dateien, Funktionen, Klassen, Configs, Docs, Services, etc. (13 Node-Typen)
  - Edges: Imports, Calls, Contains, Deploys, etc. (26 Edge-Typen)
  - Layers: Architektonische Schichten (Frontend, Backend, Database, etc.)
  - Tour: Gefuehrter Lernpfad durch die Codebase
  - Project Metadata: Name, Beschreibung, Sprachen, Frameworks, Analyse-Zeitpunkt
```

### Kombiniert-Modus Output

```
Input:  1 Codebase + Zielgruppen + Integrationsmodus
Output: BEIDES -- Knowledge Graph + HTML-Kurs-Dateien

Phase A: Knowledge Graph (wie Verstehen-Modus)
  -> .claude-learning/knowledge-graph.json
  -> Interactive Dashboard

Phase B: HTML-Kurse (wie Kurs-Modus, aber KG-gestuetzt)
  -> Verlinktes HTML-Datei-Set
  -> Besseres HS-Scoring durch KG-Metriken
  -> Logischere Modul-Struktur durch Layer-Daten
  -> Optimierter Lernpfad durch Tour-Daten
```

---

## Error Handling

### Verstehen-Modus (Subagent Errors)

- If any subagent dispatch fails, retry **once** with the same prompt plus additional context about the failure.
- Track all warnings and errors from each phase in a `$PHASE_WARNINGS` list. When using `--review`, pass this list to the graph-reviewer in Phase 6. On the default path, include accumulated warnings in the Phase 7 final report.
- If it fails a second time, skip that phase and continue with partial results.
- ALWAYS save partial results -- a partial graph is better than no graph.
- Report any skipped phases or errors in the final summary so the user knows what happened.
- NEVER silently drop errors. Every failure must be visible in the final report.

### Kurs-Modus (Datei-Erzeugung Errors)

- **Datei-Erzeugung schlägt fehl:** NUR diese Datei neu generieren.
- **Cross-ZG-Links:** Werden erst in Phase 5 gesetzt -- funktioniert unabhängig von der Erzeugungsreihenfolge.
- **Bei Problemen:** Auf rein sequenziellen Modus zurückfallen (1 Datei nach der anderen, kein Agent-Tool).

### Kombiniert-Modus

- Wenn Phase A (KG) fehlschlägt: Dem User melden und fragen ob Phase B (Kurs) trotzdem ohne KG-Daten laufen soll (dann wie reiner Kurs-Modus).
- Wenn Phase A erfolgreich aber Phase B fehlschlägt: KG + Dashboard sind trotzdem verfügbar. Nur der Kurs fehlt.
- Partial KG-Daten können trotzdem für HS-Scoring genutzt werden -- besser als gar keine KG-Daten.
