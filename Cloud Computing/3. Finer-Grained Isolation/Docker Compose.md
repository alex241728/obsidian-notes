---
tags:
  - docker-compose
---

A tool for defining and running **multi-container applications**
- Uses a `compose.yaml` file to define the applica
- **Services**: Application components such as api, db, and redis
- **Networks**: Connect services
- **Volumes**: Persist data
- Lets you start, stop, and manage multiple services together

# Why Docker Compose?
- **Best practice**: One container per responsibility (independent lifecycle, easier updates and maintenance, flexible scaling).
- Managing multiple containers manually with `docker run` becomes complex and error-prone.
- Compose defines the application in one `compose.yaml` file and manages services together.

---

# Key Concepts in `compose.yaml`
- **Services**: Define application components that run in containers.
  - `build: .`: Build custom image using Dockerfile in current directory.
  - `image: <image-name>`: Use pre-built image (e.g., `postgres:18`).
  - `ports`: Map host ports to container ports (`host:container`).
    - Only publish ports needed by something outside the network (e.g., host access to `api` at `3000:3000`).
    - Internal services (e.g., `db` on 5432) do not need published ports.
  - `depends_on`: Express dependency order (e.g., start `db` before `api`).
- **Networks**: Virtual bridge network created on the Docker host.
  - Containers on the same Compose network communicate using service name as hostname (e.g., `host: "db"`).
  - Custom bridge network defined under `networks:` with `driver: bridge`.
- **Volumes**: Docker-managed storage independent of container lifecycle.
  - Persists data when containers are deleted and recreated.
  - Declared under top-level `volumes:` and mounted in service (e.g., `db-data:/var/lib/postgresql`).

## Commands
- **Start and build services**: `docker compose up --build -d`
  - `--build`: Build images before starting containers
  - `-d`: Detached mode (run in background)
- **Stop services**: `docker compose down` (data in volumes persists)
- **Stop and remove volumes**: `docker compose down -v`
