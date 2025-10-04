# Day 07 — Secure & Seamless Access with SSH Key Authentication (100 Days of DevOps)

## 🔑 Task
Configure password-less SSH authentication from a central jump host to all application servers in a multi-user environment.

---

## 🧭 Steps Taken

### 1. Generate Secure SSH Keys
Generate a 4096-bit RSA SSH key pair on the jump host:
```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

### 2. Distribute Keys to App Servers
Copy the public key to each sudo user on all application servers:
```bash
ssh-copy-id user@app_server_1
ssh-copy-id user@app_server_2
ssh-copy-id user@app_server_3
```
*(Replace `user` and `app_server_X` with actual usernames and server addresses.)*

### 3. Verify Password-Free Connections
Test SSH connections to ensure passwordless access:
```bash
ssh user@app_server_1
ssh user@app_server_2
ssh user@app_server_3
```

---

## ✅ Result
- Secure 4096-bit RSA SSH keys generated
- Keys distributed to sudo users on all app servers
- Verified smooth, password-free connections for remote execution

---

## 💡 Reflection
Passwordless SSH authentication boosts security and efficiency, especially for automation scripts running across multiple servers.
