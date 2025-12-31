---
title: Install Podman di Ubuntu dan Jalankan Nginx sebagai Web Server
tags: [Linux, Ubuntu, Podman, Nginx, Container]
style: fill
color: primary
description: Panduan praktis menginstal Podman di Ubuntu serta menjalankan container Nginx tanpa Docker.
---

Ditulis oleh: [Hendra Hendriana](https://hendrahend.github.io/about)

<br>

{% capture list_items %}
Pendahuluan  
Langkah Instalasi Podman  
Jalankan Nginx dengan Podman  
Penutup  
Referensi  
{% endcapture %}
{% include elements/list.html title="Daftar Isi" type="toc" %}

<br>

### Pendahuluan

**Podman** adalah alat manajemen container open-source yang kompatibel dengan Docker CLI, tetapi berjalan tanpa daemon dan mendukung mode rootless—lebih aman dan ringan.  
Di Ubuntu, Podman mudah diinstal dan cocok untuk menjalankan aplikasi seperti **Nginx** dalam lingkungan container yang terisolasi.

### Langkah Instalasi Podman

#### 1. Perbarui Sistem

Pastikan sistem Anda terbaru:

```bash
sudo apt update && sudo apt upgrade -y
```

#### 2. Install Podman

```bash
sudo apt install podman -y 
```

#### 3. Verifikasi Instalasi

```bash
podman --version
```
Output contoh:

```bash
podman version 3.4.4
```

Sampai disini podman sudah terinstall dengan baik. Selanjutnya kita akan mencoba jalankan nginx untuk dijadikan webserver.

### Langkah Instalasi Nginx di Podman

#### 1. Pull/Tarik image Nginx

```bash
podman pull docker.io/library/nginx:latest

#atau

podman pull docker.io/ubuntu/nginx:latest
```

#### 2. Jalankan Container Nginx

```bash
podman run -d --name web-nginx -p 8080:80 nginx
```

- -d → Menjalankan container dalam mode detached, artinya container tetap berjalan di latar
belakang tanpa mengunci terminal.
- --name web-nginx → Memberikan nama khusus pada container agar mudah diidentifikasi dan
dikelola.
- -p 8080:80 → Melakukan port mapping dari port 8080 di host ke port 80 di dalam container.
Dengan ini, Nginx dapat diakses melalui browser host pada port 8080.
- nginx → Menentukan image yang akan digunakan untuk menjalankan container.

#### 3. Akses Web di browser
Buka browser dan kunjungi http://localhost:8080

### Penutup

Dengan Podman, Anda bisa menjalankan aplikasi container seperti Nginx tanpa menginstal Docker atau menjalankan daemon.
Ini solusi ringan, aman, dan ideal untuk pengembangan lokal maupun server produksi minimalis.

### Referensi
- Podman Official Site
- ID Networkers
