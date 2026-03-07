# Linux Architecture Notes (Short & Practical)

## Core Components of Linux
- **Kernel** — Controls CPU, memory, devices, filesystems, networking. Exposes system calls used by all programs.
- **User Space** — Shells, applications, libraries, daemons. Everything outside the kernel where users interact.
- **systemd (Init System)** — First process (PID 1). Starts services, manages dependencies, handles logging, timers, mounts, and restarts.

---

## How Processes Are Created & Managed
- Processes follow the **fork → exec** model:
  - `fork()` duplicates the current process.
  - `exec()` replaces it with a new program.
- All processes ultimately descend from **systemd (PID 1)**.
- The kernel schedules processes, handles signals, and cleans up resources.

### Process States
- **R – Running**: On CPU or ready to run.
- **S – Sleeping**: Waiting for I/O (most common).
- **D – Disk Sleep**: Uninterruptible I/O wait.
- **T – Stopped**: Paused by a signal.
- **Z – Zombie**: Process finished but parent hasn’t collected exit code.
- **Dead**: Fully removed from the process table.

---

## What systemd Does (and Why It Matters)
- Boots the system and launches all services.
- Starts units in parallel for faster startup.
- Manages service health, restarts, and dependencies.
- Provides unified logging through **journald**.
- Controls timers, sockets, mounts, and targets.
- Essential for DevOps because it centralizes service control and troubleshooting.

---

## Daily Commands for DevOps Work
- `ps aux` — View all running processes.
- `top` — Live CPU/memory usage.
- `systemctl status <service>` — Check service health.
- `journalctl -u <service>` — View logs for a service.
- `kill -9 <pid>` — Force‑terminate a stuck process.

---

## Why This Matters for DevOps
Understanding Linux internals helps you:
- Diagnose crashed or stuck services.
- Investigate CPU, memory, or I/O issues.
- Read logs effectively and respond to incidents faster.
- Understand how applications behave under load.
