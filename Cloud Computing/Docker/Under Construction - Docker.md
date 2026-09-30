---
tags:
  - cloud-computing
  - docker
  - containers
  - docker-compose
  - devops
---

# Containerization

[[Containerization|Check Explanations]]

---

# Docker

An open platform for building, sharing, and running containerized applications.
- Introduced in 2013
- Helped popularize containers for application deployment.
- Provides tools to build images and run containers consistently across different computing environments (e.g., development, testing, and production).

## Installation

[[Installation|Check Installation Instructions]]


## Docker Desktop

[Docker Desktop|Check Explanations]



---

# Docker & Containerization

## 1. Motivation: Virtual Machines vs. Containers

### VM-Based Deployment
A virtual machine provides a strongly isolated environment:
- Its own operating system
- Its own filesystem
- Virtualized CPU, memory, storage, and networking
- Software can be installed and configured independently of other VMs

### VM-Based Deployment: A Trade-off
- **A VM provides strong isolation**:
  - Different VMs can use different operating systems and configurations.
  - Problems in one VM are largely isolated from other VMs.
- **But a VM is a relatively heavyweight isolation unit**:
  - Each VM includes its own **guest operating system**.
  - Applications inside the same VM share that guest OS.
  - Guest OS consumes memory, storage, and management effort.
  - VMs provide a strong isolation boundary but at the cost of guest OS overhead.

```
+-------------------------------------------------------+
|  VM 1                     |  VM 2                     |
|  +-------+  +-------+     |  +-------+                |
|  | App 1 |  | App 2 |     |  | App 3 |                |
|  +-------+  +-------+     |  +-------+                |
|  | Bins/Libs        |     |  | Bins/Libs              |
|  +------------------+     |  +------------------------+
|  | Guest OS         |     |  | Guest OS               |
+--+------------------+-----+--+------------------------+
|  Hypervisor (Software layer allowing multiple VMs     |
|              to share the same physical hardware)     |
+-------------------------------------------------------+
|  Host OS                                              |
+-------------------------------------------------------+
|  Physical Server                                      |
+-------------------------------------------------------+
```

### Isolation Granularity
- In single-VM deployment (e.g., Assignment 1), the VM as a whole is isolated from other VMs, but inside the VM, multiple services run together (e.g., Nginx, PostgreSQL, PHP, and application code).
- These services share the same operating system environment.
- The VM itself does not give each service its own isolated environment.
- **Using a VM as the isolation unit gives us relatively coarse-grained isolation.**

### Finer-Grained Isolation
What if we want the services inside the application to run as separate isolated units?
For each service, it can have:
- Its own dependencies
- Its own configuration
- Its own lifecycle

**Could we put each service in a separate VM?**
- Yes, but each VM would require another guest OS.

### Something in Between?
- **Everything in one VM**: Simple, but coarse-grained isolation.
- **One VM per service**: Strong isolation, but high guest OS overhead.
- **What do we want?**
  - **Finer-grained isolation**:
    - Isolate individual services
    - Give each service its own runtime environment
    - Manage configuration and lifecycle independently
  - **A smaller deployment unit**:
    - Without a separate guest OS for each unit

---

## 2. Container Concepts

### Definition
A **Container** is a lightweight, isolated environment for running a service.

- **Containers provide finer-grained isolation**:
  - Containers can be configured and managed independently.
  - Each service can run in its own isolated runtime environment.
- **Containers are a smaller deployment unit than VMs**:
  - Containers **share the host operating system kernel**.
  - **No separate guest OS** is required for each container.

### VMs vs. Containers Architecture

```
         Virtual Machines                            Containers
+---------------------------------+     +---------------------------------+
|  VM 1             VM 2          |     | Container 1 Container 2 C3      |
|  +-------------+  +-----------+ |     | +---------+ +---------+ +-----+ |
|  | App 1 App 2 |  | App 3     | |     | | App 1   | | App 2   | |App3 | |
|  | Bins/Libs   |  | Bins/Libs | |     | | Bins/Lib| | Bins/Lib| |Libs | |
|  | Guest OS    |  | Guest OS  | |     +---------------------------------+
+---------------------------------+     | Container Engine                |
| Hypervisor                      |     +---------------------------------+
+---------------------------------+     | Host OS                         |
| Host OS                         |     +---------------------------------+
+---------------------------------+     | Physical Server                 |
| Physical Server                 |     +---------------------------------+
+---------------------------------+
```
* **Container Engine**: Software that creates, runs, and manages containers.

