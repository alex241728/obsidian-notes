---
tags:
  - DigitalOcean
  - VM
---
Focus on **core IaaS concepts** without unnecessary complexity.
- **Simple**: Clear interface and minimal configuration
- **Low Cost**: Virtual machines start at $4/month
- Per-second billing for virtual machines
- **Fast Setup**: Create a virtual machine in minutes
- **Enough IaaS Features**: Compute, storage, networking, APIs, …
# DigitalOcean Droplet

- A Linux VM for hosting your web application and database
- Each Droplet has:
	- Configurable CPU, memory, and storage
	- Choice of OS: Ubuntu, Debian, Fedora, etc.
	- A public IP address for Internet access
	- SSH access for remote management
	- Optional **Volume Block Storage** for additional persistent storage

- Compute: Droplets
- Storage: Volumes Block Storage, Spaces Object Storage

## Access Droplet via SSH

SSH into Droplet:
```bash
ssh root@<droplet-ip>
```
- `root` is the default administrative user for this example
- Production systems should typically use a non-root user with `sudo`

Verify access:
```bash
whoami
```

> [!Warning]
> Make sure you are using the correct SSH key
> Verify firewall settings in DigitalOcean dashboard

---

# DigitalOcean Metadata API

Provides information about a Droplet from within the VM

---
# DigitalOcean Volume

Block storage for persistent file storage

---

# DigitalOcean API

Enables programmatic access to DigitalOcean resources
