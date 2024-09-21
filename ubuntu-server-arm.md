## Ubuntu Server ARM 22

```sh
sudo apt update && sudo apt upgrade
```

```sh
sudo apt-get clean
sudo apt-get autoremove
```

Some Port:

port  | serve
:-    | :-
19999 | netdata
4401  | reminiflux
4402  | ePubViewer
4403  | PDF.js viewer (demo)
4404  | Sreadium
4405  | Vivliostyle Viewer
4406  | Kiwix JS PWA
4501  | QRcode Designer
4502  | Flood
7830  | Faster Whisper Webui
7850  | Stable Diffusion web UI
8030  | Coder Server
8040  | LanguageTool
8050  | qBittorrent
8060  | linkding
8070  | miniflux
8080  | Stirling PDF
8090  | Komga
8096  | Jellyfin
9117  | Jackett

## Change Timezone

```sh
timedatectl set-timezone Asia/Shanghai
```

## Enable WiFi

```sh
sudo apt install net-tools
ifconfig wlan0 up
iwconfig wlan0 essid <ssid> key <password>
```

↪ [Connect to WiFi network through Ubuntu terminal [duplicate]](https://askubuntu.com/questions/294257/connect-to-wifi-network-through-ubuntu-terminal)  
↪ [RPi 4 running Ubuntu Server 20.04: can't connect to WiFi](https://raspberrypi.stackexchange.com/questions/111722/rpi-4-running-ubuntu-server-20-04-cant-connect-to-wifi)

## Disable WiFi

Refer to [How To Disable Wi-Fi On Ubuntu Server (3 easy ways)](https://raspberrytips.com/disable-wi-fi-ubuntu-server/):

```sh
sudo ifconfig eth0 up
sudo ifconfig wlan0 down
```

But it don't work.

```sh
sudo rm /etc/netplan/50-cloud-init.yaml
sudo vim /etc/netplan/00-installer-config.yaml
```

```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      dhcp4: true
      optional: true
  wifis:
    wlan0:
      dhcp4: true
      optional: false
      access-points:
        "<ssid>":
          password: "<password>"
          hidden: true
```

```sh
sudo chmod 600 /etc/netplan/00-installer-config.yaml
```

```sh
sudo netplan generate
sudo netplan --debug apply
```

```sh
sudo reboot
```

```sh
ip a
```

```sh
sudo ifconfig wlan0 down
```

↪ [Configure a Static IP address for WIFI using Netplan in Ubuntu Server 22.04 on a HP Pavillion Desktop 510-p051a](https://stackoverflow.com/questions/77637274/configure-a-static-ip-address-for-wifi-using-netplan-in-ubuntu-server-22-04-on-a)  
↪ [No internet connection after ubuntu server 20.04 install, ifconfig not available](https://askubuntu.com/questions/1233934/no-internet-connection-after-ubuntu-server-20-04-install-ifconfig-not-available)

## Edit source.list

```sh
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
sudo vi /etc/apt/sources.list
```

For `ARM`:

```
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ jammy main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ jammy-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ jammy-backports main restricted universe multiverse
deb http://ports.ubuntu.com/ubuntu-ports/ jammy-security main restricted universe multiverse
```

For `x64`:

```
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-backports main restricted universe multiverse
deb http://security.ubuntu.com/ubuntu/ jammy-security main restricted universe multiverse
```

↪ [清华大学开源软件镜像站 - Ubuntu 软件仓库](https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/)

## ZeroTier One


```sh
curl -s https://install.zerotier.com | sudo bash
```

## NVMe

```sh
sudo mkdir -p /mnt/nvme
```

```sh
ls -l /mnt/nvme
```

```sh
sudo mount -o uid=<User>,gid=<User>,umask=000 /dev/sda2 /mnt/nvme
```

## FTP

```sh
sudo apt install vsftpd
```

```sh
sudo systemctl enable --now vsftpd
```

```sh
sudo vim /etc/vsftpd.conf
```

```sh
utf8_filesystem=YES
```

```
sudo adduser ftpuser
sudo mkdir -p /home/ftpuser/ftp
sudo chmod a-w /home/ftpuser/ftp
```

```sh
sudo chown ftpuser:ftpuser /home/ftpuser/ftp
```

↪ [Setting Up a Basic FTP Server on Ubuntu 22](https://reintech.io/blog/setting-up-basic-ftp-server-ubuntu-22)

## SSHFS

```sh
sudo apt install sshfs
sudo mkdir -p /mnt/nvme
```

1. Get `winfsp-*.msi` form [WinFsp](https://github.com/winfsp/winfsp/releases).
2. Get `sshfs-win-*-x64.msi` from [SSHFS-Win - Releases](https://github.com/winfsp/sshfs-win/releases).
3. Get `sshfs-win-manager-*.zip` from [SSHFS-Win Manager](https://github.com/evsar3/sshfs-win-manager/releases)

SSHFS-Win Manager → Add Connection:

```
Name: <Name>
IP: <YourHost>
User: <User>
Password: <Password>
Path: `/mnt/nvme`
```

↪ [How To Use SSHFS to Mount Remote File Systems Over SSH](https://www.digitalocean.com/community/tutorials/how-to-use-sshfs-to-mount-remote-file-systems-over-ssh)  
↪ [SSHFS-Win](https://github.com/winfsp/sshfs-win)

## Docker

↪ [清华大学开源软件镜像站 - Docker CE 软件仓库](https://mirrors.tuna.tsinghua.edu.cn/help/docker-ce/)  
↪ [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)  
↪ [Ubuntu安装Docker详细教程](https://www.huixinglaile.com/archives/117a5c58.html)

## PM2

```sh
wget https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh -O install_nvm.sh
chmod +x ./install_nvm.sh
./install_nvm.sh
source .bashrc
nvm install --lts
npm install pm2 -g
pm2 dump
pm2 startup
...
```

## qbittorrent-nox

```sh
sudo apt install qbittorrent-nox
qbittorrent-nox
```

```sh
sudo vim /etc/systemd/system/qbittorrent-nox.service
```

```
[Unit]
Description=qBittorrent-nox service
After=network.target

[Service]
Type=exec
User=qbittorrent-nox
Group=qbittorrent-nox
UMask=007
ExecStart=/usr/bin/qbittorrent-nox --webui-port=8060
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

```sh
sudo systemctl daemon-reload
```

```sh
sudo adduser --system --group qbittorrent-nox
sudo adduser <User> qbittorrent-nox
```

```sh
sudo systemctl start qbittorrent-nox
systemctl status qbittorrent-nox
sudo systemctl enable qbittorrent-nox
```

Visit `http://<yourhost>:8050`, login with:

```
User: admin
Password: adminadmin
```

↪ `Running qBittorrent without X server (WebUI only, systemd service set up, Ubuntu 15.04 or newer)` on [qBittorrent - Wiki](https://github.com/qbittorrent/qBittorrent/wiki)  
↪ [How to Install qBittorrent-NoX, a headless and web UI Torrent Client](https://saputra.org/threads/how-to-install-qbittorrent-nox-a-headless-and-web-ui-torrent-client.1099/)

Or use [Flood](https://github.com/scillidan/WEBUI-demo/blob/main/_readme/flood.md) as Web-UI.

```
User for Flood: <User>
Password for Flood: <Password>
URL: http://0.0.0.0:8050
User for qBittorrent: admin
Password for qBittorrent: adminadmin
```

Default Download Directory is on `/home/qbittorrent-nox/Downloads`.

## Jackett

```sh
sudo apt install mono-devel
```

Get `Jackett.Binaries.LinuxARM64.tar.gz` from [Jackett - Releases](https://github.com/Jackett/Jackett/releases).

```sh
tar -xvzf Jackett.Binaries.LinuxARM64.tar.gz
cd Jackett
./jackett
```

```sh
sudo ./install_service_systemd.sh
```

```sh
sudo systemctl status jackett.service
```

↪ [How to Install Jackett on Ubuntu 20.04](https://varhowto.com/install-jackett-ubuntu-20-04/)

I only used it under [ZeroTier](https://www.zerotier.com/), so not set password. See more from [Security Risk: Your instance has external access enabled without using an admin password.](https://github.com/Jackett/Jackett/wiki/Troubleshooting#security-risk-your-instance-has-external-access-enabled-without-using-an-admin-password)

## [Komga](https://github.com/gotson/komga)

```sh
sudo apt install openjdk-21-jdk postgresql postgresql-contrib -y
```

```sh
sudo su postgres
createuser komgauser --pwprompt
createdb -O komgauser komga
exit
```

```sh
sudo mkdir /opt/komga
```

```sh
sudo wget https://github.com/gotson/komga/releases/download/1.12.1/komga-1.12.1.jar -P /opt/komga/
```

```sh
sudo vim /etc/systemd/system/komga.service
```

```
[Unit]
Description=Komga Service
After=network.target

[Service]
User=root
Group=root
ExecStart=/usr/bin/java -Xms128M -Xmx256M -jar /opt/komga/komga-1.21.1.jar --server.servlet.context-path=/komga --server.port=8090
WorkingDirectory=/opt/komga
Restart=on-abnormal

[Install]
WantedBy=multi-user.target
```

↪ [How to Install Komga on Ubuntu Server Latest](https://ipv6.rs/tutorial/Ubuntu_Server_Latest/Komga/)  
↪ [Komga - Breaking changes](https://komga.org/blog/prepare-v1/#breaking-changes)  
↪ [Configuration options](https://komga.org/docs/installation/configuration)

```sh
sudo systemctl daemon-reload
sudo systemctl enable --now komga
```

## [Jellyfin](https://jellyfin.org/)

```sh
sudo dpkg -i jellyfin-server_10.9.11+ubu2204_arm64.deb jellyfin-web_10.9.11+ubu2204_all.deb
sudo dpkg -i jellyfin-ffmpeg6_6.0.1-8-jammy_arm64.deb
sudo systemctl enable --now jellyfin
systemctl status jellyfin
```

↪ [Installation - Linux](https://jellyfin.org/docs/general/installation/linux#linux-generic-amd64)  
↪ [Media - Movies](https://jellyfin.org/docs/general/server/media/movies/)  
↪ [Plugins](https://jellyfin.org/docs/general/server/plugins/)

## Plex (x)

```sh
echo deb https://downloads.plex.tv/repo/deb public main | sudo tee /etc/apt/sources.list.d/plexmediaserver.list
curl https://downloads.plex.tv/plex-keys/PlexSign.key | sudo apt-key add -
sudo apt update
sudo apt install plexmediaserver
```

```sh
sudo systemctl status plexmediaserver
```

Visit `http://<yourhost>:32400/web`

↪ [Install of plex on Ubuntu server 22.04](https://www.reddit.com/r/PleX/comments/yp13yb/install_of_plex_on_ubuntu_server_2204/)

## [dictd](https://linux.die.net/man/8/dictd)

```sh
sudo apt install dictd
```

```sh
sudo apt install p7zip-full
```

```sh
sudo apt install dictfmt dictzip
```

↪ [有人转过词典格式么](https://emacs-china.org/t/topic/25022/2)  
↪ [How can I uncompress a \*.7z file?](https://askubuntu.com/questions/219392/how-can-i-uncompress-a-7z-file)

```sh
sudo dictd --listen-to 0.0.0.0 --port 8040
```
...

```sh
dict -d ecdict dictionary
```

```sh
pgrep dictd
```

```sh
kill <pid>
```

```sh
sudo vim /etc/dictd/dictd.conf
```

```
listen_to 0.0.0.0
allow *
```

```sh
sudo systemctl enable --now dictd.service
```

...

## [Apertium](https://www.apertium.org/)

↪ [Install Apertium core using packaging](https://wiki.apertium.org/wiki/Install_Apertium_core_using_packaging)  
↪ [Install language data using packaging](https://wiki.apertium.org/wiki/Install_language_data_using_packaging)  
↪ [apertium-zho](https://github.com/apertium/apertium-zho)

## [DeepLX](https://github.com/OwO-Network/DeepLX) (x)

1. Get `deeplx_linux_arm64` from [DeepLX - Releases](https://github.com/OwO-Network/DeepLX/releases).
2. `chmod +x deeplx_linux_arm64`
3. `mv deeplx_linux_arm64 /usr/bin/deeplx`

Or build from source:

```sh
git clone --depth=1 https://github.com/OwO-Network/DeepLX
cd DeepLX
go mod tidy
go build .
```

↪ [请求添加对树莓派ARM的二进制程序](https://github.com/OwO-Network/DeepLX/issues/111)

```sh
sudo mkdir -p /opt/deeplx
sudo vim /etc/systemd/system/deeplx.service
```

```
[Unit]
Description=DeepLX Service
After=network.target

[Service]
User=root
Group=root
ExecStart=/usr/bin/deeplx
WorkingDirectory=/opt/deeplx
Restart=on-abnormal

[Install]
WantedBy=multi-user.target
```

```sh
sudo systemctl enable --now deeplx.service
```

## Weblate (TBD)

```sh
sudo apt install -y \
   libxml2-dev libxslt-dev libfreetype6-dev libjpeg-dev libz-dev libyaml-dev \
   libffi-dev libcairo-dev gir1.2-pango-1.0 libgirepository1.0-dev \
   libacl1-dev libssl-dev libpq-dev libjpeg-dev build-essential \
   python3-gdbm python3-dev python3-pip python3-virtualenv virtualenv git
```

```sh
sudo apt install -y \
   libldap2-dev libldap-common libsasl2-dev \
   libxmlsec1-dev
```

```sh
sudo apt install -y nginx uwsgi uwsgi-plugin-python3 redis-server postgresql postgresql-contrib exim4 gettext
```

```sh
sudo apt-get install git-svn
```

↪ [Installing on Debian and Ubuntu](https://docs.weblate.org/en/latest/admin/install/venv-debian.html)  
↪ [Mercurial](https://docs.weblate.org/en/latest/vcs.html#vcs-mercurial)  
↪ [Gerrit](https://docs.weblate.org/en/latest/vcs.html#vcs-gerrit)

## [Dify](https://github.com/langgenius/dify)

↪ [Start with Local Source Code](https://docs.dify.ai/getting-started/install-self-hosted/local-source-code)

## [Verba](https://github.com/weaviate/Verba)

## [Trilium](https://github.com/zadam/trilium)

↪ [Packaged server installation](https://github.com/zadam/trilium/wiki/Packaged-server-installation)

## [Coder](https://coder.com/) (x)

```sh
mkdir ~/code-server
cd ~/code-server
wget https://github.com/coder/code-server/releases/download/v4.8.2/code-server-4.92.2-linux-arm64.tar.gz
tar -xzvf code-server-4.92.2-linux-arm64.tar.gz
sudo cp -r code-server-4.8.2-linux-amd64 /usr/lib/code-server
sudo ln -s /usr/lib/code-server/bin/code-server /usr/bin/code-server
sudo mkdir /var/lib/code-server
sudo vim /lib/systemd/system/code-server.service
```

```
[Unit]
Description=code-server
After=nginx.service

[Service]
Type=simple
Environment=PASSWORD=<Password>
ExecStart=/usr/bin/code-server --bind-addr 0.0.0.0:8080 --user-data-dir /var/lib/code-server --auth password
Restart=always

[Install]
WantedBy=multi-user.target
```

```sh
sudo systemctl start code-server
sudo systemctl status code-server
sudo systemctl enable code-server
```

↪ [How To Set Up the code-server Cloud IDE Platform on Ubuntu 22.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-the-code-server-cloud-ide-platform-on-ubuntu-22-04)

1. Settings → Profile → <TargetProfile> → More → Export → <ProfileName> → Local file
2. Settings → Profile (Default) → Import Profile

↪ [Setup Guide](https://github.com/coder/code-server/blob/main/docs/guide.md)

