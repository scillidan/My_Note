## [Python](https://www.python.org/)

↪ [How to Install Python 3.9 on Ubuntu 22.04](https://vegastack.com/tutorials/how-to-install-python-3-9-on-ubuntu-22-04/)

```sh
python -m pip install -e .
python -m pip install build twine
python setup.py sdist bdist_wheel
python -m build
```

↪ [How to Publish an Open-Source Python Package to PyPI](https://realpython.com/pypi-publish-python-package/)

## [pipx](https://github.com/pypa/pipx)

```sh
python -m pip install --user pipx
pipx ensurepath
```

<!-- --8<-- [start:arch-linux] -->
```sh
sudo pacman -S python-pipx
```
<!-- --8<-- [end:arch-linux] -->

## [pyenv for Windows](https://github.com/pyenv-win/pyenv-win)

<!-- --8<-- [start:windows10] -->
```sh
git clone --depth=1 https://github.com/pyenv-win/pyenv-win ~/.pyenv
```

↪ [Installation](https://github.com/pyenv-win/pyenv-win/blob/master/docs/installation.md#git-commands)  
↪ [Add System Settings](https://github.com/pyenv-win/pyenv-win/blob/master/docs/installation.md#add-system-settings)

```sh
pyenv install -l | findstr 3.7
pyenv install -l | findstr 3.11
pyenv install 3.7.9-win32
pyenv install 3.11.9
pyenv shell <version>
```
<!-- --8<-- [end:windows10] -->

## [pyenv](https://github.com/pyenv/pyenv)

<!-- --8<-- [start:termux] -->
↪ [Build older python package - 3.9](https://github.com/termux/termux-packages/discussions/9498)
<!-- --8<-- [end:termux] -->

<!-- --8<-- [start:arch-linux] -->
```sh
sudo pacman -S pyenv
```
<!-- --8<-- [end:arch-linux] -->

<!-- --8<-- [start:ubuntu-22-arm] -->
```sh
sudo apt update
sudo apt-get install -y build-essential curl libbz2-dev libffi-dev liblzma-dev libncurses5-dev libncursesw5-dev libreadline-dev libsqlite3-dev libssl-dev libxml2-dev libxmlsec1-dev llvm make tk-dev wget xz-utils zlib1g-dev
```

↪ [ubuntu에서 pyenv 설치하기](https://jinmay.github.io/2019/03/16/linux/ubuntu-install-pyenv-1/)  
↪ [pyenv install: 3.x BUILD FAILED (Ubuntu 20.04 using python-build 20180424)](https://stackoverflow.com/questions/67807596/pyenv-install-3-x-build-failed-ubuntu-20-04-using-python-build-20180424)
<!-- --8<-- [end:ubuntu-22-arm] -->

<!-- --8<-- [start:ubuntu-24-arm] -->
```sh
sudo apt install -y build-essential libssl-dev libbz2-dev libreadline-dev libsqlite3-dev libffi-dev zlib1g-dev liblzma-dev tk-dev
```
<!-- --8<-- [end:ubuntu-24-arm] -->

```sh
git clone --depth=1 https://github.com/pyenv/pyenv.git ~/.pyenv
```

```sh
vim ~/.zshrc
```

```
export PYENV_ROOT="$HOME/.pyenv"
[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
```

```sh
source ~/.zshrc
pyenv install 3.10.11
```

Or install from files:

```sh
mkdir ~/.pyenv/cache
cd ~/.pyenv/cache
wget https://www.python.org/ftp/python/3.10.11/Python-3.10.11.tar.xz
pyenv install 3.10.11
```

```sh
pyenv global 3.10.11
pyenv local 3.10.11
```

## [pyenv-virtualenv](https://github.com/pyenv/pyenv-virtualenv)

```sh
git clone --depth=1 https://github.com/yyuu/pyenv-virtualenv.git ~/.pyenv/plugins/pyenv-virtualenv
vim ~/.zshrc
```

```
eval "$(pyenv virtualenv-init -)"
```

```sh
source ~/.zshrc
pyenv virtualenv 3.9.13 <venv>
cd <Project>
pyenv local <venv>
```

↪ [ubuntu에서 pyenv 설치하기](https://jinmay.github.io/2019/03/16/linux/ubuntu-install-pyenv-1/)

## [virtualenv](https://github.com/pypa/virtualenv)

```sh
pyenv exec pip install virtualenv
virtualenv <venv>
source <venv>/bin/activate
```

## [NPM](https://www.npmjs.com/)

```sh
npm login
npm init
npm publish
# npm version patch
```

## [nvm](https://github.com/nvm-sh/nvm)

```sh
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/refs/heads/master/install.sh | bash
vim .zshrc
```

```
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
```

```sh
source ~/.zshrc
nvm ls-remote
nvm install Gallium
nvm install Hydrogen
nvm use <version>
```

## [NVM for Windows](https://github.com/coreybutler/nvm-windows)

1. Get `nvm-noinstall.zip` from [Releases](https://github.com/coreybutler/nvm-windows/releases).
2. Decompress it to `nvm\`.
3. Add `nvm` into `PATH`.

Add these into `User Variables`:

```
NVM_HOME=C:\Users\User\.nvm
NVM_SYMLINK=C:\Program Files\nodejs
SYS_ARCH=64
```

Edit `.nvm\settings.txt`:

```
node_mirror: https://npmmirror.com/mirrors/node/
```

```sh
nvm list available
nvm install lts
nvm install <version>
nvm use <version>
```

## [pnpm](https://pnpm.io/)

```pwsh
Invoke-WebRequest https://get.pnpm.io/install.ps1 -UseBasicParsing | Invoke-Expression
```

<!-- --8<-- [start:arch-linux] -->
```sh
sudo pacman -S pnpm
```
<!-- --8<-- [end:arch-linux] -->

```sh
pnpm install -g <pkg>
```

## [Jupyter](https://github.com/jupyter/jupyter)

```sh
pip install --user ipykernel
ipython kernel install
jupyter-lab
```

## [RVM](https://github.com/rvm/rvm)

<!-- --8<-- [start:arch-linux] -->
```sh
yay -S rvm
```
<!-- --8<-- [end:arch-linux] -->

## [rbenv for Windows](https://github.com/RubyMetric/rbenv-for-windows)

```pwsh
$env:HOME = "C:\Users\<User>"
$env:RBENV_ROOT = "$env:HOME\Lib\rbenv"
iwr -useb "https://github.com/RubyMetric/rbenv-for-windows/raw/main/tool/install.ps1" | iex
$env:RBENV_USE_MIRROR = "CN"
& "$ENV:RBENV_ROOT\rbenv\bin\rbenv.ps1" init
```

1. Set variable `RBENV_ROOT=C:\Users\<User>\Lib\rbenv`.
2. Add `%RBENV_ROOT%\rbenv\bin`, `%RBENV_ROOT%\shims` into `PATH`.

## [MSYS2](https://www.msys2.org/)

↪ [Install gcc compiler on Windows with MSYS2 for C/C++](https://www.devdungeon.com/content/install-gcc-compiler-windows-msys2-cc)  
↪ [Using CMake in MSYS2](https://www.msys2.org/docs/cmake/)

↪ [How to Install GCC in Termux for C++ Programming](https://www.samgalope.dev/2024/09/03/how-to-install-gcc-in-termux-for-c-programming/)

```sh
pacman -Syyu
pacman -S mingw-w64-ucrt-x86_64-gcc
pacman -S mingw-w64-x86_64-cargo-c mingw-w64-x86_64-protobuf
cargo install atuin
pacman -S mingw-w64-ucrt-x86_64-pkg-config
```

## [Cygwin](https://www.cygwin.com/) (Cache)

```sh
apt-cyg install git vim zsh
cd /cygdrive/c/cygwin64/home/User
source .zshrc
```

## [Rust](https://rustup.rs/)

<!-- --8<-- [start:arch-linux] -->
```sh
curl https://sh.rustup.rs -sSf | sh
rustup default stable
```
<!-- --8<-- [end:arch-linux] -->

## [Cargo](https://doc.rust-lang.org/cargo/)

<!-- --8<-- [start:ubuntu-22-arm] -->
```sh
sudo apt install rustc cargo
```

↪ [How to Install Rust on Ubuntu](https://phoenixnap.com/kb/install-rust-ubuntu)
<!-- --8<-- [end:ubuntu-22-arm] -->

<!-- --8<-- [start:ubuntu-24-arm] -->
```sh
sudo apt install rustup
rustup default stable
```
<!-- --8<-- [end:ubuntu-24-arm] -->

## [goenv](https://github.com/go-nv/goenv)

```sh
git clone https://github.com/go-nv/goenv.git ~/.goenv
```

```sh
sudo vim ~/.zshrc
```

```
export GOENV_ROOT="$HOME/.goenv"
export PATH="$GOENV_ROOT/bin:$PATH"
eval "$(goenv init -)"
```

```sh
source ~/.zshrc
```

```sh
goenv install 1.22.0
```

```sh
wget https://go.dev/dl/go1.22.0.linux-arm64.tar.gz
mkdir -p ~/.goenv/cache
mv go1.22.0.linux-arm64.tar.gz ~/.goenv/cache/
goenv install 1.22.0
go version
```

```sh
go env
go env -w GO111MODULE=on
go env -w GOPROXY=https://goproxy.cn,direct
```

## [Lua](https://www.lua.org/)

<!-- --8<-- [start:windows10] -->
```sh
git clone https://github.com/Pharap/CompilingLua
cd CompilingLua
vcvarsall.bat
Compile.bat
```
<!-- --8<-- [end:windows10] -->

```sh
pkg install lua53 luarocks
pkg install clang
luarocks install luaexpat
```

## [LuaJIT](https://luajit.org/)

```sh
git clone https://luajit.org/git/luajit.git
cd luagit
git checkout v2.1
```

In `MSYS2`:

```sh
pacman -S mingw-w64-x86_64-gcc mingw-w64-x86_64-make
make CFLAGS=-DLUAJIT_ENABLE_LUA52COMPAT TARGET_LDFLAGS=-mwindows
```

↪ [How to build windowless LuaJIT for Windows](https://gist.github.com/Egor-Skriptunoff/22bf55c1abe44d7825605e132e48c084)

## [hererocks](https://github.com/mpeterv/hererocks)

```sh
pipx install hererocks
hererocks lua51 -l5.1 -rlatest
source lua51/bin/activate
luarocks install luacheck
deactivate-lua
```

Add `lua51\bin` into `PATH`.

## [GCC](https://gcc.gnu.org/)

↪ [How to Install GCC Compiler on Ubuntu](https://phoenixnap.com/kb/install-gcc-ubuntu)

## [LLVM](https://llvm.org/)

Get `clang+llvm-*-x86_64-pc-windows-msvc.tar.xz` from [Releases](https://github.com/llvm/llvm-project/releases).

## [lxml](https://lxml.de/)

↪ [[Bug]: Lxml](https://github.com/termux/termux-packages/issues/18552)
