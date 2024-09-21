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
wget https://gist.github.com/scillidan/b49eabe3a90e7e7499b5155af7f36480/raw/7b4cb38b5010a1c6b2c3a6709b0abb0305028239/.zshrc_mini -O .zshrc
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

### [autin](https://github.com/atuinsh/atuin)

```sh
pkg install atuin
```

<!-- --8<-- [start:ubuntu-22-arm] -->
Get `atuin-aarch64-unknown-linux-gnu.tar.gz` from [Atuin - releases](https://github.com/atuinsh/atuin/releases/download/).

```sh
tar -xvzf atuin-aarch64-unknown-linux-gnu.tar.gz atuin
mkdir ~/.local/bin
mv atuin-aarch64-unknown-linux-gnu/atuin ~/.local/bin/
source ~/.zshrc
```
<!-- --8<-- [end:ubuntu-22-arm] -->

### [tere](https://github.com/a8m/tree)

```sh
pkg install tere
```

### [eza](https://github.com/eza-community/eza)

```sh
pkg install eza
```

## [Github CLI](https://cli.github.com/)

```sh
pkg install gh
```

```sh
gh auth login
```

## [tmux](https://github.com/tmux/tmux)

## [Zellij](https://github.com/zellij-org/zellij)

```sh
pkg install zellij
```

Get `zellij-aarch64-unknown-linux-musl.tar.gz` from [Releases](https://github.com/zellij-org/zellij/releases).

↪ [Configuration](https://zellij.dev/documentation/configuration)  
↪ [Configuration - Options](https://zellij.dev/documentation/options)  
↪ [Configuration - Tokyo Night Light](https://zellij.dev/documentation/theme-gallery#tokyo-night-light)  
↪ [Layouts](https://zellij.dev/documentation/layouts)  
↪ [default.kdl](https://github.com/zellij-org/zellij/blob/main/zellij-utils/assets/config/default.kdl)  
↪ [Does zellij support changing tab's name according to pane file system path automatically?](https://www.reddit.com/r/zellij/comments/10skez0/does_zellij_support_changing_tabs_name_according/)