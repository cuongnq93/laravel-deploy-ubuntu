# Laravel Deployment Guide (Ubuntu 24.10)

This guide explains how to install and configure the necessary software to run a Laravel application on Ubuntu 24.10 (2 CPUs / 4GB RAM). This includes PHP 8.2, PHP-FPM, Nginx, Node.js 20, Composer, Redis, PM2, Certbot, and more.

---

## 📁 1. Clone Laravel project

```bash
cd /var/www/html
sudo git clone <your-laravel-repository-url> laravel-app
cd laravel-app
```

Replace `<your-laravel-repository-url>` with the actual Git repository URL.

---

## ⚙️ 2. Install PHP and extensions

```bash
sudo apt update
sudo apt install php -y

sudo apt install php-fpm php-cli php-mysql \
php-mbstring php-xml php-curl php-bcmath php-zip \
php-intl php-gd php-common php-tokenizer php-readline -y
```

---

## 🔌 3. Install Redis and PHP Redis extension

```bash
sudo apt install -y php-redis redis-server
```

---

## 🌐 4. Install and configure Nginx

```bash
sudo apt install -y nginx
```

### Create Nginx site config

```bash
sudo vi /etc/nginx/sites-available/domain.com.conf
```

Paste this configuration:

```nginx
server {
    listen 80;
    server_name domain.com;
    root /var/www/html/laravel-app/public;

    index index.php index.html;
    charset utf-8;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\.(?!well-known).* {
        deny all;
    }
}
```

### Enable the site:

```bash
sudo ln -s /etc/nginx/sites-available/domain.com.conf /etc/nginx/sites-enabled/
sudo nginx -t && sudo systemctl reload nginx
```

> Replace `domain.com` with your actual domain.

---

## 🧱 5. Set directory permissions

```bash
chmod -R 777 bootstrap bootstrap/cache
chmod -R 777 storage storage/app storage/framework storage/logs
chmod -R 777 /var/www/html/laravel-app/storage/framework/views
chmod -R 777 /var/www/html/laravel-app/storage/framework
```

---

## 🧰 6. Install Node.js 20 + PM2 + Yarn

```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs

npm install -g pm2
npm install -g yarn
```

---

## 🎼 7. Install Composer (PHP package manager)

```bash
curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer
composer --version
```

---

## 🔐 8. Install Certbot for free SSL (Let's Encrypt)

```bash
sudo apt install -y certbot python3-certbot-nginx
```

### Run Certbot (HTTPS setup)

```bash
sudo certbot --nginx -d domain.com
```

> Replace `domain.com` with your actual domain. Make sure DNS is pointing to your server.

---

## ✅ Final Steps

- Set up your `.env` file (`cp .env.example .env`)
- Run Laravel setup commands:
  
```bash
composer install
php artisan key:generate
php artisan migrate --force
php artisan config:cache
php artisan route:cache
php artisan view:cache
```

- Restart services:

```bash
sudo systemctl restart php8.2-fpm
sudo systemctl restart nginx
```

---

## 🧠 Notes

- This setup uses `php-fpm.sock` for Nginx <-> PHP communication
- PM2 can be used to manage Laravel queues or background jobs
- Ensure file permissions are correctly set for `storage` and `bootstrap/cache`
- Use `supervisor` or `pm2` to manage `queue:work` in production

---

Happy coding! 🚀
