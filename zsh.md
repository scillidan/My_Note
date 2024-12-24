## [Nerd Font](http://nerdfonts.com/)

```sh
mkdir -p ~/.local/share/fonts
mv <font> ~/.local/share/fonts/
fc-cache -fv
```

↪ [Install a nerd font on ubuntu](https://gist.github.com/matthewjberger/7dd7e079f282f8138a9dc3b045ebefa0)

```sh
sudo vim /etc/fonts/conf.d/50-enable-fixed.conf
```

```
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
  <selectfont>
    <acceptfont>
      <pattern>
        <patelt name="<font_family>"><string>fixed</string></patelt>
      </pattern>
    </acceptfont>
  </selectfont>
</fontconfig>
```

```sh
sudo dpkg-reconfigure fontconfig
```

```sh
wget https://github.com/ryanoasis/nerd-fonts/releases/download/v3.3.0/JetBrainsMono.tar.xz
tar -xJvf JetBrainsMono.tar.xz
rm README.md
rm OFL.txt
mv JetBrains** ~/.local/share/fonts
```

↪ [ubuntu wiki - Fonts](https://wiki.ubuntu.com/Fonts)

## [Zsh](https://www.zsh.org/)

```sh
sudo pacman -S zsh
sudo apt install zsh
pkg install zsh
```

```sh
sh -c "$(wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```

```sh
cd ~
wget https://gist.githubusercontent.com/scillidan/b49eabe3a90e7e7499b5155af7f36480/raw/1ad03938633a16651b311e4a6108ed40152110f8/.zshrc_mini -O .zshrc
source .zshrc
```

## [oh-my-zsh](https://ohmyz.sh)

```sh
sh -c "$(wget -O- https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

↪ [/etc/hosts in unwriteable even with root](reddit.com/r/termux/comments/18sz5a1/etchosts_in_unwriteable_even_with_root/)

```sh
vim install_ohmyzsh.sh
```

On PC, paste content of [install.sh](https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh) into, then:

```sh
chmod +x install_ohmyzsh.sh
./install_ohmyzsh.sh
```

```sh
exec zsh
```

## [zsh-abbr](https://github.com/olets/zsh-abbr)

↪ [abbr c does not clear abbreviations created with the pattern abbr x=y](https://github.com/olets/zsh-abbr/issues/88)

### [zsh-ssh](https://github.com/sunlei/zsh-ssh)

Read more on [Using the SSH Config File](https://linuxize.com/post/using-the-ssh-config-file/).

### [fzf](https://github.com/junegunn/fzf)

```sh
pkg install fzf
```

<!-- --8<-- [start:ubuntu-22-arm] -->
Get `fzf-*-linux_arm64.tar.gz` from [fzf - Releases](https://github.com/junegunn/fzf/releases).

```sh
mkdir ~/.local/bin
tar -xvzf fzf-*-linux_arm64.tar.gz
mv fzf ~/.local/bin/
```
<!-- --8<-- [end:ubuntu-22-arm] -->

### [Atuin](https://github.com/atuinsh/atuin)

```sh
pkg install atuin
```

<!-- --8<-- [start:ubuntu-22-arm] -->
Get `atuin-aarch64-unknown-linux-gnu.tar.gz` from [Atuin - Releases](https://github.com/atuinsh/atuin/releases).

```sh
tar -xvzf atuin-aarch64-unknown-linux-gnu.tar.gz
mv atuin-aarch64-unknown-linux-gnu/atuin ~/.local/bin/
source ~/.zshrc
```
<!-- --8<-- [end:ubuntu-22-arm] -->

### [tere](https://github.com/mgunyho/tere)

```sh
pkg install tere
```

<!-- --8<-- [start:ubuntu-22-arm] -->
Get `tere-1.6.0-aarch64-unknown-linux-gnu.zip` from [tere - Releases](https://github.com/mgunyho/tere/releases)

```sh
unzip tere-1.6.0-aarch64-unknown-linux-gnu.zip
mv tere ~/.local/bin/
```
<!-- --8<-- [end:ubuntu-22-arm] -->

### [eza](https://github.com/eza-community/eza)

```sh
pkg install eza
```

<!-- --8<-- [start:ubuntu-22-arm] -->
Get `eza_aarch64-unknown-linux-gnu.tar.gz` from [eza - Releases](https://github.com/eza-community/eza/releases).

```sh
tar -xvzf eza_aarch64-unknown-linux-gnu.tar.gz
mv eza ~/.local/bin/
```
<!-- --8<-- [end:ubuntu-22-arm] -->

## [Github CLI](https://cli.github.com/)

```sh
sudo apt install gh
pkg install gh
```

```sh
gh auth login
```

## [tmux](https://github.com/tmux/tmux)

## [Zellij](https://github.com/zellij-org/zellij)

```sh
pkg install zellij
cargo install zellij
```

<!-- --8<-- [start:ubuntu-22-arm] -->
Get `zellij-aarch64-unknown-linux-musl.tar.gz` from [Zellij - Releases](https://github.com/zellij-org/zellij/releases).

```sh
tar -xvzf zellij-aarch64-unknown-linux-musl.tar.gz
mv zellij ~/.local/bin/
```
<!-- --8<-- [end:ubuntu-22-arm] -->

↪ [Configuration](https://zellij.dev/documentation/configuration)  
↪ [Configuration - Options](https://zellij.dev/documentation/options)  
↪ [Configuration - Tokyo Night Light](https://zellij.dev/documentation/theme-gallery#tokyo-night-light)  
↪ [Layouts](https://zellij.dev/documentation/layouts)  
↪ [default.kdl](https://github.com/zellij-org/zellij/blob/main/zellij-utils/assets/config/default.kdl)  
↪ [Does zellij support changing tab's name according to pane file system path automatically?](https://www.reddit.com/r/zellij/comments/10skez0/does_zellij_support_changing_tabs_name_according/)

Get `zjframes.wasm`, `zjstatus.wasm` from [zjstatus & zjframes - Releases](https://github.com/dj95/zjstatus/releases).

```sh
mv zjframes.wasm ~/.config/zellij/plugins
mv zjstatus.wasm ~/.config/zellij/plugins
```

## [Starship](https://starship.rs/)

<!-- --8<-- [start:ubuntu-22-arm] -->
Get `starship-aarch64-unknown-linux-musl.tar.gz` from [Starship - Releases](https://github.com/starship/starship/releases).

```sh
tar -xvzf starship-aarch64-unknown-linux-musl.tar.gz
mv starship ~/.local/bin/
```
<!-- --8<-- [end:ubuntu-22-arm] -->