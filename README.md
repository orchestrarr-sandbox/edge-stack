# edge-stack

A **deliberately rotten** Docker Compose stack of a sandbox organisation: old images, `latest` tags, a privileged container, no health checks, no limits.
It exists to test an orchestrator of coding agents on infrastructure code (a version written in a compose file, a deployment, a verification).
See [SCENARIOS.md](SCENARIOS.md). Never reuse anything from it.

```bash
docker compose config -q
docker compose up -d       # http://localhost:8080/
```
