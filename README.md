# edge-stack

A **deliberately rotten** Docker Compose stack of a sandbox organisation: old images, `latest` tags, a privileged container, no health checks, no limits.
It exists to test an orchestrator of coding agents on infrastructure code (a version written in a compose file, a deployment, a verification).
See [SCENARIOS.md](SCENARIOS.md). Never reuse anything from it.

```bash
docker compose config -q
docker compose up -d       # http://localhost:8080/
```

## Upgrade note: postgres 9.6 -> 17

PostgreSQL data directories are not compatible across major versions. A `db-data` volume created by `postgres:9.6` will make `postgres:17` fail at startup ("database files are incompatible with server"). Dump the old data (`pg_dumpall`) before the upgrade and restore it into a fresh volume, or migrate with `pg_upgrade`. A fresh volume starts fine (verified with `postgres:17`, 17.12).
