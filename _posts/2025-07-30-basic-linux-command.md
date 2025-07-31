---
title: Basic Linux Command
tags: [Linux]
style: fill
color: primary
description: Beberapa perintah dasar di Linux.
---

Ditulis Oleh: [Hendra Hendriana](https://hendrahend.github.io/about)

<br>
{% capture list_items %}
Pendahuluan
Perintah Dasar
Referensi
{% endcapture %}
{% include elements/list.html title="Daftar Isi" type="toc" %}

<br>

### Pendahuluan

Linux adalah sistem operasi yang powerful dengan antarmuka command line yang sangat berguna. Untuk pengguna baru, memahami perintah-perintah dasar sangat penting untuk navigasi dan manajemen sistem. Artikel ini akan membahas perintah-perintah dasar Linux yang paling sering digunakan.

### Perintah Dasar

#### Operasi File & Direktori
```bash
ls          # Menampilkan isi direktori
ls -l       # Menampilkan detail (hak akses, pemilik, ukuran)
ls -a       # Menampilkan file tersembunyi
cd          # Pindah ke direktori home
cd /path    # Pindah ke direktori tertentu
pwd         # Menampilkan direktori saat ini
mkdir dir   # Membuat direktori baru
rmdir dir   # Menghapus direktori kosong
touch file  # Membuat file kosong
cp file1 file2  # Menyalin file
mv file1 file2  # Memindahkan/mengganti nama file
rm file     # Menghapus file
rm -r dir   # Menghapus direktori beserta isinya
```

#### Melihat & Mengedit FIle
```bash
cat file    # Menampilkan isi file
less file   # Membaca file per halaman
head file   # Menampilkan 10 baris pertama
tail file   # Menampilkan 10 baris terakhir
tail -f file # Memantau perubahan file secara real-time
nano file   # Mengedit file dengan nano
vim file    # Mengedit file dengan vim
```

#### Manage Proses
```bash
ps          # Menampilkan proses yang berjalan
top         # Menampilkan proses secara dinamis
kill PID    # Menghentikan proses dengan ID tertentu
pkill name  # Menghentikan proses berdasarkan nama
```

#### Hak Akses
```bash
chmod 755 file  # Mengubah hak akses file
chown user:group file  # Mengubah kepemilikan file
```

#### Sistem
```bash
uname -a      # Menampilkan semua informasi sistem (nama kernel, versi, arsitektur, dll.).
df -h         # Menampilkan penggunaan ruang disk di setiap partisi dalam format yang mudah dibaca.
free -h       # Menampilkan penggunaan memori (RAM) dalam format yang mudah dibaca.
hostname      # Menampilkan nama host sistem.
whoami        # Menampilkan nama pengguna yang sedang login.
date          # Menampilkan tanggal dan waktu sistem saat ini.
reboot        # Merestart sistem (membutuhkan hak akses root/sudo).
shutdown now  # Mematikan sistem segera (membutuhkan hak akses root/sudo).
```

#### File
```bash
find . -name "file_name.txt" # Mencari 'file_name.txt' di direktori saat ini dan subdirektorinya.
grep "keyword" file.txt      # Mencari 'keyword' di dalam 'file.txt'.
grep -r "keyword" .          # Mencari 'keyword' secara rekursif di semua file dalam direktori saat ini.
```

#### Jaringan
```bash
ip addr               # Menampilkan alamat IP dan konfigurasi antarmuka jaringan.
ping google.com       # Menguji konektivitas ke nama domain cth: 'google.com'.
ssh user@host         # Menghubungkan ke server lain melalui SSH. Contoh: ssh admin@192.168.1.100.
wget URL              # Mengunduh file dari internet. Contoh: wget https://example.com/file.zip.
curl URL              # Alat untuk transfer data dengan URL. Lebih fleksibel dari wget.
```

#### Bantuan
```bash
command_name --help # Menampilkan opsi bantuan singkat untuk 'command_name'. Contoh: ls --help.
```

### Referensi
Google.
