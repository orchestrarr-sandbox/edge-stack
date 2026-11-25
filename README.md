# edge-stack

A **deliberately rotten** Docker Compose stack of a sandbox organisation: old images, `latest` tags, a privileged container, no health checks, no limits.
It exists to test an orchestrator of coding agents on infrastructure code (a version written in a compose file, a deployment, a verification).
See [SCENARIOS.md](SCENARIOS.md). Never reuse anything from it.

```bash
docker compose config -q
docker compose up -d       # http://localhost:8080/
```

## Redis 4.0 -> 8.0 upgrade notes

`cache` now uses `redis:8.0` (tested: 8.0.6). Smoke test with `docker run` (PING, SET/GET) passed; no connection or protocol errors.

- No auth is configured in the compose file, and none is required by default. Redis 6+ added ACLs, but the `default` user still has open access, so unauthenticated clients keep working.
- RESP2 remains the default protocol; clients that don't send `HELLO 3` behave as before.
- The data directory is not mounted, so no RDB/AOF format migration is needed. If a volume is added later, back up the old 4.0 dump first.
- Redis 8 warns at startup that `vm.overcommit_memory` is not 1 (a host setting, harmless for this stack).
- Redis 8 is also published under a new license (RSALv2/SSPLv1/AGPLv3). Check this is acceptable for your organisation.
- Not tested: `docker compose up` for the full stack (the compose plugin is not installed here), and real application clients (none are in this repo).
