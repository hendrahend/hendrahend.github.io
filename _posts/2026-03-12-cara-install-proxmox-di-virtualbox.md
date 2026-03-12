
---
title: Cara Install Proxmox VE di VirtualBox
tags: [Proxmox, Linux, Server]
style: fill
color: secondary
description: Cara Install Proxmox VE di VirtualBox.
---

Ditulis oleh: [Hendra Hendriana](https://hendrahend.github.io/about)

<br>

{% capture list_items %}
Pendahuluan  
Persiapan  
Membuat VM di VirtualBox  
Konfigurasi VM  
Proses Instalasi  
Hal Yang Perlu Dicatat  
Penutup    
{% endcapture %}
{% include elements/list.html title="Daftar Isi" type="toc" %}

<br>

### Pendahuluan

Proxmox Virtual Environment (Proxmox VE) adalah platform virtualisasi open-source yang memungkinkan kita menjalankan virtual machine (VM) dan container dalam satu sistem. Proxmox banyak digunakan untuk membangun server virtualisasi, homelab, maupun infrastruktur server skala kecil hingga besar.

Jika tidak memiliki server fisik, kita tetap bisa belajar Proxmox dengan menjalankannya di **VirtualBox**. Cara ini cocok untuk keperluan belajar dan eksperimen sebelum menggunakannya di server sebenarnya.

Artikel ini akan membahas cara **install Proxmox VE di VirtualBox** langkah demi langkah. Lanjut ke persiapan

### Persiapan
Sebelum memulai instalasi, siapkan beberapa hal berikut:

-   **VirtualBox** [Download Disini](https://www.virtualbox.org/wiki/Downloads)

- File **ISO Proxmox VE** [Download Disini](https://www.proxmox.com/en/downloads)

-   Minimal spesifikasi VM:
    -   RAM: 4 GB (disarankan 8 GB)
    -   CPU: 2 core
    -   Storage: 32 GB

### Membuat VM Di VirtualBox 

1.  Buka **VirtualBox**
    
2.  Klik **New**
    
3.  Isi konfigurasi berikut:
    
- Nama VM: proxmox
- Type: Linux
- Version: Debian (64-bit)
- RAM: 4096 MB atau lebih
- CPU: 2 Core atau lebih
- Hard Disk
  - VDI  
  - Dynamically Allocated  
  - 32 GB atau lebih

{% capture carousel_images %}
https://bit.ly/2BBbVhc
https://bit.ly/2DOtxXB
{% endcapture %}
{% include elements/carousel.html %}


## Pengaturan Network

Agar Proxmox bisa diakses dari host, ubah network adapter menjadi:

- Bridged Adapter

atau bisa juga menggunakan:

Host Only Adapter

----------


## Proses Instalasi Proxmox

Jalankan VM dan pilih:

Install Proxmox VE

Langkah instalasi:

1.  Accept License Agreement
    
2.  Pilih target disk
    
3.  Tentukan lokasi dan timezone
    
4.  Masukkan password root
    
5.  Masukkan email administrator
    
6.  Konfigurasi network
    

Contoh konfigurasi network:

IP Address : 192.168.1.50  
Gateway : 192.168.1.1

### Mengakses Web Interface Proxmox

Setelah instalasi selesai, Proxmox dapat diakses melalui browser menggunakan alamat:

https://IP-ADDRESS:8006

Contoh:

https://192.168.1.50:8006

Login menggunakan:

Username : root  
Password : (password saat instalasi)


### Hal Yang Perlu Dicatat

Karena Proxmox dijalankan di VirtualBox, fitur **nested virtualization** mungkin tidak berjalan optimal. Oleh karena itu, performa VM di dalam Proxmox bisa terbatas.

Namun cara ini tetap sangat berguna untuk:

-   belajar Proxmox    

-   memahami virtualisasi

-   membuat lab jaringan
    
### Penutup

Proxmox VE dapat dijalankan di VirtualBox untuk keperluan belajar atau eksperimen tanpa harus menggunakan server fisik. Dengan membuat VM di VirtualBox dan memasang ISO Proxmox, kita sudah dapat mencoba berbagai fitur virtualisasi seperti membuat VM dan container.

Meskipun performanya tidak seoptimal server asli, metode ini sangat cocok untuk membangun **lab virtualisasi sederhana**.
