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

Open a terminal and run:

```bash
ssh-keygen -t rsa -b 4096

|               | Minimum      | Recommended      |
| ------------- | ------------ | ---------------- |
| **OS**        | Ubuntu 22.04 | Ubuntu 22.04 LTS |
| **CPU**       | 4 threads    | 8+ threads       |
| **RAM**       | 8 GB         | 32 GB            |
| **Storage**   | 100 GB       | 1 TB+            |
| **Bandwidth** | 100 Mbps     | 500 Mbps         |

