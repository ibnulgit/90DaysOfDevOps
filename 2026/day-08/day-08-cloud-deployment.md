# Day 08 – Cloud Server Setup (Docker, Nginx & Web Deployment)

Today I deployed a **web server on a cloud instance**, installed **Docker and Nginx**, configured **security groups**, and accessed my website from the internet.

---

# Part 1 – Launch Cloud Instance & SSH Access

### Step 1 – Create EC2 Instance

Platform used: **AWS EC2 (Free Tier)**

Configuration:

* OS: Ubuntu 22.04 LTS
* Instance Type: t2.micro
* Key Pair: `devops-key.pem`
* Security Group:

  * SSH → Port **22**
  * HTTP → Port **80**

---

### Step 2 – Connect via SSH

Command used:

```bash
ssh -i devops-key.pem ubuntu@<your-instance-ip>
```

Example:

```bash
ssh -i devops-key.pem ubuntu@13.233.120.15
```

✅ Successfully connected to the cloud server.

📸 Screenshot: **ssh-connection.png**

---

# Part 2 – Install Docker & Nginx

### Step 1 – Update System

```bash
sudo apt update
sudo apt upgrade -y
```

---

### Step 2 – Install Docker

```bash
sudo apt install docker.io -y
```

Verify installation:

```bash
docker --version
```

Start Docker service:

```bash
sudo systemctl start docker
sudo systemctl enable docker
```

---

### Step 3 – Install Nginx

```bash
sudo apt install nginx -y
```

Check if Nginx is running:

```bash
sudo systemctl status nginx
```

Expected output:

```
Active: active (running)
```

Enable Nginx on boot:

```bash
sudo systemctl enable nginx
```

---

# Part 3 – Security Group Configuration

Security group rules added:

| Type | Port | Source    |
| ---- | ---- | --------- |
| SSH  | 22   | My IP     |
| HTTP | 80   | 0.0.0.0/0 |

---

### Test Web Access

Open browser and visit:

```
http://<your-instance-ip>
```

Example:

```
http://13.233.120.15
```

✅ Nginx welcome page appeared successfully.

📸 Screenshot: **nginx-webpage.png**

---

# Part 4 – Extract Nginx Logs

### Step 1 – View Nginx Logs

Access log:

```bash
sudo tail -n 20 /var/log/nginx/access.log
```

Error log:

```bash
sudo tail -n 20 /var/log/nginx/error.log
```

---

### Step 2 – Save Logs to File

```bash
sudo cat /var/log/nginx/access.log > nginx-logs.txt
```

Check file:

```bash
cat nginx-logs.txt
```

---

### Step 3 – Download Log File to Local Machine

Run this command from your **local computer terminal**.

```bash
scp -i devops-key.pem ubuntu@<your-instance-ip>:~/nginx-logs.txt .
```

Example:

```bash
scp -i devops-key.pem ubuntu@13.233.120.15:~/nginx-logs.txt .
```

✅ File downloaded successfully.

---

# Commands Used

```bash
ssh -i devops-key.pem ubuntu@<ip>
sudo apt update
sudo apt upgrade -y
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
docker --version
sudo apt install nginx -y
sudo systemctl status nginx
sudo systemctl enable nginx
sudo tail -n 20 /var/log/nginx/access.log
sudo cat /var/log/nginx/access.log > nginx-logs.txt
scp -i devops-key.pem ubuntu@<ip>:~/nginx-logs.txt .
```

---

# Challenges Faced

**Issue:** Nginx page was not loading in browser.

**Cause:** HTTP port **80** was not open in the security group.

**Solution:**

Added rule:

```
Type: HTTP
Port: 80
Source: 0.0.0.0/0
```

After that the website worked correctly.

---

# What I Learned

* How to launch and configure a **cloud server (AWS EC2)**
* How to **connect using SSH**
* How to install and manage **Docker and Nginx**
* How to configure **security groups and firewall rules**
* How to access and export **Nginx log files**

---

# Why This Matters for DevOps

This exercise simulates real DevOps tasks:

* Deploying applications on cloud servers
* Managing infrastructure remotely
* Installing and managing services
* Debugging using logs
* Configuring network security

These are **core skills required in production environments**.

---

# Screenshots

Included in this submission:

```
ssh-connection.png
nginx-webpage.png
docker-nginx.png
```

---

# Files Submitted

```
day-08-cloud-deployment.md
nginx-logs.txt
ssh-connection.png
nginx-webpage.png
docker-nginx.png
```

---

# LinkedIn Post

**Day 08 of #90DaysOfDevOps**

Today I launched my first cloud server using AWS EC2, connected with SSH, installed Docker and Nginx, and deployed a web server accessible from the internet.

I also extracted and analyzed Nginx logs from the server.

One challenge I faced was opening port 80 in the security group, which I fixed.

#DevOpsKaJosh
#TrainWithShubham

---
