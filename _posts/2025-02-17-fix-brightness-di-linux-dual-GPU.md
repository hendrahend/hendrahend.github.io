---
title: Fix Brightness di Linux Dual GPU
tags: [Linux]
style: fill
color: info
description: Sedikit Cara Untuk Fix Brightness di Linux Jika Memakai Laptop Dual GPU.
---

Ditulis Oleh: [Hendra Hendriana](https://hendrahend.github.io/about)

<br>
{% capture list_items %}
Pendahuluan
PopOS
Distro Linux Lain
Update
Sumber & Referensi
{% endcapture %}
{% include elements/list.html title="Daftar Isi" type="toc" %}

<br>

### Pendahuluan

Berawal dari masalah ketika menginstal beberapa distro Linux, tetapi brightness slider tidak berfungsi. Jika kalian menggunakan laptop dengan dual GPU (misalnya, AMD + NVIDIA) dan mengalami masalah yang sama, tenang anda tidak sendirian.

Setelah sana sini mencari solusi, ditemukan beberapa penyebab umum, seperti konflik antara driver GPU dan power management. Artikel ini membahas solusi untuk mengatasi masalah tersebut.

---

### PopOS

Karena saya menggunakan distro PopOS!, saya hanya menemukan satu cara yang bisa dibilang agak kurang.., tetapi cukup oke lah daripada gak bisa atur brightnessnya :v.

#### 1. Cek Driver GPU
Langkah pertaka adalah cek driver GPU sudah terinstal dengan benar. PopOS! menggunakan builtin driver package yaitu

```bash
nvidia-smi #cek driver nvidia 
system76-driver-nvidia # install driver nvidia
```

#### 2. Cek Display Output
Cek nama display output yang digunakan (biasanya eDP untuk layar laptop).

```bash
xrandr --listmonitors
```

#### 3. Edit Manual Brightness
Coba cek file path backlight untuk mengatur brightness secara manual:
```bash
sudo nano /sys/class/backlight/... # sesuaikan dengan path yang sesuai
```
Contoh punyaku
```bash
sudo nano /sys/class/backlight/nvidia_wmi_ec_backlight/brightness # coba ganti valuenya lalu save
```

Jika cara ini tidak berhasil, lanjut ke langkah berikutnya.

#### 4. Gunakan `xrandr`
Jika cara di atas tidak berhasil, gunakan `xrandr` :
```bash
xrandr --output eDP --brightness 0.8 # eDP ganti sesuai poin no 2 
```
>Angka 0.7 bisa disesuaikan sesuai kebutuhan.

#### 5. Install `brightnessctl` dan Buat Script Bash

Install `brightnessctl` terlebih dahulu:

```bash
sudo apt install brightnessctl
```

Buat tiga script berikut untuk meningkatkan, menurunkan, dan merestore brightness:

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

**Script untuk merestore brightness (`res.sh`)**
```bash
#!/bin/bash
br=$(sudo brightnessctl get)
br=$(echo "scale=2; $br / 100" | bc -l)
xrandr --output eDP --brightness "$br"
```

> Ganti eDP sesuai poin no2 untuk setiap script

Ubah permission script agar bisa dieksekusi:

```bash
chmod +x inc.sh dec.sh res.sh
```

#### 6. Tambahkan `brightnessctl` ke `sudoers`

Buka file sudoers:

```bash
sudo visudo
```

Tambahkan baris berikut di bagian paling bawah:

```bash
namauser ALL=(ALL) NOPASSWD: /usr/bin/brightnessctl
```
> `namauser` ganti sesuai username masing-masing

#### 7. Buat Shortcut Keyboard
Atur shortcut keyboard untuk menjalankan `inc.sh` dan `dec.sh`. Setiap distro biasanya memiliki pengaturan keyboard shortcut.

> Panggil `res.sh` di startup application.

---

### Distro Linux Lain

Di beberapa forum Linux, metode berikut sering direkomendasikan:

#### 1. Edit GRUB
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

### Update
Update `19 Februari 2025`, akhirnya nemu buat fixnya.
1. Edit kernel parameter dengan menambah salah satu pakai salah satu dibawah,
- acpi_backlight=video
- acpi_backlight=vendor
- acpi_backlight=native

```bash
sudo kernelstub -a "acpi_backlight=native" # saya pakai native buat fixnya, kemudian reboot
```

2. Cek kernel parameter
```bash
cat /proc/cmdline
```

Jika kalian pake GRUB, tinggal edit grubnya sama seperti di **Distro Linux Lain** <br>
Donee! 🚀


--- 

## Sumber & Referensi

- Temen
- [Linux Mint Forum](https://forums.linuxmint.com/viewtopic.php?t=320955)
- [Ubuntu Forum](https://askubuntu.com/questions/935585/nvidia-backlight-brightness-problem)

