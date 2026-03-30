# Linux File System Hierarchy & Scenario-Based Practice

---

# Part 1 – Linux File System Hierarchy

## 1. `/` (Root Directory)

**Purpose**

The root directory `/` is the top-level directory in Linux. All files and directories start from here.

**Command**

```bash
ls -l /
```

**Example Output**

```
bin  boot  dev  etc  home  lib  opt  root  tmp  usr  var
```

**Observation**

Important directories like `/etc`, `/home`, `/usr`, and `/var` exist under root.

**I would use this when**

I need to understand the full directory structure of the system.

---

## 2. `/home`

**Purpose**

Contains home directories for regular users.

**Command**

```bash
ls -l /home
```

**Example Output**

```
drwxr-xr-x  user
```

**Observation**

Each user has a personal directory for files, scripts, and configurations.

**I would use this when**

Accessing user files or troubleshooting user-specific issues.

---

## 3. `/root`

**Purpose**

Home directory for the root (administrator) user.

**Command**

```bash
ls -l /root
```

**Example Output**

```
script.sh
backup.log
```

**Observation**

Root-only files and scripts are usually stored here.

**I would use this when**

Managing system-level administrative tasks.

---

## 4. `/etc`

**Purpose**

Contains system configuration files.

**Command**

```bash
ls -l /etc
```

**Example Files**

```
hostname
hosts
passwd
ssh
```

**Observation**

Files like `hostname`, `hosts`, and `ssh` configs are located here.

**I would use this when**

Editing configuration files for services.

---

## 5. `/var/log`

**Purpose**

Stores system and application log files.

**Command**

```bash
ls -l /var/log
```

**Example Files**

```
syslog
auth.log
kern.log
```

**Observation**

System activity and error logs are recorded here.

**I would use this when**

Troubleshooting system or application issues.

---

## 6. `/tmp`

**Purpose**

Stores temporary files created by applications.

**Command**

```bash
ls -l /tmp
```

**Observation**

Files here may be cleared automatically during reboot.

**I would use this when**

Applications need temporary storage.

---

## Additional Directories

### `/bin`

**Purpose**

Contains essential command binaries.

**Command**

```bash
ls -l /bin
```

**Examples**

```
ls
cp
mv
bash
```

**I would use this when**

Running core Linux commands.

---

### `/usr/bin`

**Purpose**

Stores user-level command binaries.

**Command**

```bash
ls -l /usr/bin
```

**Examples**

```
python3
git
curl
```

**I would use this when**

Running installed applications.

---

### `/opt`

**Purpose**

Contains optional or third-party software.

**Command**

```bash
ls -l /opt
```

**Observation**

Often used for custom applications.

**I would use this when**

Installing third-party software.

---

# Hands-On Tasks

### Find the largest log files

```bash
du -sh /var/log/* 2>/dev/null | sort -h | tail -5
```

**Observation**

Shows the largest log files which may consume disk space.

---

### View hostname configuration

```bash
cat /etc/hostname
```

**Observation**

Displays the system hostname.

---

### Check home directory contents

```bash
ls -la ~
```

**Observation**

Shows files and hidden configuration files in the user's home directory.

---

# Part 2 – Scenario-Based Practice

---

# Scenario 1 – Service Not Starting

A service called **myapp** failed after reboot.

### Step 1

```bash
systemctl status myapp
```

**Why**

Checks if the service is running, failed, or inactive.

---

### Step 2

```bash
journalctl -u myapp -n 50
```

**Why**

Shows the last 50 log entries to identify errors.

---

### Step 3

```bash
systemctl is-enabled myapp
```

**Why**

Checks if the service is configured to start at boot.

---

### Step 4

```bash
systemctl restart myapp
```

**Why**

Attempts to restart the service after diagnosing the issue.

---

# Scenario 2 – High CPU Usage

The server is slow.

### Step 1

```bash
top
```

**Why**

Shows live CPU and memory usage.

---

### Step 2

```bash
ps aux --sort=-%cpu | head -10
```

**Why**

Lists the top CPU-consuming processes.

---

### Step 3

```bash
htop
```

**Why**

Provides a more interactive process viewer.

---

### Step 4

```bash
kill <PID>
```

**Why**

Stops a problematic process if necessary.

---

# Scenario 3 – Finding Service Logs

Developer asks for Docker service logs.

### Step 1

```bash
systemctl status docker
```

**Why**

Checks if the Docker service is running.

---

### Step 2

```bash
journalctl -u docker -n 50
```

**Why**

Displays the latest logs for Docker.

---

### Step 3

```bash
journalctl -u docker -f
```

**Why**

Shows logs in real-time.

---

# Scenario 4 – File Permission Issue

Script `/home/user/backup.sh` is not executing.

---

### Step 1 – Check permissions

```bash
ls -l /home/user/backup.sh
```

**Why**

Shows file permissions and confirms the missing execute permission.

---

### Step 2 – Add execute permission

```bash
chmod +x /home/user/backup.sh
```

**Why**

Makes the script executable.

---

### Step 3 – Verify permissions

```bash
ls -l /home/user/backup.sh
```

**Why**

Confirms that execute permission was added.

---

### Step 4 – Run the script

```bash
./backup.sh
```

**Why**

Ensures the script now runs successfully.

---

# Key Takeaways

* Linux file system structure helps locate configs, logs, and binaries.
* Logs in `/var/log` are critical for troubleshooting.
* `systemctl` and `journalctl` are essential tools for managing services.
* Correct file permissions are required to execute scripts.

---

✅ **Day 07 Completed**

Skills practiced:

* Linux file system hierarchy
* Log discovery
* Service troubleshooting
* Process monitoring
* File permission management

---

## Example LinkedIn Post

**Day 07 of #90DaysOfDevOps**

Today I learned how the Linux file system is organized and where to find logs, configs, and binaries.

Practiced troubleshooting scenarios like service failures, high CPU usage, and permission errors.

Understanding `/etc` and `/var/log` is crucial for debugging production systems.

#DevOpsKaJosh #TrainWithShubham

---
