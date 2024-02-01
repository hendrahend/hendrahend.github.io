---
title: Build OpenWrt Menggunakan ImageBuilder
tags: [OpenWrt]
style: fill
color: danger
description: 
---

Ditulis Oleh: [Hendra Hendriana](https://hendrahend.github.io/about)

<br>

### CMD Script
1. Keluar dari Test Mode
```
bcdedit –set TESTSIGNING off
```
> Kemudian restart PC Kalian.

2. Memperbaiki File Sistem Windows
```
sfc /scannow
```
3. Melihat Konfigurasi IP
```
ipconfig
```
4. Mengecek Response Server
```
ping [hostname]
```
> Contoh ```ping google.com```
5. Memeriksa Hard Drive
```
chkdsk
```
6. Format Hard Drive
```
format [drive letter]: /fs:[file system] /q
```
> Contoh ```format F: /fs:ntfs /q```
7. Diskpart
```
diskpart
```
8. Fix Regedit tidak bisa dibuka
```
reg add "HKCU\Software\Microsoft\Windows\CurrentVersion\Policies\System" /t Reg_dword /v DisableRegistryTools /f /d 0
```
> Jika tidak berhasil, bisa coba download [file ini](https://drive.google.com/file/d/1TYwNH32-Fj9kliXFEqmuEvhrW8boZjAy/view?usp=sharing), klik kanan di file tersebut lalu install.
9. Membuka Task Manager
```
taskmgr
```
10. Mengehntikan Program
```
taskkill [nama_program/pid]
```
> Contoh ```taskkill zoom.exe``` <br>
> Untuk mengetahui program yang sedang berjalan gunakan ```tasklist```
<br>

### Sumber & Referensi

[Google](https://google.com)



