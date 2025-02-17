---
title: Fix Brightness di Linux Dual GPU
tags: [Linux]
style: fill
color: info
description: Fix Brightness di Linux Dual GPU (temporary)
---

Ditulis Oleh: [Hendra Hendriana](https://hendrahend.github.io/about)

<br>
{% capture list_items %}
Pendahuluan
PopOS! (systemd boot)
Other Linux
Sumber & Referensi
{% endcapture %}
{% include elements/list.html title="Daftar Isi" type="toc" %}

<br>

## Pendahuluan

Masalah brightness slider yang tidak berfungsi sering terjadi pada laptop dengan dual GPU (misalnya, AMD + NVIDIA) di Linux. Jika Anda mengalami hal ini, Anda tidak sendirian.

Setelah mencari solusi, ditemukan beberapa penyebab umum, seperti konflik antara driver GPU dan power management. Artikel ini membahas solusi sementara untuk mengatasi masalah ini.

---

## Pop!_OS (systemd boot)

Karena saya menggunakan Pop!_OS, berikut cara yang saya coba:

### 1. Cek Driver GPU
Pastikan driver GPU sudah terinstal dengan benar.

```bash
lspci | grep -E "VGA|3D"
```

### 2. Cek Display Output

```bash
xrandr --listmonitors
```

### 3. Coba Edit Manual Brightness File
Edit file di `/sys/class/backlight/...` (sesuaikan path-nya):

```bash
sudo nano /sys/class/backlight/intel_backlight/brightness
```

Jika cara ini tidak berhasil, lanjut ke langkah berikutnya.

### 4. Gunakan `xrandr`

```bash
xrandr --output eDP --brightness 0.8
```

### 5. Install `brightnessctl` dan Buat Script Bash

Install `brightnessctl` terlebih dahulu:

```bash
sudo apt install brightnessctl
```

Buat tiga script berikut untuk meningkatkan, menurunkan, dan mereset brightness:

**Script untuk meningkatkan brightness (`inc.sh`)**
```bash
#!/bin/bash
inc=5
sudo brightnessctl set ${inc}%+
br=$(brightnessctl get)
br=$(echo "scale=2; $br / 100" | bc -l)
xrandr --output eDP --brightness "$br"
```

**Script untuk menurunkan brightness (`dec.sh`)**
```bash
#!/bin/bash
dec=5
sudo brightnessctl set ${dec}%-
br=$(brightnessctl get)
br=$(echo "scale=2; $br / 100" | bc -l)
xrandr --output eDP --brightness "$br"
```

**Script untuk mereset brightness (`res.sh`)**
```bash
#!/bin/bash
br=$(sudo brightnessctl get)
br=$(echo "scale=2; $br / 100" | bc -l)
xrandr --output eDP --brightness "$br"
```

> `res.sh` digunakan untuk mengembalikan brightness setelah booting.

Ubah permission script agar bisa dieksekusi:

```bash
chmod +x inc.sh dec.sh res.sh
```

### 6. Tambahkan `brightnessctl` ke `sudoers`

Buka file sudoers:

```bash
sudo visudo
```

Tambahkan baris berikut di bagian paling bawah:

```bash
namauser ALL=(ALL) NOPASSWD: /usr/bin/brightnessctl
```

### 7. Buat Shortcut Keyboard
Atur shortcut keyboard untuk menjalankan `inc.sh` dan `dec.sh`. Setiap distro memiliki cara pengaturan keyboard shortcut yang berbeda.

---

## Distro Linux Lainnya

Di beberapa forum Linux, metode berikut sering direkomendasikan:

### 1. Edit GRUB
Tambahkan parameter `acpi_video`:

Buka konfigurasi GRUB:

```bash
sudo nano /etc/default/grub
```

Cari baris berikut:

```bash
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
```

Tambahkan opsi berikut:

```bash
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash acpi_backlight=video"
```

Simpan dan update GRUB:

```bash
sudo update-grub
sudo reboot
```

---

## Sumber & Referensi

- Teman
- [Linux Mint Forum](https://forums.linuxmint.com/viewtopic.php?t=320955)

---

Donee! 🚀
