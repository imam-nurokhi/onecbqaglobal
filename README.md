# OneCBQA Global — Official Website

> **Your trusted partner for global quality assurance, business auditing, and compliance solutions.**

[![Deploy Status](https://img.shields.io/badge/status-live-brightgreen)](https://onecbqaglobal.com)
[![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![TailwindCSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?logo=tailwind-css&logoColor=white)](https://tailwindcss.com)

---

## Overview

This is the official responsive website for **OneCBQA Global**, a leading quality assurance and business compliance consultancy serving 200+ organizations across 50+ countries.

### Features

- **Fully Responsive** — Mobile-first design, tested at 375px, 768px, 1024px, and 1440px
- **Performance Optimized** — Pure HTML + Tailwind CDN, no build step required
- **Accessible** — WCAG 2.1 AA compliant, keyboard navigation, screen reader friendly
- **Interactive** — Smooth scroll animations, industry tabs, mobile hamburger menu, contact form
- **SEO Ready** — Semantic HTML5, meta tags, OG tags
- **Zero Dependencies** — No framework, no Node.js required to run

### Pages / Sections

| Section | Description |
|---------|-------------|
| Hero | Full-screen landing with CTA and floating cards |
| Stats | Key performance metrics |
| About | Company mission, values, and credentials |
| Services | 6 core service offerings with cards |
| Industries | Tabbed content for 5 industries |
| Clients | Marquee logo carousel |
| Testimonials | Client quotes |
| Team | Leadership team profiles |
| Contact | Contact form with validation |
| Footer | Links, social, certifications |

---

## Tech Stack

| Tool | Purpose |
|------|---------|
| HTML5 | Structure and semantics |
| [Tailwind CSS CDN](https://tailwindcss.com) | Utility-first styling |
| Google Fonts | Poppins + Open Sans typography |
| Vanilla JavaScript | Interactions (no jQuery) |

---

## Local Development

No build step needed — just open the file:

```bash
# Option 1: Direct browser open
open index.html

# Option 2: Local server (recommended for fetch APIs)
npx serve .
# or
python3 -m http.server 8080
# Visit: http://localhost:8080
```

---

## Deployment to VPS (Nginx)

### Prerequisites
- VPS with Ubuntu/Debian
- Nginx installed
- Domain pointed to your VPS IP

### Step 1: Install Nginx (if not installed)

```bash
sudo apt update && sudo apt install -y nginx
```

### Step 2: Upload Website Files

**Option A — Git Pull (Recommended)**
```bash
# On your VPS:
cd /var/www/
sudo git clone https://github.com/YOUR_GITHUB_USERNAME/onecbqaglobal.git
sudo chown -R www-data:www-data /var/www/onecbqaglobal
```

**Option B — rsync (manual upload)**
```bash
# From your local machine:
rsync -avz --delete ./ user@YOUR_VPS_IP:/var/www/onecbqaglobal/
```

### Step 3: Configure Nginx

```bash
sudo nano /etc/nginx/sites-available/onecbqaglobal
```

Paste this configuration:

```nginx
server {
    listen 80;
    listen [::]:80;
    server_name onecbqaglobal.com www.onecbqaglobal.com;

    root /var/www/onecbqaglobal;
    index index.html;

    # Gzip compression
    gzip on;
    gzip_types text/html text/css application/javascript;
    gzip_min_length 1024;

    # Cache static assets
    location ~* \.(css|js|jpg|jpeg|png|gif|svg|ico|woff2)$ {
        expires 1y;
        add_header Cache-Control "public, immutable";
    }

    location / {
        try_files $uri $uri/ =404;
    }

    # Security headers
    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-Content-Type-Options "nosniff";
    add_header X-XSS-Protection "1; mode=block";
    add_header Referrer-Policy "strict-origin-when-cross-origin";
}
```

### Step 4: Enable the Site

```bash
sudo ln -s /etc/nginx/sites-available/onecbqaglobal /etc/nginx/sites-enabled/
sudo nginx -t  # Test config
sudo systemctl reload nginx
```

### Step 5: Enable HTTPS with Let's Encrypt (Free SSL)

```bash
sudo apt install -y certbot python3-certbot-nginx
sudo certbot --nginx -d onecbqaglobal.com -d www.onecbqaglobal.com
sudo certbot renew --dry-run  # Test auto-renewal
```

### Step 6: Auto-Deploy on Git Push (Optional)

Set up a simple deploy hook on your VPS:

```bash
# Create deploy script
sudo nano /var/www/onecbqaglobal/deploy.sh
```

```bash
#!/bin/bash
cd /var/www/onecbqaglobal
git pull origin main
sudo chown -R www-data:www-data .
echo "✅ Deployed at $(date)"
```

```bash
chmod +x /var/www/onecbqaglobal/deploy.sh
```

Then from your local machine to deploy:
```bash
ssh user@YOUR_VPS_IP "sudo /var/www/onecbqaglobal/deploy.sh"
```

---

## Project Structure

```
onecbqaglobal/
├── index.html          # Main website (single-page)
├── assets/
│   ├── css/            # Custom CSS (if extended)
│   ├── js/             # Custom JS (if extended)
│   └── images/         # Images and media
├── nginx.conf          # Nginx server configuration
├── .gitignore
└── README.md
```

---

## Customization

### Brand Colors
Edit the Tailwind config in `index.html`:
```javascript
tailwind.config = {
  theme: {
    extend: {
      colors: {
        primary: '#1E40AF',     // Navy blue
        secondary: '#3B82F6',   // Medium blue
        accent: '#F97316',      // Orange CTA
      }
    }
  }
}
```

### Content
All content is in `index.html`. Search for section comments (`<!-- HERO -->`, `<!-- SERVICES -->`, etc.) to quickly locate and update content.

---

## License

&copy; 2026 OneCBQA Global. All rights reserved.
