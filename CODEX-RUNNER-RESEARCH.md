# Recherche: offizieller Codex Runner

## Ergebnis

Für diesen Anwendungsfall gibt es derzeit keinen offiziellen OpenAI- oder Codex-Runner als GitLab-CI-Integration, den man anstelle der Pipeline-Logik einfach konfigurieren könnte.

Das offizielle Repository [`openai/codex`](https://github.com/openai/codex) stellt den **Codex CLI** bereit. Er läuft lokal oder in einer CI-Umgebung und kann dort über `codex exec` nicht-interaktiv aufgerufen werden. Das ist kein eigener GitLab Runner und keine GitLab-Integration.

Die Begriffe sind daher zu unterscheiden:

- **GitLab Runner**: führt Jobs aus; wird von GitLab bereitgestellt.
- **Codex CLI**: Coding-Agent, der innerhalb eines Jobs ausgeführt wird.
- **Codex Web/Cloud**: gehosteter OpenAI-Dienst; nicht dasselbe wie ein selbst betriebener GitLab-Runner.

## Konsequenz für dieses Repository

Die aktuelle Lösung verwendet bereits die kleinste sinnvolle Architektur:

1. GitHub Actions autorisiert das Issue und triggert GitLab.
2. Der vorhandene GitLab Runner startet die Codex CLI.
3. Die CLI bearbeitet das Issue im Checkout.
4. Der Job erstellt Branch und Pull Request.

Ein vermeintliches `codex-runner`-Paket würde aktuell keine offizielle, belastbare Vereinfachung darstellen. Drittanbieter-Templates oder Community-Repositories sollten nicht automatisch mit Zugriff auf `OPENAI_API_KEY` und Schreibrechten im Repository verwendet werden.

## Sicherheitsentscheidung

Der Agent bleibt absichtlich als normaler CI-Schritt modelliert. Dadurch sind Timeout, geschützter Runner, geschützte Variablen, `resource_group`, Netzwerkzugriff und GitHub-Token-Rechte explizit kontrollierbar. Das ist für einen produktiven ersten Aufbau transparenter als eine inoffizielle Wrapper-Action.

Wenn OpenAI künftig eine offizielle GitLab-CI-Integration veröffentlicht, kann der Job-Installations- und Aufrufteil gezielt ersetzt werden; die Issue-Autorisierung und PR-Gates sollten trotzdem im eigenen Repository bleiben.
