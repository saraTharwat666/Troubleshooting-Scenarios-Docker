# 🚦 Scenario: "San Juan" - Traefik Load Balancing Fix

## 📋 Scenario Overview
The objective was to fix a Traefik Load Balancer that was intermittently failing to route traffic to four backend application servers (`app01` to `app04`).

## 🔍 Diagnosis & Findings
After inspecting the `docker-compose.yml` and analyzing container logs, two critical misconfigurations were identified:
1. **Port Mismatch:** `app02` was configured to listen on port `81` instead of the standard port `80`, causing Traefik to fail its health checks/routing for this node.
2. **Network Isolation:** `app04` was attached to an `internal` network, isolating it from the Traefik proxy which resides on the `web` network.

## 🛠️ The Fix
Modified the `docker-compose.yml` file to standardize the environment:
- **Port Fix:** Changed `traefik.http.services.app.loadbalancer.server.port` for `app02` from `81` to `80`.
- **Network Fix:** Realigned `app04` to the `web` network to allow Traefik to discover and route traffic to it.

```bash
# Applying the changes
docker compose up -d --force-recreate
```
# Verifying Round-robin
```
for i in {1..10}; do curl -s app.sadserver | head -n1; done
```
