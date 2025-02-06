## [Vim](https://www.vim.org)

Get `gvim_*_x64_signed.zip` from [Downloading Vim](https://www.vim.org/download.php).

## [Neovim](https://neovim.io)

↪ [Neovim configuration on Windows 10](https://jdhao.github.io/2018/11/15/neovim_configuration_windows/)  
↪ [Nvim warning](https://github.com/LunarWatcher/auto-pairs#nvim-warning)  
↪ [Why you switched from Neovim to Vim?](https://www.reddit.com/r/vim/comments/16cdbyd/why_you_switched_from_neovim_to_vim/)

<!-- --8<-- [start:ubuntu-24-arm] -->
```sh
vim ~/.config/systemd/user/nvim_headless.service
```

```
[Unit]
Description=Start Neovim Headless Server

[Service]
ExecStart=nvim --headless --listen 0.0.0.0:1234
Restart=on-failure
User=<username>

[Install]
WantedBy=default.target
```

```sh
systemctl --user daemon-reload
systemctl --user enable --now nvim_headless
```
<!-- --8<-- [end:ubuntu-24-arm] -->

On PC:

```sh
C:\Users\User\Bin\Git\usr\bin\ssh.exe <username>@<your_host> -L 1234:0.0.0.0:1234 -- /home/<your_host>/.local/bin/nvim --headless --listen 0.0.0.0:1234
neovide --server <your_host>:1234
```

↪ [Run Neovide on remote SSH system](https://github.com/neovide/neovide/discussions/2853)

### [Bob](https://github.com/MordechaiHadad/bob)

Get `bob` from [Bob - Releases](https://github.com/MordechaiHadad/bob/releases).

```sh
bob list-remote
bob install 0.10.0
```

### Install from source

<!-- --8<-- [start:ubuntu-22-arm] -->
↪ [PPA not working with lazy.nvim](https://www.reddit.com/r/neovim/comments/166fpfb/ppa_not_working_with_lazynvim/)

```sh
sudo apt-get install ninja-build gettext cmake unzip curl
```

↪ [Neovim - Build prerequisites](https://github.com/neovim/neovim/blob/master/BUILD.md#build-prerequisites)

1. Get `Source code` from [Neovim - Releases](https://github.com/neovim/neovim/releases).
2. Decompress it to `neovim\`.

```sh
cd neovim
```

If re-build, first do:

```sh
rm -r build/
```

```sh
make CMAKE_EXTRA_FLAGS="-DCMAKE_INSTALL_PREFIX=$HOME/neovim"
make install
```

↪ [Install from source](https://github.com/neovim/neovim/blob/master/INSTALL.md#install-from-source)

```sh
ln -s ~/neovim/bin/nvim ~/.local/bin/
```

```sh
nvim
```

If `lazy.nvim` install failed,

```sh
rm -rf ~/.local/share/nvim/lazy/
```

```sh
nvim
```

↪ [Neovim: module 'lazy' not found](https://stackoverflow.com/questions/77510936/neovim-module-lazy-not-found/77825709)
<!-- --8<-- [end:ubuntu-22-arm] -->





## [LunarVim](https://www.lunarvim.org/)

In PowerShell:

```powershell
$env:Path += ";C:\Users\<User>\AppData\Local\bob\v0.9.0\nvim-win64\bin"
```

```sh
pwsh -c "$LV_BRANCH='release-1.3/neovim-0.9'; iwr https://raw.githubusercontent.com/LunarVim/LunarVim/release-1.3/neovim-0.9/utils/installer/install.ps1 -UseBasicParsing | iex"
```

Add to `Cmder/config/user_profile.cmd`:

```
set "XDG_CACHE_HOME=C:\Users\<User>\AppData\Local\Temp%XDG_CACHE_HOME%"
set "XDG_RUNTIME_DIR=C:\Users\<User>\AppData\Local\Temp%XDG_RUNTIME_DIR%"
set "LUNARVIM_BASE_DIR=C:\Users\<User>\AppData\Roaming\lunarvim\lvim%LUNARVIM_BASE_DIR%"
set "LUNARVIM_CACHE_DIR=C:\Users\<User>\AppData\Local\Temp\lvim%LUNARVIM_CACHE_DIR%"
set "LUNARVIM_CONFIG_DIR=C:\Users\<User>\AppData\Local\lvim%LUNARVIM_CONFIG_DIR%"
set "LUNARVIM_RUNTIME_DIR=C:\Users\<User>\AppData\Roaming\lunarvim%LUNARVIM_RUNTIME_DIR%"
```

```sh
lvim
```

↪ [Installation](https://www.lunarvim.org/docs/installation)  
↪ [No C compiler found](https://github.com/LunarVim/Neovim-from-scratch/issues/274#issuecomment-1364584526)

https://github.com/neovide/neovide/discussions/2853