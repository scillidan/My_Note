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

## 3D Printer

↪ [Printing Hextraction for my kids](https://www.jonashietala.se/blog/2024/02/09/printing_hextraction_for_my_kids/)

## Steam Deck

↪ [The killer features of the Steam Deck](https://www.jonashietala.se/blog/2023/10/24/the_killer_features_of_the_steam_deck/)

## [GPi CASE 2](https://retroflag.com/gpi_case_2.html) (TBD)
?↪ [Retro BIOSes](https://github.com/Abdess/retroarch_system)  

Get [SD Memory Card Formatter](https://www.sdcard.org/downloads/formatter/).
Get [Raspberry Pi Imager](https://www.raspberrypi.com/software/).

For [RetroArch](https://www.retroarch.com/), use [RetroArch asset server](https://github.com/NickHeap2/retroarch-asset-server).

For [RetroPie](https://retropie.org.uk/) or [Recalbox](https://www.recalbox.com/), use [Arcade manager](https://github.com/cosmo0/arcade-manager).

Backup `config.txt`

`wifikeyfile.txt`:

```
ssid="<ssid>"
psk="<WifiPassword>"
```

↪ [Retro Gaming With RetroPie, GPi CASE 2, and a Raspberry Pi](https://navendu.me/posts/retropie-gpi-case-2-setup/).

### RetroPie and [ES-DE Frontend](https://gitlab.com/es-de/emulationstation-de)

↪ [Userguide](https://gitlab.com/es-de/emulationstation-de/-/blob/master/USERGUIDE.md)  
↪ [Themes list](https://gitlab.com/es-de/themes/themes-list)  
↪ [Modern for ES-DE](https://gitlab.com/es-de/themes/modern-es-de)

### RetroPie and [Pegasus Frontend](https://github.com/mmatyas/pegasus-frontend)

[Pegasus Tools Collection](https://pegasus-frontend.org/tools/)
[Skyscraper](https://github.com/muldjord/skyscraper)

↪ [Pegasus Docs - Platform Notes: Raspberry](https://pegasus-frontend.org/docs/user-guide/platform-raspberry/#retropie)
↪ [Metadata files](https://pegasus-frontend.org/docs/user-guide/meta-files/)
↪ [Sleipnir](https://github.com/y-muller/retromega-sleipnir)

- [Controller Configuration](https://retropie.org.uk/docs/Controller-Configuration/)  
- [Hotkeys](https://retropie.org.uk/docs/RetroArch-Configuration/#hotkeys)  
- [Xbox 360](https://retropie.org.uk/docs/Xbox-360-Controller/)  
- [Setting up an 8bitdo Bluetooth controller](https://retropie.org.uk/docs/8Bitdo-Controller/)  
- [Virtual Gamepad](https://retropie.org.uk/docs/Virtual-Gamepad/)  
- [Mobile Gamepad](https://github.com/sbidolach/mobile-gamepad)  
- [Configuring WiFi](https://retropie.org.uk/docs/Wifi/)  
- [Transferring Roms](https://retropie.org.uk/docs/Transferring-Roms/)  
- [Netplay](https://retropie.org.uk/docs/Netplay/)  
- [Smaller RetroArch Screen](https://retropie.org.uk/docs/Smaller-RetroArch-Screen/)  
- [Creating Your Own EmulationStation Theme](https://retropie.org.uk/docs/Creating-Your-Own-EmulationStation-Theme/)

- [CaveStory](https://retropie.org.uk/docs/Cave-Story/)  
- [Love](https://retropie.org.uk/docs/Love/)  
- [Raspberry Pi](https://www.renpy.org/doc/html/raspi.html)  
	- [How can I recover my RetroPie after enabling the desktop OpenGL driver?](https://retropie.org.uk/docs/FAQ/#how-can-i-recover-my-retropie-after-enabling-the-desktop-opengl-driver)

On Windows:

```sh
set "HOME=C:/Users/User"
```

```sh
mkdir "%HOME%/Opt"
cd "%HOME%/Opt"
```

1. Download `pegasus-fe*.zip` from releases of [Pegasus Frontend](https://github.com/mmatyas/pegasus-frontend). Decompress it to `pegasus-fe\`.
2. Download portable [RetroArch](https://www.retroarch.com/index.php?page=platforms), liked the `Download (64bit)`. Decompress it to `RetroArch\`.
3. Download [K-Lite Codec Pack Basic](https://codecguide.com/download_k-lite_codec_pack_basic.htm). Install it.

```sh
mkdir "%HOME%/Download/pegasus"
cd "%HOME%/Download/pegasus"
mkdir pegasus-g
```

1. See [天马G PC+安卓双平台 精简Rom整合包 + 8大主题功能演示教程](https://www.bilibili.com/video/BV1vg4y1V7TB), download `跳坑者联盟 PegasusG v1.2 完整版`.
2. Goto `【2】数据文件（安卓+PC）/【1】基础包_110GB`. Select `基础包_110GB Roms.zip.001`, decompress them to `pegasus-g/Roms`.
3. Goto `【3】数据列表（安卓+PC)/【PC】metadata数据列表` , move (or copy) all to `pegasus-g/playlists`.

```
mkdir "%HOME%/Source/pegasus"
cd "%HOME%/Source/pegasus"
```

Clone some themes from [Pegasus Theme Gallery](https://pegasus-frontend.org/tools/themes).

### [Recalbox](https://www.recalbox.com/)

## Android TV (TBD)

↪ [LineageOS 21 (Android 14)](https://konstakang.com/devices/rpi4/LineageOS21/)  
↪ [用树莓派做电视盒子，安装Android TV系统](https://cloud.tencent.com/developer/article/1947011)  
↪ [Kodi](https://kodi.tv/)  
↪ [Chinese-IPTV](https://github.com/BurningC4/Chinese-IPTV)  
↪ [MATVT](https://github.com/virresh/matvt)  
↪ [Android TV Remote Control](https://android-tv-remote-control.en.uptodown.com/android)  
↪ [Home Assistant - Raspberry Pi](https://www.home-assistant.io/installation/raspberrypi/)  
↪ [Android TV Remote](https://www.home-assistant.io/integrations/androidtv_remote/)