# Day 01: Create a Linux User with Non-Interactive Shell

## Goal
Create a system/service user that cannot get an interactive shell (for safe use by services/automation). Provide key-based access if needed and verify the setup.

## Prerequisites
- SSH access to the remote server as a user with sudo/root
- A public SSH key (if enabling key-based access)
- Knowledge of your Linux distro (paths differ between RHEL/CentOS and Debian/Ubuntu)

**Common non-interactive shells:**
- RHEL/CentOS: `/sbin/nologin`
- Debian/Ubuntu: `/usr/sbin/nologin`
- Portable fallback: `/bin/false`

---

## Step-by-Step Instructions

### 1. Connect to the Remote Server
```sh
ssh ADMIN_USER@REMOTE_HOST
```

### 2. Detect nologin Path
```sh
ls -l /sbin/nologin /usr/sbin/nologin 2>/dev/null || echo "/bin/false (no nologin found)"
```

### 3. Create the User with Non-Interactive Shell
Using `useradd` (works on most distros):
```sh
sudo useradd -m -s /sbin/nologin deployuser
```
- `-m`: create home directory `/home/deployuser`
- `-s /sbin/nologin`: sets login shell to disable interactive login

Debian `adduser` alternative:
```sh
sudo adduser --disabled-password --shell /usr/sbin/nologin --gecos "" deployuser
```
- `--disabled-password`: disables password login

### 4. Lock the Account Password
```sh
sudo passwd -l deployuser
# or
sudo usermod -L deployuser
```

### 5. (Optional) Add Public SSH Key
```sh
sudo mkdir -p /home/deployuser/.ssh
sudo tee /home/deployuser/.ssh/authorized_keys > /dev/null <<'EOF'
ssh-rsa AAAA... your-public-key-comment
EOF
sudo chmod 700 /home/deployuser/.ssh
sudo chmod 600 /home/deployuser/.ssh/authorized_keys
sudo chown -R deployuser:deployuser /home/deployuser/.ssh
```

### 6. Verify User Entry in /etc/passwd
```sh
getent passwd deployuser
```
**Expected output:**
```
deployuser:x:1001:1001::/home/deployuser:/sbin/nologin
```

### 7. Check UID/GID and Groups
```sh
id deployuser
```
**Example:**
```
uid=1001(deployuser) gid=1001(deployuser) groups=1001(deployuser)
```

### 8. Inspect .ssh Directory Permissions
```sh
ls -ld /home/deployuser /home/deployuser/.ssh /home/deployuser/.ssh/authorized_keys
```

### 9. Test Interactive SSH (Should Fail)
```sh
ssh deployuser@REMOTE_HOST
```
**Expected:** "This account is currently not available." or disconnect

### 10. (Optional) SFTP-Only Access
Edit `/etc/ssh/sshd_config`:
```
Match User deployuser
    ChrootDirectory /home/deployuser
    ForceCommand internal-sftp
    AllowTCPForwarding no
    X11Forwarding no
```
Set chroot directory ownership:
```sh
sudo chown root:root /home/deployuser
sudo mkdir -p /home/deployuser/uploads
sudo chown deployuser:deployuser /home/deployuser/uploads
```
Restart SSH:
```sh
sudo systemctl restart sshd
```

---

## Final Verification (Example Outputs)
- `getent passwd deployuser`:
  - `deployuser:x:1001:1001::/home/deployuser:/sbin/nologin`
- `id deployuser`:
  - `uid=1001(deployuser) gid=1001(deployuser) groups=1001(deployuser)`
- `ls -ld /home/deployuser/.ssh`:
  - `drwx------ 2 deployuser deployuser 4096 Sep 22 12:39 /home/deployuser/.ssh`
- Interactive SSH:
  - "This account is currently not available."

These confirm: user exists, has a home directory, SSH keys installed, and interactive shell access is disabled.
