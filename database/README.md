Database image helper

Build (from repo root):

```
docker build -f database/Dockerfile -t keda-postgres:local .
```

Run locally (example):

```
docker run --rm -p 5432:5432 -e POSTGRES_DB=jobqueue -e POSTGRES_USER=jobuser -e POSTGRES_PASSWORD=jobpass123 keda-postgres:local
```

Notes:
- The repository `init.sql` is copied into `/docker-entrypoint-initdb.d/` so Postgres will automatically run it when initializing an empty database volume.
- The existing Kubernetes `database/statefulset.yml` mounts the same SQL via a `ConfigMap`; building this image is optional if you prefer the ConfigMap approach.