### VMs and Containers Are Complementary
- Containers are lighter-weight isolation and deployment units, but containers **do not replace virtual machines**.
- VMs isolate entire operating system environments.
- Containers provide finer-grained isolation within an operating system environment.
- **In practice, containers often run inside VMs**:
  - Multiple containers can share the resources of a single VM while remaining isolated from one another.
  - Containers improve resource efficiency while providing finer-grained isolation.
  - **Containers are complementary to VMs, not a replacement.**

```
+---------------------------------------------------------------+
|  Physical Server                                              |
+---------------------------------------------------------------+
|  Host OS                                                      |
+---------------------------------------------------------------+
|  VM Hypervisor                                                |
+-------------------------------+-------------------------------+
|  VM 1                         |  VM 2                         |
|  +-------------------------+  |  +-------------------------+  |
|  | Container 1 Container 2 |  |  | Container 3 Container 4 |  |
|  | App 1       App 2       |  |  | App 3       App 4       |  |
|  | Bins/Libs   Bins/Libs   |  |  | Bins/Libs   Bins/Libs   |  |
|  +-------------------------+  |  +-------------------------+  |
|  | Container Engine        |  |  | Container Engine        |  |
|  +-------------------------+  |  +-------------------------+  |
|  | VM Guest OS             |  |  | VM Guest OS             |  |
|  +-------------------------+  |  +-------------------------+  |
+-------------------------------+-------------------------------+
```

### Practical Motivation & Key Properties
Containers provide finer-grained isolation, smaller deployment units, and better resource efficiency. But a major practical motivation is **reproducible packaging**:
- Package an application with its runtime, libraries, and dependencies.
- Reduce differences between development, testing, and deployment environments.

#### Containerization
- **Containerization** packages an application and its runtime environment into a portable **container image**.
- A **container image** can include:
	  - Application code
	  - Runtime
	  - Libraries and dependencies
  - Default configuration
- The image defines a reproducible runtime environment.
- A **container** is an isolated runtime instance created from that image.

#### Consistent Environments
The same container image can be used across:
- Local development, testing environments, cloud deployments
- Each container starts from the same packaged runtime environment (same runtime, libraries, dependencies, ...)
- **Fewer environment differences $\rightarrow$ more consistent application behavior**.

#### Why Containers?
1. **Consistency**: Runtime and dependencies are packaged together in the image.
2. **Portability**: The same image can run across compatible environments.
3. **Isolation**: Services can run in separate isolated runtime environments.
4. **Efficiency**: Containers share the host OS kernel and usually use fewer resources than VMs.

### Containers in Cloud
Containers integrate naturally with cloud service models:
- **IaaS**: Run containers on VMs for more efficient resource use.
- **PaaS**: Platforms may use containers to package and run applications behind the scenes. Developers focus on application code rather than managing the underlying containers.
- **SaaS**: Providers may use containers internally to deploy and scale application components.

---

## 3. Docker Platform & Architecture

**Docker**: An open platform for building, sharing, and running containerized applications.
- Introduced in 2013
- Helped popularize containers for application deployment.
- Provides tools to build images and run containers consistently across different computing environments (e.g., development, testing, and production).

### Docker Desktop vs. Docker Engine on Linux

#### Docker Desktop (macOS / Windows)
- Docker Desktop provides a complete development environment including **Docker Engine**, **Docker CLI**, and **GUI dashboard**.
- Provides a **Linux environment** for running Linux containers on macOS and Windows:
```
Physical Machine
└── Host OS (macOS / Windows)
    └── Linux environment managed by Docker Desktop (Linux VM)
        └── Docker Engine
            └── Containers (share Linux kernel of that environment)
```
- Docker Engine runs in a Linux environment managed by Docker Desktop.
- Containers share the Linux kernel of that environment; **they do not directly use the macOS or Windows kernel**.

#### Docker Engine on Linux
- When Docker Engine is installed directly on Linux:
```
Physical Machine
└── Linux Host OS
    └── Docker Engine
        └── Containers (share host Linux kernel)
```
- No additional VM is required. Docker Engine runs directly on the Linux host.
- Containers share the host Linux kernel.
- **In both cases, the containers share a Linux kernel.**

### Docker Architecture: Client-Server Architecture
Docker Engine uses a client-server architecture:
- **Docker Client (`docker`)**:
  - The CLI tool you interact with.
  - Sends commands (e.g., `docker build`, `docker run`, `docker pull`) as requests to the daemon through the API.
- **Docker Daemon (`dockerd`)**:
  - Runs in the background and does the actual work.
  - Creates and manages Docker objects (images, containers, networks, volumes).
  - Builds images, creates and runs containers, pulls and pushes images when needed.
