# 🧠 Product Manager OS  
A self-hosted productivity & automation toolkit for Product Managers

Product Manager OS bundles essential tools into one deployable stack so PMs can automate workflows, track insights, manage data, and visualize dashboards — **all on your own VPS**.

Included tools:
- **n8n** → Automation & workflows  
- **NocoDB** → Database + no-code backend  
- **Metabase** → Business dashboards & analytics  
- **Flowise (optional)** → Build AI assistants  
- **Qdrant (optional)** → Vector DB for AI apps  
- **Webmin** → Server administration  
- **Portainer** → Docker management  
- **NGINX Proxy Manager** → Domains + SSL

---

## 🚀 Deployment Guide

Follow these steps to deploy Product Manager OS from scratch 👇  

---

### 1️⃣ Buy a VPS
Choose any provider:
- Hetzner, DigitalOcean, Linode, Vultr, Namecheap, Contabo…  
Recommended specs:
```text
CPU: 2 cores  
RAM: 4 GB minimum  
Disk: 40 GB+  
OS: Ubuntu 22.04 LTS
```

---

### 2️⃣ Buy a Domain + Connect to Cloudflare
1. Buy a domain name (Namecheap, GoDaddy, etc.)
2. Create a Cloudflare account → Add your domain
3. Replace DNS nameservers with Cloudflare’s values

Cloudflare now manages your DNS + SSL 🔐

---

### 3️⃣ Connect to Your VPS via SSH (PuTTY on Windows)
- Download PuTTY: https://www.putty.org/
- Enter your VPS IP
- Login as:
```text
username: root
password: provided by VPS host
```

---

### 4️⃣ Install Core Packages (Docker + Webmin + Portainer)

Run the following:

```bash
apt update && apt upgrade -y

# Check the last version supported by portainer from here
https://docs.portainer.io/start/requirements-and-prerequisites

# Install Docker + Docker Compose
# Select install specific version from
https://docs.docker.com/engine/install/ubuntu/

# Install Webmin
https://webmin.com/download/

# Install Portainer
https://docs.portainer.io/start/install-ce/server/docker/linux#docker-run
```

---

### 5️⃣ Create a project folder using Webmin

1. Open Webmin: `https://your-server-ip:10000`
2. Navigate to **File Manager**
3. Create a folder:
```text
/product-manager-os/
```
4. Open **Terminal** inside Webmin → run:
```bash
cd product-manager-os
```

---

### 6️⃣ Clone the GitHub Repository

```bash
git clone https://github.com/IhabTag/Product-Manager-OS .
```

Edit `.env.example` → rename to `.env` and set passwords, domain names, etc.

---

### 7️⃣ Deploy using Docker Compose

```bash
docker compose up -d
```

Check running containers on portainer

---

### 8️⃣ Configure Cloudflare DNS Subdomains

Add DNS `A` records → point to VPS IP:

| Subdomain | Tool |
|----------|------|
| `n8n.example.com` | n8n |
| `db.example.com` | NocoDB |
| `dash.example.com` | Metabase |
| `webmin.example.com` | Webmin |
| `portainer.example.com` | Portainer |
| `proxy.example.com` | NGINX Proxy Manager |
| `vector.example.com` | Qdrant (optional) |

> ⚠️ Replace `example.com` with your real domain

Cloudflare settings per DNS:
- **Proxy: ON** (orange cloud)
- Auto SSL enabled ✔️

---

### 9️⃣ Access NGINX Proxy Manager & Change Default Login
Visit:
```text
http://proxy.example.com
```

Default login:
```text
Email:    admin@example.com
Password: changeme
```

➡️ Change password immediately! 🔐

---

### 🔟 Configure Reverse Proxies in NGINX

Create one proxy host per subdomain:

| Subdomain | Forward Host | Forward Port |
|----------|---------------|--------------|
| `n8n.example.com` | n8n | 5678 |
| `db.example.com` | nocodb | 8080 |
| `dash.example.com` | metabase | 3000 |
| `webmin.example.com` | VPS IP | 10000 |
| `portainer.example.com` | portainer | 9000 |
| `vector.example.com` | qdrant | 6333 |

Enable:
✔ Force SSL  
✔ HTTP/2  
✔ HSTS  

---

### 1️⃣1️⃣ Test All Tools

| Tool | URL | Login |
|------|----|------|
| n8n | https://n8n.example.com | Your credentials |
| NocoDB | https://db.example.com | Setup on first visit |
| Metabase | https://dash.example.com | Setup on first visit |
| Portainer | https://portainer.example.com | Set admin password |
| Webmin | https://webmin.example.com | system root login |
| NGINX | https://proxy.example.com | admin login |
| Qdrant (optional) | https://vector.example.com | API access |

If everything loads — 🎉  
**Product Manager OS is live!**

---

## 🧩 What You Can Build

✔ Automate workflows (leads → Slack → email → dashboards)  
✔ Central database for customer feedback & experiments  
✔ Product metrics dashboards  
✔ AI helpers for PM workflows  
✔ Self-hosted productivity toolkit  
✔ No SaaS lock-in, full control

---

## 🛠 Maintenance

Update everything:
```bash
docker compose pull
docker compose up -d
```

View logs:
```bash
docker compose logs -f
```

Restart:
```bash
docker compose restart
```

---

## 💬 Support

Found an issue? Got an idea?  
Open GitHub Issues → we’ll improve this together!

---

## ⭐️ Star the Repo!

If Product Manager OS helps you — please support the project:

👉 https://github.com/IhabTag/Product-Manager-OS ⭐️

---

Happy Building!  
Empower your Product Management. 🚀

