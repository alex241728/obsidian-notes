---
tags:
  - docker
  - containerization
---

**Containerization** packages an application and its runtime environment into a portable **container image**. The image defines a reproducible runtime environment.

Containerization ensures consistent environments:
- The same container image can be used across:
	- Local development, testing environments, cloud deployments
	- Each container starts from the same packaged runtime environment (same runtime, libraries, dependencies, ...)
- Fewer environment differences $\rightarrow$ more consistent application behavior

# Container
an isolated runtime instance created from that image.

A **container image** can include:
- Application code
- Runtime
- Libraries and dependencies
- Default configuration

**Advantages**:
1. **Consistency**: Runtime and dependencies are packaged together in the image.
2. **Portability**: The same image can run across compatible environments.
3. **Isolation**: Services can run in separate isolated runtime environments.
4. **Efficiency**: Containers share the host OS kernel and usually use fewer resources than VMs.

**Containers in Cloud**:
Containers integrate naturally with cloud service models:
- **IaaS**: Run containers on VMs for more efficient resource use.
- **PaaS**: Platforms may use containers to package and run applications behind the scenes. Developers focus on application code rather than managing the underlying containers.
- **SaaS**: Providers may use containers internally to deploy and scale application components.