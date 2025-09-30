# Day 04 — Make a Script Executable (100 Days of DevOps)

## 📝 Task
Make a script executable on **App Server 2**.

---

## 🧭 Steps Taken

### 1. Connect to App Server 2
Log in to the target server:
```bash
ssh user@app_server_2
```
*(Replace `user` and `app_server_2` with your actual username and server address.)*

### 2. Switch to Root (if needed)
Elevate privileges to root for permission changes:
```bash
sudo -i
```

### 3. Check for the Script File
Before changing permissions, always verify the file exists:
```bash
ls -l /path/to/script.sh
```
If the file does not exist, you’ll see an error like:
```
ls: cannot access '/path/to/script.sh': No such file or directory
```

### 4. (If Needed) Create or Upload the Script
If the script is missing, create it or upload it to the server:
```bash
echo "#!/bin/bash
echo 'Hello, World!'" > /path/to/script.sh
```

### 5. Make the Script Executable
Change the file permissions to make it executable:
```bash
chmod +x /path/to/script.sh
```

### 6. Verify Permissions
Check that the script is now executable:
```bash
ls -l /path/to/script.sh
```
Expected output:
```
-rwxr-xr-x 1 root root ... /path/to/script.sh
```

### 7. Run the Script
Test the script to confirm it works:
```bash
/path/to/script.sh
```
Expected output:
```
Hello, World!
```

---

## 💡 Reflection
This task was a reminder: **always check if the file exists before changing permissions!**

- Checked permissions
- Switched to root
- Realized the file was missing
- Created/uploaded the script
- Made it executable
- Verified and ran the script

A simple but important lesson in troubleshooting and workflow.
