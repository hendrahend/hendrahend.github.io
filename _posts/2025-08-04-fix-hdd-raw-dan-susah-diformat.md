---
title: Fix HDD RAW dan Susah di Format
tags: [Windows]
style: fill
color: warning
description: FIX HDD.
---

Ditulis Oleh: [Hendra Hendriana](https://hendrahend.github.io/about)

<br>
{% capture list_items %}
Pendahuluan
Tutorial
Referensi
{% endcapture %}
{% include elements/list.html title="Daftar Isi" type="toc" %}

<br>

### Pendahuluan

Kali ini saya akan membagikan artikel untuk fix HDD yang berformat raw dan susah di format. Sebelumnya saya mau cerita sedikit, awal mula kejadiannya itu ketika HDD eksternal saya tiba tiba gak bisa dipakai, dipasang di laptop pun gak bisa di akses dan muncul keterangan, not accessible, setelah di cek di disk management ternyata format nya berubah menjadi RAW, entah mengapa bisa menjadi seperti itu, padahal terakhir kali dipakai masih normal. Setelah mencari tutorial di internet akhirnya saya menemukan  fixnya, yaitu format dengan perintah commandline. 

### Tutorial
Sebenarnya untuk fixnya dalam kasus saya sangat gampang, yaitu dengan clean/format disk di commandline, kenapa di commandline? karena sudah mencoba format di disk management atau di file manager dengan klik kanan->format pada disk yang ingin di format, proses format nya selalu gagal. untuk itu langsung ke tutorialnya

#### Backup data

{% include elements/figure.html image="[https://raw.githubusercontent.com/hendrahend/hendrahend.github.io/refs/heads/main/images/Screenshot%20(35).png](https://raw.githubusercontent.com/hendrahend/hendrahend.github.io/refs/heads/main/images/Screenshot%20(35).png)" caption="EaseUS" %}

Sebelum ke tutorialnya, alangkah baiknya backup data terlebih dahulu. Bang, kan HDD nya gak kebaca? gimana backupnya?. Tenang walaupun gak kebaca di filemanager, kalian tetap bisa backup datanya menggunakan software EASEUS Data Recovery, saya pakai software itu untuk backup datanya, atau kalian bisa cari software lain yang serupa.

#### Commandline (cmd)
{% include elements/figure.html image="[https://raw.githubusercontent.com/hendrahend/hendrahend.github.io/refs/heads/main/images/Screenshot%20(37).png](https://raw.githubusercontent.com/hendrahend/hendrahend.github.io/refs/heads/main/images/Screenshot%20(37).png)" caption="CMD" %}

Buka commandline dengan run as administrator, lalu ikuti setiap baris perintah berikut satu per satu.
```cmd
DISKPART						# Membuka diskpart
list disk   					# Menampilkan daftar drive yang kamu punya
select disk x   				# Memilih drive yang akan kamu format
attributes disk clear readonly	# Menghapus attribut drive
clean    						# Membersihkan drive
create partition primary        # Membuat partisi baru
list partition   				# Melihat partisi baru
select partition x   			# Memilih partisi yang dibuat
active  						# Mengaktifkan partisi
format fs=ntfs quick  			# Memformat drive ke ntfs
assign  						# Assign nama drive
```
Sampai disini HDD saya bisa normal kembali, dan bisa diakses.
Demikian yang dapat saya sampaikan, jika belum berhasil atau mungkin berbeda kasusnya bisa cari referensi lain. Terimakasih

### Referensi
[How to fix RAW hard drive to NTFS in Windows 11/10](https://www.thewindowsclub.com/how-to-fix-raw-partition-in-windows).
