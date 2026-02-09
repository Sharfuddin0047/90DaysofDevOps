# ☁️ Day 08 – Cloud Server Setup: Docker, Nginx & Web Deployment

This exercise focused on deploying a real web server on the cloud, managing it remotely, and verifying public access.

---

## 🚀 Commands Used

### 🔹 Launch & SSH Access
```bash
# Connect to instance (AWS example)
ssh -i my-key.pem ubuntu@<your-instance-ip>
```

---

### 🔹 Update System
```bash
sudo apt update && sudo apt upgrade -y
```

---

### 🔹 Install Docker
```bash
sudo apt install docker.io -y
sudo systemctl start docker
sudo systemctl enable docker
docker --version
```

---

### 🔹 Install Nginx
```bash
sudo apt install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx
```

### Verify Nginx Status
```bash
sudo systemctl status nginx
```

---

### 🔹 Configure Firewall / Security Group
Allowed inbound traffic on:

- **Port 22** → SSH  
- **Port 80** → HTTP (Web access)

---

### 🔹 Test Web Access
Opened browser:

```
http://<your-instance-ip>
```

✅ Successfully viewed the **Nginx Welcome Page**.

---

## 📊 Extract Nginx Logs

### View Logs
```bash
sudo tail -n 50 /var/log/nginx/access.log
```

---

### Save Logs to File
```bash
sudo cp /var/log/nginx/access.log ~/nginx-logs.txt
```

---

### Download Logs Locally
```bash
scp -i my-key.pem ubuntu@<your-instance-ip>:~/nginx-logs.txt .
```

---

## ⚠️ Challenges Faced

✅ **Nginx not accessible initially**  
- Cause: Port 80 was not allowed in the security group.  
- Fix: Added an inbound rule for HTTP traffic.

✅ **Permission denied while copying logs**  
- Cause: Log files require elevated privileges.  
- Fix: Used `sudo` before copying the file.

---

## 📚 What I Learned

- How to launch and connect to a cloud server via SSH.
- Installing and managing services like Docker and Nginx.
- Importance of security groups and firewall rules.
- How to access and export server logs.
- Verifying deployments from the public internet builds confidence in real-world setups.

---

## ⭐ Key Takeaway

Deploying a server from scratch is a fundamental DevOps skill.  
Understanding infrastructure, networking, services, and logs prepares you for real production environments.

---

✅ **Next Goal:** Try deploying a custom HTML page or containerized app to deepen your cloud skills.
