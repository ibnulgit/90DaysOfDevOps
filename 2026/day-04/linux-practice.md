# Day 04 – Linux Practice: Processes and Services

Goal: Practice basic Linux process, service, and log inspection using real commands.

---

## 🔍 Process Checks

### 1. Check all running processes
Command:
`ps aux | head`

Output:  
<img width="739" height="179" alt="image" src="https://github.com/user-attachments/assets/baf19bed-a881-4ecd-bb1a-613120b1294c" />


Observation:
- PID 1 is systemd
- Multiple background services are running

---

### 2. Find PID of a specific process
Command:
`pgrep sshd`

Output:
734
742

Observation:
- sshd is running with multiple processes (parent + child)

---

## ⚙️ Service Checks

### 3. Check status of SSH service
Command:
`systemctl status ssh`

Output:
● ssh.service - OpenBSD Secure Shell server
   Loaded: loaded (/lib/systemd/system/ssh.service)
   Active: active (running)
   Main PID: 734 (sshd)

Observation:
- Service is active and running
- systemd supervises the master sshd process

---

### 4. List running systemd services
Command:
`systemctl list-units --type=service --state=running | head`

Output:
cron.service         loaded active running Regular background program processing daemon
ssh.service          loaded active running OpenBSD Secure Shell server
systemd-journald     loaded active running Journal Service
...

Observation:
- systemd manages all core services
- Only active services are shown

---

## 📄 Log Checks

### 5. View logs for SSH service
Command:
`journalctl -u ssh --no-pager | tail -n 10`

Output:
Feb 11 10:20:01 server sshd[742]: Accepted password for user
Feb 11 10:20:05 server sshd[742]: session opened

Observation:
- Successful SSH login entries found
- Logs help confirm service activity

---

### 6. Inspect system logs
Command:
`journalctl -xe | tail -n 10`

Output:
Feb 11 10:25:12 server systemd[1]: Started Session 23 of user root.

Observation:
- No critical errors observed
- Useful during system failures

---

## 🛠 Mini Troubleshooting Flow

Scenario: SSH access issue

Steps:
1. Check if ssh process exists using `pgrep sshd`
2. Verify service state using `systemctl status ssh`
3. Inspect logs using `journalctl -u ssh`
4. Restart service if needed:
   systemctl restart ssh

Conclusion:
- Logs + service state provide clear root cause signals
- Avoid killing processes blindly; inspect first

---

## ✅ Key Learnings

- systemd supervises services via PID 1
- One service may have multiple processes
- Logs are the first place to look during failures
