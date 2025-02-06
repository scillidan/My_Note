## Install

### Log In

Login with:

```
username: root
password: root
```

↪ [alarm login?](https://github.com/altreact/archbk/issues/9)

### [Wireless](https://wiki.archlinux.org/title/Network_configuration/Wireless) (Optional)

```sh
ip link
systemctl status iwd
systemctl restart iwd
systemctl status iwd
iwctl
device list
station wlan0 scan
station wlan0 get-networks
station wlan0 connect "<SSID>"
ping archlinux.org
```

### [Pacman](https://pacman.archlinux.page/)

```sh
sudo pacman -S vim
sudo vim /etc/pacman.conf
```

```
Color
ParalleDownloads = 5
ILoveCandy
```

↪ [10 Things You MUST DO After Installing Arch Linux (2023)](https://www.youtube.com/watch?v=odgD_RdJjCU)

```sh
sudo cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.bak
sudo vim /etc/pacman.d/mirrorlist
```

```
Server = https://mirrors.ustc.edu.cn/archlinux/$repo/os/$arch
```

↪ [USTC Mirror Help - Arch Linux](https://mirrors.ustc.edu.cn/help/archlinux.html)

Refreshes the package database and upgrades all installed packages:

```sh
pacman -Syyu
```

Additional tools for `pacman`:

```sh
sudo pacman -S pacman-contrib
```

Removes older versions of packages from the cache, keeping only the two most recent versions for each one.

```sh
sudo paccache -rk 2
```

### [Users and groups](https://wiki.archlinux.org/title/Users_and_groups)

```sh
sudo useradd -m <User>
sudo vim /etc/sudoers
```

```
<User> ALL=(ALL:ALL) ALL
```

Or:

```sh
sudo addgroup sudouser
sudo usermod -aG sudouser <User>
sudo vim /etc/sudoers
```

```
sudouser ALL=(ALL)ALL
```

Finally:

```sh
reboot
```

### [Localization](https://wiki.archlinux.org/title/Localization)

```sh
sudo vim /etc/locale.gen
```

```
en_US.UTF-8 UTF-8
zh_CN.UTF-8 UTF-8
```

```sh
sudo locale-gen
```

```sh
sudo vim /etc/locale.conf
```

```
LANG=en_US.UTF-8
```

↪ [Localization/Simplified Chinese](https://wiki.archlinux.org/title/Localization/Simplified_Chinese)

### [System time](https://wiki.archlinux.org/title/System_time)

```sh
timedatectl set-timezone Asia/Chongqing
```

### [Set the hostname](https://wiki.archlinux.org/title/Network_configuration#Set_the_hostname)

```sh
sudo vim /etc/hostname
```

```
<hostname>
```

```sh
sudo systemctl restart systemd-hostnamed
```

### [Domain name resolution](https://wiki.archlinux.org/title/Domain_name_resolution)

```sh
sudo vim /etc/hosts
```

```
<ip> github.com
<ip> raw.githubusercontent.com
<ip> mirror.archlinuxarm.org
```

```sh
sudo systemctl restart systemd-resolved
```

↪ [hosts](https://man.archlinux.org/man/hosts.5)

### [NetworkManager](https://wiki.archlinux.org/title/NetworkManager)

```sh
sudo pacman -S networkmanager
sudo systemctl stop netctl
sudo systemctl disable netctl
sudo systemctl enable --now networkmanager
```

Enable system tray:

```sh
sudo pacman -S network-manager-applet
```

## Setup

### [yay](https://github.com/Jguer/yay)

<!-- --8<-- [start:virtualbox] -->
In [VirtualBox](https://www.virtualbox.org/), need to use `arch-chroot`.

```sh
sudo pacman -S fakeroot
sudo useradd -m auruser
sudo passwd auruser
su - auruser
cd yay-bin
makepkg
```
<!-- --8<-- [end:virtualbox] -->

### [Paru](https://github.com/Morganamilo/paru) (Optional)

```sh
sudo pacman -S paru
```

### [Flatpak](https://github.com/flatpak/flatpak) (Optional)

```sh
sudo pacman -S flatpak
reboot
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
flatpak install org.freefilesync.FreeFileSync
```

↪ [[Bug]: "SSL peer certificate or SSH remote key was not OK" during extra-data download, only on Ubuntu-based distros](https://github.com/flatpak/flatpak/issues/5253)

You can find apps on [Flathub](https://flathub.org/).

### [Uncomplicated Firewall](https://wiki.archlinux.org/title/Uncomplicated_Firewall)

```sh
sudo pacman -S ufw
sudo ufw status
sudo systemctl enable --now ufw
sudo ufw status
```

### SSH

↪ [enable SSH on Arch Linux](https://medium.com/@pythonaugust/enable-ssh-on-arch-linux-8f1ede0d9c88)

```sh
sudo pacman -S openssh
sudo systemctl enable --now sshd
sudo ufw allow 22/tcp
ip addr show
```

Get your `ip` of `inet`. On client machine:

```sh
ssh <user>@<ip>
```

### [Xfce](https://wiki.archlinux.org/title/Xfce)

```sh
sudo pacman -S xorg
sudo pacman -S xfce4 xfce4-goodies
```

↪ [Install XFCE Desktop on Arch Linux](https://linuxopsys.com/topics/install-xfce-desktop-on-arch-linux)

### i3 (Optional)

```sh
sudo pacman -S i3
```

↪ [How to Use i3 with XFCE](https://www.youtube.com/watch?v=nZTBxJ_gr8w)

### [Hyprland](https://hyprland.org/) (Cache)

### [Sway](https://swaywm.org/) (Cache)

↪ [Sway on Arch Linux: 2023 Edition (From Scratch)](https://www.youtube.com/watch?v=QAmTUkzpIiM)

### [Nemo](https://wiki.archlinux.org/title/Nemo) (Optional)

```sh
sudo pacman -S nemo
```

↪ [Set dark theme on dolphin in cinnamon](https://forum.manjaro.org/t/set-dark-theme-on-dolphin-in-cinnamon/122034/7)

### [LightDM](https://wiki.archlinux.org/title/LightDM)

```sh
sudo pacman -S lightdm lightdm-webkit2-greeter
```

↪ [Arch linux install lightdm (Light Display Manager)](https://gist.github.com/miguelmota/5087fb8d92599efc4748c134846c8daf)

```sh
git clone --depth=1 https://github.com/TheTerrior/lightdm-minimal
cd lightdm-minimal
chmod +x ./risky_installer.sh
sudo ./risky_installer.sh
sudo vim /etc/lightdm/lightdm.conf
```

```
[Seat:*]
greeter-session=lightdm-webkit2-greeter
```

```sh
sudo vim /etc/lightdm/lightdm-webkit2-greeter.conf
```

```
webkit_theme = minimal
```

```sh
sudo systemctl enable --now lightdm
```

↪ [A minimal LightDM WebKit2 theme](https://github.com/TheTerrior/lightdm-minimal)

### [xfce-tile](https://github.com/dodophoenix/xfce-tile) (Optional)

```sh
git clone --depth=1 https://github.com/dodophoenix/xfce-tile
cd xfce-tile
vim xfce-tile
chmod +x ./xfce-setup-shortcuts.sh
./xfce-setup-shortcuts.sh
```

### Console font (Optional)

```sh
showconsolefont
ls /user/share/kbd/showconsolefont
sudo pacman -S terminus-font
setfont drdos8x14 -m 8859-2
```

↪ [How to Change Linux Console Fonts on Arch Linux](https://www.youtube.com/watch?v=nxUTnZVdS64)  
↪ [Linux console - Fonts](https://wiki.archlinux.org/title/Linux_console#Fonts)

### Bluetooth

```sh
sudo pacman -S bluez bluez-utils blueman
sudo systemctl enable --now bluetooth
systemctl status bluetooth
sudo vim /etc/bluetooth/main.conf
```

```
AutoEnable=true
```

↪ [Bluetooth headset connection occasionally fails: br-connection-page-timeout](https://www.reddit.com/r/archlinux/comments/qnffce/bluetooth_headset_connection_occasionally_fails/)  
↪ [How to Set up Bluetooth in Arch Linux](https://www.jeremymorgan.com/tutorials/linux/how-to-bluetooth-arch-linux/)

If return `Bluetooth service was skipped because of an unmet condition check ...`:

```sh
sudo modprobe bluetooth
sudo systemctl restart bluetooth
systemctl status bluetooth
```

↪ [Bluetooth not working on computer](https://www.linuxquestions.org/questions/linux-hardware-18/bluetooth-not-working-on-computer-4175724971/)  

### Audio

```sh
sudo pacman -S pulseaudio
sudo pacman -R pulseaudio
yay -S pipewire-pulse
sudo systemctl enable --now pipewire
```

### USB drive

```sh
sudo pacman -S udisks2
```

```sh
sudo fdisk -l
udisksctl mount -b /dev/sda1
udisksctl unmount -b /dev/sda1
udisksctl power-off -b /dev/sda
```

↪ [Using USB drives on Arch](https://ejmastnak.com/tutorials/arch/usb/)

### [auto-cpufreq](https://github.com/AdnanHodzic/auto-cpufreq)

```sh
git clone --depth=1 https://github.com/AdnanHodzic/auto-cpufreq.git
cd auto-cpufreq
sudo ./auto-cpufreq-installer
sudo auto-cpufreq --install
sudo systemctl status auto-cpufreq
sudo auto-cpufreq --stats
```

↪ [10 Things You MUST DO After Installing Arch Linux (2023)](https://www.youtube.com/watch?v=odgD_RdJjCU)

### [preload](http://sourceforge.net/projects/preload)

```sh
yay -S preload
sudo systemctl enable --now preload
sudo systemctl status preload
```

```sh
sudo systemctl stop preload && sudo systemctl disable preload
sudo reboot
```

↪ [10 Things You MUST DO After Installing Arch Linux (2023)](https://www.youtube.com/watch?v=odgD_RdJjCU)

### [Timeshift](https://github.com/teejee2008/timeshift)

```sh
yay -S timeshift
```

```sh
sudo timeshift --list
sudo timeshift --restore --snapshot '20XX-XX-XX_XX-XX-XX' --skip-grub
```

↪ [10 Things You MUST DO After Installing Arch Linux (2023)](https://www.youtube.com/watch?v=odgD_RdJjCU)

### [restic](https://restic.net/) (TBD)

### Application Autostart

Settings → Session and Startup → Application Autostart → Add:

```
Name `<Name>`
Command `<Command>`
```

## Install Applications

### [picom](https://github.com/yshui/picom)

```sh
sudo pacman -S picom
```

### [dunst](https://github.com/dunst-project/dunst)

```sh
sudo pacman -S dunst
```

### [qutebrowser](https://qutebrowser.org/) (Cache)

```sh
pacman -S qutebrowser
```

qutebrowser → `:open aur.archlinux.org`

### [mpv](https://mpv.io/)

```sh
sudo pacman -S mpv
cp -r /usr/share/doc/mpv/ ~/.config/
```

### [ClamAV](https://www.clamav.net/)

```sh
sudo pacman -S clamav
```

```sh
clamd
clamscan <file>
```

If return `ERROR: Can't create freshclam.dat in /usr/local/share/clamav`:

```sh
sudo chown -R <user> /usr/local/share/clamav
```

↪ [Can't create freshclam.dat in /usr/local/share/clamav](https://docs.clamav.net/faq/faq-freshclam.html#cant-create-freshclamdat-in-usrlocalshareclamav)

### [Rime](https://rime.im/)

```sh
sudo pacman -S fcitx5-im
```

```
sudo vim /etc/environment
```

```
GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
XMODIFIERS=fcitx
SDL_IM_MODULE=fcitx
```

### Clipboard

```sh
sudo pacman -S copyq
sudo pacman -R xfce4-clipman-plugin
```

### [qView](https://interversehq.com/qview/) (Optional)

```sh
yay -S qview
```

### [Flameshot](https://flameshot.org/) (Optional)

### [eSearch](https://github.com/xushengfeng/eSearch) (Optional)

```sh
git clone --depth=1 https://aur.archlinux.org/e-search-bin.git
```

Download `eSearch-*-linux-x64.deb` from [releases](https://github.com/xushengfeng/eSearch/releases).

```sh
mv eSearch-*-linux-x64.deb e-search-*.deb
mv e-search-*.deb e-search-bin/
cd e-search-bin
makepkg
sudo pacman -U e-search-bin-*-1-x86_64.pkg.tar.zst
```

### [Umi-OCR](https://github.com/hiroi-sora/Umi-OCR)

Get `Umi-OCR_Linux_Paddle_*.tar.xz` from [Umi-OCR - Releases](https://github.com/hiroi-sora/Umi-OCR/releases).

```sh
tar -xf Umi-OCR_Linux_Paddle_*.tar.xz
mv Umi-OCR_Linux_Paddle_* Umi-OCR_Linux_Paddle
./umi-ocr.sh
```

### [Goldendict](https://github.com/goldendict/goldendict)

Download `goldendict-1_1.5.0-3-x86_64.pkg.tar.zst`, `qt5-webkit-5.212.0alpha4-22-x86_64.pkg.tar.zst` from https://sourceforge.net/projects/fabiololix-os-archive/files/Packages/

```sh
sudo pacman -U qt5-webkit-5.212.0alpha4-22-x86_64.pkg.tar.zst
sudo pacman -U goldendict-1_1.5.0-3-x86_64.pkg.tar.zst
yay -Ql goldendict
```

### [Rofi](https://github.com/davatorium/rofi)

```sh
sudo pacman -S rofi
```

### [rofi-shortcuts](https://github.com/Zeioth/rofi-shortcuts) (Optional)

```sh
git clone --depth=1 https://github.com/Zeioth/rofi-shortcuts
cd rofi-shortcuts
```

```sh
mkdir -p ~/.config/rofi/rofi-shortcuts/
mkdir -p ~/.local/share/rofi/rofi-shortcuts/
cp ./rofi-shortcuts.conf ~/.config/rofi/rofi-shortcuts/rofi-shortcuts.conf
cp ./rofi-shortcuts.sh ~/.local/share/rofi/rofi-shortcuts/rofi-shortcuts.sh
chmod u+x ~/.local/share/rofi/rofi-shortcuts/rofi-shortcuts.sh
ln -sf ~/.local/share/rofi/rofi-shortcuts/rofi-shortcuts.sh ~/.local/bin/rofi-shortcuts
```

```sh
rofi-shortcuts
```

### [rofi-calc](https://github.com/svenstaro/rofi-calc) (Optional)

```sh
sudo pacman -S rofi-calc
rofi -show calc -modi calc -no-show-match -no-sort
```

### [Rofimoji](https://github.com/fdw/rofimoji)

```sh
sudo pacman -S rofimoji
```

### [rofi-copyq](https://github.com/cjbassi/rofi-copyq)

```sh
git clone --depth=1 https://github.com/cjbassi/rofi-copyq
cd rofi-copyq
./rofi-copyq
```

### [AHK_X11](https://github.com/phil294/AHK_X11) (Cache)

```sh
yay -S ahk_x11-bin
```

### [keymapper](https://github.com/houmain/keymapper) (TBD)

```sh
yay -S keymapper
sudo systemctl enable --now keymapperd
```

### [Libre Office](https://www.libreoffice.org/) (Cache)

### [Input Leap](https://github.com/input-leap/input-leap)

```sh
yay -S input-leap-git
input-leap
```

On PC, install [Barrier](https://github.com/debauchee/barrier).

### [WeChat](https://flathub.org/apps/com.tencent.WeChat)

```sh
flatpak install flathub com.tencent.WeChat
```

### Photoshop CC (Cache)

↪ [Photoshop CC v19 installer for Linux](https://github.com/Gictorbit/photoshopCClinux)  
↪ [error: sorry something went wrong during download photoshopCC-V19.1.6-2018x64.tgz](https://github.com/Gictorbit/photoshopCClinux/issues/175)  
↪ [Dropbox link to download photoshopCC-V19.1.6-2018x64.tgz is broken](https://github.com/Gictorbit/photoshopCClinux/issues/40)

## Configure Desktop

### [Materia](https://github.com/nana-4/materia-theme)

```sh
sudo pacman -S materia-gtk-theme
```

Appearance → Style → Materia-dark-compact → Close → Log Out Account → Log In

### [Papirus](https://github.com/PapirusDevelopmentTeam/papirus-icon-theme)

```sh
sudo pacman -S papirus-icon-theme
```

Appearance → Icons → `Papirus-Dark`

### [SIF](https://github.com/BlueManCZ/SIF) (Optional)

### Cursor

1. Get `Bibata-Rainbow-*.tar.gz` from [Bibata Cursor Rainbow - Releases](https://github.com/ful1e5/Bibata_Cursor_Rainbow/releases).  
2. Get `Chroma-*.tar.xz` from [Chroma Cursors for Linux](https://www.gnome-look.org/p/2045954).

```sh
mkdir ~/.icons
cd ~/.icons
move *.tar.* ./
tar -xvf Bibata-Rainbow-Modern.tar.gz
tar -xvf Bibata-Rainbow-Original.tar.gz
tar -xvf Chroma-Black-M.tar.xz
tar -xvf Chroma-Black-S.tar.xz
```

Mouse and Touchpad → Theme → `<Theme>`

### Applications Menu

```sh
mv <png> into ~/.icons
```

Icon → Select icon from `All Icons` → Search icon → [Lake.png](https://github.com/scillidan/icon-bloodborne-caryll-runes/blob/main/png-white/Lake.png) (for example)

↪ [Desktop entries](https://wiki.archlinux.org/title/desktop_entries)

### Wallpaper

```sh
mkdir -p ~/Pictures/wallpaper
mv <wallpaper> ~/Pictures/wallpaper/
# sudo chown -R ~/Pictures/wallpaper/*.jpg
sudo pacman -S nitrogen
```

nitrogen → Preferences → Add → `~/Pictures/wallpaper` → OK → Apply

### Fonts

```sh
sudo pacman -S adobe-source-han-serif-cn-fonts
sudo pacman -S noto-fonts-cjk noto-fonts-emoji noto-fonts-extra
```

## Configure Terminal

## [Alacritty](https://alacritty.org/)

```sh
sudo pacman -S alacritty
sudo pacman -R xfce4-terminal
```

### [Starship](https://starship.rs/)

```sh
yay -S starship
```

### [Oh My Zsh](https://ohmyz.sh/)

```sh
pacman -S zsh
sh -c "$(wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```

If network error:

```sh
wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh 
sudo chmod +x ./install.sh
sudo ./install.sh
```

<!-- --8<-- [start:ubuntu-22-arm] -->
If errors about `permission` (on the ARM architecture):

```sh
export ZSH=$HOME/.oh-my-zsh
echo $ZSH
sh -c "$(wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```

↪ [Won't install for my user, only for root...](https://github.com/ohmyzsh/ohmyzsh/issues/8477)

```sh
git config --global http.version 1.1
git config --global http.postBuffer 157286400
```

```sh
git config --global http.version 2
git config --global http.postBuffer 1M
```

↪ [git-config-http-version.md](https://gist.github.com/daopk/0a95772d582cafb202142ff7871da2fc)
<!-- --8<-- [end:ubuntu-22-arm] -->

```sh
chsh -l
chsh -s /usr/bin/zsh
```

Or:

```sh
vim ~/.bashrc
```

```
exec zsh
```

↪ [Changing your default shell](https://wiki.archlinux.org/title/Command-line_shell#Changing_your_default_shell)

### [fzf](https://github.com/junegunn/fzf)

```sh
sudo pacman -S fzf
```

### [Atuin](https://github.com/atuinsh/atuin)

```sh
sudo pacman -S atuin
```

## [Zellij](https://zellij.dev/)

```sh
sudo pacman -S zellij
```

```sh
mkdir -p ~/.config/zellij/plugins
cd ~/.config/zellij/plugins
wget https://github.com/dj95/zjstatus/releases/download/v0.13.1/zjstatus.wasm
```

### [Cmus](https://cmus.github.io/)

```sh
sudo pacman -S cmus
```

### [sdcv](https://dushistov.github.io/sdcv/)

```sh
sudo pacman -S sdcv
```

### [deep-translator](https://github.com/nidhaloff/deep-translator)

```sh
pipx install deep-translator
```

## dotfile

↪ [dotfiles-linux](https://github.com/fathulfahmy/dotfiles-linux)

## [Proton](https://github.com/ValveSoftware/Proton)