---
tags:
  - docker-commands
---

# Key Commands

- Build: 
```sh
docker build -t <image-name> .
```

- Run:
```sh
docker run -d -p <host-port>:<container-port> <image-name>
```

- List running containers: 
	- `-a`: List all containers
```sh
docker ps
```

- View logs: 
```sh
docker logs <container-id>
```

- Stop container: 
```sh
docker stop <container-id>
```

> [!Note] 
> **Full reference**: docs.docker.com/reference/cli/docker/