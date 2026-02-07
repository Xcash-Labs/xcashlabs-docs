---
description: >-
  This section provides steps for managing the services around the xcash-dpops
  program, viewing logs, and monitoring activity.
---

# Management & Monitoring

## Managing Installation

You can manage your installation using the installer script:

```bash
bash -c "$(curl -sSL https://raw.githubusercontent.com/X-CASH-official/xcash-dpops/master/scripts/autoinstaller/autoinstaller.sh)"
```

The installer script allows you to install, update, and manage your `xcash-dpops` node.

## Restart Program

If you need to restart services after making changes or troubleshooting:

Run the installer and choose **option 12**.

```bash
bash -c "$(curl -sSL https://raw.githubusercontent.com/X-CASH-official/xcash-dpops/master/scripts/autoinstaller/autoinstaller.sh)"
```

## Update Program

When a new version is released:

Run the installer and choose **option 2**.

```bash
bash -c "$(curl -sSL https://raw.githubusercontent.com/X-CASH-official/xcash-dpops/master/scripts/autoinstaller/autoinstaller.sh)"
```

## Change Delegate Mode

To switch between **solo** and **shared** delegate modes, or to update fee and payout settings:

Run the installer and choose:

- **Option 9** — change delegate mode  
- **Option 10** — update fee or minimum payout

```bash
bash -c "$(curl -sSL https://raw.githubusercontent.com/X-CASH-official/xcash-dpops/master/scripts/autoinstaller/autoinstaller.sh)"
```

You will be prompted to enter:

- Delegate fee  
- Minimum payout amount

The script will update the configuration automatically.

!!! warning
    If you change your delegate fee, remember to update your public delegate information as well.

## Backup Shared Delegate Database

Shared delegates store voter payout data locally.  
Before updating or performing maintenance, you should back up this data.

Run the installer and choose **option 19**:

```bash
bash -c "$(curl -sSL https://raw.githubusercontent.com/X-CASH-official/xcash-dpops/master/scripts/autoinstaller/autoinstaller.sh)"
```

## Recover Mode

Recover mode allows you to update your delegate public address or VRF key if needed.

1. Create a DNS TXT record for your delegate domain.
2. Set the value to one or both of the following:

```
xcash-dpops:NEW_PUBLIC_ADDRESS
xcash-dpops:NEW_VRF_KEY
```

3. From any wallet, run:

```bash
delegate_recover yourdomain.com
```

The system will update the delegate configuration automatically.

## systemd Services

Linux uses **systemd** to manage background services.  
Your node services run automatically using systemd unit files.

Unit files are typically located at:

```
/lib/systemd/system/
```

### Core Services

- `xcash-dpops`
- `xcash-daemon`
- `xcash-rpc-wallet`
- `mongodb`
- `firewall`

## Service Management

### Start a service

```bash
systemctl start SERVICE
```

Example:

```bash
systemctl start xcash-dpops
```

### Restart a service

```bash
systemctl restart SERVICE
```

### Stop a service

```bash
systemctl stop SERVICE
```

### Check status

```bash
systemctl status SERVICE
```

Example:

```bash
systemctl status mongodb
```

## Monitoring Logs

To monitor logs in real time:

```bash
journalctl --unit=SERVICE --follow -n 100 --output cat
```

Examples:

```bash
journalctl --unit=xcash-dpops --follow -n 100 --output cat
journalctl --unit=xcash-daemon --follow -n 100 --output cat
journalctl --unit=xcash-rpc-wallet --follow -n 100 --output cat
journalctl --unit=mongodb --follow -n 100 --output cat
journalctl --unit=firewall --follow -n 100 --output cat
```

Daemon log file:

```bash
tail -n 100 ~/xcash-official/logs/xcash-daemon-log.txt
```

## Optional: Login Status Script

You can display basic node status when logging into your server.

Disable default login scripts:

```bash
chmod -x /etc/update-motd.d/*
```

Create a new script:

```bash
nano /etc/update-motd.d/00-xcash-node-checks
```

Paste your monitoring script inside, then make it executable:

```bash
chmod +x /etc/update-motd.d/00-xcash-node-checks
```

On login via SSH, the system can display:

- Sync status  
- Wallet balance  
- Service status

## Notes

- Adjust service names if using custom ones.
- Always back up before updating.
- Monitor logs regularly for stability.
