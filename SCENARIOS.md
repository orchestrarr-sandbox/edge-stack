# Scenarios

| # | What is wrong | Where | A good fix |
|---|---|---|---|
| E1 | **End-of-life images**: `nginx:1.14`, `redis:4.0` (the unused `postgres` service was removed, see E7) | `docker-compose.yml` | Maintained tags, one at a time; `docker compose config` still valid; a major database version is **not** bumped blindly (data) |
| E2 | **`latest` tag** on `http-echo` | `docker-compose.yml` | A pinned version |
| E3 | **A privileged container** that needs no privilege | `docker-compose.yml` | Remove `privileged` |
| E4 | **No health checks, no restart policy, no limits** | `docker-compose.yml` | Health checks and `restart`, sensible limits |
| E5 | **A password in the file** (a placeholder, not a secret) and the cache published on the host | `docker-compose.yml` | An environment variable with no default, the cache not published |
| E6 | **A CI that only checks the syntax** | `.github/workflows/ci.yml` | Also start the stack and wait for it to answer |
| E7 | **Unused PostgreSQL container** (CVE-2026-41877, no fixed version): no service, config or code connects to it | `docker-compose.yml` | Remove the `db` service and its `db-data` volume; verified by searching for `db`, `5432`, `postgres`, `DATABASE` and `depends_on` |
