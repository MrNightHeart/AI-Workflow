# Codex-Agent: GitHub Issue → Pull Request

## Ablauf

1. Ein Issue wird erstellt oder erhält das Label `ai:implement`.
2. Der GitHub-Workflow akzeptiert es nur, wenn:
   - der Autor exakt `MrNightHeart` ist;
   - das Label `ai:implement` vorhanden ist.
3. GitHub Actions startet die offizielle `openai/codex-action`.
4. Codex analysiert das Repository, implementiert die Aufgabe und führt relevante Tests aus.
5. GitHub Actions erstellt einen separaten Branch und eröffnet einen Pull Request nach `main`.
6. Es gibt keinen direkten Push nach `main` und keinen automatischen Merge.

## Einmalige GitHub-Konfiguration

In **Repository → Settings → Secrets and variables → Actions** als Repository-Secret anlegen:

- `OPENAI_API_KEY`: OpenAI API-Key; niemals ins Repository schreiben.

Der Secret wird nur an den Codex-Schritt übergeben. Die offizielle Action verwendet den Key für den Responses-API-Proxy.

## Auslösen

Ein Issue als `MrNightHeart` erstellen und anschließend das Label `ai:implement` hinzufügen. Das Label ist die bewusste Freigabe. Andere Issue-Autoren lösen keine Agent-Ausführung aus.

## Sicherheitsmaßnahmen

- `main` in GitHub schützen: Pull Request erforderlich, Statuschecks erforderlich, keine direkten Pushes.
- GitHub Actions auf die benötigten Berechtigungen beschränken.
- Die Codex Action auf einen vollständigen Commit-SHA pinnen.
- `permission-profile: ":workspace"` und `safety-strategy: drop-sudo` verwenden.
- Issue-Texte als nicht vertrauenswürdige Eingaben behandeln; sie dürfen keine Sicherheitsregeln überschreiben.
- Bei öffentlich erlaubten Issues niemals `pull_request_target` verwenden, um untrusted Inhalte mit Secrets auszuführen.
- OpenAI-API-Key regelmäßig rotieren und niemals in Logs, Commits oder Issue-Texte schreiben.
- Generierte Pull Requests immer prüfen, bevor sie gemergt werden.
