# 🕹️ Docker Scenario: "Quito" - Container-to-Host Control

The goal of this challenge was to manage a host-level container (`nginx`) from within another isolated container (`docker-access`). This simulates how CI/CD runners (like GitHub Actions) interact with a Docker daemon.

## 🔍 The Challenge
- **Isolation:** By default, containers cannot see or control other containers on the host.
- **Network Restrictions:** The environment was air-gapped (no internet), preventing me from pulling new images like `docker:latest`.
- **Status:** Both `nginx` and `docker-access` were in an `Exited` state.

## 🛠️ The Solution (Step-by-Step)

### 1. Identify Local Resources
Since I couldn't pull from Docker Hub, I identified the existing local image using:
```bash
docker ps -a
# Found local image: "docker-access"
```
2. Docker Socket Binding (The Secret Sauce)
The key to controlling Docker from inside a container is mounting the Unix Domain Socket (docker.sock). This "tunnel" allows the containerized Docker client to talk to the host's Docker engine.

I re-created the container with the following command:

```Bash
docker run -d --name docker-access \
  -v /var/run/docker.sock:/var/run/docker.sock \
  docker-access sleep infinity
```
3. Remote Execution
Once inside the "controller" container, I commanded the host to start the nginx service:

```Bash
docker exec docker-access docker start nginx
```
✅ Verification
Running docker ps inside docker-access successfully listed the running nginx container, proving the socket connection was active.
