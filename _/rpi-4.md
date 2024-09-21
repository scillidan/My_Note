## USB host boot mode

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
```

```sh
mkfs.ext4 /dev/<source>
```

```sh
sudo dd if=/dev/<source> of=/dev/<target> bs=4M status=progress
```

```sh
sync
```

```sh
lsblk
```

↪ [Boot from USB, if no then SD card](https://raspberrypi.stackexchange.com/questions/91889/boot-from-usb-if-no-then-sd-card  )
↪ [What's the best filesystem to use for an NVMe SSD?](https://www.reddit.com/r/linux4noobs/comments/lmf8ju/whats_the_best_filesystem_to_use_for_an_nvme_ssd/)

## Pi OS

Change Mirrors:

```sh
sudo cp /etc/apt/sources.list.d/raspi.list /etc/apt/sources.list.d/raspi.list.bat
sudo nano /etc/apt/sources.list.d/raspi.list
```

```
deb https://mirrors.tuna.tsinghua.edu.cn/raspberrypi/ bookworm main
```

↪ [Raspbian 软件仓库](https://mirrors.tuna.tsinghua.edu.cn/help/raspberrypi/)

```sh
sudo apt update && sudo apt upgrade
```

## SSH

Preferences → Raspberry Pi Configuration → Interfaces → SSH (On)

```sh
hostname -I
```

↪ [How to SSH into Raspberry Pi](https://www.onlogic.com/company/io-hub/how-to-ssh-into-raspberry-pi/)