- **Docker Registry**:
  - Stores and distributes images (e.g., Docker Hub, Amazon ECR).

```
[ Docker Client ]  --(Docker API)-->  [ Docker Engine (dockerd) ]  <--(Pull/Push)-->  [ Docker Registry ]
  docker build                          - Builds Images                                 (Docker Hub, ECR)
  docker run                            - Runs Containers
  docker pull                           - Manages Networks & Volumes
```

---

## 4. Basic Docker Workflow & Commands

### Core Docker Concepts
- **Dockerfile**: Instructions for building an image.
- **Image**: Read-only package containing an application and its runtime environment.
- **Container**: Runnable instance of an image.
- **Registry**: Stores and distributes images.

### The Basic Workflow

$$\text{Dockerfile} \xrightarrow{\text{Build}} \text{Docker Image} \xrightarrow{\text{Run}} \text{Docker Container}$$

1. Write a `Dockerfile` to define how the image is built.
2. Build an image from the Dockerfile:
   ```bash
   docker build -t <image-name> .
   ```
   *(Note: `docker build` creates files, but not in your project folder).*
3. Create and start a container from the image:
   ```bash
   docker run <image-name>
   ```

### Where Are Images Stored?
- Docker stores images in its **internal storage**, managed by Docker Engine.
- They do not appear as ordinary files in your project directory.
- Inspection in Docker Desktop: `Settings` $\rightarrow$ `Resources` $\rightarrow$ `Disk image location`.
- List local images:
  ```bash
  docker image ls
  ```

### Common Dockerfile Instructions
- `FROM`: Choose a base image (e.g., `FROM node:24`).
- `WORKDIR`: Set the working directory (e.g., `WORKDIR /app`).
- `COPY`: Copy files into the image (e.g., `COPY package*.json ./`).
- `RUN`: Execute commands while building the image (e.g., `RUN npm install`).
- `EXPOSE`: Document the container's listening port (e.g., `EXPOSE 3000`).
- `CMD`: Set the default command when the container starts (e.g., `CMD ["npm", "start"]`).

### Example: Node.js App in Docker

#### `docker-example/app.js`
```javascript
const express = require("express");
const app = express();
const port = 3000;

app.get("/", (req, res) => {
  res.send("Hello from Node.js inside Docker!");
});

app.listen(port, () => {
  console.log(`App running at http://localhost:${port}`);
});
```

#### `docker-example/package.json`
```json
{
  "name": "docker-example",
  "version": "1.0.0",
  "main": "app.js",
  "scripts": {
    "start": "node app.js"
  },
  "dependencies": {
    "express": "^5.2.1"
  }
}
```

#### `docker-example/Dockerfile`
```dockerfile
# Start from an official Node.js image
FROM node:24

# Set the working directory
WORKDIR /app

# Copy package metadata
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy application code
COPY app.js ./

# Document the application port
EXPOSE 3000

# Default command when a container starts
CMD ["npm", "start"]
```

### Running and Managing Containers
- **Run in Foreground with Port Mapping**:
  ```bash
  docker run -p 3000:3000 my-node-app
  ```
  `-p 3000:3000`: Maps host port 3000 to container's port 3000.
- **Run in Background (Detached Mode)**:
  ```bash
  docker run -d -p 3001:3000 my-node-app
  ```
  `-d`: Run in the background. Node.js app runs at `http://localhost:3001`.
- **List Running Containers**:
  ```bash
  docker ps
  docker ps -a   # list all containers (including stopped)
  ```
- **View Container Logs**:
  ```bash
  docker logs <container-id>
  ```
- **Stop Container**:
  ```bash
  docker stop <container-id>
  ```

---

## 5. Docker Registry & Image Distribution

After `docker build`, the image exists only on your local machine. To share with teammates, cloud VMs, or production servers, use a **Docker Registry**.

- **Docker Registry**: Stores and shares container images (e.g., Docker Hub, Amazon Elastic Container Registry - Amazon ECR).
- `Push`: Upload an image to a registry (`docker push`).
- `Pull`: Download an image from a registry (`docker pull`).

### Pushing an Image: Error vs. Correct Way
- **Common Error**:
  ```bash
  docker push my-node-app
  # Output: denied: requested access to the resource is denied
  ```
  *Reason*: `docker push` tries to push to Docker Hub's default registry (`docker.io`) under the `library/` namespace, which is reserved for official images that you do not own.

