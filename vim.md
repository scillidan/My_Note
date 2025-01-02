## [Vim](https://www.vim.org)

Get `gvim_*_x64_signed.zip` from [Downloading Vim](https://www.vim.org/download.php).

## [Neovim](https://neovim.io)

```sh
sudo apt install neovim
pkg install neovim
```

↪ [Neovim configuration on Windows 10](https://jdhao.github.io/2018/11/15/neovim_configuration_windows/)  
↪ [Nvim warning](https://github.com/LunarWatcher/auto-pairs#nvim-warning)  
↪ [Why you switched from Neovim to Vim?](https://www.reddit.com/r/vim/comments/16cdbyd/why_you_switched_from_neovim_to_vim/)

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

## [Neovide](https://neovide.dev)

↪ [Installation](https://neovide.dev/installation.html).

`init.lua` part:

```lua
local alpha = function()
  return string.format("%x", math.floor(255 * vim.g.transparency or 0.75))
end

if vim.g.neovide then
    vim.g.neovide_padding_top = 0
    vim.g.neovide_padding_bottom = 0
    vim.g.neovide_padding_right = 0
    vim.g.neovide_padding_left = 0
    vim.g.neovide_transparency = 0.75
    vim.g.transparency = 0.75
    vim.g.neovide_background_color = "#0f1117" .. alpha()
    vim.g.neovide_floating_blur_amount_x = 1.0
    vim.g.neovide_floating_blur_amount_y = 1.0
    vim.g.neovide_cursor_animation_length = 0
    vim.g.neovide_cursor_trail_size = 0
    vim.g.neovide_remember_window_size = true
    vim.g.neovide_hide_mouse_when_typing = true
end
```

Create `nv.cmd`:

```sh
neovide.exe --size=1250x720 --frame none --no-tabs --neovim-bin nvim.exe -- -u "init.lua" %*
```

Create `lv.cmd`:

```sh
neovide.exe --neovim-bin nvim.exe --geometry 100x30 --notabs --frame none -- -u "%LUNARVIM_BASE_DIR%\init.lua" %*
```

### `init.lua`

`init.lua`:

```lua
vim.api.nvim_command("language en_US.UTF-8")
vim.o.guifont = "MonaspiceAr NFP + Sarasa Gothic SC + WFM Sans SC:h9"
vim.o.number = true
vim.o.relativenumber = true
vim.o.tabstop = 2
vim.o.shiftwidth = 2
vim.o.timeout = true
vim.o.timeoutlen = 300
vim.o.signcolumn = "yes:1"
vim.o.cmdheight = 1
vim.g.mapleader = " "
```

↪ [How do I change my language in my init.lua? - neovim](https://vi.stackexchange.com/questions/36426/how-do-i-change-my-language-in-my-init-lua-neovim)  
↪ [Install a Nerd Font](https://www.lunarvim.org/docs/installation/post-install#install-a-nerd-font)  
↪ [Only just discovered 'set signcolumn=number', I like it](https://www.reddit.com/r/neovim/comments/neaeej/only_just_discovered_set_signcolumnnumber_i_like/)

### [lazy.nvim](https://github.com/folke/lazy.nvim)

### [packer.nvim](https://github.com/wbthomason/packer.nvim)

↪ [How to Install and Use Packer in Neovim/Nvim](https://linovox.com/install-and-use-packer-in-neovim/)

### `:checkhealth`

```sh
nvim
```

```
:checkhealth
```

```sh
pip install --upgrade pynvim
```

### LSP

↪ [Configuring Language Server Protocol (LSP) in Neovim](https://linovox.com/configuring-language-server-protocol-lsp-in-neovim/)

### cmp

↪ [How to Install and Use nvim cmp Autocompletion](https://linovox.com/install-and-use-nvim-cmp/)
<!-- ↪ [Autocomplete with nvim-cmp](https://www.jonashietala.se/blog/2024/05/26/autocomplete_with_nvim-cmp/) -->

### [mason.nvim](https://github.com/williamboman/mason.nvim)

```
:MasonInstall python-lsp-server
:MasonInstall lua-language-server
:MasonInstall luacheck
:MasonInstall ltex-ls
:MasonInstall harper-ls
```

### [nvim-treesitter](https://github.com/nvim-treesitter/nvim-treesitter)

1. Install [MinGW GCC G++ Compiler](https://techdecodetutorials.com/download/)
2. Install [zig](https://ziglang.org/)

↪ [nvim-treesitter doesn't seem to work in windows.](https://github.com/nvim-treesitter/nvim-treesitter/issues/2135)

```
:TSInstall python
```

<!-- ↪ [Let's create a Tree-sitter grammar](https://www.jonashietala.se/blog/2024/03/19/lets_create_a_tree-sitter_grammar/) -->

### [nvim-devdocs](https://github.com/luckasRanarison/nvim-devdocs)

```
:TSInstall html
```

Edit `init.lua`:

```lua
vim.g.plenary_curl_bin_path = "curl.exe"
```

Save `https://devdocs.io/docs.json` to `%LOCALAPPDATA%\nvim-data\devdocs\`, as `registery.json`.

Save `...` to `%LOCALAPPDATA%\nvim-data\devdocs\docs`

↪ [:DevdocsFetch raises "nvim-devdocs: Error when fetching registery, exit code: 2"](https://github.com/luckasRanarison/nvim-devdocs/issues/31)  
↪ [Cannot install cpp documentation](https://github.com/luckasRanarison/nvim-devdocs/issues/71)

### [telescope.nvim](https://github.com/nvim-telescope/telescope.nvim)

↪ [How to change telescope theme](https://github.com/LazyVim/LazyVim/discussions/1127)

### [rime-ls](https://github.com/wlh320/rime-ls)

1. Get `Source code` from [rime-ls - Releases](https://github.com/wlh320/rime-ls/releases).
2. Decompress it to `rime-ls\`.

```sh
cd rime-ls
sudo apt install librime-dev
cargo build --release
ln ~/.cargo/tmp/release/rime_ls ~/.local/bin/rime_ls
```

<!-- --8<-- [start:ubuntu-22-arm] -->
```sh
git clone --depth=1 https://github.com/wlh320/rime-ls
cd rime-ls
rustup target add aarch64-unknown-linux-gnu
cargo build --target aarch64-unknown-linux-gnu --release
```
<!-- --8<-- [end:ubuntu-22-arm] -->

### [cmp-lsp-rimels](https://github.com/liubianshi/cmp-lsp-rimels)

↪ [莫名奇妙的参数类型错误](https://github.com/liubianshi/cmp-lsp-rimels/issues/1)

### [NVIM-RSS](https://github.com/EMPAT94/nvim-rss)

```sh
pkg install sqlite
```

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