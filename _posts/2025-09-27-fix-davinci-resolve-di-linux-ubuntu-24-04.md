---
title: Fix Davinci Resolve di Linux (Ubuntu 24.04)
tags: [Linux, Ubuntu, Davinci Resolve]
style: fill
color: danger
description: Tutorial memperbaiki Davinci Resolve di Ubuntu 24.04 dengan memakai library secara manual.
---

Ditulis oleh: [Hendra Hendriana](https://hendrahend.github.io/about)

<br>

{% capture list_items %}
Pendahuluan  
Langkah Perbaikan
Referensi  
{% endcapture %}
{% include elements/list.html title="Daftar Isi" type="toc" %}

<br>

### Pendahuluan

Di **Ubuntu 24.04**, **Davinci Resolve** gagal berjalan karena beberapa library grafis bawaan hilang/berubah.  
Kita bisa memperbaikinya **tanpa menginstal .deb langsung**, melainkan mengekstrak dan menguji library terlebih dahulu.  
Metode ini aman karena tidak merusak sistem utama.

### Langkah Perbaikan

#### 1. Download Paket Library

Unduh paket `.deb` dari Ubuntu Jammy (22.04) berikut:

- [libpango](https://packages.ubuntu.com/jammy-updates/libpango-1.0-0)  
- [libpangoft2](https://packages.ubuntu.com/jammy-updates/libpangoft2-1.0-0)  
- [libpangocairo](https://packages.ubuntu.com/jammy-updates/libpangocairo-1.0-0)  
- [libgdk-pixbuf](https://packages.ubuntu.com/jammy-updates/libgdk-pixbuf2.0-0)

Semua file `.deb` akan berada di folder yang sama, yaitu `~/Downloads`.

#### 2. Ekstrak ke Folder Sementara

Daripada langsung install, kita ekstrak dulu:

```bash
mkdir -p /tmp/dr/files
dpkg-deb -x namapaket.deb /tmp/dr/files/
```
> Ganti namapaket.deb sesuai file yang diunduh, jalankan perintah ini untuk tiap paket.

#### 3. Jalankan Resolve dari Terminal

Tes Resolve dengan menambahkan path library hasil ekstrak:

```bash
LD_LIBRARY_PATH=/tmp/dr/files/usr/lib/x86_64-linux-gnu /opt/resolve/bin/resolve
```

Jika Resolve bisa dibuka tanpa error berarti library sudah cocok.

#### 4. Salin Library ke Folder libs

Agar permanen, salin library ke folder libs Davinci Resolve:

```bash
sudo cp /tmp/dr/files/usr/lib/x86_64-linux-gnu/lib* /opt/resolve/libs
```

### Referensi
- [Blackmagic Forum](https://forum.blackmagicdesign.com/viewtopic.php?f=38&t=200276)
- [Youtube](https://www.youtube.com/watch?v=Y87MFmcy3lc) 
- [Ubuntu Packages](https://packages.ubuntu.com/jammy-updates/)  
