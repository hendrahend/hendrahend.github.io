---
title: Cara Install Microsoft Office 2013 di Linux (Ubuntu 20.04)
style: fill
color: success
description: Install Microsoft Office 2013 (Ms Word, Ms PowerPoint, Ms Outlook, Ms OneNote) dengan PlayOnLinux
---

Ditulis Oleh: [Hendra Hendriana](https://hendra-hendriana.github.io/about)

<br>

{% capture list_items %}
Instalasi
Konfigurasi
{% endcapture %}
{% include elements/list.html title="Daftar Isi" type="toc" %}

<br>

### Instalasi
Pertama Install PlayOnLinux
```
sudo apt-get install PlayOnLinux
```
Install Winbind
```
sudo apt-get install winbind
```
Install wine
```
wget https://dl.winehq.org/wine-builds/Release.key
sudo apt-key add Release.key
sudo apt-add-repository 'https://dl.winehq.org/wine-builds/ubuntu/'

sudo apt-get update
sudo apt-get install wine-stable winehq-stable 
```

<br>

### Konfigurasi
1. Buka PlayOnLinux > Tools > Manage Wine Version . Install wine 3.1 & 2.20-stagging
2. Buka tab Configure > Klik **New** > 32bit instalation > pilih wine 3.1 > Lalu isi nama virtual drive dengan **Office2013**
3. Klik **Office2013** > pilih tab Miscellanous > Open a shell > Lalu run script dibawah
4. Jika sudah selesai, pilih tab General > ubah wine version ke 2.20-stagging
<br>

```shell
#!/bin/bash
  
# CHANGELOG
# [Quentin PÂRIS] (2015-11-26 22-01)
# Initial version
# minorly modified Version by overflyer87 
# (NOT CREDIT WORTHY, JUST TRYING TO HELP REGULAR USERS DYING FOR OFFICE 2013)
  
[ "$PLAYONLINUX" = "" ] && exit 0
source "$PLAYONLINUX/lib/sources"
  
PREFIX="Office2013"
WINEVERSION="3.1"
TITLE="Microsoft Office 2013"
  
POL_GetSetupImages "http://files.playonlinux.com/resources/setups/Office/top.jpg" "http://files.playonlinux.com/resources/setups/Office/left.png" "$TITLE"
  
POL_SetupWindow_Init
  
POL_SetupWindow_presentation "$TITLE" "Microsoft" "http://www.microsoft.com" "Quentin PÂRIS" "$PREFIX"
  
POL_RequiredVersion 4.0.18 || POL_Debug_Fatal "$TITLE won't work with $APPLICATION_TITLE $VERSION\nPlease update"
  
if [ "$POL_OS" = "Linux" ]; then
        wbinfo -V || POL_Debug_Fatal "Please install winbind before installing $TITLE"
fi
POL_Debug_Init
POL_System_SetArch "x86"
  
  
POL_SetupWindow_InstallMethod "LOCAL"
  
POL_SetupWindow_browse "$(eval_gettext 'Please select the setup file to run')" "$TITLE"
SetupIs="$APP_ANSWER"

  
POL_Wine_SelectPrefix "$PREFIX"
POL_Wine_PrefixCreate "$WINEVERSION"
 
Set_OS "win7"
  
POL_Wine_WaitBefore "$TITLE"
[ "$CDROM" ] && cd "$CDROM"
  
if [ ! "$(file $SetupIs | grep 'x86-64')" = "" ]; then
    POL_Debug_Fatal "$(eval_gettext "The 64bits version is not compatible! Sorry")";
fi
POL_Wine "$SetupIs"
POL_Wine_WaitExit "$TITLE"
  
# See http://forum.winehq.org/viewtopic.php?f=8&t=23126&p=95555#p95555
POL_Wine_OverrideDLL "native,builtin" "riched20"
  
# Fix a crash when loading a file
# This line was now calling POL_Call POL_Install_msxml6 which always failed since msxml6.dll is already present in 
# even freshly created wineprefix and the question of if that file should be deleted and answered with n or y
# always results in crash of this Install function of POL. Install msxml6 manually via POL.
  
POL_Shortcut "WINWORD.EXE" "Microsoft Word 2013" "" "" "Office;WordProcessor;"
POL_Shortcut "EXCEL.EXE" "Microsoft Excel 2013" "" "" "Office;Spreadsheet;"
POL_Shortcut "POWERPNT.EXE" "Microsoft Powerpoint 2013" "" "" "Office;Presentation;"
POL_Shortcut "ONENOTE.EXE" "Microsoft OneNote 2013" "" "" "Network;InstantMessaging;" # No category for collaborative work?
POL_Shortcut "OUTLOOK.EXE" "Microsoft Outlook 2013" "" "" "Network;Email;" # Calendar;ContactManagement; ? :p
  
POL_Extension_Write doc "Microsoft Word 2013"
POL_Extension_Write docx "Microsoft Word 2013"
POL_Extension_Write xls "Microsoft Excel 2013"
POL_Extension_Write xlsx "Microsoft Excel 2013"
POL_Extension_Write ppt "Microsoft Powerpoint 2013"
POL_Extension_Write pptx "Microsoft Powerpoint 2013"
  
POL_SetupWindow_message "$(eval_gettext '$TITLE has been installed successfully\n\nIf an installation Windows prevent your programs from running, you must remove and reinstall $TITLE')" "$TITLE"
POL_SetupWindow_Close
exit
```


<br>

Sekian yang dapat saya sampaikan, terimakasih.
