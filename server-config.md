# Jenkins + Docker Setup on Ubuntu Server

This document contains the steps used to install Java, Docker, and Jenkins on an Ubuntu server, along with basic verification commands.

---

## 1. Update Package List

```bash
apt update
```

---

## 2. Install Java (OpenJDK 21)

```bash
apt install openjdk-21-jdk-headless -y
```

### Verify Java Installation

```bash
java --version
```

---

## 3. Install Docker

```bash
apt install docker.io -y
```

### Verify Docker Installation

```bash
docker --version
```

---

## 4. Add Jenkins Repository

### Download Jenkins GPG Key

```bash
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
https://pkg.jenkins.io/debian-stable/jenkins.io-2026.key
```

### Add Jenkins Repository

```bash
echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/" | \
sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
```

---

## 5. Update Package List

```bash
sudo apt update
```

---

## 6. Install Jenkins

```bash
sudo apt install jenkins
```

---

## 7. Verify Jenkins Installation

```bash
jenkins --version
```

---

## 8. Get Jenkins Initial Admin Password

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Use this password during the first login to the Jenkins web interface.

---

## 9. Configure Passwordless Sudo for Jenkins User (Optional)

Open the sudoers file:

```bash
visudo
```

Add the following line:

```text
jenkins ALL=(ALL) NOPASSWD: ALL
```

Save and exit.

---

## 10. Docker Commands

### List Running Containers

```bash
docker ps
```

### List All Docker Images

```bash
docker images
```

### View Container Resource Usage

```bash
docker container stats
```

---

# Useful Service Commands

## Jenkins

Start Jenkins:

```bash
sudo systemctl start jenkins
```

Enable Jenkins on Boot:

```bash
sudo systemctl enable jenkins
```

Check Jenkins Status:

```bash
sudo systemctl status jenkins
```

Restart Jenkins:

```bash
sudo systemctl restart jenkins
```

---

## Docker

Start Docker:

```bash
sudo systemctl start docker
```

Enable Docker on Boot:

```bash
sudo systemctl enable docker
```

Check Docker Status:

```bash
sudo systemctl status docker
```

Restart Docker:

```bash
sudo systemctl restart docker
```

---

# Verification Checklist

| Component | Verification Command |
|-----------|----------------------|
| Java | `java --version` |
| Docker | `docker --version` |
| Jenkins | `jenkins --version` |
| Jenkins Status | `sudo systemctl status jenkins` |
| Docker Status | `sudo systemctl status docker` |

---

# Access Jenkins

After installation, open:

```
http://<YOUR_SERVER_IP>:8080
```

Retrieve the initial admin password:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Paste the password into the Jenkins setup page and continue with the installation.
