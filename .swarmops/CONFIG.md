# ⚙️ SwarmOps Konfiguration

> Systemweite Einstellungen für das Multi-Agent-Koordinationssystem.

---

## Task-Einstellungen

| Setting                  | Wert       | Beschreibung                                    |
|--------------------------|------------|------------------------------------------------|
| `max_concurrent_workers` | `5`        | Maximale Anzahl gleichzeitiger Worker-Agents    |
| `require_review`         | `false`    | Müssen Tasks reviewed werden vor `done`?        |
| `auto_number_tasks`      | `true`     | Planner nummeriert Tasks automatisch            |
| `task_size_limit`        | `L`        | Maximale Task-Größe (S/M/L/XL)                 |

---

## Prioritäts-Regeln

| Priorität    | Beschreibung                              | Claim-Reihenfolge |
|-------------|-------------------------------------------|-------------------|
| 🔴 HIGH     | Blocker, kritische Bugs, Kern-Features    | Zuerst            |
| 🟡 MEDIUM   | Wichtige Features, Verbesserungen         | Danach            |
| 🟢 LOW      | Nice-to-have, Refactoring, Doku           | Zuletzt           |

---

## Task-Größen (Richtwerte)

| Größe | Beschreibung                                | Geschätzte Dauer |
|-------|---------------------------------------------|-----------------|
| S     | Einzelne Funktion, kleiner Fix              | < 10 Min        |
| M     | Feature-Teil, mehrere Funktionen            | 10–30 Min       |
| L     | Ganzes Feature, mehrere Dateien             | 30–60 Min       |
| XL    | Komplexes Feature, Architektur-Änderung     | > 60 Min        |

> **Regel**: Tasks größer als das `task_size_limit` sollten vom Planner aufgeteilt werden.

---

## Dependency-Regeln

- Ein Task mit `Depends-On: TASK-XXX` darf erst geclaimed werden, wenn `TASK-XXX` in `done/` liegt
- Zirkuläre Dependencies sind verboten
- Der Planner muss Dependencies beim Erstellen auf Korrektheit prüfen

---

## Review-Einstellungen

*Nur relevant wenn `require_review = true`*

| Setting            | Wert       | Beschreibung                               |
|--------------------|------------|-------------------------------------------|
| `reviewer`         | `planner`  | Wer reviewed? (`planner` / `human`)       |
| `review_checklist` | siehe unten | Was wird beim Review geprüft?             |

### Review-Checkliste

- [ ] Alle Akzeptanzkriterien erfüllt
- [ ] Code folgt den Coding-Standards aus MOTD.md
- [ ] Keine unbeabsichtigten Seiteneffekte
- [ ] Progress Log ist vollständig

---

## Agent-Identifikation

Jeder Agent identifiziert sich mit einer eindeutigen ID im Format:

- **Planner**: `PLANNER-1`
- **Worker**: `WORKER-1`, `WORKER-2`, `WORKER-3`, ...

Diese ID wird im Progress Log und im `Claimed-By` Feld verwendet.

---

*Letzte Aktualisierung: <!-- Datum & Uhrzeit -->*
