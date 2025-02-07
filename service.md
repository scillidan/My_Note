## Ubuntu Server ARM 22

```sh
sudo apt update && sudo apt upgrade -y
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
mkdir -p /etc/apt/sources.list.d
sudo cp /etc/apt/sources.list.d/ubuntu.sources /etc/apt/sources.list.d/ubuntu.sources.bak
sudo vim /etc/apt/sources.list.d/ubuntu.sources
```

```
Types: deb
URIs: https://mirrors.ustc.edu.cn/ubuntu-ports
Suites: jammy jammy-updates jammy-backports
Components: main restricted universe multiverse
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg

Types: deb
URIs: https://mirrors.ustc.edu.cn/ubuntu-ports
Suites: jammy-security
Components: main universe restricted multiverse
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg
```

For `Ubuntu 24.04 LTS`:

```sh
sudo cp /etc/apt/sources.list.d/ubuntu.sources /etc/apt/sources.list.d/ubuntu.sources.bak
sudo vim /etc/apt/sources.list.d/ubuntu.sources
```

```
Types: deb
URIs: https://mirrors.ustc.edu.cn/ubuntu-ports
Suites: noble noble-updates noble-backports
Components: main restricted universe multiverse
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg

Types: deb
URIs: https://mirrors.ustc.edu.cn/ubuntu-ports
Suites: noble-security
Components: main universe restricted multiverse
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg
```

