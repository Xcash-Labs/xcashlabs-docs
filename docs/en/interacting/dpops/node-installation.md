---
title: Node Program Installation
description: Guide to installing, configuring, and running an XCash Labs delegate node.
---

# Node Program Installation

## Introduction

!!! info
    This guide assumes you have already followed the [Server Setup Guide](../server-setup/) or are comfortable managing a Linux server.

This guide walks you through installing, registering, and preparing a delegate node. By the end of the guide, your node will be ready to participate in securing the X-Cash public network (once elected as a delegate 😉).

The `xcash-dpops` program manages block validation, delegate communication, block production, and voter reward distribution.

---

## Requirements

### Dependencies

!!! info
    Dependencies are automatically installed and maintained by the installer script.

---

### Time Synchronization

The `xcash-dpops` program relies on accurate system time. Clock drift can prevent proper consensus participation.

Check time sync status:

```bash
timedatectl
