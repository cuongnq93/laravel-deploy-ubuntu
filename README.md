# Laravel Deployment Stack for Ubuntu 24.10

[![Laravel](https://img.shields.io/badge/Laravel-10.x-red?logo=laravel)](https://laravel.com)
[![Ubuntu](https://img.shields.io/badge/Ubuntu-24.10-E95420?logo=ubuntu)](https://ubuntu.com)
[![PHP](https://img.shields.io/badge/PHP-8.2-777BB4?logo=php)](https://www.php.net/)
[![Node.js](https://img.shields.io/badge/Node.js-20.x-339933?logo=node.js)](https://nodejs.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> A production-ready Laravel server stack setup on Ubuntu 24.10 with PHP 8.2, Nginx, Node.js 20, Redis, PM2, and Let's Encrypt SSL via Certbot.

---

## 🚀 Stack Overview

| Component      | Version   | Description                          |
|----------------|-----------|--------------------------------------|
| OS             | Ubuntu 24.10 | Server base system                  |
| PHP            | 8.2       | Laravel runtime via PHP-FPM          |
| Laravel        | 10.x      | PHP framework                         |
| Nginx          | Latest    | Web server                            |
| Node.js        | 20.x      | JS runtime for asset compilation      |
| Composer       | Latest    | PHP package manager                   |
| Redis          | Latest    | Cache and queue system                |
| PM2            | Latest    | Process manager for queue workers     |
| Certbot        | Latest    | Let's Encrypt SSL certificates        |

---

## 📦 Installed PHP Extensions

- php-fpm
- php-cli
- php-mysql
- php-mbstring
- php-xml
- php-curl
- php-bcmath
- php-zip
- php-intl
- php-gd
- php-common
- php-tokenizer
- php-readline
- php-redis

---

## 🔧 Global npm Packages

- `pm2`
- `yarn`

---

## 📜 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

## 📘 Full Installation Guide

Please refer to the full step-by-step setup instructions here:

👉 [Laravel_Deployment_Guide_Ubuntu_24.10.md](./Laravel_Deployment_Guide_Ubuntu_24.10.md)
