---
title: Management & Monitoring
description: This section is designed to gather steps for managing the different services around the xcash-dpops program, getting logs and monitoring the activity.
---

# Management & Monitoring

## Managing Installation

You can manage your program installation with the installer script:

```bash
bash -c "$(curl -fsSL https://raw.githubusercontent.com/Xcash-Labs/xcash-labs-dpops/master/scripts/autoinstaller/autoinstaller.sh)"
```

The installation script enables you to install and manage your `xcash-dpops` program easily.

### Restart Program

If you encounter issues with your programs or need to apply configuration changes, it is recommended to restart the services using the installer script. This ensures all components are restarted in the correct order and with the proper settings.

Run the installer script and choose **Restart Programs**.

```bash
bash -c "$(curl -fsSL https://raw.githubusercontent.com/Xcash-Labs/xcash-labs-dpops/master/scripts/autoinstaller/autoinstaller.sh)"
```

### Update program

When a new version of the software is released, you will need to update your node to stay in sync with the network and ensure everything continues running smoothly. The easiest way to perform updates is by using the auto-installer script, which can download the latest version and restart the services for you.

Run the installer script and choose **Restart Programs**.

```bash
bash -c "$(curl -fsSL https://raw.githubusercontent.com/Xcash-Labs/xcash-labs-dpops/master/scripts/autoinstaller/autoinstaller.sh)"
```

### Back up your local database

As a shared delegate, you are responsible for distributing payouts to your voters. Voter information and reward share data are stored locally in your delegate node database. Before performing updates, maintenance, or any changes to your server, it is strongly recommended to back up this data to prevent accidental loss.

To backup your shared delegate database, chose **Backup**:

```bash
bash -c "$(curl -fsSL https://raw.githubusercontent.com/Xcash-Labs/xcash-labs-dpops/master/scripts/autoinstaller/autoinstaller.sh)"
```

## systemd services

`systemd` is commonly used on Linux systems to manage background services and core programs. It provides a reliable way to start programs automatically on boot, as well as to monitor, stop, and restart services when needed.

In systemd, a unit represents any resource the system can manage, such as a service or process. These resources are defined through configuration files called unit files, which tell systemd how and when to run each program.

!!! info
    All the **`unit`** files are located in **`/lib/systemd/system/`**

The different services needed for the XCash-Labs consensus running on the server are listed below:

- **/lib/systemd/system/xcash-daemon.service** : Runs the DPoPS (Delegated Proof of Private Stake) consensus program. This service handles delegate communication, block verification, voting, and block production for the network.
- **xcash-dpops.service** : Runs the DPoPS (Delegated Proof of Private Stake) consensus program. This service handles delegate communication, block verification, voting, and block production for the network.
- **xcash-rpc-wallet.service** : Runs the wallet RPC service used by the delegate wallet. It manages the wallet in the background so rewards can be received, tracked, and distributed without keeping the CLI wallet open.
- **firewall.service** : Manages the server’s firewall rules. It ensures only the required ports and services are accessible, helping secure the node from unwanted connections.
- **mongodb.service** : Runs the MongoDB database used by the delegate node. It stores delegate data such as voter information, payout tracking, statistics, and other local node records.

### **Services Management**

At some point, you might have to need to restart or check the status of the services, either to reflect a change you have made, to update, or to run the program with different parameters.

**Service-names:**
- xcash-daemon
- xcash-dpops
- xcash-rpc-wallet
- firewall
- mongodb

### Start a service

To **start** a `systemd` service, run:
- systemctl start <Service-name>

**Example:**

```bash
    systemctl start xcash-dpops
```

### Restart a service

To **restart** a `systemd` service, run:
- systemctl restart <Service-name>

**Example:**

```bash
    systemctl restart xcash-dpops
```

### Stop a service

To **stop** a `systemd` service, run:
- systemctl stop <Service-name>

**Example:**

```bash
    systemctl stop xcash-dpops
```

### Service status

To get the **status** of a `systemd` service, run:
- systemctl status <Service-name>

**Example:**

```bash
    systemctl status xcash-dpops
```

### **Monitoring & Logging**

To check the status and live logs of the XCash-Labs services, run the commands that correspond to the process you want to inspect. These commands show the most recent log entries and continue streaming new output in real time.

For clearer, easier-to-read live logs, the examples below use parameters that limit the output to recent entries while following new activity as it happens.

- journalctl --unit=SERVICE --follow -n 100 --output cat

To check the **`xcash-dpops`** services, you can copy the following commands:

```bash
journalctl --unit=xcash-dpops --follow -n 100 --output cat
```

```bash
journalctl --unit=xcash-daemon --follow -n 100 --output cat
```

```bash
journalctl --unit=xcash-rpc-wallet --follow -n 100 --output cat
```

```bash
journalctl --unit=mongodb --follow -n 100 --output cat
```

```bash
journalctl --unit=firewall --follow -n 100 --output cat
```

!!! info
    The **`xcash-daemon`** service export its logs in a different location than the other services. To display the latest log, use the following command:

```bash
tail -n 100 ~/xcash-labs/logs/xcash-daemon-log.txt
```