## sudo

```sh
su -
```

↪ [VirtualBox Ubuntu 22.04: how to add sudo rights?](https://askubuntu.com/questions/1440032/virtualbox-ubuntu-22-04-how-to-add-sudo-rights)

## SSH

```sh
sudo apt install openssh-server
sudo systemctl status ssh
```

Target Machine → Machine → Settings → Network → Adapter 1 → Advanced → Port Forwarding → Add:

```
Name `SSH port forwading`
Protocol `TCP`
Host IP `127.0.0.1`
Host Port `2222`
Guest IP `10.0.2.15`
Guest Port `22`
```

↪ [How to SSH Into a VirtualBox Ubuntu Server](https://www.makeuseof.com/how-to-ssh-into-virtualbox-ubuntu/)

## [Flatpak](https://flatpak.org/)

```sh
sudo add-apt-repository ppa:flatpak/stable
sudo apt update
sudo apt install flatpak
```

```sh
sudo apt install gnome-software-plugin-flatpak
```

```sh
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
reboot
```

↪ [Ubuntu Quick Setup](https://flatpak.org/setup/Ubuntu)

```sh
export GIO_MODULE_DIR=/usr/lib/x86_64-linux-gnu/gio/modules/
```

```sh
flatpak install flathub
```

↪ [TLS support is not available](https://github.com/flatpak/flatpak/issues/1207)

## Remove ubuntu-desktop (x)

```sh
sudo apt-get purge ubuntu-desktop
sudo apt-get autoremove
```

↪ [How do you completely remove ubuntu-desktop along with all installed packages with it?](https://askubuntu.com/questions/856373/how-do-you-completely-remove-ubuntu-desktop-along-with-all-installed-packages-wi)

## crontab (x)

[Scheduling StartUp and ShutDown](https://askubuntu.com/questions/83685/scheduling-startup-and-shutdown)

```sh
sudo vim /etc/crontab
```

```
00 23 * * * root /usr/sbin/rtcwake -m off -s 28800
```

## [headscale](https://github.com/juanfont/headscale) (x)

Get `headscale_<version>_linux_arm64.deb` from [](https://github.com/juanfont/headscale/releases).

```sh
sudo apt install ./headscale.deb
sudo systemctl enable --now headscale
systemctl status headscale
```

```sh
sudo dpkg --remove headscale
sudo dpkg --purge headscale
```

## [Headscale-UI](https://github.com/gurucomputing/headscale-ui) (x)

```sh
git clone https://github.com/gurucomputing/headscale-ui
cd headscale-ui
nvm install Hydrogen
nvm use 18.20.1
npm install
npm run build
npm add -g serve
```

## Alacritty

```sh
sudo add-apt-repository ppa:aslatter/ppa -y
sudo apt install alacritty
```

↪ [How to install Alacritty Terminal on Ubuntu 22.04 LTS](https://linux.how2shout.com/how-to-install-alacritty-terminal-on-ubuntu-22-04-lts/)

## [LocalSend](https://localsend.org/)

```sh
flatpak install flathub org.localsend.localsend_app
flatpak run org.localsend.localsend_app
```

LocalSend → Send → Nearby devices → Send mode → Share via link → Open one of these links in the browser on Vbox → Confirm in the Requests