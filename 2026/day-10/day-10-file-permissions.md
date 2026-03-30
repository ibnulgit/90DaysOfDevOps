# Day 10 – File Permissions & File Operations Challenge

Today I practiced **creating files, reading files, and modifying file permissions** in Linux.
Understanding file permissions is critical for **security, scripting, and server management** in DevOps.

---

# Task 1 – Create Files

### Create an Empty File

```bash
touch devops.txt
```

Verify:

```bash
ls -l devops.txt
```

Example Output:

```
-rw-r--r-- 1 user user 0 Mar 19 devops.txt
```

---

### Create notes.txt with Content

```bash
echo "Learning Linux permissions" > notes.txt
```

Verify:

```bash
cat notes.txt
```

Output:

```
Learning Linux permissions
```

---

### Create script.sh using vim

```bash
vim script.sh
```

Inside vim:

```bash
echo "Hello DevOps"
```

Save and exit.

Verify:

```bash
ls -l
```

Example Output:

```
-rw-r--r-- 1 user user 0 Mar 19 devops.txt
-rw-r--r-- 1 user user 25 Mar 19 notes.txt
-rw-r--r-- 1 user user 20 Mar 19 script.sh
```

---

# Task 2 – Read Files

### Read notes.txt

```bash
cat notes.txt
```

---

### View script.sh in read-only mode

```bash
vim -R script.sh
```

This prevents accidental modification.

---

### Display First 5 Lines of /etc/passwd

```bash
head -n 5 /etc/passwd
```

Example Output:

```
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
```

---

### Display Last 5 Lines of /etc/passwd

```bash
tail -n 5 /etc/passwd
```

---

# Task 3 – Understand Permissions

Command:

```bash
ls -l devops.txt notes.txt script.sh
```

Example Output:

```
-rw-r--r-- devops.txt
-rw-r--r-- notes.txt
-rw-r--r-- script.sh
```

Permission breakdown:

| Permission | Meaning                |
| ---------- | ---------------------- |
| rw-        | Owner can read & write |
| r--        | Group can read         |
| r--        | Others can read        |

Numeric representation:

| Permission | Value |
| ---------- | ----- |
| r          | 4     |
| w          | 2     |
| x          | 1     |

Example:

```
rw-r--r-- = 644
```

---

# Task 4 – Modify Permissions

### Make script.sh Executable

```bash
chmod +x script.sh
```

Verify:

```bash
ls -l script.sh
```

Example Output:

```
-rwxr-xr-x script.sh
```

Run script:

```bash
./script.sh
```

Output:

```
Hello DevOps
```

---

### Set devops.txt to Read-Only

Remove write permission:

```bash
chmod a-w devops.txt
```

Verify:

```bash
ls -l devops.txt
```

Example:

```
-r--r--r-- devops.txt
```

---

### Set notes.txt to Permission 640

```bash
chmod 640 notes.txt
```

Verify:

```bash
ls -l notes.txt
```

Example:

```
-rw-r----- notes.txt
```

Meaning:

| User   | Permission   |
| ------ | ------------ |
| Owner  | read + write |
| Group  | read         |
| Others | none         |

---

### Create Directory project/

```bash
mkdir project
```

Set permissions to **755**

```bash
chmod 755 project
```

Verify:

```bash
ls -ld project
```

Example:

```
drwxr-xr-x project
```

---

# Task 5 – Test Permissions

### Try Writing to Read-Only File

```bash
echo "Test" >> devops.txt
```

Error:

```
Permission denied
```

---

### Try Executing File Without Execute Permission

Remove execute permission:

```bash
chmod -x script.sh
```

Try running:

```bash
./script.sh
```

Error:

```
Permission denied
```

Add execute permission again:

```bash
chmod +x script.sh
```

---

# Files Created

```
devops.txt
notes.txt
script.sh
project/
```

---

# Permission Changes

| File       | Before    | After     |
| ---------- | --------- | --------- |
| script.sh  | rw-r--r-- | rwxr-xr-x |
| devops.txt | rw-r--r-- | r--r--r-- |
| notes.txt  | rw-r--r-- | rw-r----- |
| project/   | default   | rwxr-xr-x |

---

# Commands Used

```
touch
echo
vim
cat
head
tail
ls -l
chmod
mkdir
```

---

# What I Learned

* How Linux file permissions control **read, write, and execute access**
* How to modify permissions using **chmod**
* Why execute permission is required for running scripts
* How directory permissions affect access to files
* How DevOps engineers secure files on servers

---

# Why This Matters for DevOps

File permissions are important because:

* Scripts must be executable to run deployments
* Config files must be protected from unauthorized changes
* Secure permissions prevent production issues
* Proper permissions are essential for **CI/CD pipelines and automation**

---

# Screenshots

Included:

```
file-creation.png
permission-change.png
script-execution.png
permission-error.png
```

---

# LinkedIn Post

**Day 10 of #90DaysOfDevOps**

Today I practiced Linux file permissions and file operations.

Learned how to create files, modify permissions using `chmod`, and understand the rwx permission model.

One key lesson: scripts must have execute permission before they can run.

#90DaysOfDevOps
#DevOpsKaJosh
#TrainWithShubham