- **Correct Way**:
  1. Log in to Docker Hub:
     ```bash
     docker login
     ```
  2. Tag the image:
     ```bash
     docker tag <image-name> <docker-username>/<docker-hub-repo-name>:<tag-name>
     # Example:
     docker tag my-node-app cying25/ece1779-images:v1.0
     ```
  3. Push the image:
     ```bash
     docker push <docker-username>/<docker-hub-repo-name>:<tag-name>
     # Example:
     docker push cying25/ece1779-images:v1.0
     ```

### Verifying and Pulling Images
- **Verify**: Check repository at `https://hub.docker.com/repository/docker/<docker-username>/<repo-name>`. A repository can contain multiple tags identifying versions or variants (e.g., `v1.0`, `v1.1`, `latest`).
- **Pull and Run on Target Machine**:
  ```bash
  docker pull cying25/ece1779-images:v1.0
  docker run -d -p 3000:3000 cying25/ece1779-images:v1.0
  ```

### Full Docker Workflow Summary
1. Write a `Dockerfile` to define how the image is built.
2. Build an image: `docker build`
3. Push the image to a registry: `docker push`
4. Pull the image on a target system: `docker pull`
5. Create and run a container from the image: `docker run`

### Pre-Built vs. Custom Images
- **Pre-built image**: Ready to use. Useful for common software such as Nginx, PostgreSQL, Redis.
  ```bash
  docker pull nginx:stable
  docker run -d -p 3002:80 nginx:stable
  ```
- **Custom image**: Built for your own application. Lets you define the runtime, dependencies, and configuration.

---

## 6. Multi-Container Applications & Docker Compose

### When Applications Grow
Real-world applications often require multiple services working together.
*(Example: Assignment 2 task management application with Node.js REST API, PostgreSQL Database, and Redis Cache).*

#### Why not "One Big Container"?
Putting web server, database, and cache into one container causes:
- **Lifecycle**: Cannot restart or scale components independently.
- **Maintenance**: Updating one service may require rebuilding the whole image.
- **Reuse**: Services are tightly coupled and harder to reuse independently.
- **Best Practice**: **One container per responsibility**.

#### The Challenge
Running each service in its own container grants independent lifecycles, easier maintenance, and flexible scaling. However, managing multiple containers manually with `docker run` quickly becomes complex and error-prone.

---

## 7. Docker Compose

### What is Docker Compose?
- A tool for defining and running multi-container applications.
- Uses a `compose.yaml` file to define the application.
- Defines:
  - **Services**: Application components such as `api`, `db`, and `redis`.
  - **Networks**: Connect services.
  - **Volumes**: Persist data.
- Lets you start, stop, and manage multiple services together.

### Basic Commands
- Start complete application stack:
  ```bash
  docker compose up --build -d
  ```
  - `--build`: Build images before starting containers.
  - `-d`: Detached mode: run containers in the background.
- Stop all services:
  ```bash
  docker compose down
  ```
- Stop services and delete volumes:
  ```bash
  docker compose down -v
  ```

---

## 8. Networking in Docker Compose

- Containers need a way to communicate with each other; Docker Compose handles this automatically.
- **Default Network**: Compose creates a default network for the application using the **bridge driver** (typically named `<project-name>_default`).
- **Bridge Network**: A virtual network created by Docker on one Docker host (the Linux system where Docker Engine runs).
- **Service Name as Hostname**:
  - Services on the same Compose network can reach each other using **service names as hostnames**.
  - Example: `api` can connect to PostgreSQL using `host: "db"` on port `5432`.
- **When to Publish Ports**:
  - Ports only need to be published when something **outside that network** needs access.
  - Access `api` via `localhost:3000` on the host $\rightarrow$ Port `3000` must be published (`ports: - "3000:3000"`).
  - `db` is only accessed by `api` on the Compose network $\rightarrow$ Port `5432` **does not need to be published**.

---

## 9. Data Persistence: Docker Volumes

### Why Volumes?
- By default, files written inside a container live inside that container.
- If the container is removed (`docker compose down`), **data is lost**.

### Docker Volumes
- Docker-managed storage used by containers.
- Managed by Docker Engine and stored on the Docker host (inside the Linux VM when using Docker Desktop).
- **Independent of container lifecycle**: Persist data when containers are deleted and recreated.
- **Typical Use Cases**: Databases (e.g., PostgreSQL), application data that must survive container recreation.

### Cloud Block Storage vs. Docker Volumes
| Dimension | Cloud Block Storage (e.g., DigitalOcean Volumes) | Docker Volumes |
| :--- | :--- | :--- |
| **Management** | Managed by cloud provider | Managed by Docker |
| **Attached To** | Attached to VMs | Mounted into containers |
| **Creation** | Created via cloud dashboard/API | Defined in `compose.yaml` |
| **Storage Target** | Store data for VMs | Store data for containers |

