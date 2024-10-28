## Uconsole CM4 (Cache)

Format the SDcard:

```sh
sudo wipefs --all /dev/sdc
sudo fdisk --list
```

```sh
sudo fdisk /dev/sdc
```

```sh
sudo mkfs.vfat /dev/sdc1
sudo mkfs.ext4 /dev/sdc2
```

Mount:

```sh
mount
sudo umount /mnt/boot
sudo umount /mnt
mount
```

```sh
sudo fdisk --list
sudo mount /dev/sdc2 /mnt
sudo mkdir /mnt/boot
sudo mount /dev/sdc1 /mnt/boot
```

```sh
sudo pacman -Sy
sudo pacman -S qemu-user-static qemu-user-static-binfmt arch-install-scripts
```

```sh
sudo bsdtar -xpf ArchLinuxARM-aarch64-latest.tar.gz -C /mnt
ls -l /mnt
sudo genfstab -U /mnt | sudo tee -a /mnt/etc/fstab
```

Install `linux-uconsole-cm3-rpi64*.pkg.zst`:

```sh
sudo arch-chroot /mnt
pacman-key --init
pacman-key --populate archlinuxarm
pacman -Sy raspberrypi-bootloader firmware-raspberrypi
pacman -R linux-aarch64
pacman -U --noconfirm linux-uconsole-cm3-rpi64*.pkg.zst
pacman -U --noconfirm ap6256-firmware*.pkg.tar
pacman -S iwe
```

If not `*.pkg.zst` here:

```sh
git clone https://github.com/PotatoMania/uconsole-cm3
git clone https://github.com/systematiccaos/uconsole-cm3-cm4
cd uconsole-cm3/PKGBUILDs/linux-uconsole-cm3-rpi64
```

```sh
git clone --depth=1 -b rpi-6.1.y https://github.com/raspberrypi/linux.git
tar -czvf linux.tar.gz linux
```

```sh
tar -xzvf linux.tar.gz linux
cd linux
git status
git restore --source=HEAD :/
```

```sh
sudo pacman -S cpio pahole aarch64-linux-gnu-gcc make flex bison patch
makepkg
pacman -Syu
```

And:

```
useradd -m auruser
passwd auruser
echo "auruser ALL=(ALL) ALL" > /etc/sudoers.d/auruser
chmod 440 /etc/sudoers.d/auruser
chmod u+w /home/auruser/ap6256-firmware
pacman -S fakeroot sudo
su - auruser
ls -l /home/auruser/ap6256-firmware
export PKGDEST=/tmp/my_package_destination
export SRCDEST=/tmp/my_source_directory
export BUILDDIR=/tmp/my_build_directory
makepkg
pacman -U /tmp/my_package_destination/ap6256-firmware-0.1.20231120-1-any.pkg.tar.xz
```

Edit `config.txt`:

```sh
sudo vim /mnt/boot/config.txt
```

```
ignore_lcd=1
disable_fw_kms_setup=1
max_framebuffers=2
arm_boost=1

# setup headphone detect pin
gpio=10=ip,np

# boot kernel directly
kernel=Image.gz
arm_64bit=1
initramfs initramfs-linux.img followkernel

# overlays
dtoverlay=dwc2,dr_mode=host
dtoverlay=vc4-kms-v3d
dtoverlay=audremap,pins_12_13
dtparam=audio=on
dtoverlay=uconsole
```

