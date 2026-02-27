# 🐳 Docker Troubleshooting: "Salta" Scenario (SadServers)

This repository contains my solution for the "Salta" challenge from SadServers. This lab focused on debugging a Node.js application that failed to start due to port configuration mismatches.

## 📋 Problem Description
- **Target:** Run a "dockerized" Node.js app in `/home/admin/app`.
- **Constraint:** Access the web app via `localhost:8888`.
- **Challenge:** The container would start, but the web service was unreachable, and there were port conflicts on the host.

## 🛠️ Debugging Steps & Solution

### 1. Initial Build
First, I built the image from the provided source code:
```bash
docker build -t salta-app .
```
2. Identifying Port Conflict
When trying to run the container on port 8888, I encountered an address already in use error. I used Linux networking tools to find and kill the process occupying the port:

```Bash
# Locate the process
sudo ss -tulpn | grep :8888
```
```Kill the process
sudo fuser -k 8888/tcp
```
3. Log Analysis (The Breakthrough)
The Dockerfile stated EXPOSE 8880, but after running the container and checking the logs:
```Bash
docker logs <container_id>
# Output: "Server Started on: 8888"
```
I discovered that the internal application was actually listening on port 8888, contradicting the Dockerfile documentation.

4. Final Correct Deployment
I re-ran the container with the correct port mapping (Host 8888 -> Container 8888):

```Bash
docker run -d -p 8888:8888 --name salta-final salta-app
```
5. Verification
```Bash
curl localhost:8888
```
# Success Output: Hello World!
