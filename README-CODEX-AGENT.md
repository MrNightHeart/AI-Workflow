# Codex-Agent einrichten

Die vollständige Einrichtung steht in [`CODEX-AGENT.md`](CODEX-AGENT.md).

## Architektur

Es gibt derzeit keinen offiziellen OpenAI-Codex-GitLab-Runner. Der GitLab Runner führt deshalb die offizielle Codex CLI als nicht-interaktiven CI-Schritt aus. Die Recherche und Abgrenzung steht in [`CODEX-RUNNER-RESEARCH.md`](CODEX-RUNNER-RESEARCH.md).

Kurzfassung:

- GitHub Actions autorisiert ausschließlich Issues von `MrNightHeart` mit Label `ai:implement`.
- Actions triggert eine GitLab-Pipeline.
- Codex CLI läuft im GitLab Runner und eröffnet einen Pull Request.
- `OPENAI_API_KEY` wird als Secret in GitLab CI/CD gespeichert, nicht in GitHub.
