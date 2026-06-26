# Kasm Workspaces Migration & Secure Remote Access Platform

## 📖 Project Overview

This project documents the migration of a **Kasm Workspaces** deployment from an **Ubuntu Proxmox LXC container** to a dedicated **RHEL 9 Virtual Machine** running Docker.

The original deployment experienced networking limitations caused by running Docker inside an unprivileged LXC container. During an upgrade to Kasm 1.17, Docker networking plugins required kernel features that were unavailable within the LXC environment.

To create a more stable and maintainable deployment, I migrated the application to a dedicated virtual machine, integrated it with **Cloudflare Tunnel**, and validated a successful production-style deployment.

---

## Architecture

```text
                    Internet
                        │
                Cloudflare DNS
                        │
              Cloudflare Tunnel
                        │
               cloudflared Connector
                        │
        RHEL 9 Virtual Machine (Docker)
                        │
              Kasm Workspaces Platform
                        │
        Browser-Based Linux Workspaces
```

---

## Technologies Used

- RHEL 9
- Docker
- Kasm Workspaces 1.17
- Proxmox VE
- Cloudflare Tunnel
- Linux Administration
- Docker Networking
- HTTPS / TLS
- Git
- GitHub

---

## Objectives

- Deploy Kasm Workspaces in a production-style environment
- Migrate from an unsupported LXC deployment to a dedicated VM
- Secure remote access using Cloudflare Tunnel
- Validate Docker networking and application health
- Build an upgrade-friendly architecture

---

## Challenges Encountered

### Docker Networking Limitations

While upgrading Kasm Workspaces inside an Ubuntu LXC container, the installation failed due to Docker networking requirements.

Error:

```text
/dev/net/tun: no such file or directory
```

The issue was caused by the Docker sidecar networking plugin requiring kernel capabilities unavailable within an unprivileged Proxmox LXC.

---

### Cloudflare Tunnel HTTPS Errors

After migrating to the RHEL virtual machine, Cloudflare initially returned:

```text
502 Bad Gateway
```

The issue was traced to Cloudflare validating Kasm's default self-signed certificate.

Resolution:

- Updated the Cloudflare Tunnel origin settings
- Enabled **No TLS Verify**
- Successfully restored secure connectivity

---

## Solution

Migrated Kasm to a dedicated RHEL 9 virtual machine running Docker.

Benefits of the migration included:

- Native Docker support
- Improved networking compatibility
- Simplified upgrades
- Better long-term maintainability
- Elimination of LXC kernel restrictions

---

## Security

- HTTPS access through Cloudflare Tunnel
- No inbound firewall ports exposed to the Internet
- Secure remote access without port forwarding
- Docker container isolation

---

## 📊 Validation

Successfully verified:

- Kasm services healthy
- Docker containers operational
- Cloudflare Tunnel connectivity
- HTTPS access
- Browser-based workspaces launching successfully

---

## Lessons Learned

This project reinforced several infrastructure concepts:

- Selecting the appropriate virtualization platform
- Docker networking requirements
- Container vs. Virtual Machine tradeoffs
- Cloudflare Tunnel configuration
- TLS certificate validation
- Linux troubleshooting
- Infrastructure migration planning

---

## 📸 Screenshots

### Proxmox Environment

<img width="1659" height="518" alt="image" src="https://github.com/user-attachments/assets/20efc063-9b02-4cf9-ae9a-e8d29045ef45" />

---

### Containers

<img width="1550" height="364" alt="image" src="https://github.com/user-attachments/assets/f11479d8-61a0-4639-ba29-c6e2270d3c61" />


---

### Cloudflare Tunnel

<img width="808" height="54" alt="image" src="https://github.com/user-attachments/assets/95fce382-bbc4-4e08-ad35-0bad8078779e" />


---

### Kasm Dashboard

<img width="1844" height="842" alt="image" src="https://github.com/user-attachments/assets/288a9eaa-1ac4-491d-9cfd-bfbe2efc3423" />


---

## Future Improvements

- Configure Cloudflare Access for Zero Trust authentication
- Integrate LDAP/Active Directory authentication
- Deploy persistent user storage
- Automate deployment using Ansible
- Implement monitoring with Uptime Kuma
- Automate backups

---

## Skills Demonstrated

- Linux Administration
- Docker
- Virtualization
- Proxmox
- Cloudflare Tunnel
- HTTPS/TLS
- Infrastructure Troubleshooting
- Platform Migration
- Networking
- System Administration
- Homelab Engineering

---

## Repository Purpose

This repository demonstrates my ability to troubleshoot infrastructure issues, evaluate architectural tradeoffs, and migrate production-style workloads to more reliable environments while maintaining secure remote access and operational stability.
