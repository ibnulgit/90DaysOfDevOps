## Target Service / Process

Service inspected: **ssh (OpenSSH server)**

Purpose: Verify system health and inspect logs for any SSH related issues.

---

# 1. Environment Basics

## Command

```bash
uname -a
```

### Output

```bash
Linux ubuntu 6.5.0-21-generic #21-Ubuntu SMP x86_64 GNU/Linux
```

### Observation

System is running Ubuntu Linux kernel 6.5 on x86_64 architecture.

---

## Command

```bash
lsb_release -a
```

### Output

```bash
Distributor ID: Ubuntu
Description: Ubuntu 22.04.3 LTS
Release: 22.04
Codename: jammy
```

### Observation

System is Ubuntu 22.04 LTS which is stable and widely used in production environments.

---

# 2. Filesystem Sanity Check

## Command

```bash
mkdir /tmp/runbook-demo
```

### Observation

Temporary directory created successfully for testing file operations.

---

## Command

```bash
cp /etc/hosts /tmp/runbook-demo/hosts-copy && ls -l /tmp/runbook-demo
```

### Output

```bash
-rw-r--r-- 1 root root 247 Mar 16 12:20 hosts-copy
```

### Observation

File copy works correctly; filesystem permissions and operations appear normal.

---

# 3. CPU & Memory Snapshot

## Command

```bash
ps -o pid,pcpu,pmem,comm -p $(pgrep sshd)
```

### Output

```bash
PID %CPU %MEM COMMAND
945 0.0 0.2 sshd
```

### Observation

SSH service is using minimal CPU and memory resources.

---

## Command

```bash
free -h
```

### Output

```bash
              total        used        free      shared  buff/cache   available
Mem:          7.6Gi       2.1Gi       3.2Gi       210Mi       2.3Gi       5.0Gi
Swap:         2.0Gi       0.0Gi       2.0Gi
```

### Observation

System memory usage is healthy; plenty of free and cached memory available.

---

# 4. Disk & IO Snapshot

## Command

```bash
df -h
```

### Output

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        50G   20G   28G  42% /
```

### Observation

Root filesystem usage is at 42%, which is within a safe range.

---

## Command

```bash
du -sh /var/log
```

### Output

```bash
220M /var/log
```

### Observation

Log directory size is moderate and not consuming excessive disk space.

---

# 5. Network Snapshot

## Command

```bash
ss -tulpn | grep ssh
```

### Output

```bash
tcp   LISTEN  0  128  0.0.0.0:22  0.0.0.0:*  users:(("sshd",pid=945))
```

### Observation

SSH service is actively listening on port 22.

---

## Command

```bash
curl -I https://google.com
```

### Output

```bash
HTTP/1.1 200 OK
```

### Observation

Internet connectivity is working properly.

---

# 6. Logs Reviewed

## Command

```bash
journalctl -u ssh -n 50
```

### Output (snippet)

```bash
Mar 16 12:15:02 ubuntu sshd[1021]: Accepted password for user from 192.168.1.5
Mar 16 12:16:10 ubuntu sshd[1034]: Connection closed by authenticating user
```

### Observation

SSH authentication attempts appear normal with no error spikes.

---

## Command

```bash
tail -n 50 /var/log/auth.log
```

### Output (snippet)

```bash
Mar 16 12:15:02 ubuntu sshd[1021]: Accepted password for user
Mar 16 12:16:10 ubuntu sshd[1034]: Disconnected from user
```

### Observation

Logs confirm normal login activity with no suspicious failed login attempts.

---

# Quick Findings

System health indicators are stable:

* CPU usage is minimal.
* Memory usage is healthy.
* Disk usage is within safe limits.
* SSH service is running and listening on port 22.
* Logs show normal authentication activity without errors.

No immediate issues detected.

---

# If This Worsens (Next Steps)

1. Restart SSH service if connection issues occur

```bash
sudo systemctl restart ssh
```

2. Increase SSH log verbosity in `/etc/ssh/sshd_config` to debug authentication issues.

3. Capture deeper diagnostics using tools such as:

```bash
strace -p <pid>
```

or

```bash
top
```

to identify resource spikes.

---

# Summary

This troubleshooting drill demonstrates a repeatable method for diagnosing system health and service behavior using system resource checks, network inspection, and log analysis.

The approach prioritizes **evidence collection before taking action**, which is a key DevOps operational practice.

---