### Volume Lifecycle
- `docker compose down`: Containers are removed, but data in volumes persists.
- `docker compose up`: Containers are recreated and re-mount the existing volume without losing data.
- `docker compose down -v`: Explicitly removes volumes when no longer needed.

---

## 10. Complete Multi-Container Example (Node.js + PostgreSQL)

### Project Structure
```
compose-example/
├── app.js          # Express API and PostgreSQL queries
├── package.json    # Node.js dependencies and start script
├── Dockerfile      # Build the API container image
├── init.sql        # Initialize database schema and data
└── compose.yaml    # Define services, network, and volume
```

### File Definitions

#### 1. `compose-example/init.sql`
The official PostgreSQL image automatically runs scripts in `/docker-entrypoint-initdb.d/` when initializing a new database (runs only when the data directory is empty; existing data is left unchanged on subsequent container starts).
```sql
CREATE TABLE IF NOT EXISTS items (
  id SERIAL PRIMARY KEY,
  name TEXT NOT NULL
);

INSERT INTO items (name) VALUES ('Sample Item');
```

#### 2. `compose-example/package.json`
```json
{
  "name": "compose-example",
  "version": "1.0.0",
  "main": "app.js",
  "scripts": {
    "start": "node app.js"
  },
  "dependencies": {
    "express": "^5.2.1",
    "pg": "^8.23.0"
  }
}
```

#### 3. `compose-example/Dockerfile`
```dockerfile
FROM node:24
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY app.js ./
EXPOSE 3000
CMD ["npm", "start"]
```

#### 4. `compose-example/app.js`
`db` is resolved to the PostgreSQL container through Docker Compose networking:
```javascript
const express = require("express");
const { Pool } = require("pg");
const app = express();
const port = 3000;

const pool = new Pool({
  host: "db", // Service name from compose.yaml
  port: 5432,
  user: "user",
  password: "password",
  database: "mydb",
});

app.get("/", async (req, res) => {
  const result = await pool.query("SELECT * FROM items");
  res.json({ items: result.rows });
});

app.listen(port, () => console.log(`API running on http://localhost:${port}`));
```

#### 5. `compose-example/compose.yaml`
```yaml
services:
  api:
    build: .
    ports:
      - "3000:3000"
    depends_on:
      - db
    networks:
      - app-network

  db:
    image: postgres:18
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
      POSTGRES_DB: mydb
    volumes:
      - db-data:/var/lib/postgresql
      - ./init.sql:/docker-entrypoint-initdb.d/init.sql
    networks:
      - app-network

networks:
  app-network:
    driver: bridge

volumes:
  db-data:
```

### Running and Verifying
1. Build and start services:
   ```bash
   docker compose up --build -d
   ```
2. Access the app:
   ```bash
   curl http://localhost:3000
   # Response:
   {"items":[{"id":1,"name":"Sample Item"}]}
   ```
3. Stop services:
   ```bash
   docker compose down       # Preserves db-data volume
   docker compose down -v    # Stops services and removes db-data volume
   ```

---

## 11. Potential Issues & Caveats

1. **Security**:
   - PostgreSQL credentials (`POSTGRES_USER`, `POSTGRES_PASSWORD`) are hard-coded in `compose.yaml` and `app.js`.
   - Not appropriate for production environments.
2. **`depends_on` limitation**:
   - `depends_on: - db` starts `db` before `api`.
   - However, it **does not guarantee that PostgreSQL is ready to accept connections** when `api` starts up (container started $\neq$ database service ready).

---

## 12. Key Docker Commands Cheat Sheet

| Task | Command |
| :--- | :--- |
| **Verify Installation** | `docker version` |
| **List Local Images** | `docker image ls` |
| **Build Image** | `docker build -t <image-name> .` |
| **Tag Image** | `docker tag <image-name> <docker-username>/<repo-name>:<tag>` |
| **Push Image** | `docker push <docker-username>/<repo-name>:<tag>` |
| **Pull Image** | `docker pull <image-name>` |
| **Run Container** | `docker run -d -p <host-port>:<container-port> <image-name>` |
| **List Running Containers** | `docker ps` |
| **List All Containers** | `docker ps -a` |
| **View Logs** | `docker logs <container-id>` |
| **Stop Container** | `docker stop <container-id>` |
| **Start Compose Stack** | `docker compose up --build -d` |
| **Stop Compose Stack** | `docker compose down` |
| **Stop Stack & Wipe Volumes** | `docker compose down -v` |
