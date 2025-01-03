## Install Termux

```sh
pkg update && pkg upgrade
pkg install curl wget git vim
```

### [Termux:Styling](https://github.com/termux/termux-styling) (Cache)

### [Nerd Font](https://www.nerdfonts.com/font-downloads)

```sh
wget https://raw.githubusercontent.com/scillidan/Nerd-Sarasa-Merge/main/MonaspiceArNFP-SarasaGothicSC-WFMSansSC.ttf -O font.ttf
cp font.ttf ~/.termux/font.ttf
termux-reload-settings
```

↪ [[Info] How to setup nerd font in order to work lsd properly in Termux(Android)](https://github.com/lsd-rs/lsd/issues/423)

### Keyboard

```sh
cp .termux/termux.properties .termux/termux.properties.bak
vim .termux/termux.properties
```

```
extra-keys = [[ \
  {key: TAB, popup: KEYBOARD}, \
  {key: ESC, popup: '<'}, \
  {key: CTRL, popup: '['}, \
  {key: ALT, popup: '\{'}, \
  {key: 'BACKSLASH', popup: '|'}, \
  {key: '_', popup: '='}, \
  {key: UP, popup: PGUP}, \
  {key: DOWN, popup: PGDN}, \
  {key: LEFT, popup: HOME}, \
  {key: RIGHT, popup: END} \
]]
```

↪ [Can I hide this keyboard? I have a physical one attached](https://www.reddit.com/r/termux/comments/qaenv5/can_i_hide_this_keyboard_i_have_a_physical_one/)  
↪ [Disabling the up-arrow key rebinding?](https://github.com/atuinsh/atuin/issues/51#issuecomment-1641211422)

### Input Method

↪ [copy and paste using Ctrl-C Ctrl-V or right click menu](https://github.com/termux/termux-app/issues/1891)  
↪ [Text Input View](https://wiki.termux.com/wiki/Touch_Keyboard#Text_Input_View)

### [SSH](https://wiki.termux.com/wiki/Remote_Access#SSH)

```sh
pkg install openssh
```

```sh
passwd
```

```sh
sshd
```

On PC:

```sh
ssh -p 8022 <AnyUsername>@<HostnameOrIp>
```

### [Termux-setup-storage](https://wiki.termux.com/wiki/Termux-setup-storage)

```sh
termux-setup-storage
```

### Linux file system

```sh
pkg install proot
termux-chroot
ls /usr
```

↪ [Termux is not FHS compliant](https://wiki.termux.com/wiki/Differences_from_Linux#Termux_is_not_FHS_compliant)  
↪ [Access Termux from a file manager](https://wiki.termux.com/wiki/Internal_and_external_storage)

### Username

↪ [Termux is single-user](https://wiki.termux.com/wiki/Differences_from_Linux#Termux_is_single-user)

### Desktop

↪ [Graphical Environment](https://wiki.termux.com/wiki/Graphical_Environment)  
↪ [Termux Desktop](https://github.com/adi1090x/termux-desktop)  
↪ [termux-desktop-xfce](https://github.com/Yisus7u7/termux-desktop-xfce)

### [root-termux](https://github.com/hctilg/root-termux)

### [code-server](https://github.com/coder/code-server/)

↪ [Install - npm](https://coder.com/docs/code-server/npm)  
↪ [Usage - Termux](https://coder.com/docs/code-server/termux)  
↪ [How to install VS Code in an Android Phone?](https://www.codewithharry.com/blogpost/install-vs-code-in-android/)

### Troubleshoot

↪ [apt-get update fails to fetch files, “Temporary failure resolving …” error](https://askubuntu.com/questions/91543/apt-get-update-fails-to-fetch-files-temporary-failure-resolving-error)  
↪ [cargo install: specify a /tmp substitute?](https://stackoverflow.com/questions/64572901/cargo-install-specify-a-tmp-substitute/64616981#64616981)  
↪ [Can not install on android - target 'aarch64-linux-android' not found in channel.](https://github.com/rust-lang/rustup/issues/2872)