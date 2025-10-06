# Day 09 — MariaDB Service Troubleshooting (100 Days of DevOps)

## 🛠️ Task
Troubleshoot and fix MariaDB service issues inside a Linux environment.

---

## 🧭 Steps Taken

### 1. Resolve Permission Problems
Fix permissions for the MariaDB data directory:
```bash
sudo chown -R mysql:mysql /var/lib/mysql
```

### 2. Restore SELinux Contexts
Restore SELinux contexts for the data directory:
```bash
sudo restorecon -Rv /var/lib/mysql
```

### 3. Restart and Enable MariaDB
Restart MariaDB and enable it to start on boot:
```bash
sudo systemctl restart mariadb
sudo systemctl enable mariadb
```

### 4. Verify Service Status
Check the status of MariaDB:
```bash
sudo systemctl status mariadb
```

---

## ✅ Result
- Permission problems resolved
- SELinux contexts restored
- MariaDB restarted and enabled for persistent availability

---

## 💡 Reflection
Combining Linux permissions, SELinux policies, and service management is crucial for maintaining a healthy database environment.
