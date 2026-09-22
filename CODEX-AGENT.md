# Codex-Agent: GitHub Issue → GitLab Runner

## Ablauf

1. Ein Issue wird erstellt oder erhält das Label `ai:implement`.
2. Der GitHub-Workflow akzeptiert es nur, wenn:
   - der Autor exakt `MrNightHeart` ist;
   - das Label `ai:implement` vorhanden ist.
3. GitHub Actions triggert eine Pipeline in GitLab.
4. Der GitLab Runner lädt Issue und Repository, startet Codex und erstellt einen Branch.
5. Nach Tests wird ein Pull Request nach `main` eröffnet. Es gibt keinen direkten Push nach `main`.

## Einmalige GitHub-Konfiguration

In **Settings → Secrets and variables → Actions** als Repository-Secrets anlegen:

- `GITLAB_TRIGGER_TOKEN`: GitLab Pipeline trigger token; niemals ins Repository schreiben.
- `GITLAB_PROJECT_ID`: numerische GitLab-Projekt-ID.

Der OpenAI-Key gehört **nicht** in GitHub, weil der Agent im GitLab Runner läuft. Er wird als maskierte/protected CI/CD-Variable `OPENAI_API_KEY` in GitLab hinterlegt.

## Einmalige GitLab-Konfiguration

In **Settings → CI/CD → Variables** anlegen:

- `OPENAI_API_KEY`: OpenAI API-Key, masked und protected.
- `GITHUB_TOKEN`: fein beschränktes GitHub Fine-grained PAT oder besser GitHub-App-Token mit Zugriff nur auf dieses Repository und den benötigten Rechten für Clone, Branch-Push und Pull-Request-Erstellung; masked und protected.

Die Pipeline läuft von `main`. Deshalb sollten `main` und der verwendete GitLab-Runner geschützt sein. Bei einem öffentlichen Repository keinen ungeschützten/shared Runner mit weitreichenden Berechtigungen verwenden.

## Auslösen

Ein Issue als `MrNightHeart` erstellen und anschließend das Label `ai:implement` hinzufügen. Das Label ist die bewusste Freigabe. Andere Issue-Autoren lösen keine Pipeline aus.

## Sicherheitsmaßnahmen

- `main` in GitHub schützen: Pull Request erforderlich, Statuschecks erforderlich, keine direkten Pushes.
- GitHub-Repository möglichst privat halten, wenn der Code nicht öffentlich sein soll.
- GitLab-Variablen maskieren und schützen; Schlüssel regelmäßig rotieren.
- `resource_group` verhindert parallele Agent-Läufe im selben Projekt.
- Bei öffentlich erlaubten Issues niemals `pull_request_target` verwenden, um Issue-Text oder PR-Code mit Secrets auszuführen.
- Vor dem Merge immer Diff und CI-Ergebnis prüfen.
