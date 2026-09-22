# Recherche: Codex Action statt eigener Runner-Logik

## Ergebnis

Es gibt eine offizielle OpenAI GitHub Action: [`openai/codex-action`](https://github.com/openai/codex-action).

Sie installiert die Codex CLI, startet bei Verwendung eines API-Keys den Responses-API-Proxy und führt `codex exec` mit kontrollierten Berechtigungen aus. Sie ist **kein GitLab Runner**; sie läuft als GitHub-Action-Job auf einem GitHub-hosted Runner.

Die zuvor vorbereitete GitLab-Variante war daher unnötig komplex. Für den gewünschten GitHub-Issue-Workflow ist die offizielle Action die passendere Lösung.

## Aktuelle Architektur

1. GitHub Issue wird erstellt oder erhält das Label `ai:implement`.
2. Der Workflow akzeptiert ausschließlich Issues von `MrNightHeart`.
3. `openai/codex-action` läuft mit `permission-profile: ":workspace"` und `safety-strategy: drop-sudo`.
4. Die Änderungen werden in einen Branch gepusht und als Pull Request nach `main` eröffnet.
5. `main` wird nicht direkt verändert.

Die Action prüft zusätzlich standardmäßig, ob der auslösende Benutzer Schreibzugriff auf das Repository besitzt. Das ersetzt nicht die explizite Autor-/Label-Prüfung im Workflow.

## Sicherheit

- `OPENAI_API_KEY` wird als GitHub-Repository-Secret gespeichert.
- Die Action ist im Workflow auf einen vollständigen Commit-SHA gepinnt; der lesbare Versionshinweis ist nur Dokumentation.
- Der Key wird nur im Codex-Schritt verwendet.
- `drop-sudo` und das Workspace-Berechtigungsprofil reduzieren den Zugriff des Agenten.
- Issue-Texte bleiben eine Prompt-Injection-Grenze; sie dürfen keine Workflow-Sicherheitsregeln überschreiben.
- Pull Requests werden nicht automatisch gemergt.
- Für produktive Nutzung sollten `main`-Branch-Schutz, erforderliche Checks und eine manuelle Review aktiviert sein.
