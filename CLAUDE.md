# Semesterplaner – Hinweise für Claude Code

Planer für den Bachelor Wirtschaftsinformatik an der TU Darmstadt. Die ganze App steckt in **`Semesterplaner.html`**: Daten, Designsystem TUDa UI mit eingebetteten Schriften und die Logik in JavaScript. Sie lädt nichts aus dem Netz und speichert nur im `localStorage` (Schlüssel `winf-semesterplaner-*`).

## Aufbau

| Pfad | Inhalt |
|---|---|
| `Semesterplaner.html` | die App; Daten am Anfang des zweiten `<script>`-Blocks: `PLANS` (Prüfungspläne je Semester, `WS2026` = WiSe 2026/27), `MODULES`, `AREAS`, `CATALOG`, `DEFAULT_PLAN` |
| `docs/` | Projektseite mit Screenshots (GitHub Pages) |
| `.github/workflows/pages.yml` | veröffentlicht bei jedem Push auf `main`: Projektseite unter `/`, App unter `/app/`; bricht ab, wenn die App externe Dateien einbindet |
| `lizenzen/` | Lizenztexte der eingebetteten Schriften |

Planer-Assistent und Speicherung im Konto laufen nur, wenn dieselbe App als Claude-Artifact geöffnet wird; in der HTML-Datei bleiben sie ausgeblendet.

## Arbeiten an der App

- Die Datei ist rund 700 KB groß, einzelne Zeilen (Schriften, `PLANS`) haben über 100.000 Zeichen. Nicht ganz lesen: Stellen mit Grep suchen und gezielt ausschnittweise lesen.
- Größere Änderungen als Skript mit verankerten Ersetzungen bauen: Jede Ersetzung muss genau einmal greifen, sonst abbrechen.
- Testen: `python -m http.server 8000`, dann `http://localhost:8000/Semesterplaner.html`. Konsole ohne Fehler, Desktop- und Handybreite, helles und dunkles Design.
- Bewegung nur bei Interaktionen, keine Animationen beim Scrollen. Animationen dürfen nicht aus ihrem Scroll-Container ragen (Windows zeigt sonst kurz Scrollleisten).
- Texte in der App auf Deutsch, per du, kurz und konkret.

## Git und GitHub

- `main` ist live: Jeder Push auf `main` aktualisiert die öffentliche Seite. Änderungen auf einem Branch `claude/<thema>` machen und als Pull Request gegen `main` einreichen; vor jedem Push nachfragen.
- Commit-Nachrichten auf Deutsch: erste Zeile kurz und beschreibend, darunter bei Bedarf Stichpunkte.
- Keine exportierten Pläne (`semesterplan-*.json`) committen; sie enthalten den Studienstand.
- Zeilenenden im Repo sind LF (`.gitattributes`), Dateien UTF-8.
- GitHub-Aufgaben über die GitHub CLI `gh` (PRs, Issues, Läufe der Actions).
