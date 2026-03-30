# Day 11 – File Ownership Challenge (chown & chgrp)

Today I practiced **Linux file ownership management** using `chown` and `chgrp`.
These commands allow administrators to control **who owns files and which group can access them**.

---

# Task 1 – Understanding Ownership

### Check Files in Home Directory

```bash
ls -l
```

Example Output

```
-rw-r--r-- 1 user user  0 Mar 20 devops.txt
-rw-r--r-- 1 user user 25 Mar 20 notes.txt
-rwxr-xr-x 1 user user 18 Mar 20 script.sh
```

### Format Explanation

```
-rw-r--r-- 1 owner group size date filename
```

| Field | Meaning                           |
| ----- | --------------------------------- |
| owner | User who owns the file            |
| group | Group that has access to the file |

### Difference Between Owner and Group

* **Owner**: The primary user who controls the file.
* **Group**: A set of users who can share access to the file depending on permissions.

---

# Task 2 – Basic chown Operations

### Create File

```bash
touch devops-file.txt
```

### Check Owner

```bash
ls -l devops-file.txt
```

Example

```
-rw-r--r-- 1 user user 0 Mar 20 devops-file.txt
```

---

### Change Owner to tokyo

```bash
sudo chown tokyo devops-file.txt
```

Verify

```bash
ls -l devops-file.txt
```

Example

```
-rw-r--r-- 1 tokyo user 0 Mar 20 devops-file.txt
```

---

### Change Owner to berlin

```bash
sudo chown berlin devops-file.txt
```

Verify

```bash
ls -l devops-file.txt
```

Example

```
-rw-r--r-- 1 berlin user 0 Mar 20 devops-file.txt
```

---

# Task 3 – Basic chgrp Operations

### Create File

```bash
touch team-notes.txt
```

Check Group

```bash
ls -l team-notes.txt
```

Example

```
-rw-r--r-- 1 user user 0 Mar 20 team-notes.txt
```

---

### Create Group

```bash
sudo groupadd heist-team
```

---

### Change Group Ownership

```bash
sudo chgrp heist-team team-notes.txt
```

Verify

```bash
ls -l team-notes.txt
```

Example

```
-rw-r--r-- 1 user heist-team 0 Mar 20 team-notes.txt
```

---

# Task 4 – Combined Owner & Group Change

### Create File

```bash
touch project-config.yaml
```

### Change Owner and Group

```bash
sudo chown professor:heist-team project-config.yaml
```

Verify

```bash
ls -l project-config.yaml
```

Example

```
-rw-r--r-- 1 professor heist-team 0 Mar 20 project-config.yaml
```

---

### Create Directory

```bash
mkdir app-logs
```

### Change Ownership

```bash
sudo chown berlin:heist-team app-logs
```

Verify

```bash
ls -ld app-logs
```

Example

```
drwxr-xr-x 2 berlin heist-team 4096 Mar 20 app-logs
```

---

# Task 5 – Recursive Ownership

### Create Directory Structure

```bash
mkdir -p heist-project/vault
mkdir -p heist-project/plans
touch heist-project/vault/gold.txt
touch heist-project/plans/strategy.conf
```

---

### Create Group

```bash
sudo groupadd planners
```

---

### Change Ownership Recursively

```bash
sudo chown -R professor:planners heist-project
```

---

### Verify

```bash
ls -lR heist-project
```

Example Output

```
heist-project/
vault/
gold.txt
plans/
strategy.conf
```

All files now owned by:

```
professor:planners
```

---

# Task 6 – Practice Challenge

### Create Directory

```bash
mkdir bank-heist
```

---

### Create Files

```bash
touch bank-heist/access-codes.txt
touch bank-heist/blueprints.pdf
touch bank-heist/escape-plan.txt
```

---

### Create Groups

```bash
sudo groupadd vault-team
sudo groupadd tech-team
```

---

### Set Ownership

```bash
sudo chown tokyo:vault-team bank-heist/access-codes.txt
sudo chown berlin:tech-team bank-heist/blueprints.pdf
sudo chown nairobi:vault-team bank-heist/escape-plan.txt
```

---

### Verify

```bash
ls -l bank-heist
```

Example

```
-rw-r--r-- 1 tokyo   vault-team access-codes.txt
-rw-r--r-- 1 berlin  tech-team  blueprints.pdf
-rw-r--r-- 1 nairobi vault-team escape-plan.txt
```

---

# Files & Directories Created

```
devops-file.txt
team-notes.txt
project-config.yaml
app-logs/
heist-project/
bank-heist/
```

---

# Ownership Changes

| File                | Before    | After                |
| ------------------- | --------- | -------------------- |
| devops-file.txt     | user:user | berlin:user          |
| team-notes.txt      | user:user | user:heist-team      |
| project-config.yaml | user:user | professor:heist-team |
| app-logs            | user:user | berlin:heist-team    |
| heist-project/*     | user:user | professor:planners   |
| access-codes.txt    | user:user | tokyo:vault-team     |
| blueprints.pdf      | user:user | berlin:tech-team     |
| escape-plan.txt     | user:user | nairobi:vault-team   |

---

# Commands Used

```
ls -l
touch
mkdir
groupadd
chown
chgrp
chown -R
```

---

# What I Learned

* The difference between **file owner and group ownership**
* How to change file ownership using **chown**
* How to change group ownership using **chgrp**
* How recursive ownership changes work for directories
* Why correct ownership is important for **application deployments and server security**

---

# Why This Matters for DevOps

File ownership is important in DevOps because:

* Applications must have correct permissions to access files
* Log directories must be owned by the correct services
* Deployment pipelines create files that must be accessible to multiple users
* Containers often rely on correct ownership for mounted volumes

---

# Screenshots Included

```
ownership-before.png
ownership-after.png
recursive-ownership.png
bank-heist-files.png
```

---

# LinkedIn Post

**Day 11 of #90DaysOfDevOps**

Today I practiced Linux file ownership using `chown` and `chgrp`.

Learned how to assign users and groups to files and directories, and how recursive ownership works in real environments.

This is critical for application deployments and managing shared resources.

#90DaysOfDevOps
#DevOpsKaJosh
#TrainWithShubham
