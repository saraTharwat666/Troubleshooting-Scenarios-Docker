# 🐳 Docker Troubleshooting & Lab Solutions (SadServers)

![Project Banner](https://levelup.gitconnected.com/docker-networking-modes-406ff4548dfa)

Welcome to my specialized repository for **Docker Infrastructure Troubleshooting**. This project documents my journey through solving complex, real-world container scenarios from [SadServers](https://sadservers.com/), focusing on Linux systems, container networking, and microservices orchestration.

---

## 🚀 Overview
In this repository, I tackle various "broken" scenarios where Docker containers fail to start, communicate, or replicate. Each lab solution includes:
- **Root Cause Analysis:** Identifying why the system failed.
- **Linux Forensics:** Using tools like `ss`, `lsof`, and `journalctl` to trace errors.
- **The Fix:** Step-by-step commands to restore service.
- **DevOps Best Practices:** Applying CI/CD principles and Docker optimization.

---

## 🛠️ Docker Mastery Cheat Sheet
Here are the most critical commands I use during my troubleshooting sessions:

| Category | Command | Description |
| :--- | :--- | :--- |
| **Inspection** | `docker ps -a` | List all containers (including failed ones) |
| **Forensics** | `docker logs -f <id>` | Follow real-time container logs |
| **Deep Dive** | `docker inspect <id>` | View low-level JSON metadata (IPs, Mounts) |
| **Execution** | `docker exec -it <id> sh` | Open an interactive shell inside a container |
| **Networking** | `docker network ls` | List all virtual networks on the host |
| **Cleanup** | `docker system prune -a` | Remove all unused data (Images, Containers) |
| **Resources** | `docker stats` | Live stream of container resource usage |

---

## 📁 Repository Structure
- `/Salta`: Fixing port mapping and Dockerfile inconsistencies.
- `/Helsingør`: Debugging Postgres physical replication in Docker Compose.
- `/Venice`: Container escape detection and system forensics.
- `/Cape-Town`: Fixing startup crashes and volume mounts.

---

## 🐧 Linux & DevOps Skills Demonstrated
- **Process Management:** Killing conflicting ports using `fuser` and `kill`.
- **Networking:** Bridge networks, Port Forwarding (NAT), and DNS resolution.
- **Storage:** Volume binding, permissions (`chmod/chown`), and persistence.
- **Automation:** Writing Dockerfiles and `docker-compose.yml` for CI/CD pipelines.

---

## 🤝 Let's Connect!
If you're interested in Docker, AWS, or Linux DevOps, feel free to explore my solutions or reach out!

---
*“In a world of broken containers, the logs are your best friend.”*
