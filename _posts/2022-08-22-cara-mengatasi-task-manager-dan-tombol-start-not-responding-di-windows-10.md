---
title: 3 Cara Mengatasi Taskbar dan Tombol Windows Not Responding di Windows 10
tags: [Windows]
style: fill
color: primary
description: Mengatasi Taskbar Not Responding di Windows .
---

Ditulis Oleh: [Hendra Hendriana](https://hendra-hendriana.github.io/about)

<br>

{% capture list_items %}
Penyebab Masalah
Cara Pertama
Cara Kedua
Cara Ketiga
{% endcapture %}
{% include elements/list.html title="Daftar Isi" type="toc" %}

<br>

### Penyebab Masalah
Pernahkah kalian mengalami Taskbar dan Tombol Windows Not Responding di Windows?, jika pernah, biasanya itu disebabkan oleh Update Sistem yang tidak berhasil atau bisa juga disebabkan oleh program program yang tidak berjalan dengan baik di Windows .
<br>
<br>
Lalu bagaimana cara mengatasinya? , disini ada beberapa solusi jika kalian mengalami hal seperti yang di jelaskan di atas , saya sendiri pernah mengalami hal yang serupa , dan berhasil menggunakan cara yang ketiga .

<br>

### Cara Pertama
Cara Pertama yaitu dengan menggunakan cmd . Karena Tombol Start/Windows Tidak berfungsi , maka kita tidak bisa menggunakan **Windows + R** atau mencari cmd di pencarian .
- Buka cmd melalui File Explorer.
- Buka File Explorer melalui **Reycle Bin**, masuk ke Direktori `C:\Users\namauser\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\System Tools`
- Klik kanan pada **Command Prompt > Run as Administrator**
- Ketikan `sfc /scannow` tunggu prosesnya sampai selesai.
- reboot dengan perintah `shutdown /r`
<br>
{% capture carousel_images %}
https://raw.githubusercontent.com/hendra-hendriana/hendra-hendriana.github.io/main/images/Screenshot%202022-08-25%20184816.png
https://raw.githubusercontent.com/hendra-hendriana/hendra-hendriana.github.io/main/images/Screenshot%202022-08-25%20184825.png
{% endcapture %}
{% include elements/carousel.html %}

<br>

### Cara Kedua
Cara Kedua yaitu menggunakan Task Manager.
- Buka **CTRL+SHIFT+ESC** atau **CTRL+ALT+DELETE** untuk masuk ke Task Manager.
- Dibagian menu **Process** Scroll lalu cari **Windows Explorer**
- Klik kanan pada Windows Explorer tersebut lalu pilih end task
- Klik **File > Run New Task** lalu tuliskan `explorer.exe` lalu enter
<br>
{% capture carousel_images %}
https://raw.githubusercontent.com/hendra-hendriana/hendra-hendriana.github.io/main/images/Screenshot%202022-08-25%20185745.png
https://raw.githubusercontent.com/hendra-hendriana/hendra-hendriana.github.io/main/images/Screenshot%202022-08-25%20185903.png
https://raw.githubusercontent.com/hendra-hendriana/hendra-hendriana.github.io/main/images/Screenshot%202022-08-25%20190038.png
{% endcapture %}
{% include elements/carousel.html %}

<br>

### Cara Ketiga 
Menggunakan Windows Powershell
- Buka File Explorer melalui **Reycle Bin**, masuk ke Direktori `C:\Users\namauser\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Windows PowerShell`
- Klik kanan pada **Windows Powershell > Run as Administrator**
- Copy Paste script berikut
```
 Get-AppXPackage -AllUsers | Foreach {Add-AppXPackage -DisableDevelopmentMode -Register "$($_.InstallLocation)\AppXManifest.xml"}
```
- Tunggu sampai proses selesai.
- reboot dengan perintah 
```
restart-computer
```
<br>
{% include elements/figure.html image="https://raw.githubusercontent.com/hendra-hendriana/hendra-hendriana.github.io/main/images/Screenshot%202022-08-26%20212827.png" caption="Windows Powershell" %}

<br>

Sekian yang dapat saya sampaikan, terimakasih.
