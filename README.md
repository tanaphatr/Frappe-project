# 📦 Frappe + ERPNext + LMS + HRMS Installation Guide (v15)

This guide walks you through setting up a full Frappe ecosystem with **ERPNext**, **LMS**, and **HRMS** using Frappe version 15.

---

## ⚙️ Requirements

- Ubuntu 22.04 / Debian / WSL
- Python 3.10+
- Node.js 16+
- Redis
- MariaDB
- wkhtmltopdf (with patched Qt)
- Yarn
- Git, pip, curl

---

## 🔧 Step-by-Step Installation

### 1. System Update

```bash
sudo apt update && sudo apt upgrade -y
```

---

### 2. Install Required Packages

```bash
sudo apt install -y git python3-dev python3.10 python3.10-dev python3.10-venv   python3-pip redis-server mariadb-server mariadb-client   curl xvfb libfontconfig wkhtmltopdf libmysqlclient-dev   libxrender1 libxext6 libx11-6 xfonts-75dpi xfonts-base   nodejs npm
```

---

### 3. Setup MariaDB

```bash
sudo mysql -u root
```

In the MariaDB shell:

```sql
ALTER USER 'root'@'localhost' IDENTIFIED BY 'yourpassword';
FLUSH PRIVILEGES;
EXIT;
```

Replace `'yourpassword'` with your actual desired password.

---

### 4. Install Yarn

```bash
sudo npm install -g yarn
```

---

### 5. Install Bench CLI

```bash
sudo pip3 install frappe-bench
```

---

### 6. Create a Bench

```bash
bench init frappe-bench --frappe-branch version-15
cd frappe-bench
```

---

### 7. Create a New Site

```bash
bench new-site your-site.local
```

Set:
- MySQL root password (from step 3)
- Frappe admin password

---

### 8. Get Applications

```bash
bench get-app learning --branch main https://github.com/frappe/lms
bench get-app frappe_hr --branch version-15 https://github.com/frappe/hrms
bench get-app erpnext --branch version-15
```

---

### 9. Install Apps to Site

```bash
bench --site your-site.local install-app lms
bench --site your-site.local install-app hrms
bench --site your-site.local install-app erpnext
```

---

### 10. Start the Server

```bash
bench start
```

Access it at:
```
http://localhost:8000
```
Or if using `.local`:
```
http://your-site.local:8000
```

---

## 📝 Optional: Add Site to `/etc/hosts`

```bash
sudo nano /etc/hosts
```

Add:

```
127.0.0.1 your-site.local
```

---

## 📌 Notes

- Use `bench start` for development.
- For production, setup Nginx and Supervisor with `bench setup production`.
- Compatible with Ubuntu and WSL.

---

## ✅ Example

```bash
bench init frappe-bench-vasvox --frappe-branch version-15
cd frappe-bench-vasvox
bench new-site vasvox.local
bench get-app learning --branch main https://github.com/frappe/lms
bench get-app frappe_hr --branch version-15 https://github.com/frappe/hrms
bench get-app erpnext --branch version-15
bench --site vasvox.local install-app lms
bench --site vasvox.local install-app hrms
bench --site vasvox.local install-app erpnext
bench start
```

---

## ✨ Result

You will have:
- Frappe Framework (v15)
- ERPNext
- LMS
- HRMS

Running at: `http://localhost:8000`
