# Day 12 – Revision & Breather (Days 01–11)

Today I reviewed the key concepts from the first 11 days of the **#90DaysOfDevOps challenge**.
The goal was to reinforce Linux fundamentals and practice important commands again.

---

# 1️⃣ Mindset & Learning Plan Review

### Day 01 Goal Check

My goal was to:

* Build strong Linux fundamentals
* Practice daily hands-on commands
* Understand how DevOps engineers troubleshoot servers

### Adjustment

I realized I should:

* Spend more time practicing **logs and troubleshooting**
* Focus more on **permissions and ownership**

---

# 2️⃣ Processes & Services Review

### Check Running Processes

Command:

```bash
ps aux | head
```

Observation:

Shows running processes with **CPU, memory usage, and process owner**.

---

### Check Service Status

Command:

```bash
systemctl status nginx
```

Observation:

Nginx service was **active (running)**.

---

### Check Service Logs

Command:

```bash
journalctl -u nginx -n 20
```

Observation:

Logs showed normal requests and no errors.

---

# 3️⃣ File Skills Practice

### Append Text to File

Command:

```bash
echo "DevOps practice" >> notes.txt
```

Result:

New line successfully added to the file.

---

### Change File Permission

Command:

```bash
chmod +x script.sh
```

Result:

Script became executable.

---

### Change File Owner

Command:

```bash
sudo chown tokyo script.sh
```

Result:

File owner successfully changed.

---

# 4️⃣ Cheat Sheet Refresh (Top 5 Commands)

These are the commands I would use first during troubleshooting:

| Command            | Purpose                              |
| ------------------ | ------------------------------------ |
| `ls -l`            | Check file permissions and ownership |
| `ps aux`           | View running processes               |
| `systemctl status` | Check service health                 |
| `journalctl -u`    | View service logs                    |
| `chmod`            | Modify file permissions              |

---

# 5️⃣ User & Group Practice

### Create Test User

```bash
sudo useradd testuser
```

---

### Verify User

```bash
id testuser
```

Example Output:

```
uid=1002(testuser) gid=1002(testuser) groups=1002(testuser)
```

---

### Change File Ownership

```bash
sudo chown testuser notes.txt
```

Verify

```bash
ls -l notes.txt
```

Result:

```
-rw-r--r-- 1 testuser user notes.txt
```

---

# Mini Self-Check

### 1️⃣ Which 3 commands save you the most time right now?

**ls -l**

* Quickly shows permissions, owner, and group.

**systemctl status**

* Instantly tells if a service is running or failing.

**journalctl -u**

* Helps troubleshoot service errors quickly.

---

### 2️⃣ How do you check if a service is healthy?

Commands:

```bash
systemctl status nginx
journalctl -u nginx -n 20
ps aux | grep nginx
```

These commands show:

* Service status
* Logs
* Running processes

---

### 3️⃣ How do you safely change ownership and permissions?

Example:

```bash
sudo chown tokyo:developers file.txt
chmod 640 file.txt
```

Explanation:

* Assign correct **owner and group**
* Set safe permissions so only required users can access.

---

### 4️⃣ What will you focus on improving in the next 3 days?

* Practicing **Linux troubleshooting scenarios**
* Learning **networking commands**
* Understanding **Docker basics**

---

# Key Takeaways

* Linux troubleshooting relies heavily on **logs and system services**
* File permissions and ownership are critical for **security and deployments**
* Commands like `systemctl`, `journalctl`, and `ls -l` are used frequently in real DevOps environments
* Hands-on practice helps build **muscle memory for command usage**

---

# Commands Revisited

```
ps aux
systemctl status
journalctl -u
ls -l
chmod
chown
echo >>
id
```

---

# LinkedIn Post

**Day 12 of #90DaysOfDevOps**

Today was a revision day. I reviewed Linux fundamentals like processes, services, file permissions, and ownership.

One command I now remember confidently is **journalctl**, which is extremely useful for troubleshooting services.

#90DaysOfDevOps
#DevOpsKaJosh
#TrainWithShubham
