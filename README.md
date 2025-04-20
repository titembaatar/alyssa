# LXC Programming Environment Setup

This guide covers setting up a secure programming environment in an LXC container with two user accounts and SSH access.

## Initial Setup

### 1. Update the system and install required packages

```bash
apt update && apt upgrade -y
apt install sudo openssh-server fail2ban ufw -y
```

### 2. Create user accounts

```bash
adduser <user>
usermod -aG sudo <user>
```

### 3. Set up SSH on custom port

```bash
nano /etc/ssh/sshd_config
```

Modify or add these settings in the SSH configuration file:
```
# Change SSH port from 22 to <port>
Port <port>

# We'll set these security settings AFTER adding SSH keys
# PermitRootLogin no
# PasswordAuthentication no 
# PubkeyAuthentication yes
# AllowUsers <user> # <user>...
```

Restart SSH service with the new port:
```bash
systemctl restart sshd
```

### 4. Set up SSH keys for Linux/Mac

**On your local Linux/Mac machine:**

```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "mail@address.com"
ssh-copy-id -i ~/.ssh/id_ed25519.pub <user>@<lxc-ip>
```

### 5. Set up SSH keys for Windows

**On your local Windows machine:**
Key will be at `C:\Users\<user>/.ssh/id_ed25519.pub`

```bash
# Generate SSH key
ssh-keygen
type $env:USERPROFILE\.ssh\id_ed25519.pub | ssh <lxc-ip> "cat >> .ssh/authorized_keys"
```

### 6. Test SSH access with keys before securing further

On your local machine, test connecting with your key:
```bash
ssh -p <port> <user>@<lxc-ip>
```

### 7. Secure SSH configuration

Once you've confirmed both users can log in with key authentication, secure SSH:

```bash
# Edit SSH configuration
sudo nano /etc/ssh/sshd_config
```

Now add/uncomment these security settings:
```
Port <port>
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
AllowUsers <user> # <user>...
```

Restart SSH to apply changes:
```bash
sudo systemctl restart sshd
```

## Firewall Configuration

Set up the firewall to only allow necessary connections:

```bash
sudo ufw allow <port>/tcp
sudo ufw enable
sudo ufw status verbose
```

## Fail2Ban Setup

Configure Fail2Ban to protect against brute force attacks:

```bash
sudo nano /etc/fail2ban/jail.d/ssh.conf
```

Add this configuration:
```
[sshd]
enabled = true
port = <port>
filter = sshd
logpath = /var/log/auth.log
maxretry = 3
findtime = 600
bantime = 3600
```

Start and enable Fail2Ban:
```bash
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
sudo fail2ban-client status sshd
```

## Router Configuration

Configure port forwarding on your router:
- Forward external port <port> to your LXC container's IP address on port <port>

## Connection Instructions for Users

Connect to the LXC from outside your network:
```bash
ssh -p <port> -i ~/.ssh/id_ed25519 <user>@your-public-ip
```

