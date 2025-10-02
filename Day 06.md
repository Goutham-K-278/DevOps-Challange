# Day 06 — Automating Server Tasks with Cron (100 Days of DevOps)

## 🤖 Task
Configure scheduled automation for application servers using cron in a simulated production environment.

---

## 🧭 Steps Taken

### 1. Install Cronie Package
Install the cronie package (for RHEL/CentOS):
```bash
sudo yum install -y cronie
```
Or for Debian/Ubuntu systems:
```bash
sudo apt-get install -y cron
```

### 2. Enable and Start the crond Service
Enable and start the cron daemon:
```bash
sudo systemctl enable crond
sudo systemctl start crond
```
For Debian/Ubuntu:
```bash
sudo systemctl enable cron
sudo systemctl start cron
```

### 3. Set Up a Root-Level Cron Job
Edit the root user's crontab to run a job every 5 minutes:
```bash
sudo crontab -e
```
Add the following line:
```
*/5 * * * * /path/to/your/script.sh
```
*(Replace `/path/to/your/script.sh` with the actual script path.)*

### 4. Verify Cron Job Configuration
List the current root cron jobs:
```bash
sudo crontab -l
```
Check the cron service status:
```bash
sudo systemctl status crond
```
Or for Debian/Ubuntu:
```bash
sudo systemctl status cron
```

### 5. Ensure Consistency Across All Servers
Repeat the above steps on all application servers to ensure consistent automation.

---

## ✅ Result
- Cronie package installed and configured
- crond service enabled and running
- Root-level cron job scheduled every 5 minutes
- Consistent configuration across all servers

---

## 💡 Reflection
Automating server tasks with cron is essential for reliable operations in production environments. Consistent configuration ensures tasks run smoothly and maintenance is simplified.
