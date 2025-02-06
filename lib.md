## [Python](https://www.python.org/)

↪ [How to Install Python 3.9 on Ubuntu 22.04](https://vegastack.com/tutorials/how-to-install-python-3-9-on-ubuntu-22-04/)

```sh
python -m pip install -e .
python -m pip install build twine
python setup.py sdist bdist_wheel
python -m build
```

↪ [How to Publish an Open-Source Python Package to PyPI](https://realpython.com/pypi-publish-python-package/)

## [uv](https://github.com/astral-sh/uv)

<!-- --8<-- [start:windows10] -->
```sh
uv python list
uv python install <cpython-*-windows-x86_64-none>
uv python pin cpython-*-windows-x86_64-none
```

```sh
uv venv --python cpython-*-windows-x86_64-none
.venv\Scripts\activate.bat
uv pip install -e .
```
<!-- --8<-- [end:windows10] -->

<!-- --8<-- [start:ubuntu-24-arm] -->
```sh
wget $(curl -s https://api.github.com/repos/astral-sh/uv/releases/latest | grep 'browser_download_url.*uv-aarch64-unknown-linux-gnu.tar.gz' | cut -d '"' -f 4)
sha256sum -c uv-aarch64-unknown-linux-gnu.tar.gz.sha256
tar -xzf uv-aarch64-unknown-linux-gnu.tar.gz -C uv
chmod +x uv-aarch64-unknown-linux-gnu
mv uv-aarch64-unknown-linux-gnu/* .local/bin/
```

↪ [Installing uv](https://docs.astral.sh/uv/getting-started/installation/)
<!-- --8<-- [end:ubuntu-24-arm] -->

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

## [NPM](https://www.npmjs.com/)

```sh
npm login
npm init
npm publish
# npm version patch
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
nvm use lts
nvm install <version>
nvm use <version>
```

## [Jupyter](https://github.com/jupyter/jupyter)

```sh
pip install --user ipykernel
ipython kernel install
jupyter-lab
```

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

## [gvm](https://github.com/olimpias/gvm)

<!-- --8<-- [start:windows10] -->
1. Get `gvm.windows.amd64.exe.zip` from [Releases](https://github.com/olimpias/gvm/releases).
2. Decompress it to `gvm\`.

Get versions list from [All releases](https://go.dev/dl/).

```sh
gvm dl 1.21.0
gvm use 1.21.0
```
<!-- --8<-- [end:windows10] -->

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

Add `lua51\bin` into `PATH`.

## [GCC](https://gcc.gnu.org/)

↪ [How to Install GCC Compiler on Ubuntu](https://phoenixnap.com/kb/install-gcc-ubuntu)

## [LLVM](https://llvm.org/)

Get `clang+llvm-*-x86_64-pc-windows-msvc.tar.xz` from [Releases](https://github.com/llvm/llvm-project/releases).

## [lxml](https://lxml.de/)

↪ [[Bug]: Lxml](https://github.com/termux/termux-packages/issues/18552)
