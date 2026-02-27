# 🕵️‍♂️ Linux Forensic: "Venice" Scenario (SadServers)

This lab is an exploration of the Linux system to determine the underlying virtualization technology.

## 📋 The Goal
Determine if the current shell is running inside a **Docker Container** or a **Virtual Machine**.

## 🔍 Investigation Checklist

| Method | Command | Indicator of a Container |
| :--- | :--- | :--- |
| **Hidden File** | `ls -a /.dockerenv` | File exists |
| **Control Groups** | `cat /proc/1/cgroup` | Contains 'docker' or 'containerd' |
| **Init Process** | `ps -p 1` | Command is NOT `systemd` (e.g., `/bin/sh`) |
| **File System** | `mount \| grep overlay` | Root filesystem is `overlay` |
| **Hardware Info** | `sudo dmidecode` | Fails or returns limited info (not a real BIOS) |

## 💡 Conclusion
In this scenario, I confirmed I was in a **[Container/VM]** based on the existence of the `/.dockerenv` file and the output of `/proc/1/cgroup` which showed the container isolation path.

## 🐧 Linux Concepts Used
- **/proc filesystem:** Real-time kernel information.
- **Namespaces & Cgroups:** The building blocks of Linux containers.
- **Process Management:** Analyzing the init system.
