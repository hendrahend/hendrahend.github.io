---
title: Cara Menambahkan Microsoft Access ke Office 365 Home & Student
style: fill
color: success
description: Add Microsoft Access
---

Ditulis Oleh: [Hendra Hendriana](https://hendra-hendriana.github.io/about)

<br>
{% capture list_items %}
Persyaratan
Instalasi
{% endcapture %}
{% include elements/list.html title="Daftar Isi" type="toc" %}

<br>

### Persyaratan
- Windows 10/11 x64/x86

<br>

### Instalasi

1. Download Microsoft Office Deployment Tool [Disini](https://www.microsoft.com/en-us/download/details.aspx?id=49117)
2. Ekstrak file tersebut .
3. Edit file configuration , lalu tambahkan script dibawah

```
Edit :
<Add OfficeClientEdition="64" Channel="Current">
    <Product ID="O365ProPlusRetail">
      <Language ID="en-us" />
    </Product>
    <Product ID="VisioProRetail">
      <Language ID="en-us" />
    </Product>
  </Add>

Menjadi :
<Add OfficeClientEdition="64">
    <Product ID="Access2019Retail">
      <Language ID="en-us" />
    </Product>
  </Add>
```

> Sesuaikan dengan Sistem Operasi kalian , jika x64/64 bit edit configuration-x64, jika x86/32 bit edit configuration-x86, jangan lupa untuk mengubah **OfficeClientEdition="32"** jika kalian OS kalian 32 bit

4. Buka powershell di folder tersebut dengan klik shift + klik kanan, jalankan script dibawah
```
./setup.exe \configure /configuration-x64.xml 
```
5. nanti otomatis akan ada instalasi microsoft access, tunggu sampai selesai
6. untuk mengaktifkan lisensi , buka cmd run as admin, tempel script dibawah
```
Windows 10 :

if exist "C:\Program Files\Microsoft Office\Office16\ospp.vbs" cd /d "C:\Program Files\Microsoft Office\Office16"

if exist "C:\Program Files (x86)\Microsoft Office\Office16\ospp.vbs" cd /d "C:\Program Files (x86)\Microsoft Office\Office16"

 

cscript ospp.vbs /inslic:"..\root\Licenses16\Access2019VL_KMS_Client_AE-ppd.xrm-ms"

cscript ospp.vbs /inslic:"..\root\Licenses16\Access2019VL_MAK_AE-ul-oob.xrm-ms"

cscript ospp.vbs /inslic:"..\root\Licenses16\Access2019VL_MAK_AE-ul-phn.xrm-ms"

cscript ospp.vbs /inslic:"..\root\Licenses16\Access2019VL_KMS_Client_AE-ul.xrm-ms"

cscript ospp.vbs /inslic:"..\root\Licenses16\Access2019VL_MAK_AE-pl.xrm-ms"

cscript ospp.vbs /inslic:"..\root\Licenses16\Access2019VL_MAK_AE-ppd.xrm-ms"

cscript ospp.vbs /inslic:"..\root\Licenses16\Access2019VL_KMS_Client_AE-ul-oob.xrm-ms"

 

cscript ospp.vbs /inpkey:9N9PT-27V4Y-VJ2PD-YXFMF-YTFQT

cscript ospp.vbs /sethst:kms.teevee.asia

cscript ospp.vbs /act

 

Windows 11 :

 

if exist "C:\Program Files\Microsoft Office\Office16\ospp.vbs" cd /d "C:\Program Files\Microsoft Office\Office16"

if exist "C:\Program Files (x86)\Microsoft Office\Office16\ospp.vbs" cd /d "C:\Program Files (x86)\Microsoft Office\Office16"

 

cscript ospp.vbs /inpkey:9N9PT-27V4Y-VJ2PD-YXFMF-YTFQT

cscript ospp.vbs /sethst:kms.teevee.asia

cscript ospp.vbs /act

```

DONE

<br>


