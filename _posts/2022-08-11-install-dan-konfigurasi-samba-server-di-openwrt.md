---
title: Cara Install dan Konfigurasikan Samba Server di OpenWrt
tags: [OpenWrt]
style: fill
color: danger
description: Samba adalah program yang bersifat sumber terbuka yang menyediakan layanan berbagi berkas dan berbagi alat pencetak. [Wikipedia]
---

Ditulis Oleh: Hendra Hendriana

<br>
{% capture list_items %}
Persyaratan
Mounting HDD/FD
Instalasi
Konfigurasi
Credit
{% endcapture %}
{% include elements/list.html title="Daftar Isi" type="toc" %}

<br>

### Persyaratan
- Router dengan OS OpenWrt
- HDD/FD Sebagai media penyimpanan
- Akses Internet

<br>

### Mounting HDD/FD
Sebelum ke instalasi dan konfigurasi , kita akan melakukan mounting HDD/FD terlebih dahulu , disini saya memakai Flashdrive sebagai media penyimpanan nya.

1. Siapkan HDD/FD untuk media penyimpanannya, lalu format HDD/FD tersebut dengan format NTFS
2. Lalu Colokan HDD/FD tersebut ke Router
3. Akses ip router di browser , buka **System > Mount Points** atau bisa juga cek di **System > Disk Manager** cek apakah HDD/FD sudah ter-mount
> Jika belum ada package **Disk Manager** , bisa install manual dengan perintah: `opkg update && opkg install luci-app-diskman`
<br>
Lanjut tahap instalasi
<br>

### Instalasi
Akses ip router kalian menggunakan terminal/putty
<br>
*contoh menggunakan terminal*
```
ssh root@192.168.1.1
```
kemudian copy & pastekan command berikut di terminal
```
opkg update && opkg install samba4-server luci-app-samba4 ntfs-3g
```
Atau bisa juga install dengan cara akses ip router di browser masuk ke menu **System > Software** kemudian update terlebih dahulu dengan memilih **Update List** kemudian cari package **samba4-server, luci-app-samba4, ntfs-3g** kemudian install package tersebut.

<br>

### Konfigurasi
Lanjut ke step konfigurasi .
<br>
edit `/etc/config/firewall`
```
nano /etc/config/firewall
```
lalu tambahkan dipaling bawah
```
config rule
    option src 'lan'
    option proto 'udp'
    option dest_port '137-138'
    option target 'ACCEPT'
config rule
    option src 'lan'
    option proto 'tcp'
    option dest_port '139'
    option target 'ACCEPT'
config rule
    option src 'lan'
    option proto 'tcp'
    option dest_port '445'
    option target 'ACCEPT'
```
Simpan dengan CTRL+X , y , lalu enter.


edit `/etc/rc.local`
```
nano /etc/rc.local 
```
sebelum "exit 0" tambahkan 
```
sleep 1
ntfs-3g /sda1 /mnt/sda1 -o rw,lazytime,noatime,big_writes
smbd -D
nmbd -D
```
> Sesuaikan `/sda1` dan `/mnt/sda1` dengan letak HDD/FD kalian
<br>

Simpan dengan CTRL+X , y , lalu enter.
Pastikan samba server enable dengan perintah:
```
/etc/init.d/samba4 enable
/etc/init.d/samba4 start
```

Reboot router openwrt dengan perintah:
```
reboot
```
Akses samba server via PC dengan cara Windows+R dan masukkan ip router kalian.

<br>

### Credit
Thanks To:
<br>
Youtube, [Indonesian Tech Channel](https://www.youtube.com/c/IndonesianTechChannel)
<br>
Youtube, [aryobrokolly](https://www.youtube.com/c/aryobrokolly)

<br>


