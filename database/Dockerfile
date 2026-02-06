# Custom Postgres image that includes DB init SQL
FROM postgres:15.4-alpine

# Copy the repository-level init.sql into the official init folder
# Build from repository root with: docker build -f database/Dockerfile -t keda-postgres:local .
COPY init.sql /docker-entrypoint-initdb.d/init.sql

# Ensure readable permissions and create `postgress` user/group
# We create the user but keep the image's default runtime user (`postgres`) to avoid
# breaking the official Postgres entrypoint. The init SQL is owned by `postgress`
# and world-readable so the entrypoint (running as `postgres`) can read it too.
USER root
RUN chmod 644 /docker-entrypoint-initdb.d/init.sql \
 && addgroup -S postgress || true \
 && adduser -S -G postgress postgress || true \
 && chown postgress:postgress /docker-entrypoint-initdb.d/init.sql

# restore default runtime user from base image
USER postgres
EXPOSE 5432


