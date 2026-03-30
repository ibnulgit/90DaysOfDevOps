## Linux File Read & Write Practice

### 1. Create a File

**Command**

```bash
touch notes.txt
```

**Explanation**

Creates an empty file named `notes.txt`.

---

## 2. Write Text to File (Overwrite)

**Command**

```bash
echo "Line 1: Learning Linux file operations" > notes.txt
```

**Explanation**

`>` writes text to the file. If the file already has content, it will **overwrite** it.

---

## 3. Append New Line

**Command**

```bash
echo "Line 2: Practicing file write operations" >> notes.txt
```

**Explanation**

`>>` **appends** text to the file without removing existing content.

---

## 4. Append and Display Using tee

**Command**

```bash
echo "Line 3: Using tee command to append text" | tee -a notes.txt
```

**Explanation**

`tee -a` writes the text to the file **and displays it in the terminal at the same time**.

---

## 5. Read the Full File

**Command**

```bash
cat notes.txt
```

**Example Output**

```
Line 1: Learning Linux file operations
Line 2: Practicing file write operations
Line 3: Using tee command to append text
```

**Explanation**

`cat` displays the **entire contents** of the file.

---

## 6. Read First Lines of File

**Command**

```bash
head -n 2 notes.txt
```

**Example Output**

```
Line 1: Learning Linux file operations
Line 2: Practicing file write operations
```

**Explanation**

`head` shows the **first few lines** of the file.

---

## 7. Read Last Lines of File

**Command**

```bash
tail -n 2 notes.txt
```

**Example Output**

```
Line 2: Practicing file write operations
Line 3: Using tee command to append text
```

**Explanation**

`tail` shows the **last few lines** of the file.

---

# Final Content of notes.txt

```
Line 1: Learning Linux file operations
Line 2: Practicing file write operations
Line 3: Using tee command to append text
```

---

# Key Commands Practiced

| Command | Purpose                  |
| ------- | ------------------------ |
| `touch` | Create a new file        |
| `echo`  | Write text               |
| `>`     | Overwrite file           |
| `>>`    | Append text              |
| `tee`   | Write and display output |
| `cat`   | Read entire file         |
| `head`  | Show first lines         |
| `tail`  | Show last lines          |

---

✅ **Task Completed:**

* Created file
* Wrote text
* Appended lines
* Read file using multiple commands

---

## Example LinkedIn Post

You can post this:

**Day 06 of #90DaysOfDevOps**

Practiced Linux file operations today.
Learned how to create, write, append, and read files using `touch`, `echo`, `tee`, `cat`, `head`, and `tail`.

The command I'll use a lot in debugging is **tail** for checking logs quickly.

#DevOpsKaJosh #TrainWithShubham

---

# NEXT

Great 👍 Let’s continue with the **3 things I mentioned** so you can stay ahead in the **90DaysOfDevOps challenge**.

---

# 1️⃣ How to Push Day 06 to GitHub (Step-by-Step)

### Step 1 — Go to your forked repository

Open your fork of **90DaysOfDevOps** on your computer.

Clone it if you haven’t already:

```bash
git clone https://github.com/YOUR_USERNAME/90DaysOfDevOps.git
```

---

### Step 2 — Move into the repo

```bash
cd 90DaysOfDevOps
```

---

### Step 3 — Navigate to Day 06 folder

```bash
cd 2026/day-06
```

If the folder doesn't exist:

```bash
mkdir -p 2026/day-06
cd 2026/day-06
```

---

### Step 4 — Create the markdown file

```bash
nano file-io-practice.md
```

Paste the content I gave you earlier.

Save with:

```
CTRL + O
ENTER
CTRL + X
```

---

### Step 5 — Add the file

```bash
git add file-io-practice.md
```

---

### Step 6 — Commit the changes

```bash
git commit -m "Completed Day 06 - Linux file read and write practice"
```

---

### Step 7 — Push to GitHub

```bash
git push origin main
```

Your submission will now appear in your forked repo.

---

# 2️⃣ How DevOps Engineers Use These Commands in Real Life

These commands are **used constantly in production servers**.

### 🔹 Checking logs

```bash
tail -f /var/log/nginx/access.log
```

Used to **watch logs in real time** when debugging.

---

### 🔹 Checking recent errors

```bash
tail -n 50 /var/log/syslog
```

Shows the **last 50 log lines**.

---

### 🔹 Reading configuration files

```bash
cat /etc/nginx/nginx.conf
```

Used to inspect **server configs**.

---

### 🔹 Writing configuration quickly

```bash
echo "PORT=3000" >> .env
```

Used in **deployments and automation scripts**.

---

### 🔹 Logging output from scripts

```bash
./deploy.sh | tee deploy.log
```

This shows the output **and saves it to a file**.

Very common in **CI/CD pipelines**.

---

# 3️⃣ Preview of Day 07 (Linux Permissions)

Most likely Day 07 will cover **file permissions**.

These are critical in DevOps.

### Example permission

```bash
-rwxr-xr-x
```

Meaning:

| Symbol | Meaning |
| ------ | ------- |
| r      | read    |
| w      | write   |
| x      | execute |

---

### Changing permissions

```bash
chmod +x script.sh
```

Makes a script **executable**.

---

### Changing ownership

```bash
chown ubuntu:ubuntu file.txt
```

Used frequently in **Docker containers and servers**.

---

# 🔥 Pro DevOps Tip

One command every DevOps engineer uses daily:

```bash
tail -f logfile.log
```

Example:

```bash
tail -f /var/log/nginx/error.log
```

This **live streams logs**, which is critical during incidents.

---

# ⭐ Your Progress So Far

You’ve already practiced:

✅ System troubleshooting
✅ CPU / Memory inspection
✅ Logs
✅ File operations