↪ [USTC Mirror Help - Ubuntu Ports](https://mirrors.ustc.edu.cn/help/ubuntu-ports.html)
<!-- 
↪ [How to fix "Failed to fetch <sources.list links> 404 Not Found [IP: <some_ip>]"](https://askubuntu.com/questions/1348375/how-to-fix-failed-to-fetch-sources-list-links-404-not-found-ip-some-ip)
 -->

## [curl](https://curl.se/) (Optional)

```sh
dpkg -l | grep libcurl4t64
sudo apt-get remove --purge libcurl4t64
sudo apt-get update
sudo apt-get install libcurl4t64
dpkg --get-selections | grep hold
sudo apt-get install -f
sudo apt-get autoremove
```

## NVMe

```sh
sudo mkdir -p /mnt/nvme
```

```sh
ls -l /mnt/nvme
```

```sh
sudo mount -o uid=root,gid=root,umask=000 /dev/sda2 /mnt/nvme
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
IP: <Host>
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

## Samba

<!-- --8<-- [start:arch-linux] -->
```sh
sudo pacman -S samba
sudo pacman -Qi samba
wget https://raw.githubusercontent.com/zentyal/samba/refs/heads/master/examples/smb.conf.default -O smb.conf
```
<!-- --8<-- [end:arch-linux] -->

<!-- --8<-- [start:ubuntu-22-arm] -->
```sh
sudo apt install samba
sudo systemctl status smbd
sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.backup
sudo vim /etc/samba/smb.conf
```

```
workgroup = SAMBAGROUP
...
[sambashare1]
comment = Samba Share
path = /mnt/nvme/sambashare
read only = no
browsable = yes
writable = yes
guest ok = no
# path = /data/smb/share1
# create mask = 0700
# directory mask = 0700
```

↪ [Installing and Configuring Samba on Ubuntu 22](https://reintech.io/blog/installing-configuring-samba-ubuntu-22)
<!-- --8<-- [end:ubuntu-22-arm] -->

```sh
sudo groupadd -r sambausers
sudo useradd -m sambauser
sudo usermod -aG sambausers sambauser
sudo smbpasswd -a sambauser
sudo mkdir -p /mnt/nvme/sambashare
sudo systemctl restart smbd
# sudo chown -R :sambausers /mnt/nvme/sambashare
# sudo chmod 1770 /mnt/nvme/sambashare
# sudo systemctl enable --now smb
# sudo systemctl enable --now nmb
# testparm
```

<!-- --8<-- [start:arch-linux] -->
```sh
sudo mkdir /home/sambauser/server
sudo chown -R sambauser /home/sambauser/server
sudo mount -t cifs //<ip>/sambashare /home/sambauser/server -o username=sambauser,password=YourPassword,workgroup=SAMBAGROUP
sudo systemctl daemon-reload
sudo mount
```

↪ [How to Install and Configure SAMBA on Arch Linux](https://linuxways.net/arch/install-configure-samba-arch-linux/)  
↪ [Samba error code 22](https://forum.manjaro.org/t/samba-error-code-22/106741/1)
<!-- ↪ [How to Set Up a Samba Share on a Linux Server](https://chuck.is/samba/) -->

If `mount error: cifs filesystem not supported by the system`:

```sh
sudo reboot
sudo mount -t cifs //<ip>/sambashare /home/sambauser/server -o username=sambauser,password=YourPassword,workgroup=ARCHGROUP
```

↪ [Mounting a NAS using systemd - mount error: cifs filesystem not supported by the system](https://forum.manjaro.org/t/mounting-a-nas-using-systemd-mount-error-cifs-filesystem-not-supported-by-the-system/119153)

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

↪ [missing_ufw_samba.md](https://gist.github.com/ammgws/1dbd8b3bb38b588c1bb8b3f70dd4fd2c)  
↪ [UFW firewall still blocking SMB despite adding rules](https://askubuntu.com/questions/36608/ufw-firewall-still-blocking-smb-despite-adding-rules)  
↪ [nemo SMB not working](https://www.linuxquestions.org/questions/linux-networking-3/nemo-smb-not-working-4175717802/)  
↪ [Cinnamon Nemo File Manager not open Network shares](https://forum.endeavouros.com/t/cinnamon-nemo-file-manager-not-open-network-shares/12404)
<!-- --8<-- [end:arch-linux] -->

<!-- --8<-- [start:windows10] -->
1. PC → 计算机管理 → 本地用户和组 → 用户 → 右键 → 新用户:
  ```
  用户名 `sambauser`
  用户不能更改密码 On 
  密码永不过期 On
  ```
2. 本地用户和组 → 组 → 右键 → 新建组 → 组名 `SAMBAGROUP` → 添加 → 输入对象名称来选择 `sambauser` → 确认 → 创建
3. 资源管理器 → 此电脑 → 右键 → 添加一个网络位置 → 指定网站的位置 → `\\<your_host>\sambashare` → 请键入该网络位置的名称 `sambashare`
4. 网络位置 → `sambashare` → 右键 → 映射网络驱动器 → 登录时重新连接 On → 完成
<!-- --8<-- [end:windows10] -->

## VNC

<!-- --8<-- [start:arch-linux] -->
```sh
sudo pacman -S tigervnc
vncpasswd
sudo useradd -m vncuser
sudo passwd vncuser
sudo groupadd -r vncusers
sudo usermod -aG vncusers vncuser
sudo vim /etc/tigervnc/vncserver.users
```

```
:1=vncuser
```

Used [LXDE](https://www.lxde.org/) as desktop (Optional):

```sh
sudo pacman -S lxde
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

Or used [Xfce](https://www.xfce.org/):

```sh
rm -rf ~/.vnc
mkdir ~/.vnc
vim ~/.vnc/config
```

```
session=xfce
geometry=1280x720
localhost
alwaysshared
```

On remote:

```sh
vncserver :1
```

On Windows 10, used [TightVNC](https://www.tightvnc.com/download.php):

```sh
tvnviewer <ip>::5901 -password=<vncpasswd>
```

Enable vncserver as service (not recommended):

```sh
sudo systemctl enable --now vncserver@:1
systemctl status vncserver@:1
```

↪ [Setting up tigervncserver on arch linux (raspberry-pi)](https://rushichaudhari.github.io/posts/2020-10-29-setting-up-tigervncserver-on-arch-linux-raspberry-pi/)  
↪ [TigerVNC Server in Manjaro (Arch Linux) - Headless Guide 2021!](https://www.youtube.com/watch?v=w1HS_xVnFFo)  
↪ [How to Install & Configure VNC Server on Ubuntu 22.04](https://bytexd.com/how-to-install-configure-vnc-server-on-ubuntu/)
<!-- --8<-- [end:arch-linux] -->

<!-- --8<-- [start:ubuntu-server-arm-22] -->
```sh
sudo apt install xfce4 xfce4-goodies
sudo apt install tightvncserver
vncserver
vncserver -kill :1
mv ~/.vnc/xstartup ~/.vnc/xstartup.bak
vim ~/.vnc/xstartup
```

```bash
#!/bin/bash
xrdb $HOME/.Xresources
startxfce4 &
```

```sh
chmod +x ~/.vnc/xstartup
vncserver
```

Create service:

```sh
sudo vim /etc/systemd/system/vncserver@.service
```

```
[Unit]
Description=Start TightVNC server at startup
After=syslog.target network.target

[Service]
Type=forking
User=<username>
Group=<username>
WorkingDirectory=/home/<username>

PIDFile=/home/<username>/.vnc/%H:%i.pid
ExecStartPre=-/usr/bin/vncserver -kill :%i > /dev/null 2>&1
ExecStart=/usr/bin/vncserver -depth 24 -geometry 1280x860 -localhost :%i
ExecStop=/usr/bin/vncserver -kill :%i

[Install]
WantedBy=multi-user.target
```

```sh
sudo systemctl daemon-reload
sudo systemctl enable --now vncserver@1.service
sudo systemctl status vncserver@1
```

↪ [How to Install and Configure VNC on Ubuntu 22.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-vnc-on-ubuntu-22-04)
<!-- --8<-- [end:ubuntu-server-arm-22] -->

## [Watchtower](https://github.com/containrrr/watchtower)

↪ [How to Automatically Update Docker Container Images with Watchtower on Ubuntu 22.04](https://www.digitalocean.com/community/tutorials/how-to-automatically-update-docker-container-images-with-watchtower-on-ubuntu-22-04)

## [Ansible](https://github.com/ansible/ansible)

## [PM2](https://pm2.keymetrics.io/)

<!-- --8<-- [start:ubuntu-server-arm-22] -->
```sh
wget https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh -O install_nvm.sh
chmod +x ./install_nvm.sh
./install_nvm.sh
source .bashrc
nvm install --lts
sudo apt install npm
npm install pm2 -g
pm2 dump
pm2 startup
```

↪ [Vue packages version mismatch](https://github.com/nuxt/nuxt/issues/10305)  
↪ [how to modify nuxt server start port ,default port is 3000](https://github.com/nuxt/nuxt/issues/490)
<!-- --8<-- [end:ubuntu-server-arm-22] -->

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

## [Docker](https://www.docker.com/)

<!-- --8<-- [start:ubuntu-server-arm-22] -->
```sh
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
sudo apt-get update
sudo apt-get install ca-certificates wget
sudo install -m 0755 -d /etc/apt/keyrings
sudo wget -O /etc/apt/keyrings/docker.asc https://download.docker.com/linux/ubuntu/gpg
sudo chmod a+r /etc/apt/keyrings/docker.asc
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

↪ [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)

```sh
sudo mkdir -p /etc/docker
sudo vim /etc/docker/daemon.json
```

```
{
  # "data-root": "/mnt/nvme/docker",
  "dns": ["8.8.8.8", "8.8.4.4"],
  "registry-mirrors": [
    "https://docker.1panel.top",
    "https://docker.1panel.live",
    "https://proxy.1panel.live",
    "https://dockerproxy.1panel.live"
  ]
}
```

```sh
sudo mkdir -p /etc/containers/registries.conf.d
sudo vim /etc/containers/registries.conf.d/docker.conf
```

```
unqualified-search-registries = ["docker.io"]

[[registry]]
location = "docker.io"

[[registry.mirror]]
location = "docker.1panel.top"
```

```sh
sudo systemctl daemon-reload
sudo systemctl restart docker
```

↪ [Docker / Podman 安装与换源](https://wcbing.top/linux/containers/install/)  
↪ [How to Change Docker’s Default Data Directory](https://linuxiac.com/how-to-change-docker-data-directory/)

```sh
sudo docker run -p 8080:80 --rm nginx
sudo ufw allow 8080
sudo run -d -v /mnt/nvme:/mnt/nvme <docker_image>
sudo docker ps
sudo docker stop <container_id/name>
sudo docker volume ls
sudo docker volume <volume_name>
```

```sh
sudo docker compose up -d
sudo docker compose stop
```

```sh
```

↪ [Docker Hub - Quickstart](https://docs.docker.com/docker-hub/quickstart/)
<!-- --8<-- [end:ubuntu-server-arm-22] -->

## [Podman](https://podman.io/)

```sh
sudo apt install podman podman-compose
cd <dir>
podman-compose --help
podman-compose up --help
podman-compose up -d
podman ps
podman-compose down
```

```sh
podman run -d --name <name>_server -p 63
```

<!-- --8<-- [start:ubuntu-server-arm-22] -->
```sh
pip3 install podman-compose
~/.local/bin/podman-compose --help
```

↪ [How to Install Podman Compose on Ubuntu 22.04?](https://itslinuxfoss.com/install-podman-compose-ubuntu-22-04/)
<!-- --8<-- [end:ubuntu-server-arm-22] -->

↪ [Starting Containers with systemd](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux_atomic_host/7/html/managing_containers/running_containers_as_systemd_services_with_podman#starting_containers_with_systemd)

<!-- --8<-- [start:arch-linux] -->
```sh
sudo pacman -S docker
sudo systemctl enable --now docker.service
```
<!-- --8<-- [end:arch-linux] -->

## [Dokploy](https://github.com/Dokploy/dokploy)

```sh
curl -sSL https://dokploy.com/install.sh | sh
```

## [postgresql](https://www.postgresql.org/)

```sh
sudo apt install postgresql
sudo systemctl enable --now postgresql
sudo systemctl status postgresql
sudo vim /etc/postgresql/17/main/postgresql.conf
```

```
listen_addresses = '0.0.0.0'
```

```sh
sudo systemctl restart postgresql
sudo su postgres
```

↪ [Install and configure PostgreSQL](https://ubuntu.com/server/docs/install-and-configure-postgresql)

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
wget -qO- https://install.zerotier.com | sudo bash
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

## [Tailscale](https://tailscale.com)

```sh
curl -fsSL https://pkgs.tailscale.com/stable/ubuntu/noble.noarmor.gpg | sudo tee /usr/share/keyrings/tailscale-archive-keyring.gpg >/dev/null
curl -fsSL https://pkgs.tailscale.com/stable/ubuntu/noble.tailscale-keyring.list | sudo tee /etc/apt/sources.list.d/tailscale.list
sudo apt-get update
sudo apt-get install tailscale
sudo tailscale up
ip addr show tailscale0
sudo tailscale login
```

↪ [Setting up Tailscale on Ubuntu 24.04 (noble)](https://tailscale.com/kb/1476/install-ubuntu-2404)  
↪ [Coding on iPad using VSCode, Caddy, and code-server](https://tailscale.com/kb/1166/vscode-ipad)

## [headscale](https://github.com/juanfont/headscale) (Cache)

<!-- --8<-- [start:ubuntu-server-arm-24] -->
Get `headscale_<version>_linux_arm64` from [Headscale - Releases](https://github.com/juanfont/headscale/releases).

```sh
sudo mv headscale_<version>_linux_arm64 headscale
sudo chmod +x headscale
mv headscale /usr/local/bin/
sudo useradd --create-home --home-dir --system --user-group --shell /usr/sbin/nologin headscale
sudo mkdir -p /etc/headscale
sudo wget https://headscale.net/stable/packaging/headscale.systemd.service -O /etc/systemd/system/headscale.service
sudo vim /etc/headscale/config.yaml
```

```yaml
unix_socket: /var/run/headscale/headscale.sock
```

```sh
sudo systemctl daemon-reload
sudo systemctl enable --now headscale
systemctl status headscale
```

↪ [Using standalone binaries (advanced)](https://headscale.net/stable/setup/install/official/#using-standalone-binaries-advanced)  
↪ [How To Install Headscale on Ubuntu 24.04|22.04|20.04](https://computingforgeeks.com/install-and-configure-headscale-on-ubuntu/)
<!-- --8<-- [end:ubuntu-server-arm-24] -->

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
sudo apt --fix-broken install
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

1. Visit `<your_host>:4567`.
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

## [Black Candy](https://github.com/blackcandy-org/blackcandy)

```sh
sudo docker run -d -p 3000:3000 -v /mnt/nvme/<dir>:/media_data -e MEDIA_PATH=/media_data ghcr.io/blackcandy-org/blackcandy:latest 
```

↪ [Media Files Mounts](https://github.com/blackcandy-org/blackcandy#media-files-mounts)

1. Visit `http://<your_host>:3000`
2. User → Settings → Library → Sync

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

## [mpd](https://github.com/MusicPlayerDaemon/MPD) (Cache)

## [PlaylistDir](https://github.com/TheWicklowWolf/PlaylistDir) (Cache)

```sh
mkdir PlaylistDir
cd PlaylistDir
vim docker-compose.yml
```

Copy from [here](https://github.com/TheWicklowWolf/PlaylistDir#run-using-docker-compose).

```sh
sudo docker compose up -d
```

## [Mopidy](https://mopidy.com/) (Cache)

↪ [Installation - Debian/Ubuntu](https://docs.mopidy.com/stable/installation/debian/)

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
unzip LanguageTool-stable.zip
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
sudo apt install make g++
git clone --depth=1 https://github.com/facebookresearch/fastText
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

## [DeepLX](https://github.com/OwO-Network/DeepLX) (Cache)

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

## [LibreTranslate](https://github.com/LibreTranslate/LibreTranslate) (Cache)

↪ [Contributing.md](https://github.com/LibreTranslate/LibreTranslate/blob/main/CONTRIBUTING.md)

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

If clear `postgresql-16`:

```sh
sudo systemctl stop postgresql
sudo systemctl disable postgresql
pg_lsclusters
sudo systemctl stop postgresql@16-main
sudo pg_dropcluster 16 main --stop
sudo apt-get remove --purge postgresql-16
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

<!-- --8<-- [start:ubuntu-server-arm-24] -->
Get `code-server-*-linux-arm64.tar.gz` from [releases](https://github.com/coder/code-server/releases).

```sh
tar -xzvf code-server-*-linux-arm64.tar.gz
sudo cp -r code-server-*-linux-amd64 /usr/lib/code-server
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
Environment=PASSWORD=<password>
ExecStart=/usr/bin/code-server --bind-addr 0.0.0.0:8010 --user-data-dir /var/lib/code-server --auth password
Restart=always

[Install]
WantedBy=multi-user.target
```

```sh
sudo systemctl enable --now code-server
```

↪ [How To Set Up the code-server Cloud IDE Platform on Ubuntu 22.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-the-code-server-cloud-ide-platform-on-ubuntu-22-04)
<!-- --8<-- [end:ubuntu-server-arm-24] -->

1. Settings → Profile → <TargetProfile> → More → Export → <ProfileName> → Local file
2. Settings → Profile (Default) → Import Profile

↪ [Setup Guide](https://github.com/coder/code-server/blob/main/docs/guide.md)

## [VS Code LaTeX Devcontainer](https://github.com/a-nau/latex-devcontainer) (Cache)

## [Zasper](https://github.com/zasper-io/zasper) (Cache)

<!-- --8<-- [start:docker-arm] -->
```sh
git clone --depth=1 https://github.com/zasper-io/zasper
cd zasper/docker
sudo docker compose build
sudo docker compose up -d
```

↪ [Dokcer](https://github.com/zasper-io/zasper/tree/main/docker)
<!-- --8<-- [end:docker-arm] -->

## [Jupyter](https://jupyter.org/)

↪ [jupyterhub-deploy-docker](https://github.com/jupyterhub/jupyterhub-deploy-docker)  
↪ [JupyterHub deployment in use at Université de Versailles](https://github.com/defeo/jupyterhub-docker)  
↪ [Install and Running Jupyter notebook on ARM64](https://linaro.atlassian.net/wiki/spaces/BDDS/pages/26092012207/Install+and+Running+Jupyter+notebook+on+ARM64)

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

## [DevDocs](https://github.com/freeCodeCamp/devdocs)

<!-- --8<-- [start:windows10] -->
```sh
git clone --depth=1 https://github.com/freeCodeCamp/devdocs
cd devdocs
cp Gemfile Gemfile.bak
```

Edit `Gemfile`:

```
ruby '3.3.4'
```

In `pwsh.exe`:

```pwsh
rbenv install 3.3.4
rbenv shell 3.3.4
gem install bundler
bundle install
```

1. Get `curl-*-win64-mingw.zip` from [curl for Windows](https://curl.se/windows/).
2. Decompress it to `curl\`.
3. `cp curl\bin\libcurl-x64.dll <RBENV_ROOT>\3.3.4-1\bin\libcurl.dll`

↪ [Any pod command fails for lack of libcurl.dll on a Windows machine.](https://github.com/CocoaPods/CocoaPods/issues/9955)

1. Get `Binaries` from [Gzip for Windows](https://gnuwin32.sourceforge.net/packages/gzip.htm).
2. Decompress it to `gzip\`.
3. Add `gzip\bin` into `PATH`.
4. `mklink gzip\bin\gunzip.exe gzip\bin\gzip.exe`

↪ [Not installable on Windows](https://github.com/freeCodeCamp/devdocs/issues/1152)

```pwsh
bundle exec thor docs:download bash
bundle exec rackup
```

The data is on `public\docs`.
<!-- --8<-- [end:windows10] -->

<!-- --8<-- [start:docker-arm] -->
```sh
mkdir devdocs
cd devdocs
vim docker-compose.yml
```

```yaml
version: '3.8'

services:
  devdocs:
    image: ghcr.io/freecodecamp/devdocs:latest
    container_name: devdocs
    ports:
      - "9292:9292"
    restart: always
```

```sh
sudo docker compose up -d
```

↪ [Using Docker (Recommended)](https://github.com/freeCodeCamp/devdocs#using-docker-recommended)
<!-- --8<-- [end:docker-arm] -->

## [Instant Recipe Search](https://github.com/typesense/showcase-recipe-search)

<!-- --8<-- [start:windows10 -->
```sh
git clone --depth=1 https://github.com/typesense/showcase-recipe-search
cd showcase-recipe-search
rbenv install 2.7.2
rbenv shell 2.7.2
gem install bundler -v 2.4.22
bundle install
corepack enable
cp yarn.lock yarn.lock.bk
rm yarn.lock
yarn install
yarn run typesenseServer
```

```sh
cp .env.development .env
set BATCH_SIZE=1000
yarn run indexer:transformDataset
yarn run indexer:importToTypesense
yarn start
```
<!-- --8<-- [end:windows10] -->

<!-- --8<-- [start:arch-linux] -->
```sh
sudo pacman -S rbenv
rbenv init
```
<!-- --8<-- [end:arch-linux] -->

## [Graphite](https://github.com/GraphiteEditor/Graphite) (Cache)

<!-- --8<-- [start:ubuntu-server-arm-24] -->
```sh
cargo install cargo-watch
cargo install wasm-pack
cargo install -f wasm-bindgen-cli@0.2.99
sudo apt install libgtk-3-dev libsoup2.4-dev libjavascriptcoregtk-4.0-dev libwebkit2gtk-4.0-dev
git clone --depth=1 https://github.com/GraphiteEditor/Graphite
cd Graphite/frontend
cargo install cargo-about
cargo install wasm-opt
npm install vite --save-dev
npm run build
pm2 serve dist 4321 --name graphite --spa
```

↪ [Project setup](https://graphite.rs/volunteer/guide/project-setup/)
<!-- --8<-- [end:ubuntu-server-arm-24] -->

## [audiobookshelf](https://github.com/advplyr/audiobookshelf) (Cache)

![](https://img.shields.io/github/license/advplyr/audiobookshelf?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/audiobookshelf/main?label=&style=flat-square)](https://github.com/scillidan/audiobookshelf)

<!-- --8<-- [start:windows10] -->
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
<!-- --8<-- [end:windows10] -->

<!-- --8<-- [start:docker-arm] -->
```sh
sudo docker run -d --name audiobookshelf -p 13378:80 -v /mnt/nvme/audiobook:/mnt/nvme/audiobook -v ./audiobooks:/audiobooks -v ./podcasts:/podcasts -v ./metadata:/metadata -v ./config:/config --restart=unless-stopped docker.1panel.top/advplyr/audiobookshelf:latest
sudo docker stop audiobookshelf
```

Or:

```sh
vim docker-compose.yml
```

```yaml
version: '3.8'

services:
  audiobookshelf:
    image: <docker_image_proxy>/advplyr/audiobookshelf:latest
    container_name: audiobookshelf
    ports:
      - "13378:80"
    volumes:
      - /mnt/nvme/audiobook:/mnt/nvme/audiobook
      - ./audiobooks:/audiobooks
      - ./podcasts:/podcasts
      - ./metadata:/metadata
      - ./config:/config
    restart: unless-stopped
```

```sh
sudo docker compose up -d
```
<!-- --8<-- [end:docker-arm] -->

## [Storyteller](https://gitlab.com/smoores/storyteller) (Todo)

<!-- --8<-- [start:docker] -->

↪ [Getting started](https://smoores.gitlab.io/storyteller/docs/getting-started/)  
↪ [Installing the NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html)
<!-- --8<-- [end:docker] -->

## [LinguaCafe](https://github.com/simjanos-dev/LinguaCafe) (Cache)

<!-- --8<-- [start:docker] -->
```sh
mkdir docker-linguacafe
cd docker-linguacafe
wget https://raw.githubusercontent.com/simjanos-dev/LinguaCafe/refs/heads/main/docker-compose.yml
mkdir storage
sudo docker compose up -d
```

1. Visit `http://<your_host>:9191`
2. Create first/admin user, then login-in with it
3. Admin settings → Languages → Chinese → Install

↪ [Updating to the latest version](https://github.com/simjanos-dev/LinguaCafe#updating-to-the-latest-version)  
↪ [Importing dictionaries](https://github.com/simjanos-dev/LinguaCafe/wiki/2.-Setup#importing-dictionaries)
<!-- --8<-- [end:docker] -->

## [dir2opds](https://github.com/dubyte/dir2opds)

<!-- --8<-- [start:ubuntu-server-arm-22] -->
```sh
mkdir dir2opds
cd dir2opds
wget https://github.com/dubyte/dir2opds/releases/download/v1.2.0/dir2opds_1.2.0_linux_arm64.tar.gz
tar xvf dir2opds_1.2.0_linux_arm64.tar.gz
sudo vim /etc/systemd/system/dir2opds.service
```

```
[Unit]
Description=dir2opds
Documentation=https://github.com/dubyte/dir2opds
After=network-online.target

[Service]
User=root
Group=root
Restart=on-failure
ExecStart=/home/<username>/dir2opds/dir2opds -dir /mnt/nvme/audioebook -port 8080

[Install]
WantedBy=multi-user.target
```

```sh
sudo systemctl enable --now dir2opds.service
```
<!-- --8<-- [end:ubuntu-server-arm-22] -->

## [COPS](https://github.com/seblucas/cops) (Cache)

<!-- --8<-- [start:ubuntu-server-arm-22] -->
↪ [Here is COPS : Calibre OPDS (and HTML) PHP Server](https://blog.slucas.fr/projects/calibre-opds-php-server/)
<!-- --8<-- [end:ubuntu-server-arm-22] -->

## [Calibre-Web-Automated-Book-Downloader](https://github.com/calibrain/calibre-web-automated-book-downloader) (Cache)

## [Calibre](https://calibre-ebook.com/)

<!-- --8<-- [start:windows10] -->
1. Calibre → Preferences → Sharing/Sharing over ht net → The port on which to listen for connections `<Port>`
2. Calibre → Connect/share → Start Content server

But can't add books with `calibredb add <Book> --with-library <CalibreData>` when `calibre-server.exe --port <Port> <CalibreData>` running.
<!-- --8<-- [end:windows10] -->

<!-- --8<-- [start:docker-arm] -->
```sh
mkdir calibre
cd calibre
vim docker-compose.yml
```

Copy from [here](https://docs.linuxserver.io/images/docker-calibre/#docker-compose-recommended-click-here-for-more-info).

```sh
vim docker-compose.yml
```

```yaml
    volumes:
      - ./config:/config
      - /mnt/nvme/book:/book
      - /mnt/nvme/sambashare/audioebook:/audioebook
```

```sh
sudo docker compose up -d
```

1. Cabibre → Preferences → Sharing → Sharing over the net → Run server automatically when calibre starts (On) → Start server.
2. Get `http://<your_host>:8081/opds`.

↪ [linuxserver/calibre](https://docs.linuxserver.io/images/docker-calibre)
<!-- ↪ [How To Install Calibre Server & Calibre Web On Ubuntu 22.04](https://kenfavors.com/code/how-to-install-calibre-server-calibre-web-on-ubuntu-22-04/) -->
<!-- --8<-- [end:docker-arm] -->

## [Calibre-Web](https://github.com/janeczku/calibre-web) (Cache)

<!-- --8<-- [start:windows10] -->
```sh
git clone --depth=1 https://github.com/janeczku/calibre-web
cd calibre-web
python -m venv venv
venv\Scripts\activate.bat
pip install calibreweb[metadata]
cps
```

1. Visit `localhost:8083`. If your want to shotdown the process, `Ctrl+C` and refresh the web-page.
2. Login with default Username `admin` and Password `admin123`. If you want to edit account:
  - admin → Edit `Username`, `Email`, `Password`
3. Calibre → Add books. You should get `Calibre Library\` now.
4. Calibre-Web → Admin → Edit Cabibre Database Configuration → Select folder contains the `metadata.db`.
<!-- --8<-- [end:windows10] -->
<!-- --8<-- [start:docker-arm] -->
```sh
mkdir calibre-web
cd calibre-web
vim docker-compose.yml
```

Copy from [here](https://docs.linuxserver.io/images/docker-calibre-web/#docker-compose-recommended-click-here-for-more-info).

```sh
vim docker-compose.yml
```

```yaml
    volumes:
      - ./data:/config
      - /mnt/nvme/share/calibre/library:/books
```

```sh
mkdir -p /mnt/nvme/share/calibre/library
sudo docker compose up -d
```

↪ [linuxserver/calibre-web](https://docs.linuxserver.io/images/docker-calibre-web)
<!-- --8<-- [end:docker-arm] -->

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

## [ntfy.sh](https://ntfy.sh/)

<!-- --8<-- [start:ubuntu-server-arm-24] -->
```sh
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://archive.heckel.io/apt/pubkey.txt | sudo gpg --dearmor -o /etc/apt/keyrings/archive.heckel.io.gpg
sudo apt install apt-transport-https
sudo sh -c "echo 'deb [arch=arm64 signed-by=/etc/apt/keyrings/archive.heckel.io.gpg] https://archive.heckel.io/apt debian main' \
    > /etc/apt/sources.list.d/archive.heckel.io.list"
sudo apt update
sudo apt install ntfy
sudo systemctl enable --now ntfy
```

↪ [Installing ntfy - Debian/Ubuntu repository](https://docs.ntfy.sh/install/#debianubuntu-repository)
<!-- --8<-- [end:ubuntu-server-arm-24] -->

## [Paperless-ngx](https://github.com/paperless-ngx/paperless-ngx)

<!-- --8<-- [start:docker-arm] -->
```sh
mkdir -v ~/paperless-ngx
wget https://raw.githubusercontent.com/paperless-ngx/paperless-ngx/refs/heads/main/docker/compose/docker-compose.postgres.yml -O docker-compose.yml
vim docker-compose.yml
```

```
    volumes:
      - /mnt/nvme/paper:/usr/src/paperless/consume
```

```sh
wget https://raw.githubusercontent.com/paperless-ngx/paperless-ngx/refs/heads/main/docker/compose/docker-compose.env
vim docker-compose.env
```

```
PAPERLESS_OCR_LANGUAGES=chi-sim chi-sim-vert chi-tra chi-tra-vert
PAPERLESS_SECRET_KEY=vK9dUZiSkAO7bjv35VCNKTaA6GdyzTrHcP0jjiCi
```

```sh
docker compose pull
sudo docker compose run --rm webserver createsuperuser
sudo docker compose up -d
sudo docker compose down
```

↪ [Docker using the Installation Script](https://docs.paperless-ngx.com/setup/#docker_script)  
↪ [Paperless-ngx - Bare Metal Route](https://docs.paperless-ngx.com/setup/#bare_metal)
<!-- --8<-- [end:docker-arm] -->

## [Teable](https://github.com/teableio/teable) (Cache)

<!-- --8<-- [start:docker-arm] -->
```sh
mkdir teable
cd teable
```

1. Create `docker-compose.yml` and `.env`.
2. Copy from [Install Teable - Incloude Redis (Recommend)](https://help.teable.io/deployment/docker-compose#docker-compose).

```sh
sudo docker-compose pull
sudo docker compose up -d
sudo docker compose stop
```

↪ [Install Teable - Docker Compose](https://help.teable.io/deployment/docker-compose#docker-compose)  
↪ [CORS error after Dockerizing? How to fix?](https://www.reddit.com/r/docker/comments/yk0x2l/cors_error_after_dockerizing_how_to_fix/)
<!-- --8<-- [end:docker-arm] -->

## [NocoDB](https://nocodb.com/)

```sh
bash <(curl -sSL http://install.nocodb.com/noco.sh) <(mktemp)
```

```
Enter the IP address or ... `<host>`
Show Advanced Options `Y`
Enter the MinIO domain name `Y`
Service Management Menu `Stop Service`
```

```sh
cd nocodb
vim docker.env
```

```
NC_S3_REGION=cn-north-1
```

```sh
bash <(curl -sSL http://install.nocodb.com/noco.sh) <(mktemp)
```

```
Do you want to reinstall NocoDB `N`
Service Management Menu `Start Service`
```

↪ [Self Hosting - Auto-Upstall](https://docs.nocodb.com/getting-started/self-hosted/installation/auto-upstall)

## [Datasette](https://datasette.io)

```sh
mkdir <dir>
cd <dir>
python.exe -m venv venv
venv\Scripts\activate.bat
pip install datasette
# pip install csvs-to-sqlite
# csvs-to-sqlite database.csv database.db
datasette serve <database.db>
```

```sh
datasette serve <database.db> -m metadata.json
```

↪ [Metadata](https://docs.datasette.io/en/stable/metadata.html)

Optional:

```sh
pip install datasette-sitemap
pip install datasette-block-robots
pip install datasette-backup
pip install datasette-parquet
pip install datasette-search-all
pip install qlite-utils
sqlite-utils enable-fts <database.db> <table> <column_1> <column_2>
pip install datasette-render-images
# pip install datasette-media
pip install datasette-render-markdown
pip install datasette-multiline-links
pip install datasette-external-links-new-tabs
pip install datasette-copyable
```

↪ [Datasette charcoal theme](https://github.com/julien040/charcoal-datasette-theme)  
↪ [datasette-block-robots](https://github.com/simonw/datasette-block-robots)  
↪ [datasette-sitemap](https://github.com/simonw/datasette-sitemap)  
↪ [datasette-search-all](https://github.com/simonw/datasette-search-all)  
↪ [Configuring FTS using sqlite-utils](https://docs.datasette.io/en/stable/full_text_search.html#configuring-fts-using-sqlite-utils)  
↪ [datasette-render-markdown](https://github.com/simonw/datasette-render-markdown)  
↪ [datasette-external-links-new-tabs](https://github.com/ocdtrekkie/datasette-external-links-new-tabs)  
↪ [datasette-multiline-links](https://github.com/simonw/datasette-multiline-links)  
↪ [datasette-parquet](https://github.com/cldellow/datasette-parquet)  
↪ [datasette-publish-vercel](https://github.com/simonw/datasette-publish-vercel)  

<!--
↪ [datasette-atom](https://github.com/simonw/datasette-atom)  
↪ [datasette-write-ui](https://github.com/datasette/datasette-write-ui)  
↪ [datasette-upload-csvs](https://github.com/simonw/datasette-upload-csvs)  
↪ [datasette-insert](https://github.com/simonw/datasette-insert)  
↪ [datasette-export](https://github.com/simonw/datasette-export)  
↪ [datasette-mutable-downloads](https://github.com/cldellow/datasette-mutable-downloads)
-->

## [n8n](https://n8n.io/)

<!-- --8<-- [start:docker-arm] -->
```sh
mkdir n8n-docker
cd n8n-docker
vim docker-compose.yml
```

Copy from [here](https://docs.n8n.io/hosting/installation/server-setups/docker-compose/#5-create-docker-compose-file) ande edit:

```yaml
services:
  traefik:
    command:
      - "--entrypoints.web.address=:8070"
      - "--entrypoints.websecure.address=:453"
    ports:
      - "8070:8070"
      - "453:453"
  n8n:
    images: <docker_image_proxy>/n8nio/n8n
    ports:
      - "0.0.0.0:5678:5678"
    environment:
      - N8N_SECURE_COOKIE=false
    volumes:
      - /mnt/nvme/share/n8n:/files
      - n8n_data:/home/node/.n8n

```

```sh
sudo docker volume create n8n_data
sudo docker volume create traefik_data
sudo docker compose up -d
```

↪ [Server setups - Docker-Compose](https://docs.n8n.io/hosting/installation/server-setups/docker-compose/)
<!-- --8<-- [end:docker-arm] -->

## [Gitea](https://about.gitea.com/) (Cache)
<!-- --8<-- [start:ubuntu-server-arm-24] -->
Get `gitea-*-linux-arm64` from [here](https://dl.gitea.com/gitea/1.22.6/gitea-1.22.6-darwin-10.12-arm64).

```sh
gpg --keyserver keys.openpgp.org --recv 7C9E68152594688862D62AF62D9AE806EC1592E2
gpg --verify gitea-*-linux-amd64.asc gitea-*-linux-amd64
mv gitea-*-linux-arm64 gitea
sudo chmod +x gitea
sudo adduser --system --shell /bin/bash --gecos 'Git Version Control' --group --disabled-password --home /home/git git
sudo mkdir -p /var/lib/gitea/{custom,data,log}
sudo chown -R git:git /var/lib/gitea/
sudo chmod -R 750 /var/lib/gitea/
sudo mkdir /etc/gitea
sudo chown root:git /etc/gitea
sudo chmod 770 /etc/gitea
sudo cp gitea /usr/local/bin/gitea
sudo vim /etc/systemd/system/gitea.service
```

```
[Unit]
Description=Gitea
After=network.target

[Service]
User=git
Group=git
WorkingDirectory=/var/lib/gitea/
Environment=GITEA_WORK_DIR=/var/lib/gitea/
ExecStart=/usr/local/bin/gitea web -c /etc/gitea/app.ini
Restart=always
RestartSec=10

[Install]
WantedBy=multi-user.target
```

```sh
sudo systemctl start --now gitea.service
sudo chmod 750 /etc/gitea
sudo chmod 640 /etc/gitea/app.ini
```

↪ [Installation from binary](https://docs.gitea.com/installation/install-from-binary)
<!-- --8<-- [end:ubuntu-server-arm-24] -->
## [Sourcebot](https://github.com/sourcebot-dev/sourcebot)

<!-- --8<-- [start:docker-arm] -->
```sh
mkdir Docker/sourcebot
cd Docker/sourcebot
vim docker-compose.yml
```

```yaml
version: '3.8'

services:
  sourcebot:
    image: ghcr.io/sourcebot-dev/sourcebot:latest
    ports:
      - "3100:3100"
    restart: unless-stopped
```

```sh
sudo docker compose up -d
```

↪ [Getting Started](https://github.com/sourcebot-dev/sourcebot#getting-started)
<!-- --8<-- [end:docker-arm] -->

## [immich](https://immich.app/)

<!-- --8<-- [start:docker-arm] -->
```sh
mkdir ./immich-app
cd ./immich-app
wget -O docker-compose.yml https://github.com/immich-app/immich/releases/latest/download/docker-compose.yml
wget -O .env https://github.com/immich-app/immich/releases/latest/download/example.env
sudo docker compose up -d
```

Upgrade:

```sh
docker compose pull && sudo docker compose up -d
```

↪ [Docker Compose [Recommended]](https://immich.app/docs/install/docker-compose)
<!-- --8<-- [end:docker-arm] -->

## [ttyd](https://github.com/tsl0922/ttyd) (Cache)

<!-- --8<-- [start:ubuntu-server-arm-22] -->
```sh
sudo apt-get update
sudo apt-get install -y build-essential cmake git libjson-c-dev libwebsockets-dev
git clone --depth=1 https://github.com/tsl0922/ttyd
cd ttyd && mkdir build && cd build
cmake ..
make && sudo make install
```

```sh
sudo vim /etc/systemd/system/ttyd.service
```

```
[Unit]
Description=ttyd service
After=network.target

[Service]
Type=simple
User=<username>
Group=<username>
ExecStart=/usr/local/bin/ttyd --cwd /home/<username> --writable zsh
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

```sh
sudo systemctl enable --now ttyd
```

↪ [ttyd - Basic Usage](https://github.com/tsl0922/ttyd/wiki/Example-Usage)
<!-- --8<-- [end:ubuntu-server-arm-22] -->

## [RegExr](https://github.com/gskinner/regexr)

```sh
mkdir regexr
vim docker-compose.yml
```

```yaml
version: '3.8'

services:
  regexr:
    image: gufertum/regexr
```

```sh
sudo docker compose up -d
```

↪ [docker-regexr](https://github.com/gufertum/docker-regexr)

## [beaverhabits](https://github.com/daya0576/beaverhabits) (Cache)

<!-- --8<-- [start:docker-arm] -->
```sh
mkdir beaverhabits
```

```sh
sudo docker run -d --name beaverhabits \
  -e FIRST_DAY_OF_WEEK=0 \
  -e HABITS_STORAGE=USER_DISK \
  -e MAX_USER_COUNT=1 \
  -v ./beaverhabits:/app/.user/ \
  -p 8070:8080 \
  --restart unless-stopped \
  daya0576/beaverhabits:latest
```
<!-- --8<-- [end:docker-arm] -->

Beaver Habit Tracker → More → Add ...

## [TeXdoc online](https://gitlab.com/islandoftex/images/texdoc-online) (Todo)

```sh
git clone --depth=1 https://gitlab.com/islandoftex/images/texdoc-online
cd texdoc-online
sudo docker compose up -d
```

## [Cal.com](https://cal.com)

↪ [Getting Started - Docker](https://cal.com/docs/self-hosting/docker)

## [CasaOS](https://github.com/IceWhaleTech/CasaOS)

<!-- --8<-- [srart:docker-arm] -->
```sh
wget -qO- https://get.casaos.io | sudo bash
sudo ufw allow 80
```

Uninstall:

```sh
sudo casaos-uninstall
```
<!-- --8<-- [end:docker-arm] -->

### [ttydBridge](https://github.com/Cp0204/ttydBridge) (Cache)

<!-- --8<-- [start:docker-arm] -->
```sh
sudo docker run -d \
  --name ttdybridge \
  -e PORT=2222 \
  -v /opt:/opt \
  --pid host \
  --privileged \
  --restart unless-stopped \
  cp0204/ttdybridge:latest
```
<!-- --8<-- [end:docker-arm] -->

## [File Browser](https://github.com/filebrowser/filebrowser)

<!-- --8<-- [start:docker-arm] -->
```sh
mkdir filebrowser-docker
cd filebrowser-docker
vim docker-compose.yml
```

Copy from [here](https://docs.techdox.nz/filebrowser/#docker-compose-file-docker-composeyml).

```sh
sudo docker compose up -d
```

↪ [Setting Up Filebrowser with Docker Compose](https://docs.techdox.nz/filebrowser/)

## [Twenty](https://github.com/twentyhq/twenty)

```sh
curl -o docker-compose.yml https://raw.githubusercontent.com/twentyhq/twenty/refs/heads/main/packages/twenty-docker/docker-compose.yml
curl -o .env https://raw.githubusercontent.com/twentyhq/twenty/refs/heads/main/packages/twenty-docker/.env.example
openssl rand -base64 32
vim .env
```

```
APP_SECRET=<random_string>
PGPASSWORD_SUPERUSER=<password>
```

```sh
sudo docker compose up -d
```

↪ [1-Click w/ Docker Compose](https://twenty.com/developers/section/self-hosting/docker-compose)

## [Dashy](https://github.com/Lissy93/dashy)

↪ [Dashy - Quick Start](https://dashy.to/docs/quick-start)  
↪ [Dashy Showcase - System Monitor](https://dashy.to/docs/showcase/#system-monitor)

## [Windows](https://github.com/dockur/windows) (Cache)

## [OSX](https://github.com/dockur/macos) (Cache)

<!--
## [Plane](https://github.com/makeplane/plane)
## [Maybe](https://github.com/maybe-finance/maybe)
## [Mpv Shelf](https://github.com/aramrw/mpv-shelf)
## [ArchiveBox](https://github.com/ArchiveBox/ArchiveBox) 
 -->