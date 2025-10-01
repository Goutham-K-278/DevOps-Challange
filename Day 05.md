# Day 05 — SELinux Setup on App Server 3 (100 Days of DevOps)

## 🛡️ Task
Enhance server security by setting up SELinux on **App Server 3**.

---

## 🧭 Steps Taken

### 1. Connect to App Server 3
Log in to the target server:
```bash
ssh user@app_server_3
```
*(Replace `user` and `app_server_3` with your actual username and server address.)*

### 2. Install SELinux Packages
Install the required SELinux packages:
```bash
sudo yum install -y selinux-policy selinux-policy-targeted policycoreutils
```
Or for Debian/Ubuntu systems:
```bash
sudo apt-get install -y selinux selinux-policy-default policycoreutils
```

### 3. Check SELinux Status
Verify the current SELinux status:
```bash
sestatus
```
Or:
```bash
getenforce
```

### 4. Update SELinux Configuration
Edit the SELinux configuration file to disable it temporarily (as per the audit plan):
```bash
sudo vi /etc/selinux/config
```
Change the following line:
```
SELINUX=disabled
```
Save and exit the file.

### 5. Prepare for Maintenance Reboot
SELinux changes require a reboot to take effect. Ensure everything is ready for the next scheduled maintenance reboot.

---

## ✅ Result
- SELinux packages installed
- Configuration updated to temporarily disable SELinux
- System ready for next maintenance reboot

---

## 💡 Reflection
Setting up SELinux is a key step in hardening server security. For this audit, SELinux was disabled temporarily, but the system is now prepared for future policy enforcement and compliance.
