---
title: Fix HDD RAW dan Susah di Format
tags: [Windows]
style: fill
color: warning
description: Cara memperbaiki HDD yang berformat RAW dan sulit diformat.
---

Ditulis oleh: [Hendra Hendriana](https://hendrahend.github.io/about)

<br>

{% capture list_items %}
Pendahuluan  
Tutorial  
Referensi  
{% endcapture %}
{% include elements/list.html title="Daftar Isi" type="toc" %}

<br>

### Pendahuluan

Kali ini saya akan membagikan tutorial untuk memperbaiki HDD yang berubah menjadi format **RAW** dan sulit diformat. Kejadian ini saya alami sendiri—HDD eksternal saya tiba-tiba tidak bisa diakses. Saat dicolok ke laptop, muncul pesan *"not accessible"*. Setelah dicek di **Disk Management**, ternyata format-nya berubah menjadi RAW. Padahal sebelumnya masih normal.

Setelah mencari berbagai referensi di internet, akhirnya saya menemukan solusi yang berhasil, yaitu memformat melalui **Command Prompt (CMD)** karena metode melalui Disk Management maupun klik kanan → Format selalu gagal.

### Tutorial

Untuk kasus saya, solusinya cukup mudah: melakukan **clean dan format** lewat CMD. Kenapa harus CMD? Karena cara biasa seperti lewat File Explorer atau Disk Management selalu gagal.

#### 1. Backup Data

{% include elements/figure.html image="https://raw.githubusercontent.com/hendrahend/hendrahend.github.io/refs/heads/main/images/Screenshot%20(35).png" caption="EaseUS Data Recovery" %}

Sebelum memformat, **backup data** terlebih dahulu. Mungkin kamu berpikir, "Bang, HDD-nya aja gak kebaca, gimana mau backup?"

Tenang. Meskipun tidak terbaca di File Explorer, kamu tetap bisa menyelamatkan data dengan software seperti **EaseUS Data Recovery**. Saya sendiri menggunakan software ini untuk backup sebelum memformat. Kalau tidak cocok, kamu bisa gunakan alternatif lainnya seperti Recuva atau MiniTool.

#### 2. Format Melalui CMD

{% include elements/figure.html image="https://raw.githubusercontent.com/hendrahend/hendrahend.github.io/refs/heads/main/images/Screenshot%20(37).png" caption="Command Prompt (CMD)" %}

Buka **Command Prompt** sebagai administrator, lalu ketik perintah-perintah berikut satu per satu:

```cmd
diskpart                                 # Membuka diskpart
list disk                                # Menampilkan daftar drive
select disk X                            # Pilih nomor disk yang akan diformat (ganti X dengan angka sesuai drive)
attributes disk clear readonly           # Hapus atribut read-only
clean                                    # Bersihkan seluruh partisi
create partition primary                 # Buat partisi baru
list partition                           # Lihat partisi yang tersedia
select partition X                       # Pilih partisi (ganti X sesuai nomor partisi)
active                                   # Aktifkan partisi
format fs=ntfs quick                     # Format cepat ke NTFS
assign                                   # Tetapkan drive letter
```
