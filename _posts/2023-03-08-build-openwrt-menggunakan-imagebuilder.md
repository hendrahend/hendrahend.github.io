---
title: Build OpenWrt Menggunakan ImageBuilder
tags: [OpenWrt]
style: fill
color: danger
description: OpenWrt adalah sebuah sistem operasi distribusi GNU / Linux yang berbasis firmware. Sistem operasi ini digunakan untuk perangkat yang tertanam terutama pada perangkat router. [Wikipedia]
---

Ditulis Oleh: [Hendra Hendriana](https://hendra-hendriana.github.io/about)

<br>
{% capture list_items %}
Persyaratan
Step Pertama
Step Kedua
Sumber & Referensi
{% endcapture %}
{% include elements/list.html title="Daftar Isi" type="toc" %}

<br>

### Persyaratan
- Akses Internet
- Linux / VmWare dengan OS Linux

<br>

### Step Pertama
1. Download OpenWrt ImageBuilder 21.02.5
```
https://downloads.openwrt.org/releases/21.02.5/targets/armvirt/64/openwrt-imagebuilder-21.02.5-armvirt-64.Linux-x86_64.tar.xz
```
> Jika ingin memakai versi lain bisa download di `https://downloads.openwrt.org/releases/` sesuaikan targetnya dengan sbc kalian.
<br>
2. Extract dan masuk ke foldernya
```
tar -xfv openwrt-imagebuilder-21.02.5-armvirt-64.Linux-x86_64.tar.xz && cd openwrt-imagebuilder-21.02.5-armvirt-64.Linux-x86_64.tar.xz
```
3. Sesuaikan Config, Files, Packages . Kemudian jika sudah disesuaikan build dengan perintah berikut
```
make image PROFILE="Default" PACKAGES="\
cgi-io libiwinfo libiwinfo-data libiwinfo-lua liblua liblucihttp liblucihttp-lua \
libubus-lua lua luci luci-app-firewall luci-app-opkg luci-base luci-lib-base \
luci-lib-ip luci-lib-jsonc luci-lib-nixio luci-mod-admin-full luci-mod-network \
luci-mod-status luci-mod-system luci-proto-ipv6 luci-proto-ppp luci-ssl \
luci-theme-bootstrap px5g-wolfssl rpcd rpcd-mod-file rpcd-mod-iwinfo rpcd-mod-luci \
rpcd-mod-rrdns uhttpd uhttpd-mod-ubus luci-compat \
ath9k-htc-firmware btrfs-progs hostapd hostapd-utils kmod-ath kmod-ath9k kmod-ath9k-common \
kmod-ath9k-htc kmod-cfg80211 kmod-crypto-acompress kmod-crypto-crc32c kmod-crypto-hash \
kmod-fs-btrfs kmod-mac80211 wireless-tools wpa-cli wpa-supplicant \
" FILES="files"
```
4. Hasil OpenWrt akan berada di /bin/targets/armvirt/64/

<br>

### Step Kedua
1. Update dan Install package yang dibutuhkan
<br>
Ubuntu
```
sudo apt-get update -y
sudo apt-get full-upgrade -y
sudo apt-get install -y $(curl -fsSL https://raw.githubusercontent.com/ophub/amlogic-s9xxx-armbian/main/compile-kernel/tools/script/ubuntu2004-openwrt-depends)
```
<br>
Arch
```
pacman -Syyy
pacman -S base-devel
```
2. Clone Repo Ophub
*Clone Repo*
```
git clone --depth 1 https://github.com/ophub/amlogic-s9xxx-openwrt.git
```
masuk ke folder dan buat folder openwrt-armvirt
```
cd amlogic-s9xxx-openwrt && mkdir openwrt-armvirt
```
copy rootfs dari hasil build openwrt tadi ke folder amlogic-s9xxx-openwrt
3. kemudian
```
sudo ./make -b s905x -k 5.15.94 -s 1024
```
<br>

### Step Terakhir

### Sumber & Referensi
<br>
Youtube, [Indonesian Tech Channel](https://www.youtube.com/c/IndonesianTechChannel)
<br>
Youtube, [aryobrokolly](https://www.youtube.com/c/aryobrokolly)

<br>



