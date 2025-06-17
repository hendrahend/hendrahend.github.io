---
title: Fix Screen Glitch di Linux (AMD GPU)
tags: [Linux, AMD, GPU, Troubleshooting, Kernel, Display]
style: fill
color: success
description: Fix screen glitch yang kadang muncul di amd gpu
---

Ditulis Oleh: [Hendra Hendriana](https://hendrahend.github.io/about)

<br>
{% capture list_items %}
Pendahuluan
Mengapa Glitch Terjadi?
Tutorial
Sumber & Referensi
{% endcapture %}
{% include elements/list.html title="Daftar Isi" type="toc" %}

<br>

### Pendahuluan

Bagi para pengguna Linux yang mengandalkan GPU AMD, harapan akan pengalaman visual yang mulus dan tanpa hambatan adalah hal yang wajar. Namun, tidak jarang kita dihadapkan pada masalah yang cukup mengganggu yang dikenal sebagai "screen glitch." Fenomena visual ini dapat bermanifestasi dalam berbagai bentuk, mulai dari kedipan sesaat, munculnya artefak visual yang tidak diinginkan, hingga garis-garis aneh yang melintas secara acak pada layar Anda. Meskipun umumnya tidak menyebabkan kerusakan fatal pada sistem, glitch ini secara signifikan dapat menurunkan kenyamanan penggunaan, mengganggu produktivitas saat bekerja, atau mengurangi kualitas pengalaman saat menikmati konten multimedia. Artikel ini hadir untuk membahas secara tuntas bagaimana cara mengatasi screen glitch ini agar Anda dapat kembali menikmati pengalaman Linux yang optimal.

### Mengapa Glitch Terjadi?

Screen glitch pada sistem Linux dengan AMD GPU bisa disebabkan oleh berbagai faktor. Salah satu penyebab umum terkait dengan interaksi antara driver grafis AMD (biasanya `amdgpu` open-source) dengan komponen display di dalam kernel Linux. Terkadang, pengaturan default atau bug pada driver tertentu dapat memicu masalah rendering yang kemudian bermanifestasi sebagai glitch visual.

Parameter `amdgpu.dcdebugmask` yang akan kita gunakan adalah salah satu cara untuk mengatur perilaku driver AMD GPU secara lebih spesifik, terutama dalam hal Display Core (DC) atau yang sering disebut Display Code, yang bertanggung jawab atas output display. Dengan menyesuaikan nilai parameter ini, kita dapat "memberi tahu" driver untuk mengatasi kondisi tertentu yang menyebabkan glitch

---

### Tutorial
JIka anda menggunakan linux dengan systemd boot seperti PopOS! maka cara ikuti cara ini
Edit kernel parameter dengan menambah `amdgpu.dcdebugmask=0x410`

```bash
sudo kernelstub -a "amdgpu.dcdebugmask=0x410"
```

>`cat /proc/cmdline` untuk melihat kernel parameter <br>

Donee! 🚀

**Untuk Distribusi Non-Pop!_OS (Pengguna GRUB):**

Jika Anda tidak menggunakan `kernelstub` (misalnya, pada Ubuntu, Fedora, Debian, atau Arch Linux), Anda perlu memodifikasi file konfigurasi GRUB secara manual.

1.  Buka file `/etc/default/grub` dengan editor teks sebagai root:
	```bash
	sudo nano /etc/default/grub
	```
2. Cari baris yang dimulai dengan `GRUB_CMDLINE_LINUX_DEFAULT`. Tambahkan `amdgpu.dcdebugmask=0x410` di dalam tanda kutip ganda. Contoh:
    
    ```
    GRUB_CMDLINE_LINUX_DEFAULT="quiet splash amdgpu.dcdebugmask=0x410"
    ```
    
    Jika sudah ada parameter lain, pisahkan dengan spasi:
    ```
    GRUB_CMDLINE_LINUX_DEFAULT="quiet splash pci=noaer amdgpu.dcdebugmask=0x410"
    
    ```
    
3. Simpan file dan keluar dari editor.
4. Perbarui GRUB untuk menerapkan perubahan:
	```bash
	sudo update-grub
	```
### Sumber & Referensi

- Google
