<!--
port  | serve
:-    | :-
19999 | netdata
2628  | dictd
4401  | reminiflux
4402  | ePubViewer
4403  | PDF.js viewer (demo)
4404  | Sreadium
4405  | Vivliostyle Viewer
4406  | Kiwix JS PWA
4501  | QRcode Designer
4502  | Flood
7820  | Fish Speech
7830  | Faster Whisper Webui
7840  | IOPaint
7850  | Stable Diffusion web UI
8020  | Coder Server
8030  | LanguageTool
8050  | qBittorrent
8060  | linkding
8070  | miniflux
8080  | Stirling PDF
8090  | Komga
8096  | Jellyfin
9117  | Jackett
-->

## Ubuntu Server ARM 22

```sh
sudo apt update && sudo apt upgrade
```

```sh
sudo apt-get clean
sudo apt-get autoremove
```

## Change Timezone

```sh
timedatectl set-timezone Asia/Shanghai
```

## Enable WiFi

```sh
sudo apt install network-manager
nmcli d
sudo nmcli r wifi on
nmcli d wifi list
sudo nmcli d wifi connect <ssid> password <password>
```

↪ [Establish a Wireless Connection](https://ubuntu.com/core/docs/networkmanager/configure-wifi-connections)

<!--
```sh
sudo apt install net-tools
ifconfig wlan0 up
iwconfig wlan0 essid <SSID> key <Password>
```

↪ [Connect to WiFi network through Ubuntu terminal [duplicate]](https://askubuntu.com/questions/294257/connect-to-wifi-network-through-ubuntu-terminal)  
↪ [RPi 4 running Ubuntu Server 20.04: can't connect to WiFi](https://raspberrypi.stackexchange.com/questions/111722/rpi-4-running-ubuntu-server-20-04-cant-connect-to-wifi)
-->

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
sudo netplan generate
sudo netplan --debug apply
sudo reboot
```

```sh
ip a
sudo ifconfig wlan0 down
```

↪ [Configure a Static IP address for WIFI using Netplan in Ubuntu Server 22.04 on a HP Pavillion Desktop 510-p051a](https://stackoverflow.com/questions/77637274/configure-a-static-ip-address-for-wifi-using-netplan-in-ubuntu-server-22-04-on-a)  
↪ [No internet connection after ubuntu server 20.04 install, ifconfig not available](https://askubuntu.com/questions/1233934/no-internet-connection-after-ubuntu-server-20-04-install-ifconfig-not-available)

## Use repository mirror

For `Ubuntu 22.04 LTS`:

```sh
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
sudo vim /etc/apt/sources.list
```

```
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ jammy main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ jammy-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ jammy-backports main restricted universe multiverse
deb http://ports.ubuntu.com/ubuntu-ports/ jammy-security main restricted universe multiverse
```

For `Ubuntu 24.04 LTS`:

```sh
sudo cp /etc/apt/sources.list.d/ubuntu.sources /etc/apt/sources.list.d/ubuntu.sources.bak
sudo vim /etc/apt/sources.list.d/ubuntu.sources
```

```
Types: deb
URIs: https://mirrors.tuna.tsinghua.edu.cn/ubuntu
Suites: noble noble-updates noble-backports
Components: main restricted universe multiverse
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg

Types: deb
URIs: http://security.ubuntu.com/ubuntu/
Suites: noble-security
Components: main restricted universe multiverse
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg
```

[清华大学开源软件镜像站 - Ubuntu Ports 软件仓库](https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu-ports/)

For `x64`:

```
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-backports main restricted universe multiverse
deb http://security.ubuntu.com/ubuntu/ jammy-security main restricted universe multiverse
```

↪ [清华大学开源软件镜像站 - Ubuntu 软件仓库](https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/)

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

## NFS (Cache)

```sh
sudo apt install nfs-kernel-server
sudo systemctl start nfs-kernel-server.service
```

↪ [Network File System (NFS)](https://ubuntu.com/server/docs/network-file-system-nfs)

## Docker

↪ [清华大学开源软件镜像站 - Docker CE 软件仓库](https://mirrors.tuna.tsinghua.edu.cn/help/docker-ce/)  
↪ [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)  
↪ [Ubuntu安装Docker详细教程](https://www.huixinglaile.com/archives/117a5c58.html)

## [PM2](https://pm2.keymetrics.io/)

<!-- --8<-- [start:windows10] -->
Run commands as Admin:

```sh
git clone https://github.com/jessety/pm2-installer
cd pm2-installer
npm run configure
npm run setup
pm2 start ...
pm2 save
```

Windows 10 → Control Panel → Administrative Tools > Services → PM2 → Properties → Log On → local system account → Go back to first tab → Start

↪ [pm2-installer](https://github.com/jessety/pm2-installer)
↪ [Persistent applications](https://pm2.keymetrics.io/docs/usage/startup/)
↪ [State is now: Stopped](https://github.com/jessety/pm2-installer/issues/69)
<!-- --8<-- [end:windows10] -->

<!-- --8<-- [start:ubuntu-server-arm-22] -->
```sh
wget https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh -O install_nvm.sh
chmod +x ./install_nvm.sh
./install_nvm.sh
source .bashrc
nvm install --lts
npm install pm2 -g
pm2 dump
pm2 startup
```

↪ [Vue packages version mismatch](https://github.com/nuxt/nuxt/issues/10305)  
↪ [how to modify nuxt server start port ,default port is 3000](https://github.com/nuxt/nuxt/issues/490)
<!-- --8<-- [end:ubuntu-server-arm-22] -->

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

Visit `http://<YourHost>:8050`, login with:

```
User: admin
Password: adminadmin
```

↪ `Running qBittorrent without X server (WebUI only, systemd service set up, Ubuntu 15.04 or newer)` on [qBittorrent - Wiki](https://github.com/qbittorrent/qBittorrent/wiki)  
↪ [How to Install qBittorrent-NoX, a headless and web UI Torrent Client](https://saputra.org/threads/how-to-install-qbittorrent-nox-a-headless-and-web-ui-torrent-client.1099/)

## [ZeroTier One](https://www.zerotier.com/)

1. Log-in [ZeroTier](https://my.zerotier.com).
2. Create a Network.

<!-- --8<-- [start:ubuntu-22-arm] -->
```sh
curl -s https://install.zerotier.com | sudo bash
sudo systemctl enable --now zerotier-one.service
systemctl status zerotier-one.service
sudo zerotier-cli join <NetworkID>
sudo zerotier-cli listnetworks
```

↪ [Debian 11 with ufw firewall is blocking zerotier](https://discuss.zerotier.com/t/debian-11-with-ufw-firewall-is-blocking-zerotier/13072)
<!-- --8<-- [end:ubuntu-22-arm] -->

<!-- --8<-- [start:archlinux] -->
```sh
sudo pacman -S zerotier-one
```
<!-- --8<-- [end:archlinux] -->

## [ztncui](https://github.com/key-networks/ztncui)

## [headscale](https://github.com/juanfont/headscale) (Cache)

Get `headscale_<version>_linux_arm64.deb` from [Headscale - Releases](https://github.com/juanfont/headscale/releases).

```sh
sudo apt install ./headscale.deb
sudo systemctl enable --now headscale
systemctl status headscale
```

```sh
sudo dpkg --remove headscale
sudo dpkg --purge headscale
```

## [Headscale-UI](https://github.com/gurucomputing/headscale-ui) (Cache)

```sh
git clone --depth=1 https://github.com/gurucomputing/headscale-ui
cd headscale-ui
nvm install Hydrogen
nvm use 18.20.1
npm install
npm run build
npm add -g serve
```

## [Flood](https://github.com/jesec/flood)

```sh
npm install
npm run build
npm run start
```

<!-- --8<-- [start:windows10] -->
qBittorrent → Tools → Options → Web UI → Web USer Interface (On) → port `4321` → Authentication → Set `<User>`, `<Password>`

Visit `localhost:4321`, login.
<!-- --8<-- [end:windows10] -->

<!-- --8<-- [start:ubuntu-server-arm-22] -->
Edit `package.json`:

```
  "script": {
    "start": "node --enable-source-maps --use_strict dist/index.js",
```

To:

```
  "script": {
    "start": "node --enable-source-maps --use_strict dist/index.js --host 0.0.0.0 --port 4321",
```

```sh
pm2 start npm --name "flood" -- run start
```

If you forget `<User>` or `<Password>`, delete `~/.local/shared/flood/`. Reload or re-create flood's PM2-app:

```
User for Flood: <User>
Password for Flood: <Password>
URL: http://0.0.0.0:8050
User for qBittorrent: admin
Password for qBittorrent: adminadmin
```

Default Download Directory is on `/home/qbittorrent-nox/Downloads`.
<!-- --8<-- [end:ubuntu-server-arm-22] -->

## [Jackett](https://github.com/Jackett/Jackett)

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

<!-- --8<-- [start:windows10] -->
```sh
java.exe -jar "komga.jar" --komga.config-dir="config"
```
<!-- --8<-- [end:windows10] -->

<!-- --8<-- [start:ubuntu-server-arm-22] -->
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
<!-- --8<-- [end:ubuntu-server-arm-22] -->

## [Suwayomi-Server](https://github.com/Suwayomi/Suwayomi-Server)

<!-- --8<-- [start:ubuntu-server-arm-22] -->
Get `Suwayomi-Server-v*-debian-all.deb` from [Suwayomi-Server - Releases](https://github.com/Suwayomi/Suwayomi-Server/releases).

```sh
sudo dpkg -i Suwayomi-Server-v*-debian-all.deb
apt --fix-broken install
sudo vim /etc/systemd/system/suwayomi-server.service
```

```
[Unit]
Description=Suwayomi Server
After=network.target

[Service]
User=root
Group=root
ExecStart=suwayomi-server
Restart=on-abnormal

[Install]
WantedBy=multi-user.target
```

```sh
sudo systemctl enable --now suwayomi-server
sudo systemctl status suwayomi-server
```

1. Visit `0.0.0.0:4567`.
2. The service may take several minutes to start until you can see it.

↪ [can you make it easier to install on ubuntu , and tutorial need to update](https://github.com/Suwayomi/Suwayomi-Server/issues/896)

Suwayomi → Settings → Brower settings → Extension repositories → Add repository:

```
https://raw.githubusercontent.com/ThePBone/tachiyomi-extensions-revived/repo/index.min.json
```

↪ [Tachiyomi Extensions Revived](https://github.com/timschneeb/tachiyomi-extensions-revived)
<!-- --8<-- [end:ubuntu-server-arm-22] -->

## [Jellyfin](https://jellyfin.org/)

<!-- --8<-- [start:windows10] -->
```sh
mprocs "jellyfin.exe --service" "timeout 20 && jellyfin-mpv-shim\run.exe"
```
<!-- --8<-- [end:windows10] -->

<!-- --8<-- [start:ubuntu-server-arm-22] -->
```sh
sudo dpkg -i jellyfin-server_10.9.11+ubu2204_arm64.deb jellyfin-web_10.9.11+ubu2204_all.deb
sudo dpkg -i jellyfin-ffmpeg6_6.0.1-8-jammy_arm64.deb
sudo systemctl enable --now jellyfin
systemctl status jellyfin
```

↪ [Installation - Linux](https://jellyfin.org/docs/general/installation/linux#linux-generic-amd64)  
↪ [Media - Movies](https://jellyfin.org/docs/general/server/media/movies/)  
↪ [Plugins](https://jellyfin.org/docs/general/server/plugins/)
<!-- --8<-- [end:ubuntu-server-arm-22] -->

## [Plex](https://www.plex.tv/) (Cache)

<!-- --8<-- [start:ubuntu-server-arm-22] -->
```sh
echo deb https://downloads.plex.tv/repo/deb public main | sudo tee /etc/apt/sources.list.d/plexmediaserver.list
curl https://downloads.plex.tv/plex-keys/PlexSign.key | sudo apt-key add -
sudo apt update
sudo apt install plexmediaserver
```

```sh
sudo systemctl status plexmediaserver
```

Visit `http://<YourHost>:32400/web`

↪ [Install of plex on Ubuntu server 22.04](https://www.reddit.com/r/PleX/comments/yp13yb/install_of_plex_on_ubuntu_server_2204/)
<!-- --8<-- [end:ubuntu-server-arm-22] -->

## [dictd](https://linux.die.net/man/8/dictd)

<!-- --8<-- [start:ubuntu-server-arm-22] -->
```sh
sudo apt install dictd
```

Test:

```sh
dict -d ecdict <word>
pgrep dictd
kill <pid>
```

For used on PC in LAN:

```sh
sudo vim /etc/dictd/dictd.conf
```

```
global {
listen_to 0.0.0.0
}

access {
allow *
}
```

```sh
sudo vim /var/lib/dictd/db.list
```

For example:

```
database ecdict {
  data /mnt/nvme/share/dictd/ecdict.dict.dz
  index /mnt/nvme/share/dictd/ecdict.index
}
database 21th-en22zh {
  data /mnt/nvme/share/dictd/21shijishuangxiangcidian.dict.dz
  index /mnt/nvme/share/dictd/21shijishuangxiangcidian.index
}
database etymonline {
  data /mnt/nvme/share/dictd/etymonline.dict.dz
  index /mnt/nvme/share/dictd/etymonline.index
}
database gcide {
  data /mnt/nvme/share/dictd/gcide.dict.dz
  index /mnt/nvme/share/dictd/gcide.index
}
database dict-en-en {
  data /mnt/nvme/share/dictd/dict-en-en.dict.dz
  index /mnt/nvme/share/dictd/dict-en-en.index
}
database wikdict-en-zh {
  data /mnt/nvme/share/dictd/wikdict-en-zh.dict.dz
  index /mnt/nvme/share/dictd/wikdict-en-zh.index
}
database wikdict-zh-en {
  data /mnt/nvme/share/dictd/wikdict-zh-en.dict.dz
  index /mnt/nvme/share/dictd/wikdict-zh-en.index
}
```

```sh
sudo systemctl enable --now dictd.service
```
<!-- --8<-- [end:ubuntu-server-arm-22] -->

↪ [dictd.conf](https://gist.github.com/wind0204/d65c7d1b5d7794c4c7fa1a02d5151acc)

## [SilverDict](https://github.com/Crissium/SilverDict)

```sh
git clone --depth=1 https://github.com/Crissium/SilverDict
cd client
yarn install
yarn build
mv build ../server/
```

```sh
cd ../server
python310 -m venv venv
venv\Scripts\activate.bat
pip install -r requirements.txt
pip install lxml
python server.py
```

Visit `localhost:2628`.

Setting → Sources → add `yourpath` then `Enter` → Wait for import.

In addition, some cache saved on `C:\Users\<User>\.silverdict` and `C:\Users\<User>\.cache\SilverDict`.

With PM2:

```sh
pm2 start server.py --name silverdict --interpreter "venv/Scripts/python.exe" --cwd "SilverDict/server" 
```

## [LanguageTool](https://languagetool.org/)

1. Get `ngrams-en-*.zip` from [here](https://languagetool.org/download/ngram-data/).
2. Get `LanguageTool Desktop version for offline use` from [LanguageTool embedded HTTP Server](https://dev.languagetool.org/http-server).

<!-- --8<-- [start:windows10] -->
1. Install [OpenJDK](https://jdk.java.net)，I tested it on [openjdk17](https://jdk.java.net/17/).
2. Decompress `ngrams-en-*.zip` to `ngrams\`
3. Decompress `LanguageTool-stable.zip` to `LanguageTool\`

```sh
java.exe -cp LanguageTool\languagetool-server.jar org.languagetool.server.HTTPServer --languagemodel <ngrams-dir> --port <port> --allow-origin
```

For running it liked service, create `languagetool_service.cmd` from the command above. Then create `languagetool_service.vbs`:

```
Set WshShell = CreateObject("WScript.Shell")
  WshShell.Run chr(34) & "languagetool_service.cmd" & Chr(34), 0
Set WshShell = Nothing
```

Create shortcut of `languagetool_service.vbs`, put it into `C:\Users\<User>\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\`.
<!-- --8<-- [end:windows10] -->

<!-- --8<-- [start:ubuntu-server-arm-22] -->
Decompress `ngrams-en-*.zip` to `/mnt/<nvme>/share/ngrams/`.

```sh
sudo apt install openjdk-21-jdk
sudo unzip LanguageTool-stable.zip
sudo mv LanguageTool-* /opt/languagetool
```

```sh
git clone --depth=1 https://github.com/facebookresearch/fastText.git
cd fastText
make
sudo vim /opt/languagetool/server.properties
```

```
fasttextModel=fasttext/lid.176.bin
fasttextBinary=fasttext/fasttext
```

```sh
sudo vim /etc/systemd/system/languagetool.service
```

```
[Unit]
Description=LanguageTool Service
After=network.target

[Service]
User=root
Group=root
ExecStart=java -cp /opt/languagetool/languagetool-server.jar org.languagetool.server.HTTPServer --languagemodel /mnt/<nvme>/share/ngrams --port 8040 --allow-origin --public
WorkingDirectory=/opt/languagetool
Restart=on-abnormal

[Install]
WantedBy=multi-user.target
```

```sh
sudo systemctl enable --now languagetool.service
```
<!-- --8<-- [end:ubuntu-server-arm-22] -->

↪ [LanguageTool embedded HTTP Server](https://dev.languagetool.org/http-server)  
↪ [Anyone self-hosting languagetool?](https://www.reddit.com/r/selfhosted/comments/ksvmii/anyone_selfhosting_languagetool/)  
↪ [Finding errors using n-gram data](https://dev.languagetool.org/finding-errors-using-n-gram-data)

Used in browser:

1. Install [Browser Extension](https://languagetool.org/services#browsers)
2. Browser Extension → Settings → Advanced settings → Other server → `http://<host>:<port>/v2`
3. General settings → Show in right-click menu (On)

## [DeepLX](https://github.com/OwO-Network/DeepLX)

<!-- --8<-- [start:windows10] -->
1. Get `deeplx_windows_amd64.exe` from [DeepLX - Releases](https://github.com/OwO-Network/DeepLX/releases).
2. Run `deeplx_windows_amd64.exe`.
<!-- --8<-- [end:windows10] -->

Build from source:

```sh
git clone --depth=1 https://github.com/OwO-Network/DeepLX
cd DeepLX
go mod tidy
go build .
```

↪ [请求添加对树莓派ARM的二进制程序](https://github.com/OwO-Network/DeepLX/issues/111)

<!-- --8<-- [start:ubuntu-server-arm-22] -->
1. Get `deeplx_linux_arm64` from [DeepLX - Releases](https://github.com/OwO-Network/DeepLX/releases).
2. `chmod +x deeplx_linux_arm64`
3. `mv deeplx_linux_arm64 /usr/bin/deeplx`

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
<!-- --8<-- [end:ubuntu-server-arm-22] -->

## [Weblate](https://weblate.org) (Cache)

<!-- --8<-- [start:ubuntu-server-arm-22] -->
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
<!-- --8<-- [end:ubuntu-server-arm-22] -->

## [Miniflux](https://miniflux.app/)

<!-- --8<-- [start:windows10] -->
Install requirements:

1. Get `miniflux-windows-amd64` from [releases](https://github.com/miniflux/v2/releases), rename it to `miniflux.exe`.
2. [PostgreSQL](https://www.postgresql.org/) (test on v14)
3. [mprocs](https://github.com/pvolok/mprocs) (optional)
4. [gsudo](https://github.com/gerardog/gsudo) (optional)

```sh
initdb --locale=C --username=miniflux --pgdata=miniflux
postgres -D miniflux
```

↪ [initdb](https://www.postgresql.org/docs/current/app-initdb.html)

Keep the command-line window. Run `pgAdmin 4\runtime\pgAdmin4.exe`.

Context-menu of `Servers` → Register → Server → Tab `General`:

```
Name `miniflux_server`
```

Tab `Connection`:

```
host name `localhost`
Maintenance database `miniflux`
Username `miniflux`
```

Servers → miniflux_server → Context-menu of `Databases` → Create → Database → Tab `General`:

```
Database `miniflux`
```

Tab `Definition`:

```
Encoding `None`
```

↪ [Server Dialog](https://www.pgadmin.org/docs/pgadmin4/development/server_dialog.html)

Create `miniflux.conf`. Set `ADMIN_USERNAME` and `ADMIN_PASSWORD` for login:

```
DATABASE_URL=user=miniflux password=secret dbname=miniflux sslmode=disable
RUN_MIGRATIONS=1
POLLING_FREQUENCY=60
CREATE_ADMIN=1
ADMIN_USERNAME=...
ADMIN_PASSWORD=...
DEBUG=on
WORKER_POOL_SIZE=10
PORT=8070
```

↪ [Configuration Parameters](https://miniflux.app/docs/configuration.html)

Create a new command-line window. Test connect and login on `localhost:8070`:

```sh
miniflux -config-file miniflux.conf
```

Finally, create `miniflux_service.cmd`:

```sh
mprocs "gsudo postgres.exe -D miniflux_db" "timeout 5 && miniflux.exe -config-file miniflux.conf
```

I don't want to use `Windows Task Scheduler`, and I don't try [NSSM](https://nssm.cc/).

Create `miniflux_server.vbs`:

```
Set WshShell = CreateObject("WScript.Shell")
  WshShell.Run chr(34) & "miniflux_service.cmd" & Chr(34), 0
Set WshShell = Nothing
```

1. Create shortcut of `.vbs`.
2. Put the `.lnk` into `C:\Users\<User>\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\`.
3. It will autorun at startup.
<!-- --8<-- [end:windows10] -->

<!-- --8<-- [start:ubuntu-server-arm-22] -->
```sh
cd /etc/apt/sources.list.d
sudo touch miniflux.list
echo "deb [trusted=yes] https://repo.miniflux.app/apt/ * *" | sudo tee /etc/apt/sources.list.d/miniflux.list > /dev/null
sudo apt update
sudo apt install miniflux
```
↪ [Debian Installation](https://miniflux.app/docs/debian.html)

```sh
sudo apt install -y postgresql-common
sudo /usr/share/postgresql-common/pgdg/apt.postgresql.org.sh
sudo apt install postgresql-16
```

```sh
sudo -u postgres psql
```

↪ [How do I solve this problem to use psql? | psql: error: FATAL: role "postgres" does not exist](https://stackoverflow.com/questions/65222869/how-do-i-solve-this-problem-to-use-psql-psql-error-fatal-role-postgres-d)  
↪ [How To Completely Uninstall PostgreSQL](https://kb.objectrocket.com/postgresql/how-to-completely-uninstall-postgresql-757)  
↪ [Linux downloads (Ubuntu)](https://www.postgresql.org/download/linux/ubuntu/)

```sh
CREATE USER miniflux WITH ENCRYPTED PASSWORD 'miniflux';
CREATE DATABASE miniflux;
GRANT ALL PRIVILEGES ON DATABASE miniflux TO miniflux;
ALTER USER miniflux WITH SUPERUSER;
\q
```

```sh
sudo vim /etc/miniflux.conf
```

```
RUN_MIGRATIONS=1
DATABASE_URL=user=miniflux password=miniflux dbname=miniflux sslmode=disable
LISTEN_ADDR=/run/miniflux/miniflux.sock
PORT=8070
```

```sh
miniflux -c /etc/miniflux.conf -migrate
miniflux -c /etc/miniflux.conf -create-admin
```

```sh
miniflux -c /etc/miniflux.conf
```

↪ [Proper Way To Install Miniflux RSS Reader on Ubuntu 22](https://ntmv.net/posts/proper-way-to-install-miniflux/)

If `postgresql` not run:

```sh
sudo systemctl start postgresql
```

```sh
sudo systemctl enable --now miniflux
sudo systemctl enable --now postgresql
```

Other options:

↪ [miniflux-theme-reeder](https://github.com/rootknight/Miniflux-Theme-Reeder)  
↪ [Feed Filtering Rules](https://miniflux.app/docs/rules.html#feed-filtering-rules)
<!-- --8<-- [end:ubuntu-server-arm-22] -->

Backup data:

```sh
pg_dump -U miniflux -h 127.0.0.1 -p 5432 -F t miniflux > miniflux.tar
```

## [linkding](https://github.com/sissbruecker/linkding)

<!-- --8<-- [start:windows10] -->
Install requirements:

- [Python](https://www.python.org/) (test on 3.10)
- [fnm](https://github.com/Schniz/fnm)
- [mprocs](https://github.com/pvolok/mprocs)

```sh
fnm install 18.15.0
fnm use 18.15.0
```

```sh
git clone --depth=1 https://github.com/sissbruecker/linkding
cd linkding
npm install
npm run build
```

```sh
python310 -m venv venv
venv\Scripts\activate.bat
python -m pip install -r requirements.txt
python -m pip install -r requirements.prod.txt
pip install -r requirements.txt
python manage.py migrate
python manage.py createsuperuser --username=<User> --email=<Email>
```

Test it:

```sh
npm run dev
```

Create a new command-line window:

```sh
python manage.py runserver 8002
```

Visit `localhost:8002`.

↪ [Development](https://github.com/sissbruecker/linkding#development)

Finally, create `linkding_service.cmd`:

```sh
cd linkding ^
  && set LD_SUPERUSER_NAME=<User> ^
  && set LD_SUPERUSER_PASSWORD=<Password> ^
  && mprocs ^
  "npm run dev" ^
  "timeout 5 && venv\Scripts\python.exe manage.py runserver 8002"
```

Add `linkding_server.vbs`:

```
Set WshShell = CreateObject("WScript.Shell")
  WshShell.Run chr(34) & "linkding_service.cmd" & Chr(34), 0
Set WshShell = Nothing
```

1. Create shortcut of `.vbs`.
2. Put the `.lnk` into `C:\Users\<User>\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\`.
3. It will autorun at startup.
<!-- --8<-- [end:windows10] -->

<!-- --8<-- [start:ubuntu-server-arm-22] -->
```sh
vim requirements.dev.txt
```

Edit `rcssmin==1.1.1` to `rcssmin`.

↪ [ModuleNotFoundError: No module named 'ruamel'](https://github.com/fair-workflows/nanopub/issues/106)

```sh
npm install -g concurrently
```

```sh
vim package.json
```

```sh
{
  "scripts": {
    "start": "concurrently \"rollup -c -w\" \"python manage.py runserver 0.0.0.0:8060\""
```

```sh
pm2 start npm --name "linkding" -- run start
pm2 save
```

↪ [linkding - Setup](https://github.com/sissbruecker/linkding/blob/master/README.md#setup)
<!-- --8<-- [end:ubuntu-server-arm-22] -->

## [Netdata](https://www.netdata.cloud/)

<!-- --8<-- [start:ubuntu-server-arm-22] -->
```sh
sudo apt install netdata -y
```

```sh
sudo vim /etc/netdata/netdata.conf
```

```
[global]
  run as user = netdata
  web files owner = root
  web files group = root
  # Netdata is not designed to be exposed to potentially hostile
  # networks. See https://github.com/netdata/netdata/issues/164
  bind socket to IP = 0.0.0.0
```

```sh
sudo systemctl enable --now netdata
```

↪ [How to Install Netdata on Ubuntu 22.04](https://wiki.crowncloud.net/?how_to_Install_netdata_monitoring_tool_ubuntu_22_04)
<!-- --8<-- [end:ubuntu-server-arm-22] -->

### Browser Extension

1. Install the [linkding extension](https://github.com/sissbruecker/linkding-extension)
2. `127.0.0.1:8002` → Settings → Integrations → Integrations → REST API → Copy this
3. linkding extension → Configuration
  - Base URL `http://127.0.0.1:8002`
  - API Authentication Token `<Token>`

You can also install [linkding injector](https://github.com/fivefold/linkding-injector).

### Witchcraft

Install [jq](https://jqlang.github.io/jq/).

```sh
pip install linkding-cli ruamel_yaml
pnpm install ramda-cli
cargo install xsv
```

Get `tidy-viewer-*-x86_64-pc-windows-msvc.zip` from [tv - Releases](https://github.com/alexhallam/tv/releases). Decompress it.

Create a `ding.cmd`:

```sh
linkding.exe --url "http://127.0.0.1:8002" --token "<Token>" bookmarks all -q %* ^
  | jq ".results[]" ^
  | ramda -c -o csv ^
  | xsv select tag_names,url,website_title ^
  | tidy-viewer -u 45
```

List all bookmarks:

```sh
ding .
```

Search bookmark:

```sh
ding <String>
```

## [Stirling PDF](https://github.com/Stirling-Tools/Stirling-PDF)

↪ [LocalRunGuide.md](https://github.com/Stirling-Tools/Stirling-PDF/blob/main/LocalRunGuide.md)

## [CompressioWeb](https://github.com/naamhaiabdullah/compressioweb) (Cache)

## [Coder](https://coder.com/) (Cache)

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

## [Trilium](https://github.com/zadam/trilium) (Cache)

Get `trilium-linux-x64-server-*.tar.xz` from [Trilium - Releases](https://github.com/zadam/trilium/releases).

```sh
tar -xvf trilium-linux-x64-server-*.tar.xz
sudo mv trilium-linux-x64-server /opt/trilium
sudo vim /etc/systemd/system/trilium.service
```

```
[Unit]
Description=Trilium Daemon
After=syslog.target network.target

[Service]
User=root
Group=root
Type=simple
ExecStart=/opt/trilium/trilium.sh
WorkingDirectory=/opt/trilium/

TimeoutStopSec=20
Restart=always

[Install]
WantedBy=multi-user.target
```

```sh
sudo systemctl enable --now trilium
```

## [audiobookshelf](https://github.com/advplyr/audiobookshelf) (Cache)

![](https://img.shields.io/github/license/advplyr/audiobookshelf?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/audiobookshelf/main?label=&style=flat-square)](https://github.com/scillidan/audiobookshelf)

```sh
nvm install 16.20.0
nvm use 16.20.0
git clone --depth=1 https://github.com/advplyr/audiobookshelf
set NODE_ENV=production
npm install
npm install sequelize sequelize-cli --save
cd clinet
npm install
npm update vue
npm update fork-ts-checker-webpack-plugin
npm run generate
cd ..
npm start
```

And:

```sh
cd client
npm start
```

Change host or port by editing client/nuxt.config.js:

```
module.exports = {
  server: {
    ...
  },
```

## [Bukubrow](https://github.com/samhh/bukubrow-webext) (Cache)

![](https://img.shields.io/github/license/samhh/bukubrow-webext?label=&style=flat-square)

Install `Bukubrow` browser extension.

```sh
pipx install "buku[server]"
bukuserver run --host 127.0.0.1 --port 5001
```

↪ [Bukuserver](https://github.com/jarun/buku/tree/master/bukuserver)

```sh
git clone https://github.com/samhh/bukubrow-host
cd bukubrow-host
cargo build --release
./target/release/bukubrow --install-chrome
```

<!--
## [Teable](https://github.com/teableio/teable)
## [Plane](https://github.com/makeplane/plane)
## [Maybe](https://github.com/maybe-finance/maybe)
## [Mpv Shelf](https://github.com/aramrw/mpv-shelf)
## [ArchiveBox](https://github.com/ArchiveBox/ArchiveBox) 
 -->