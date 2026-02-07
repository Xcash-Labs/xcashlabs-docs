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

To **start** a `systemd` service, run:

```bash
systemctl start <Service-name>


_**Example:**_

```text
systemctl start xcash-dpops
```



To **restart** a `systemd` service, run:

```text
systemctl restart SERVICE
```

_**Example:**_

```text
systemctl restart xcash-rpc-wallet
```



To **stop** a `systemd` service, run:

```text
systemctl stop SERVICE
```

_**Example:**_

```text
systemctl stop xcash-daemon
```



To check the **status** of a `systemd` service, run:

```text
systemctl status SERVICE
```

_**Example:**_

```text
systemctl status mongodb
```

**Output:**

```text
● mongodb.service - MongoDB Database Server
   Loaded: loaded (/lib/systemd/system/mongodb.service; disabled; vendor preset: enabled)
   Active: active (exited) since Mon 2020-06-08 11:50:51 CEST; 38min ago
 Main PID: 14852 (code=exited, status=0/SUCCESS)
   CGroup: /system.slice/mongodb.service
           └─14854 /root/xcash-official/mongodb-linux-x86_64-ubuntu1804-4.2.3/bin/mongod --fork --syslog --dbpath /data/db/
```



### **Monitoring & Logging**

To check the status and live logs of the XCash-Labs services, run the commands that correspond to the process you want to inspect. These commands show the most recent log entries and continue streaming new output in real time.

For clearer, easier-to-read live logs, the examples below use parameters that limit the output to recent entries while following new activity as it happens.

```text
journalctl --unit=SERVICE --follow -n 100 --output cat
```

To check the **`xcash-dpops`** services, you can copy the following commands:



```text
journalctl --unit=xcash-dpops --follow -n 100 --output cat
```



```text
journalctl --unit=xcash-daemon --follow -n 100 --output cat
```



```text
journalctl --unit=xcash-rpc-wallet --follow -n 100 --output cat
```



```text
journalctl --unit=mongodb --follow -n 100 --output cat
```



```text
journalctl --unit=firewall --follow -n 100 --output cat
```



!!! info
    The **`xcash-daemon`** service export its logs in a different place. To display the latest log, use the following command:

```text
tail -n 100 ~/xcash-official/logs/xcash-daemon-log.txt
```


### **Login service checking**

We can change the motd generated when we login to our server to make it show us basic node information like the service status, our balance and blockchain syncronization status

Optionally, we can to disable all the automatic scripts executed when we log in and only enable ours.

```bash
chmod -x /etc/update-motd.d/*
```

We need to place our script in the `update-motd.d` directory, we will name it `00-xcash-node-checks` and put our script inside

```bash
#!/bin/bash

# Adjust this variable to the name of your xcash-daemon unit file name
XCASH_DAEMON_SRV=xcash-daemon

# Adjust this variable to the name of your xcash-wallets unit file name
XCASH_WALLET_SRV=xcash-rpc-wallet

# Adjust this variable to the name of your xcash-dpops unit file name
XCASH_DPOPS_SRV=xcash-dpops

# Adjust this variable to the name of your mongodb unit file name
MONGODB_SRV=mongodb

DAEMON_URL="http://127.0.0.1:18281/json_rpc"
WALLET_URL="http://127.0.0.1:18285/json_rpc"
CURL='curl -w "\n" -s -H "Content-Type: application/json" -X'

red="\033[01;31m"
green="\033[01;32m"
reset="\033[0m"

function check_height(){
    if lsof -Pi :18281 -sTCP:LISTEN -t >/dev/null ; then
        DATA=`$CURL GET $DAEMON_URL -d '{"jsonrpc":"2.0","id":"0","method":"get_block_count"}'`

        HEIGHT=$(echo "$DATA" | grep '"count"' | awk {'print $2'} | sed s'|,||g' | tr -d $'\r')
        STATUS=$(echo "$DATA" | grep '"status"' | awk {'print $2'} | sed s'|"||g' | tr -d $'\r')

        if [ $STATUS == "OK" ]; then
            STATUS=${green}OK${reset}
        else
            SATTUS=${red}FAIL${reset}
        fi

        echo
        echo -e "Blockhain sync status: $STATUS"
        echo "Blockchain height: $HEIGHT"
    else
        echo
        echo "X-Cash Daemon service is not running...."
        echo "Check the $XCASH_DAEMON_SRV service status"
    fi
}

function get_node_balance(){
    if lsof -Pi :18285 -sTCP:LISTEN -t >/dev/null ; then
        DATA=`$CURL GET $WALLET_URL -d '{"jsonrpc":"2.0","id":"0","method":"get_balance","params":{"account_index":0,"address_indices":[0]}}'`

        ADDR=$(echo "$DATA" | grep '"address"' | awk {'print $2'} | sed s'|"||g' | sed s'|,||g' | head -1 | tr -d $'\r')
        UNSPENT_OUTPUTS=$(echo "$DATA" | grep '"num_unspent_outputs"' | awk {'print $2'} | sed s'|"||g' | sed s'|,||g' | head -1 | tr -d $'\r')

        ATOMIC_TOTAL_BALANCE=$(echo "$DATA" | grep '"balance"' | awk {'print $2'} | sed s'|,||g' | head -1 | tr -d $'\r')
        ATOMIC_UNLOCKED_BALANCE=$(echo "$DATA" | grep '"unlocked_balance"' | awk {'print $2'} | sed s'|,||g' | head -1 | sed s"|^M||g" | tr -d $'\r')
        TOTAL_BALANCE=$((ATOMIC_TOTAL_BALANCE/1000000))
        UNLOCKED_BALANCE=$((ATOMIC_UNLOCKED_BALANCE/1000000))

        echo
        echo "Public address:   $ADDR"
        echo "Unspent outputs:  $UNSPENT_OUTPUTS"
        echo "Total balance:    $TOTAL_BALANCE XCASH"
        echo "Unlocked balance: $UNLOCKED_BALANCE XCASH"
    else
        echo
        echo "X-Cash RCP Wallet service is not running...."
        echo "Check the $XCASH_WALLET_SRV service status"
    fi
}

function check_services_status(){
    echo
    MONGODB_UP_SINCE=$(systemctl show $MONGODB_SRV --property=ActiveEnterTimestamp | sed s"|ActiveEnterTimestamp=||g")
    XCASH_DAEMON_UP_SINCE=$(systemctl show $XCASH_DAEMON_SRV --property=ActiveEnterTimestamp | sed s"|ActiveEnterTimestamp=||g")
    XCASH_WALLET_UP_SINCE=$(systemctl show $XCASH_WALLET_SRV --property=ActiveEnterTimestamp | sed s"|ActiveEnterTimestamp=||g")
    XCASH_DPOPS_UP_SINCE=$(systemctl show $XCASH_DPOPS_SRV --property=ActiveEnterTimestamp | sed s"|ActiveEnterTimestamp=||g")

    systemctl is-active $MONGODB_SRV --quiet \
        && echo -e ${green}MongoDB service is running since...............$MONGODB_UP_SINCE${reset} \
        || echo -e ${red}MongoDB service is not running${reset}

    systemctl is-active $XCASH_DAEMON_SRV --quiet \
        && echo -e ${green}X-Cash Daemon service is running since.........$XCASH_DAEMON_UP_SINCE${reset} \
        || echo -e ${red}X-Cash Daemon service is not running${reset}

    systemctl is-active $XCASH_WALLET_SRV --quiet \
        && echo -e ${green}X-Cash RPC Wallet service is running since.....$XCASH_WALLET_UP_SINCE${reset} \
        || echo -e ${red}X-Cash RPC Wallet service is not running${reset}

    systemctl is-active $XCASH_DPOPS_SRV --quiet \
        && echo -e ${green}X-Cash DPoPS service is running since..........$XCASH_DPOPS_UP_SINCE${reset} \
        || echo -e ${red}X-Cash DPoPS service is not running${reset}
}

check_height
get_node_balance
check_services_status
echo
```

!!! info
    If you have custom service names you need to adjust the service variable names at the beginning of the script


Then, we need to make it executable

```bash
chmod +x /etc/update-motd.d/00-xcash-node-checks
```

After that, every time we log in to our server by ssh we will see something like this.



