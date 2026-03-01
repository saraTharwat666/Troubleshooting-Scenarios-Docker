# DevOps Practice: From Cloud Infrastructure to Kubernetes Mastery

This repository contains my solutions for various DevOps challenges, ranging from AWS IAM policies to troubleshooting complex Kubernetes deployments.

## 🚀 Projects Included

### 1. AWS IAM Security
- **Task:** Created a read-only policy for EC2 (iampolicy_mark) to allow specific access to instances, AMIs, and snapshots.
- **Tech:** AWS IAM, JSON Policies.

### 2. Docker Networking & Environment Fix (Bern Scenario)
- **Challenge:** WordPress couldn't connect to MariaDB due to hostname mismatch.
- **Solution:** Manually mapped the container IP to the expected hostname in `/etc/hosts` and corrected environment variables.
- **Tech:** Docker, Bash Scripting.

### 3. Kubernetes Local Registry & Deployment (Singara Scenario)
- **Challenge:** Pods stuck in `ImagePullBackOff` because the image was local-only.
- **Solution:** Deployed a local Docker Registry (port 5000), tagged and pushed the image, then updated K8s manifests to pull from the local registry.
- **Tech:** K3s, Kubernetes Manifests (YAML), Docker Registry.

## 🐧 Linux Knowledge Base
Daily insights into Linux administration, networking, and automation recorded during this journey.
