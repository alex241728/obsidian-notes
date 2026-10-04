---
tags:
  - dockerfile
---

**Dockerfile**: Instructions for building an image

# Workflow

1. Write a `Dockerfile` to define how the image is built

2. Build an image from the Dockerfile:
```sh
docker build -t <image-name>
```

3. Create and start a container from the image:
```sh
docker run <image-name>
```

---

# Common Dockerfile Instructions
- `FROM`: Choose a base image
- `WORKDIR`: Set the working directory
- `COPY`: Copy files into the image
- `RUN`: Execute commands while building the image
- `EXPOSE`: Document the container’s listening port
- `CMD`: Set the default command when the container starts

> [!Note] 
> **Full reference**: docs.docker.com/reference/dockerfile

