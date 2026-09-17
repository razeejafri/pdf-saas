# VPS Deployment & GitHub Actions CI/CD Guide

Is guide se aap apne VPS (Ubuntu/Debian) par PDF SaaS ko setup karke automatic GitHub Actions deployment activate kar sakte hain.

---

## 📋 1. VPS Par One-Time Server Setup

VPS me login karein (`ssh root@your-vps-ip`):

```bash
# System Update
sudo apt update && sudo apt upgrade -y

# Docker & Docker Compose Install karein
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo apt install -y docker-compose-plugin git

# Verify Docker
docker --version
docker compose version
```

---

## 📁 2. Project Directory Setup on VPS

```bash
# Directory banayein (e.g. /var/www/pdf-saas)
sudo mkdir -p /var/www/pdf-saas
sudo chown -R $USER:$USER /var/www/pdf-saas

# Repository Clone karein
git clone https://github.com/<YOUR_GITHUB_USERNAME>/<YOUR_REPO>.git /var/www/pdf-saas
cd /var/www/pdf-saas

# Environment file create karein
mkdir -p apps/web
cat << 'EOF' > apps/web/.env
NODE_ENV=production
NEXT_PUBLIC_APP_URL=https://yourdomain.com
EOF

# Initial Docker Build test karein
docker compose up -d --build
```

---

## 🔑 3. GitHub Actions SSH Key Setup

GitHub Actions ko aapke VPS se connect karne ke liye ek dedicated SSH Key banayein:

### Step A: VPS par key generate karein
```bash
ssh-keygen -t ed25519 -C "github-actions-pdf-saas" -f ~/.ssh/github_actions_deploy -N ""
```

### Step B: Public key ko authorized_keys me add karein
```bash
cat ~/.ssh/github_actions_deploy.pub >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
chmod 700 ~/.ssh
```

### Step C: Private Key copy karein
```bash
cat ~/.ssh/github_actions_deploy
```
*(Poora output copy karein `-----BEGIN OPENSSH PRIVATE KEY-----` se `-----END OPENSSH PRIVATE KEY-----` tak)*

---

## ⚙️ 4. GitHub Repository Secrets Add Karein

Apne GitHub Repo par jayein: **Settings** → **Secrets and variables** → **Actions** → **New repository secret**:

| Secret Name | Value Example | Description |
|---|---|---|
| `VPS_HOST` | `123.45.67.89` | Aapke VPS ka Public IP |
| `VPS_USER` | `root` ya `ubuntu` | VPS username |
| `VPS_SSH_KEY` | `-----BEGIN OPENSSH PRIVATE KEY----- ...` | Step 3 me copy ki hui private key |
| `VPS_PORT` | `22` | SSH Port (default 22) |
| `VPS_DEPLOY_PATH` | `/var/www/pdf-saas` | VPS par project ka path |

---

## 🌐 5. Nginx & Domain SSL Setup (Optional but Recommended)

Agar domain connect karna hai:

```bash
sudo apt install -y nginx certbot python3-certbot-nginx
```

Nginx config `/etc/nginx/sites-available/pdf-saas`:
```nginx
server {
    server_name yourdomain.com www.yourdomain.com;

    # Allow large PDF uploads (e.g. 100MB)
    client_max_body_size 100M;

    location / {
        proxy_pass http://127.0.0.1:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

Enable karein aur SSL lagayein:
```bash
sudo ln -s /etc/nginx/sites-available/pdf-saas /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx

# Free SSL (HTTPS) Certificate:
sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com
```

---

## ⚡ 6. Kaise Test Karein?

Apne local PC se code push karein:
```bash
git add .
git commit -m "ci: add vps auto deployment workflow"
git push origin main
```
GitHub Actions tab par jayein — workflow run hoga aur automatic aapke VPS par latest code pull karke Docker restart kar dega!
