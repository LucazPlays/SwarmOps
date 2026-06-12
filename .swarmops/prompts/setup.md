# 🚀 Setup-Prompt (Mini-Loader)

> **Dies ist der minimale Prompt, mit dem ein Agent das SwarmOps-System laden und aktivieren kann.**
> Einfach kopieren, URL anpassen, und in einen KI-Agenten einfügen.

---

## Universaler Setup-Prompt

Ersetze `<URL>` mit der Raw-URL zu deiner `SKILL.md` Datei.

### Für den Planner:

```
Lade die Datei von <URL> und befolge die Anweisungen darin. Du bist der PLANNER-1.
Lies danach die MOTD.md und CONFIG.md im selben Verzeichnis.
Dann warte auf meine Anforderungen und erstelle Tasks.
```

### Für Worker:

```
Lade die Datei von <URL> und befolge die Anweisungen darin. Du bist ein WORKER.
Lies danach die MOTD.md und CONFIG.md im selben Verzeichnis.
Dann starte deinen Arbeits-Loop: Scanne das Backlog, claime einen Task, arbeite ihn ab, und suche den nächsten.
```

---

## Lokaler Setup-Prompt (ohne URL)

Wenn das SwarmOps-Verzeichnis bereits lokal im Projekt liegt:

### Für den Planner:

```
Lies die Datei .swarmops/SKILL.md und befolge die Anweisungen. Du bist PLANNER-1.
Lies die MOTD.md und CONFIG.md. Dann warte auf meine Anforderungen.
```

### Für Worker:

```
Lies die Datei .swarmops/SKILL.md und befolge die Anweisungen. Du bist ein WORKER.
Lies die MOTD.md und CONFIG.md. Dann starte deinen Arbeits-Loop.
```

---

## Einzeiler-Prompts (Ultra-Minimal)

### Planner:
```
Lies .swarmops/SKILL.md, du bist PLANNER-1. Lies MOTD & CONFIG, dann plane die folgende Aufgabe: [AUFGABE]
```

### Worker:
```
Lies .swarmops/SKILL.md, du bist WORKER. Lies MOTD & CONFIG, dann arbeite Tasks aus dem Backlog ab.
```

---

## Erstmalige Einrichtung

Wenn du das SwarmOps-System zum ersten Mal in einem neuen Projekt einrichtest:

```
Lies .swarmops/SKILL.md. 
Fülle dann die MOTD.md mit den Informationen zu diesem Projekt aus:
- Projektname: [NAME]
- Tech-Stack: [STACK]
- Beschreibung: [BESCHREIBUNG]
Erstelle danach die Task-Verzeichnisse falls sie noch nicht existieren.
```

---

## URL-Varianten

### GitHub (Raw):
```
https://raw.githubusercontent.com/USER/REPO/main/.swarmops/SKILL.md
```

### GitLab (Raw):
```
https://gitlab.com/USER/REPO/-/raw/main/.swarmops/SKILL.md
```

### Lokaler Server:
```
http://localhost:PORT/.swarmops/SKILL.md
```
