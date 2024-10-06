## Arch Linux

<!-- Part 1 -->

## Log In

Login with:

```
username: root
password: root
```

↪ [alarm login?](https://github.com/altreact/archbk/issues/9)

## [Wireless](https://wiki.archlinux.org/title/Network_configuration/Wireless) (Optional)

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

## [Pacman](https://pacman.archlinux.page/)

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
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinux/$repo/os/$arch
```

↪ [USTC Mirror Help - Arch Linux](https://mirrors.ustc.edu.cn/help/archlinux.html)  
↪ [清华大学开源软件镜像站 - Arch Linux 软件仓库](https://mirrors.tuna.tsinghua.edu.cn/help/archlinux/)

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

## [Users and groups](https://wiki.archlinux.org/title/Users_and_groups)

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

## [Localization](https://wiki.archlinux.org/title/Localization)

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

## [System time](https://wiki.archlinux.org/title/System_time)

```sh
timedatectl set-timezone Asia/Chongqing
```

## [Set the hostname](https://wiki.archlinux.org/title/Network_configuration#Set_the_hostname)

```sh
sudo vim /etc/hostname
```

```
<HostName>
```

```sh
sudo systemctl restart systemd-hostnamed
```

## [Domain name resolution](https://wiki.archlinux.org/title/Domain_name_resolution)

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

## [NetworkManager](https://wiki.archlinux.org/title/NetworkManager)

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

<!-- Part 2 -->

## [yay](https://github.com/Jguer/yay)

```sh
sudo pacman -S go
go env -w GO111MODULE=on
go env -w GOPROXY=https://goproxy.cn,direct
go env
```

↪ [How to Install and Use Yay on Arch Linux](https://www.makeuseof.com/install-and-use-yay-arch-linux/)

```sh
sudo pacman -S --needed git base-devel
git clone --depth=1 https://aur.archlinux.org/yay-bin.git
cd yay-bin
makepkg
sudo pacman -U yay-bin*.pkg.tar.xz
yay
```

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

## [Paru](https://github.com/Morganamilo/paru) (Optional)

```sh
yay -S paru
```

## [Flatpak](https://github.com/flatpak/flatpak) (Optional)

```sh
sudo pacman -S flatpak
reboot
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
flatpak install org.freefilesync.FreeFileSync
```

↪ [[Bug]: "SSL peer certificate or SSH remote key was not OK" during extra-data download, only on Ubuntu-based distros](https://github.com/flatpak/flatpak/issues/5253)

You can find apps on [Flathub](https://flathub.org/).

## [Uncomplicated Firewall](https://wiki.archlinux.org/title/Uncomplicated_Firewall)

```sh
sudo pacman -S ufw
sudo ufw status
sudo systemctl enable --now ufw
sudo ufw status
```

## SSH

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

## [Xfce](https://wiki.archlinux.org/title/Xfce)

```sh
sudo pacman -S xorg
sudo pacman -S xfce4 xfce4-goodies
```

↪ [Install XFCE Desktop on Arch Linux](https://linuxopsys.com/topics/install-xfce-desktop-on-arch-linux)

## [Nemo](https://wiki.archlinux.org/title/Nemo) (Optional)

```sh
sudo pacman -S nemo
```

↪ [Set dark theme on dolphin in cinnamon](https://forum.manjaro.org/t/set-dark-theme-on-dolphin-in-cinnamon/122034/7)

## [LightDM](https://wiki.archlinux.org/title/LightDM)

```sh
sudo pacman -S lightdm lightdm-webkit2-greeter
```

↪ [Arch linux install lightdm (Light Display Manager)](https://gist.github.com/miguelmota/5087fb8d92599efc4748c134846c8daf)

```sh
git clone https://github.com/TheTerrior/lightdm-minimal
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

## [xfce-tile](https://github.com/dodophoenix/xfce-tile)

```sh
git clone https://github.com/dodophoenix/xfce-tile
cd xfce-tile
vim xfce-tile
chmod +x ./xfce-setup-shortcuts.sh
./xfce-setup-shortcuts.sh
```

## [Materia](https://github.com/nana-4/materia-theme)

```sh
sudo pacman -S materia-gtk-theme
```

Appearance → Style → Materia-dark-compact → Close → Log Out Account → Log In

## [Papirus](https://github.com/PapirusDevelopmentTeam/papirus-icon-theme)

```sh
sudo pacman -S papirus-icon-theme
```

Appearance → Icons → `Papirus-Dark`

## [SIF](https://github.com/BlueManCZ/SIF) (Optional)

## i3 (Optional)

```sh
sudo pacman -S i3
```

↪ [How to Use i3 with XFCE](https://www.youtube.com/watch?v=nZTBxJ_gr8w)

I used `xfce` desktop, but I configured it with reference to [dotfiles-linux](https://github.com/fathulfahmy/dotfiles-linux).

```sh
yay -S alacritty starship rofi
```

## [picom](https://github.com/yshui/picom)

```sh
sudo pacman -S picom
```

## [dunst](https://github.com/dunst-project/dunst)

```sh
sudo pacman -S dunst
```

## Applications Menu

↪ https://wiki.archlinux.org/title/desktop_entries

Put `.png` into `~/.icons`.

Icon → Select icon from `All Icons` → Search icon

↪ https://github.com/scillidan/icon-bloodborne-caryll-runes/blob/main/png-white/Lake.png

## Cursor

↪ https://github.com/ful1e5/Bibata_Cursor_Rainbow
↪ https://www.gnome-look.org/p/2045954

```sh
mkdir ~/.icons
cd ~/.icons
```

Move the `.tar.gz` and `.tar.xz` here, then:

```sh
tar -xvf Bibata-Rainbow-Modern.tar.gz
tar -xvf Bibata-Rainbow-Original.tar.gz
tar -xvf Chroma-Black-M.tar.xz
tar -xvf Chroma-Black-S.tar.xz
```

Mouse and Touchpad → Theme → `TheTheme`

## Wallpaper

```sh
mkdir -p ~/Pictures/wallpaper
```

Put wallpapers in.

```sh
sudo pacman -S nitrogen
```

nitrogen → Preferences → Add → `~/Pictures/wallpaper` → OK → Apply

```sh
sudo chown -R *.jpg
```

↪ https://github.com/scillidan/Cos_Cache/blob/main/wallpaper/%E9%A2%A8%E8%88%B9%E3%81%AE%E6%97%85%E7%AB%8B%E3%81%A1_2k.png

## Hyprland (x)

## sway 

↪ https://www.youtube.com/watch?v=QAmTUkzpIiM

## terminus-font (Optional)

↪ https://www.youtube.com/watch?v=nxUTnZVdS64
↪ https://wiki.archlinux.org/title/Linux_console#Fonts

```sh
showconsolefont
ls /user/share/kbd/showconsolefont
sudo pacman -S terminus-font
setfont drdos8x14 -m 8859-2
```

## Bluetooth

```sh
sudo pacman -S bluez bluez-utils blueman
sudo systemctl enable --now bluetooth
systemctl status bluetooth
```

```sh
sudo vim /etc/bluetooth/main.conf
```

```sh
AutoEnable=true
```

If `Bluetooth service was skipped because of an unmet condition check ...`:

```sh
sudo modprobe bluetooth
sudo systemctl restart bluetooth
systemctl status bluetooth
```

↪ https://www.linuxquestions.org/questions/linux-hardware-18/bluetooth-not-working-on-computer-4175724971/

## Audio

```sh
sudo pacman -S pulseaudio
sudo pacman -R pulseaudio
```

```sh
yay -S pipewire-pulse
sudo systemctl enable --now pipewire
```

## ZeroTier

Log-in [ZeroTier](https://my.zerotier.com) to create a Network.

```sh
sudo pacman -S zerotier-one
sudo systemctl enable --now zerotier-one.service
systemctl status zerotier-one.service
sudo zerotier-cli join <NetworkID>
```

Go back to `Network` board of ZeroTier, check the newly discovered machine.

## USB (Optional)

↪ https://ejmastnak.com/tutorials/arch/usb/

```sh
sudo pacman -S udisks2
sudo fdisk -l
udisksctl mount -b /dev/sda1
udisksctl unmount -b /dev/sda1
udisksctl power-off -b /dev/sda
```

## Samba

↪ https://linuxways.net/arch/install-configure-samba-arch-linux/  
↪ https://forum.manjaro.org/t/samba-error-code-22/106741/9

```sh
sudo pacman -S samba
sudo pacman -Qi samba
sudo vim /etc/samba/smb.conf
```

Copy from https://git.samba.org/samba.git/?p=samba.git;a=blob_plain;f=examples/smb.conf.default;hb=HEAD.

```
workgroup = SAMBAGROUP
```

```
[sambashare1]
comment = My Samba Share
path = /data/smb/share1
writable = yes
browsable = yes
create mask = 0700
directory mask = 0700
read only = no
guest ok = no
```

```sh
sudo groupadd -r smbusers
sudo useradd -m sambauser
sudo usermod -aG smbusers sambauser
sudo smbpasswd -a sambauser
sudo mkdir -p /data/smb/share1
sudo chown -R :smbusers /data/smb/share1
sudo chmod 1770 /data/smb/share1
sudo systemctl enable --now smb
sudo systemctl enable --now nmb
testparm
```

On PC, 计算机管理 → 本地用户和组 → 用户 → 右键 → 新用户:

```
用户名 `sambauser`
用户不能更改密码 On 
密码永不过期 On
```

本地用户和组 → 组 → 右键 → 新建组 → 组名 `SAMBAGROUP` → 添加 → 输入对象名称来选择 `sambauser` → 确认 → 创建

资源管理器 → 此电脑 → 右键 → 添加一个网络位置 → 指定网站的位置 → `\\YourIP\sambashare` → 请键入该网络位置的名称 `sambashare` → 

`sambashare` → 右键 → 映射网络驱动器 → 登录时重新连接 On → 完成

```sh
sudo mkdir /home/sambauser/server
sudo chown -R sambauser /home/sambauser/server
sudo mount -t cifs //YourIP/sambashare /home/sambauser/server -o username=sambauser,password=YourPassword,workgroup=SAMBAGROUP
sudo systemctl daemon-reload
sudo mount
```

↪ https://forum.manjaro.org/t/mounting-a-nas-using-systemd-mount-error-cifs-filesystem-not-supported-by-the-system/119153

If `mount error: cifs filesystem not supported by the system`:

```sh
sudo reboot
sudo mount -t cifs //YourIP/sambashare /home/sambauser/server -o username=sambauser,password=YourPassword,workgroup=ARCHGROUP
```

↪ https://gist.github.com/ammgws/1dbd8b3bb38b588c1bb8b3f70dd4fd2c  
↪ https://askubuntu.com/questions/36608/ufw-firewall-still-blocking-smb-despite-adding-rules

```sh
sudo vim /etc/ufw/applications.d/samba
```

```
[Samba]
title=LanManager-like file and printer server for Unix
description=The Samba software suite is a collection of programs that implements the SMB/CIF$
ports=137,138/udp|139,445/tcp
```

```sh
sudo ufw allow samba
sudo ufw status
```

Finally. If not work, try:

```sh
sudo systemctl status smb.service
sudo systemctl status nmb.service
sudo mkdir -p /usr/local/samba/var
sudo systemctl restart nmb.service
sudo systemctl status nmb.service
sudo systemctl restart smb.service
sudo systemctl status smb.service
sudo mount
sudo umount server/
sudo mount -t cifs //YourIP/sambashare /home/sambauser/server -o username=sambauser,password=YourPassword,workgroup=ARCHGROUP
sudo systemctl daemon-reload
sudo mount
```

↪ https://www.linuxquestions.org/questions/linux-networking-3/nemo-smb-not-working-4175717802/
↪ https://forum.endeavouros.com/t/cinnamon-nemo-file-manager-not-open-network-shares/12404

## NFS (Cache)

↪ https://www.youtube.com/watch?v=ZparikqAo3E

## VNC

↪ https://rushichaudhari.github.io/posts/2020-10-29-setting-up-tigervncserver-on-arch-linux-raspberry-pi/  
↪ https://www.youtube.com/watch?v=w1HS_xVnFFo  
↪ https://bytexd.com/how-to-install-configure-vnc-server-on-ubuntu/

```sh
sudo pacman -S tigervnc
vncpasswd
```

```sh
sudo useradd -m vncuser
sudo passwd vncuser
sudo groupadd -r vncusers
sudo usermod -aG vncusers vncuser
```

```sh
sudo vim /etc/tigervnc/vncserver.users
```

```
:1=vncuser
```

LXDE相比Xfce有着更低的功耗。

```sh
sudo pacman -S lxde
```

```sh
mkdir ~/.vnc 
vim ~/.vnc/xstartup
```

```
#!/bin/bash
exec lxde &>/dev/null
```

```sh
vim ~/.vnc/config
```

```
session=lxde
geometry=1280x720
localhost
alwaysshared
```

```sh
vncserver :1
```

On PC:

```sh
tvnviewer YourIP::5901 -password=YourVNCPassword
```

```sh
sudo systemctl enable --now vncserver@:1
systemctl status vncserver@:1
```

But I:

```sh
rm -rf ~/.vnc
mkdir ~/.vnc
vim ~/.vnc/config
```

```sh
session=xfce
geometry=1280x720
# localhost
alwaysshared
```

## auto-cpufreq

↪ https://www.youtube.com/watch?v=odgD_RdJjCU

```sh
git clone https://github.com/AdnanHodzic/auto-cpufreq.git
cd auto-cpufreq
sudo ./auto-cpu-freq-installer
sudo auto-cpufreq --install
sudo systemctl status auto-cpufreq
sudo auto-cpufreq --stats
```

## preload

↪ https://www.youtube.com/watch?v=odgD_RdJjCU

```sh
yay -S preload
sudo systemctl enable --now preload
sudo systemctl status preload
```

```sh
sudo systemctl stop preload && sudo systemctl disable preload
sudo reboot
```

## timeshift

↪ https://www.youtube.com/watch?v=odgD_RdJjCU

```sh
yay -S timeshift
```

```sh
sudo timeshift --list
sudo timeshift --restore --snapshot '20XX-XX-XX_XX-XX-XX' --skip-grub
```

## Fonts

```sh
sudo pacman -S adobe-source-han-serif-cn-fonts
sudo pacman -S noto-fonts-cjk noto-fonts-emoji noto-fonts-extra
```

## Rime

```sh
sudo pacman -S fcitx5-im

sudo vim /etc/environment
```

```
GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
XMODIFIERS=fcitx
SDL_IM_MODULE=fcitx
```

## Clipboard

```sh
sudo pacman -S copyq
sudo pacman -R xfce4-clipman-plugin
```

## qutebrowser (Optional)

```sh
pacman -S qutebrowser
```

```sh
:open aur.archlinux.org
```

左键点击 > Y > Enter

## Zsh

↪ https://ohmyz.sh/#install

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

↪ https://github.com/ohmyzsh/ohmyzsh/issues/8477

If errors about `permission` on the ARM architecture:

```sh
export ZSH=$HOME/.oh-my-zsh
echo $ZSH
sh -c "$(wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```

↪ https://gist.github.com/daopk/0a95772d582cafb202142ff7871da2fc

```sh
git config --global http.version 1.1
git config --global http.postBuffer 157286400
```

```sh
git config --global http.version 2
git config --global http.postBuffer 1M
```

↪ https://wiki.archlinux.org/title/Command-line_shell#Changing_your_default_shell

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

## fzf

```sh
sudo pacman -S fzf
```

## Atuin

```sh
sudo pacman -S atuin
```

## Starship (Optional)

↪ https://starship.rs/

## Alacritty

```sh
sudo pacman -S alacritty
sudo pacman -R xfce4-terminal
```

## Zellij

```sh
sudo pacman -S zellij
```

```sh
mkdir -p ~/.config/zellij/plugins
cd ~/.config/zellij/plugins
wget https://github.com/dj95/zjstatus/releases/download/v0.13.1/zjstatus.wasm
```

### pyenv

↪ https://github.com/pyenv/pyenv

```sh
sudo pacman -S pyenv
```

```sh
vim ~/.zshrc
```

```
export PYENV_ROOT="$HOME/.pyenv"
[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
```

```sh
source ~/.zshrc
pyenv install 3.9.13
```

If network errors:

```sh
mkdir ~/.pyenv/cache
cd ~/.pyenv/cache
wget https://www.python.org/ftp/python/3.9.13/Python-3.9.13.tar.xz
wget https://www.python.org/ftp/python/3.10.11/Python-3.10.11.tar.xz
```

```sh
pyenv install 3.9.13
pyenv install 3.10.11
```

```sh
pyenv local 3.9.13
pyenv exec pip install virtualenv
virtualenv virtualenv
source virtualenv/bin/activate
```

## pyenv-virtualenv

↪ https://jinmay.github.io/2019/03/16/linux/ubuntu-install-pyenv-1/

```sh
git clone https://github.com/yyuu/pyenv-virtualenv.git ~/.pyenv/plugins/pyenv-virtualenv
vim ~/.zshrc
```

```
eval "$(pyenv virtualenv-init -)"
```

```sh
source ~/.zshrc
pyenv virtualenv 3.9.13 test-venv
cd MyProject
pyenv local test-venv
```

## pipx

```
sudo pacman -S python-pipx
```

## nvm

↪ https://github.com/nvm-sh/nvm#installing-and-updating

```sh
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```

```sh
vim .zshrc
```

```
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
```

```sh
source ~/.zshrc
nvm ls-remote
nvm install Gallium
nvm install Hydrogen
nvm use 18.20.1
```

## pnpm

↪ https://pnpm.io/installation

```sh
sudo pacman -S pnpm
```

## Rust

↪ https://rustup.rs/

```sh
curl https://sh.rustup.rs -sSf | sh
rustup default stable
```

## rvm

```
yay -S rvm
```

## Docker (x)

↪ https://itsfoss.com/install-docker-arch-linux/

```sh
sudo pacman -S docker
sudo systemctl enable --now docker.service
```

## Rofi

↪ https://github.com/davatorium/rofi

```sh
sudo pacman -S rofi
```

## rofi-shortcuts

↪ https://github.com/Zeioth/rofi-shortcuts

```sh
git clone https://github.com/Zeioth/rofi-shortcuts
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

## rofi-calc

↪ https://github.com/svenstaro/rofi-calc

```sh
sudo pacman -S rofi-calc
rofi -show calc -modi calc -no-show-match -no-sort
```

## Rofimoji

↪ https://github.com/fdw/rofimoji

```sh
sudo pacman -S rofimoji
```

## rofi-copyq

↪ https://github.com/cjbassi/rofi-copyq

```sh
git clone https://github.com/cjbassi/rofi-copyq
cd rofi-copyq
./rofi-copyq
```

## Recoll (Optional)

```sh
nvim ~/.recoll/recoll.conf
```

```
topdirs = ~/Github
indexext = .md .txt .csv
```

```sh
recollindex -z
recoll <search>
```

## zzzfoo (Optional)

↪ https://github.com/andersju/zzzfoo

## Cmus

```sh
sudo pacman -S cmus
```

## dbus (x)

↪ https://bbs.archlinux.org/viewtopic.php?id=261924

## vbox to img (x)

↪ https://www.youtube.com/watch?v=eZUXtXU4YHQ

## Goldendict

↪ https://aur.archlinux.org/packages/goldendict

Download `goldendict-1_1.5.0-3-x86_64.pkg.tar.zst`, `qt5-webkit-5.212.0alpha4-22-x86_64.pkg.tar.zst` from https://sourceforge.net/projects/fabiololix-os-archive/files/Packages/

```sh
sudo pacman -U qt5-webkit-5.212.0alpha4-22-x86_64.pkg.tar.zst
sudo pacman -U goldendict-1_1.5.0-3-x86_64.pkg.tar.zst
```

## GoldenDict Windows Full Dark Theme

https://github.com/scillidan/GoldenDict-Full-Dark-Theme

```sh
yay -Ql goldendict
```

## sdcv

```sh
sudo pacman -S sdcv
```

## deep-translator

```sh
pipx install deep-translator
```

## Translate Shell (Optional)

```sh
sudo pacman -S translate-shell
```

## eSearch

↪ https://github.com/xushengfeng/eSearch

```sh
git clone https://aur.archlinux.org/e-search-bin.git
```

Download `eSearch-****-linux-x64.deb` from [releases](https://github.com/xushengfeng/eSearch/releases).

```sh
mv eSearch-****-linux-x64.deb e-search-****.deb
mv e-search-****.deb e-search-bin/
cd e-search-bin
makepkg
```

```sh
sudo pacman -U e-search-bin-****-1-x86_64.pkg.tar.zst
```

## mpv

```sh
sudo pacman -S mpv
cp -r /usr/share/doc/mpv/ ~/.config/
```

## ahk_x11-bin (Optional)

↪ https://github.com/Gustice/AHK-KeyMap

```sh
yay -S ahk_x11-bin
```

## Termius

```sh
yay -S termius
```

```sh
git clone https://aur.archlinux.org/termius.git
cd termius
wget ***.snap
mv ***.snap termius-8.11.0.snap
makepkg
sudo pacman -U ***.tar.zst
```

## WeChat

? https://flathub.org/apps/com.tencent.WeChat

```sh
flatpak install flathub com.tencent.WeChat
```

## ClamAV

↪ https://docs.clamav.net/manual/Usage/Scanning.html

```sh
sudo pacman -S clamav
```

```sh
clamd
clamscan <file>
```

↪ https://docs.clamav.net/faq/faq-freshclam.html#cant-create-freshclamdat-in-usrlocalshareclamav

```sh
sudo chown -R <user> /usr/local/share/clamav
```

## Photoshop CC

↪ https://github.com/Gictorbit/photoshopCClinux
↪ https://github.com/Gictorbit/photoshopCClinux/issues/175
↪ https://github.com/Gictorbit/photoshopCClinux/issues/40

## keymapper

↪ https://github.com/houmain/keymapper?tab=readme-ov-file#key-aliases

```sh
yay -S keymapper
sudo systemctl enable --now keymapperd
```

## Input Leap

```sh
yay -S input-leap-git
```

↪ https://github.com/debauchee/barrier

Settings → Session and Startup → Application Autostart → Add → `input-leap`

## Libre Office

## NXEngine-evo

```sh
git clone https://github.com/nxengine/translations
cd translations
cp build-local.sh build-local.sh.bak
vim build-local.sh
```

```
# wget https://github.com/nxengine/tsc-converter/releases/download/v1.1/tsc.tar.gz
# tar -zxf tsc.tar.gz
# rm -f tsc.tar.gz
# 
# wget https://github.com/nxengine/nx-fontgen/releases/download/v1.3/fontbm.tar.gz
# tar -zxf fontbm.tar.gz
# rm -f fontbm.tar.gz

# rm -f fontbm
# rm -f fontbm.bin
# rm -f tsc
# rm -rf assets
# rm -rf lib
```

```
cd local
wget https://github.com/nxengine/tsc-converter/releases/download/v1.1/tsc.tar.gz
tar -zxf tsc.tar.gz
wget https://github.com/nxengine/nx-fontgen/releases/download/v1.3/fontbm.tar.gz
tar -zxf fontbm.tar.gz
```

Download `ark-pixel-font-12px-proportional-ttf-****.zip` from [releases](https://github.com/TakWolf/ark-pixel-font/releases). Unzip it. Then copy `ark-pixel-12px-proportional-zh_cn.ttf` into `assets/`.

```
git clone https://github.com/nxengine/lang_chinese lang_chinese
cp ./lang_chinese/metadata ./lang_chinese/metadata.bak
vim ./lang_chinese/metadata
```

Change `assets/unifont-10.0.06.ttf` to `assets/ark-pixel-12px-proportional-zh_cn.ttf`.

```sh
cd ..
./build-local.sh
```

↪ https://github.com/nxengine/nxengine-evo/wiki/Building-on-Linux

```sh
git clone https://github.com/nxengine/nxengine-evo
cd nxengine-evo
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=Release -DPORTABLE=ON ..
make
cd ..
```

```sh
wget https://www.cavestory.org/downloads/cavestoryen.zip
unzip cavestoryen.zip
```

Copy files from  `translations/local/data/lang/chinese/` into `CaveStory/data/`.

```sh
cp -r CaveStory/Doukutsu.exe CaveStory/data ./
./build/nxextract
mkdir dest
cp -r build/nxengine-evo data dest/
./dest/nxengine-evo
```

```sh
cp -r ~/Git/translations/local/data/lang/chinese/** ./dest/data/
./dest/nxengine-evo
```

## qView

```sh
yay -S qview
```

<!-- Part 3 -->

## Bluetooth

↪ [Bluetooth headset connection occasionally fails: br-connection-page-timeout](https://www.reddit.com/r/archlinux/comments/qnffce/bluetooth_headset_connection_occasionally_fails/)  
↪ [How to Set up Bluetooth in Arch Linux](https://www.jeremymorgan.com/tutorials/linux/how-to-bluetooth-arch-linux/)

## IME

↪ [Arch Linux - 中文输入法](https://zhuanlan.zhihu.com/p/393746270)

## [Flameshot](https://flameshot.org/)

↪ [Easy OCR](https://github.com/flameshot-org/flameshot/issues/1344)

<!-- 
[Linux 软件构建一次到处运行](https://www.rectcircle.cn/posts/linux-build-once-run-anywhere/)
 -->