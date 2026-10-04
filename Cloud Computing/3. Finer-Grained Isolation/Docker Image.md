---
tags:
  - docker-image
---

Read-only package containing an application and its runtime environment

# Docker Registry

Stores and shares container images

- **Examples**: Docker Hub, Amazon Elastic Container Registry (Amazon ECR)

## Push Image

Upload an image to a registry 

1. Log in to Docker Hub: 
```sh
docker login
```

2.  Tag the image: `docker tag <image-name> <docker-username>/<docker-hub-repo-name>:<tag-name>`:
```sh
docker tag my-node-app cying25/ece1779-images:v1.0
```

3. Push the image: `docker push <docker-username>/<docker-hub-repo-name>:<tag-name>`:
```sh
docker push cying25/ece1779-images:v1.0
```

### Verify Push

Check your Docker Hub repository
- URL: `https://hub.docker.com/repository/docker/<docker-username>/<repo-name>`
	- A repository can contain multiple tags
- Tags commonly identify versions or variants
	- Example: v1.0, v1.1, latest

## Pull Image

Download an image from a registry

- Download the image `docker pull <docker-username>/<repo-name>:<tag-name>`
```sh
docker pull cying25/ece1779-images:v1.0
```

- Run a container
```sh
docker run -d -p 3000:3000 cying25/ece1779-images:v1.0
```



