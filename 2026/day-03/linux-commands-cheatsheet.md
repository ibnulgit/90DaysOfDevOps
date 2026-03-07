# Linux Commands Cheat Sheet (Process, Filesystem, Networking)

## Process Management
- `ps aux` — Show all running processes with details.
- `top` — Live CPU, memory, and process usage.
- `htop` — Interactive process viewer (if installed).
- `pidof <name>` — Get PID of a running process.
- `pgrep <pattern>` — Find PIDs by process name.
- `kill <pid>` — Gracefully stop a process.
- `kill -9 <pid>` — Force‑kill a stuck process.
- `pkill <pattern>` — Kill processes by name.
- `systemctl status <service>` — Check service health and logs.
- `systemctl restart <service>` — Restart a service quickly.
- `journalctl -u <service>` — View logs for a specific service.

## File System & Disk
- `ls -l` — List files with permissions and metadata.
- `cd <dir>` — Change directory.
- `pwd` — Show current working directory.
- `du -sh <path>` — Show disk usage of a directory.
- `df -h` — Display disk space usage of all filesystems.
- `find <path> -name "<pattern>"` — Search for files by name.
- `grep -R "<text>" <path>` — Search text inside files recursively.
- `tail -f <file>` — Stream live logs from a file.
- `chmod 755 <file>` — Change file permissions.
- `chown user:group <file>` — Change file ownership.

## Networking Troubleshooting
- `ping <host>` — Test connectivity and latency.
- `ip addr` — Show network interfaces and IP addresses.
- `curl -I <url>` — Fetch HTTP headers for quick checks.
- `dig <domain>` — Perform DNS lookups.
- `ss -tulpn` — Show listening ports and associated processes.
- `traceroute <host>` — Trace the network path to a destination.

## Quick Troubleshooting Flow
- Check process health → `top`, `ps aux`, `systemctl status`
- Inspect logs → `journalctl`, `tail -f`
- Verify disk space → `df -h`, `du -sh`
- Test network → `ping`, `curl`, `dig`
- Restart or kill safely → `systemctl restart`, `kill`
