---
title: Server Setup Guide
description: Step-by-step guide to preparing a Linux server for running an XCash-Labs delegate node.
---

# Server Setup Guide

This guide is aimed at users who are not familiar with Linux servers or hosting services.

---

## Introduction

Running a delegate node requires some familiarity with Linux and networking.  
However, it should be accessible to anyone willing to learn.

This guide will help you:

- understand basic server concepts
- securely access your server
- prepare a Linux environment
- harden your system for production
- get ready to install the delegate node software

If you get stuck, the community can help you along the way.

---

## Prerequisites

### Generate an SSH Key

Using SSH key authentication is strongly recommended.  
It is more secure than password-only login and will be used to access your server.

---

### Windows (PuTTYgen)

1. Download PuTTY / PuTTYgen
2. Generate a new RSA key
3. Save:
   - the **public key**
   - the **private key** (`.ppk`)

---

### Linux / macOS

This will generate:

~/.ssh/id_rsa (private key)
~/.ssh/id_rsa.pub (public key)

Open a terminal and run:

```bash
ssh-keygen -t rsa -b 4096

Choose a Linux Server
System Requirements

Delegates exchange large amounts of data and must remain online reliably.

|               | Minimum      | Recommended      |
| ------------- | ------------ | ---------------- |
| **OS**        | Ubuntu 22.04 | Ubuntu 22.04 LTS |
| **CPU**       | 4 threads    | 8+ threads       |
| **RAM**       | 8 GB         | 32 GB            |
| **Storage**   | 100 GB       | 1 TB+            |
| **Bandwidth** | 100 Mbps     | 500 Mbps         |

---
title: Server Setup Guide
description: Prepare a Linux server for running an XCash-Labs delegate node.
---

# Server Setup Guide

This guide walks through preparing a Linux server for running an XCash-Labs delegate node.

It assumes little prior Linux experience and focuses on a secure, production-ready setup.

---

## Generate an SSH Key

On Linux or macOS:

```bash
ssh-keygen -t rsa -b 4096
```

This creates:

- ~/.ssh/id_rsa (private key)  
- ~/.ssh/id_rsa.pub (public key)

---

## Choose a Linux Server

Delegate nodes exchange a large amount of data and must remain reliable.

| | Minimum | Recommended |
|---|---|---|
| OS | Ubuntu 22.04 | Ubuntu 22.04 LTS |
| CPU | 4 threads | 8+ threads |
| RAM | 8 GB | 32 GB |
| Storage | 100 GB | 1 TB+ |
| Bandwidth | 100 Mbps | 500 Mbps |

!!! info ""
    These requirements are designed to be future-proof as the network grows.

### Hosting Providers

You may use any provider you are comfortable with:

- Hetzner  
- OVH  
- DigitalOcean  
- AWS  
- Google Cloud  
- Self-hosted hardware  

Choose a server that meets the requirements above.

---

## Install Linux

Most providers allow installing Ubuntu directly from their dashboard.

Recommended distribution:

Ubuntu 22.04 LTS

Once installed, note your server’s IP address.

---

## Connect to Your Server

### Initial Login (password)

```bash
ssh root@SERVER_IP
```

Confirm the fingerprint and enter the password provided by your host.

### Login with SSH Key

```bash
ssh -i ~/.ssh/id_rsa root@SERVER_IP
```

---

## Add Your SSH Key to the Server

If your provider did not add your SSH key automatically:

```bash
nano ~/.ssh/authorized_keys
```

Paste your public key into the file.

Set permissions:

```bash
chmod 600 ~/.ssh/authorized_keys
chmod 700 ~/.ssh
```

Restart SSH:

```bash
systemctl restart ssh
```

---

## Create a Dedicated User

Running services as root is discouraged.

```bash
adduser xcash
usermod -aG sudo xcash
```

Switch to the new user:

```bash
su - xcash
```

---

## System Updates

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install curl git build-essential -y
```

---

## Time Synchronization

Check:

```bash
timedatectl
```

Enable if needed:

```bash
sudo timedatectl set-ntp true
sudo systemctl restart systemd-timesyncd
```

---

## Basic Security Hardening

### Firewall

```bash
sudo apt install ufw -y
sudo ufw allow OpenSSH
sudo ufw enable
sudo ufw status
```

### Fail2Ban

```bash
sudo apt install fail2ban -y
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```

---

## Optional: Disable Root Login

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

## Optional: Domain Name

Purchase a domain and create an A record:

```
delegate.yourdomain.com → SERVER_IP
```

Optional but recommended for shared delegates.

---

## Final Check

Make sure:

- SSH keys work  
- Firewall is enabled  
- Time sync is active  
- Logged in as `xcash`  
- System updated  

---

## Next Step

Your server is now ready.

Proceed to:

**Delegate Node Installation Guide**
