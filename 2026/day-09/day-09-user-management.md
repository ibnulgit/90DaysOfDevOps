# Day 09 – Linux User & Group Management Challenge

Today I practiced **Linux user and group management**, created shared directories, and configured group permissions to simulate a team collaboration environment.

---

# Users & Groups Created

### Users

* tokyo
* berlin
* professor
* nairobi

### Groups

* developers
* admins
* project-team

---

# Task 1 – Create Users

### Create Users with Home Directories

```bash
sudo useradd -m tokyo
sudo useradd -m berlin
sudo useradd -m professor
```

### Set Passwords

```bash
sudo passwd tokyo
sudo passwd berlin
sudo passwd professor
```

### Verify Users

Check `/etc/passwd`

```bash
cat /etc/passwd | grep tokyo
cat /etc/passwd | grep berlin
cat /etc/passwd | grep professor
```

Check home directories

```bash
ls /home
```

Example Output

```
tokyo
berlin
professor
```

---

# Task 2 – Create Groups

### Create Groups

```bash
sudo groupadd developers
sudo groupadd admins
```

### Verify Groups

```bash
cat /etc/group | grep developers
cat /etc/group | grep admins
```

Example Output

```
developers:x:1002:
admins:x:1003:
```

---

# Task 3 – Assign Users to Groups

### Assign tokyo to developers

```bash
sudo usermod -aG developers tokyo
```

### Assign berlin to developers and admins

```bash
sudo usermod -aG developers berlin
sudo usermod -aG admins berlin
```

### Assign professor to admins

```bash
sudo usermod -aG admins professor
```

### Verify Group Membership

```bash
groups tokyo
groups berlin
groups professor
```

Example Output

```
tokyo : tokyo developers
berlin : berlin developers admins
professor : professor admins
```

---

# Task 4 – Shared Directory for Developers

### Create Directory

```bash
sudo mkdir /opt/dev-project
```

### Set Group Ownership

```bash
sudo chgrp developers /opt/dev-project
```

### Set Permissions

```bash
sudo chmod 775 /opt/dev-project
```

### Verify Permissions

```bash
ls -ld /opt/dev-project
```

Example Output

```
drwxrwxr-x 2 root developers 4096 Mar 18 12:00 /opt/dev-project
```

### Test File Creation

Create file as tokyo

```bash
sudo -u tokyo touch /opt/dev-project/tokyo-file.txt
```

Create file as berlin

```bash
sudo -u berlin touch /opt/dev-project/berlin-file.txt
```

Verify files

```bash
ls /opt/dev-project
```

Example Output

```
tokyo-file.txt
berlin-file.txt
```

---

# Task 5 – Team Workspace

### Create User

```bash
sudo useradd -m nairobi
sudo passwd nairobi
```

### Create Group

```bash
sudo groupadd project-team
```

### Add Users to Group

```bash
sudo usermod -aG project-team nairobi
sudo usermod -aG project-team tokyo
```

### Create Workspace Directory

```bash
sudo mkdir /opt/team-workspace
```

### Assign Group

```bash
sudo chgrp project-team /opt/team-workspace
```

### Set Permissions

```bash
sudo chmod 775 /opt/team-workspace
```

### Verify Permissions

```bash
ls -ld /opt/team-workspace
```

Example Output

```
drwxrwxr-x 2 root project-team 4096 Mar 18 12:20 /opt/team-workspace
```

### Test File Creation

```bash
sudo -u nairobi touch /opt/team-workspace/nairobi-file.txt
```

Check files

```bash
ls /opt/team-workspace
```

Example Output

```
nairobi-file.txt
```

---

# Commands Used

```
useradd
passwd
groupadd
usermod
groups
cat /etc/passwd
cat /etc/group
mkdir
chgrp
chmod
ls -ld
sudo -u
touch
```

---

# What I Learned

* How to create and manage Linux users and groups.
* How group permissions allow multiple users to collaborate on shared directories.
* How to assign users to multiple groups using `usermod -aG`.
* How to manage directory ownership and permissions with `chgrp` and `chmod`.
* How DevOps engineers manage team access on production servers.

---

# Why This Matters for DevOps

User and group management is important in DevOps because:

* Multiple engineers need controlled access to servers.
* Permissions protect sensitive files and configurations.
* Shared directories allow teams to collaborate on deployments and projects.
* Proper user management improves security and operational control.

---

# Screenshots Included

```
user-creation.png
group-verification.png
directory-permissions.png
file-creation-test.png
```

---

# LinkedIn Post

**Day 09 of #90DaysOfDevOps**

Today I completed a Linux user and group management challenge.

I created multiple users, assigned them to groups, and configured shared directories with group permissions. This helped me understand how teams collaborate securely on Linux servers.

One interesting part was testing file creation using `sudo -u username`.

#DevOpsKaJosh
#TrainWithShubham

---
