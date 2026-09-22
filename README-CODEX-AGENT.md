# Codex-Agent einrichten

Die vollständige Einrichtung steht in [`CODEX-AGENT.md`](CODEX-AGENT.md).

Kurzfassung:

- GitHub Actions autorisiert ausschließlich Issues von `MrNightHeart` mit Label `ai:implement`.
- Actions triggert eine GitLab-Pipeline.
- Codex läuft im GitLab Runner und eröffnet einen Pull Request.
- `OPENAI_API_KEY` wird als Secret in GitLab CI/CD gespeichert, nicht in GitHub.