↪ [How to install ArchLinux on uConsole/CM3 from scratch](https://github.com/PotatoMania/uconsole-cm3)  
↪ [uConsole CM3](https://github.com/PotatoMania/uconsole-cm3/blob/dev/doc/how-to-install-archlinux-from-scratch.md)

Edit `cmdline.txt`:

```sh
sudo vim /mnt/boot/config.txt
```

```
[all]
ignore_lcd=1
disable_fw_kms_setup=1
disable_audio_dither
pwm_sample_bits=20

# setup headphone detect pin
gpio=10=ip,np

# boot custom kernel
kernel=Image.gz
arm_64bit=1
initramfs initramfs-linux.img followkernel

dtoverlay=dwc2,dr_mode=host
dtoverlay=audremap,pins_12_13
dtparam=audio=on

[pi3]
dtoverlay=vc4-kms-v3d
dtoverlay=uconsole

[cm4]
arm_boost=1
max_framebuffers=2
dtoverlay=vc4-kms-v3d-pi4
dtoverlay=uconsole,cm4

[all]
# whatever you need
```

↪ [Wifi not working on CM4](https://github.com/PotatoMania/uconsole-cm3-arch-image-builder/issues/1)

Finally, unmount:

```sh
sudo umount /mnt/boot /mnt
```

## [Raspberry Pi 4](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/) / [CM4](https://www.raspberrypi.com/products/compute-module-4/)

### USB host boot mode

```sh
sudo vim /root/firmware/config.txt
```

At the end, add:

```
[all]
program_usb_boot_mode=0
otg_mode=1
```

↪ [USB host boot mode](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#usb-host-boot-mode)

```sh
lsblk
mkfs.ext4 /dev/<source>
sudo dd if=/dev/<source> of=/dev/<target> bs=4M status=progress
sync
lsblk
```

↪ [Boot from USB, if no then SD card](https://raspberrypi.stackexchange.com/questions/91889/boot-from-usb-if-no-then-sd-card)  
↪ [What's the best filesystem to use for an NVMe SSD?](https://www.reddit.com/r/linux4noobs/comments/lmf8ju/whats_the_best_filesystem_to_use_for_an_nvme_ssd/)

### Pi OS

Change Mirrors:

```sh
sudo cp /etc/apt/sources.list.d/raspi.list /etc/apt/sources.list.d/raspi.list.bat
sudo vim /etc/apt/sources.list.d/raspi.list
```

Edit and save:

```
deb https://mirrors.tuna.tsinghua.edu.cn/raspberrypi/ bookworm main
```

↪ [清华大学开源软件镜像站 - Raspbian 软件仓库](https://mirrors.tuna.tsinghua.edu.cn/help/raspberrypi/)

```sh
sudo apt update && sudo apt upgrade
```

Enable SSH:

Preferences → Raspberry Pi Configuration → Interfaces → SSH (On)

```sh
hostname -I
```

↪ [How to SSH into Raspberry Pi](https://www.onlogic.com/company/io-hub/how-to-ssh-into-raspberry-pi/)

## [GPi CASE 2](https://retroflag.com/gpi_case_2.html)

Flash OS to SD card:

1. Get [SD Memory Card Formatter](https://www.sdcard.org/downloads/formatter/). Use it to format SD card.
2. Get [Raspberry Pi Imager](https://www.raspberrypi.com/software/).
3. Raspberry Pi Imager:
	1. Raspberry Pi Device → Raspberry Pi 4
	2. 请选择需要写入的操作系统 → Emulation and game OS → Recalbox / RetroPie
	3. 储存卡 → SD card
	4. Next

RetroPie used [EmulationStation](https://gitlab.com/es-de/emulationstation-de) as default frontend. Recalbox used [Modern](https://gitlab.com/es-de/themes/modern-es-de) theme for [ES-DE](https://gitlab.com/es-de/emulationstation-de).

Read more:

↪ [Placing games and other resources on network shares](https://gitlab.com/es-de/emulationstation-de/-/blob/master/USERGUIDE.md#placing-games-and-other-resources-on-network-shares)  
↪ [Arcade manager](https://github.com/cosmo0/arcade-manager)  
↪ [RetroArch asset server](https://github.com/NickHeap2/retroarch-asset-server)  
↪ [Renpy Documentation - Raspberry Pi](https://www.renpy.org/doc/html/raspi.html)  
↪ [FAQ - How can I recover my RetroPie after enabling the desktop OpenGL driver?](https://retropie.org.uk/docs/FAQ/#how-can-i-recover-my-retropie-after-enabling-the-desktop-opengl-driver)

### Emulator [Löve](https://love2d.org/) (Experimental) (Cache)

1. Config → RetroPie Setup → Manage packages → Manage optional packages → love-0.10.2, love
2. `mv <game>.love <path>/roms/love/``

Some games:

Get `CurseOfTheArrow-V1.8.3-universal.love` form [Curse of the Arrow](https://egordorichev.itch.io/curse-of-the-arrow).

```sh
unzip CurseOfTheArrow-V1.8.3-universal.love -d CurseOfTheArrow-V1.8.3-universal
cd CurseOfTheArrow-V1.8.3-universal
vim conf.lua
```

```
t.window.width = 96*5
t.window.height = 64*5
t.window.minwidth = 96
t.window.minheight = 64
```

```sh
7z a -tzip CurseOfTheArrow-V1.8.3-universal-640x480.love *
mv CurseOfTheArrow-V1.8.3-universal-640x480.love <RetroPie>/home/pi/RetroPie/roms/love/
```

Get `Source code (zip)` from [mari0 - Releases](https://github.com/Stabyourself/mari0/releases).

```sh
unzip mari0-1.6.2.zip -d mari0-1.6.2
cd mari0-1.6.2/mari0-1.6.2
7z a -tzip mari0-1.6.2.love *
mv mari0-1.6.2.love <RetroPie>/home/pi/RetroPie/roms/love/
```

↪ [RetroPie Docs - Love](https://retropie.org.uk/docs/Love/)  
↪ [PyGame LÖVE (love2d) in RecalBox](https://forum.recalbox.com/topic/19222/pygame-l%C3%B6ve-love2d-in-recalbox)

### [Recalbox](https://www.recalbox.com/)

Enable SSH:

1. Menu → Network Name → Enable WiFi → On
2. Network Name → <SSID>
3. WiFi Password → <Password> → Start
4. Connect with:
	```
	host `recalbox` (or ip-address)
	port `22`
	username `root`
	password `recalboxroot`
	```

Update games lists:

Menu → UI Settings → Update Games Lists

[Add a Bluetooth controller](https://wiki.recalbox.com/en/basic-usage/first-use-and-configuration):

Menu → Controller settings → Pair a bluetooth controller

[Add themes into frontend](https://wiki.recalbox.com/en/tutorials/frontend-customization/add-themes-into-emulationstation):

`share\themes

Hide preinstalled games:

Menu → UI Settings → Game Filters → Hide Preinstalled Games

Read more:

↪ [Gamelists](https://github.com/recalbox/recalbox-emulationstation/blob/master/GAMELISTS.md)  
↪ [Netplay (online games)](https://wiki.recalbox.com/en/basic-usage/features/netplay-online-games)

### [RetroPie](https://retropie.org.uk/) (TBD)

Install display patch and safe-shutdown script:

1. Get `GPi_Case2_patch.zip` from [GPiCase2-Script](https://github.com/RetroFlag/GPiCase2-Script).
2. Decompress it to `GPi_Case2_patch\`.
3. Copy all files under `GPi_Case2_patch_retropie` to `<SD card>\`.
4. Run `Install_patch.bat`.

Create `gpi.sh`:

```sh
wget -O - "https://raw.githubusercontent.com/RetroFlag/GPiCase2-Script/main/retropie_install_gpi2.sh" | sudo bash
```

First Boot:

1. Insert SD card into GPi Case 2, turn it on.
2. After first boot, hold a button to configure keymap. ou can hold down the button until it is be skipped.

Set Up WiFi:

1. Configuration → WiFi → ... → Localisation Options → Set WiFi country → Save and exit
2. After reboot, connect to WiFi

Install safe-shutdown script:

1. Configuration → File Manager → Edit `/etc/hosts`:
	```
	140.82.112.4	github.com
	185.199.108.133	raw.githubusercontent.com
	```
2. Reboot.
3. Configuration → File Manager → Run `/boot/gpi.sh`.

↪ [Retro Gaming With RetroPie, GPi CASE 2, and a Raspberry Pi](https://navendu.me/posts/retropie-gpi-case-2-setup/).

Enable SSH:

1. Configuration → Raspi-config → Interface Options → SSH → Yes
2. Connect with:
	```
	host `retropie` (or ip-address)
	port `22`
	username `pi`
	password `raspberry`
	```

↪ [RetroPie - SSH](https://retropie.org.uk/docs/SSH/)  
↪ [RetroPie - SFTP](https://retropie.org.uk/docs/Transferring-Roms/#sftp)

Refresh the game listing:

Menu → Quit → Restart EmulationStation

↪ [Transferring Roms](https://retropie.org.uk/docs/Transferring-Roms/)

Enable Pegasus Frontend:

System Menu → RetroPie Setup → Manage packages → Manage experimental packages → pegasus-fe → Install from pre-compiled binary

↪ [Pegasus Docs - Platform Notes: Raspberry](https://pegasus-frontend.org/docs/user-guide/platform-raspberry/#retropie)

```sh
nano /opt/retropie/configs/all/autostart.sh
```

```
pegasus-fe
```

Reboot.

If you use other controllers:

↪ [Xbox 360](https://retropie.org.uk/docs/Xbox-360-Controller/)  
↪ [Setting up an 8bitdo Bluetooth controller](https://retropie.org.uk/docs/8Bitdo-Controller/)  
↪ [Virtual Gamepad](https://retropie.org.uk/docs/Virtual-Gamepad/)  
↪ [Mobile Gamepad](https://github.com/sbidolach/mobile-gamepad)

### [Nxengine-Evo-RPi](https://github.com/Exarkuniv/Nxengine-Evo-RPi)

Unofficial installation scripts for RetroPie:

```sh
git clone --depth=1 https://github.com/Exarkuniv/RetroPie-Extra.git
cd RetroPie-Extra
./install-extras.sh
```

Choose which modules to install → `nxengine-evo.sh` → Ok

System Menu → RetroPie Setup → Manage packages → Manage experimental packages → nxengine-evo → Install from source

## [GitHub Actions Runner Images](https://github.com/actions/runner-images#preinstallation-policy) (TBD)

↪ [Ubuntu 24.04](https://github.com/actions/runner-images/blob/main/images/ubuntu/Ubuntu2404-Readme.md)  
↪ [About GitHub-hosted runners](https://docs.github.com/en/actions/using-github-hosted-runners/using-github-hosted-runners/about-github-hosted-runners#supported-runners-and-hardware-resources)

## Steam Deck (TBD)

↪ [The killer features of the Steam Deck](https://www.jonashietala.se/blog/2023/10/24/the_killer_features_of_the_steam_deck/)

## 3D Printer (TBD)

↪ [Printing Hextraction for my kids](https://www.jonashietala.se/blog/2024/02/09/printing_hextraction_for_my_kids/)

## [postmarketOS](https://postmarketos.org/) (Cache)

1. Windows 10 → 计算机管理 → 系统工具 → 设备管理器 → 便携设备 → ONEPLUS A5010
2. 驱动程序 → 更新驱动程序 → 浏览我的电脑以查找驱动程序 → `usb_driver\`

↪ [Using ADB and fastboot](https://wiki.lineageos.org/adb_fastboot_guide)  
↪ [Get the Google USB Driver](https://developer.android.com/studio/run/win-usb)  
↪ [Install a USB driver](https://developer.android.com/studio/run/oem-usb#InstallingDriver)

1. OnePlus 5 → 设置 → 关于手机 → 版本号 → 点击7下
2. 设置 → 开发者选项 → OEM解锁 → 启用
3. 拔掉USB → 电源键+音量上键 → FastBoot Mode
4. 插上USB → 在PC上运行`fastboot oem unlock`

↪ [postmarketOS Wiki - OnePlus 5](https://wiki.postmarketos.org/wiki/OnePlus_5_(oneplus-cheeseburger))  
↪ [Enable USB Debugging and OEM Unlock](https://doc.e.foundation/pages/enable-usb-debugging)

## [Android TV](https://www.android.com/tv/) (Cache)

↪ [LineageOS 21 (Android 14)](https://konstakang.com/devices/rpi4/LineageOS21/)  

## [OSMC](https://osmc.tv/) (Cache)

↪ [Installing OSMC on the Raspberry Pi](https://pimylifeup.com/raspberry-pi-osmc/)  
↪ [Chinese-IPTV](https://github.com/BurningC4/Chinese-IPTV)  
↪ [MATVT](https://github.com/virresh/matvt)

## [Home Assistant](https://www.home-assistant.io/) (Cache)

↪ [Home Assistant - Raspberry Pi](https://www.home-assistant.io/installation/raspberrypi/)  
↪ [Android TV Remote](https://www.home-assistant.io/integrations/androidtv_remote/)

## [Charybdis](https://bastardkb.com/charybdis/)

↪ [Required tools](https://docs.bastardkb.com/bg_charybdis/03required_tools.html)  
↪ [Video build guides](https://docs.bastardkb.com/bg_charybdis/video_guides.html)  
↪ [Installing the screw inserts](https://docs.bastardkb.com/bg_charybdis/04screw_inserts.html)  
↪ [Installing the diodes](https://docs.bastardkb.com/bg_charybdis/05diodes.html)  
↪ [Installing the RGB components](https://docs.bastardkb.com/bg_charybdis/06rgb_components.html)  
↪ [Installing the Ribbon Cables](https://docs.bastardkb.com/bg_charybdis/07ribbon_cables.html)  
↪ [Preparing the Splinktegrated](https://docs.bastardkb.com/bg_charybdis/08splinktegrated.html)  
↪ [Preparing the Splinky](https://docs.bastardkb.com/bg_charybdis/08splinky.html)  
↪ [Connecting the ribbon cables to the Splinky](https://docs.bastardkb.com/bg_charybdis/09cables_to_splinky.html)  
↪ [Installing the switches](https://docs.bastardkb.com/bg_charybdis/10install_the_switches.html)  
↪ [Installing the sensor assembly](https://docs.bastardkb.com/bg_charybdis/11sensor_assembly.html)  
↪ [Closing up the case](https://docs.bastardkb.com/bg_charybdis/12final_screws.html)  
↪ [Using your keyboard](https://docs.bastardkb.com/bg_charybdis/13customize.html)

## [Custom QMk 20KeyPad](https://github.com/smrini/QMK-20keyPad) (Cache)