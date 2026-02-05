---
title: Server Setup Guide
description: Step-by-step guide for preparing a Linux server for an XCash-Labs delegate node.
---

# Server Setup Guide

This guide is aimed at people not familiar with Linux servers or hosting services.

Running a delegate node does require some technical knowledge, but this guide walks step-by-step through preparing a secure server.

If you get stuck, the community can help you.

---

# Prerequisites

## Generate an SSH Key

We strongly recommend using SSH key authentication.

### Windows

Use **PuTTYgen** to create a key pair.

### Linux / macOS

```bash
ssh-keygen -t rsa -b 4096
```

This creates:

- `~/.ssh/id_rsa` (private key)
- `~/.ssh/id_rsa.pub` (public key)

---

# Server Requirements

## Server Requirements

| Requirement | Minimum | Recommended |
|---|---:|---:|
| **OS** | Ubuntu 22.04 | Ubuntu 22.04 LTS |
| **CPU** | 4 cores | 8+ cores |
| **RAM** | 8 GB | 32 GB |
| **Storage** | 100 GB | 1 TB |
| **Bandwidth** | 100 Mbps | 500 Mbps |


---

# Choose a Server Provider

Any provider works:

- Hetzner  
- OVH  
- AWS  
- DigitalOcean  
- Google Cloud  
- Self-hosted  

Choose what you're comfortable with.

---

# Install Linux

Install **Ubuntu 22.04 LTS** from your provider dashboard.

Once installed, note your server IP.

---

# Connect to Your Server

### First Login

```bash
ssh root@SERVER_IP
```

Enter the password provided by your host.

---

### Add Your SSH Key

On the server:

```bash
nano ~/.ssh/authorized_keys
```

Paste your public key inside.

Set permissions:

```bash
chmod 600 ~/.ssh/authorized_keys
chmod 700 ~/.ssh
```

Restart SSH:

```bash
systemctl restart ssh
```

Now login using key:

```bash
ssh -i ~/.ssh/id_rsa root@SERVER_IP
```

---

# Create a Delegate User

Running everything as root is discouraged.

```bash
adduser xcash
usermod -aG sudo xcash
su - xcash
```

---

# Update System

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install curl git build-essential -y
```

---

# Time Sync (Important)

```bash
timedatectl
```

If not synced:

```bash
sudo timedatectl set-ntp true
sudo systemctl restart systemd-timesyncd
```

---

# Firewall Setup

```bash
sudo apt install ufw -y
sudo ufw allow OpenSSH
sudo ufw enable
sudo ufw status
```

---

# Install Fail2Ban

```bash
sudo apt install fail2ban -y
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```

---

# Optional: Disable Root Login

Once SSH keys work:

```bash
sudo nano /etc/ssh/sshd_config
```

Set:

```
PermitRootLogin no
PasswordAuthentication no
```

Restart SSH:

```bash
sudo systemctl restart ssh
```

---

# Optional: Domain Name

Buy a domain and point an A record:

```
delegate.yourdomain.com → SERVER_IP
```

Recommended for public delegates.

---

# Final Checklist

- SSH key login works  
- Logged in as `xcash`  
- System updated  
- Firewall enabled  
- Time synced  

---

# Next Step

Your server is ready.

➡ Continue to **Delegate Node Installation Guide**
