# Codex-Agent einrichten

Die vollständige Einrichtung steht in [`CODEX-AGENT.md`](CODEX-AGENT.md).

## Architektur

Der Agent läuft vollständig in **GitHub Actions** mit der offiziellen [`openai/codex-action`](https://github.com/openai/codex-action). Einen separaten externen Runner oder eine zusätzliche CI-Plattform benötigt dieser Workflow nicht.

Kurzfassung:

- GitHub Actions autorisiert ausschließlich Issues von `MrNightHeart` mit Label `ai:implement`.
- Die offizielle Codex Action läuft in einem GitHub-hosted Runner.
- Codex implementiert die Aufgabe und erstellt anschließend einen Pull Request.
- `OPENAI_API_KEY` wird als GitHub Actions Repository-Secret gespeichert.
- `main` wird nicht direkt verändert; der Pull Request benötigt menschliche Prüfung.
