## [Python](https://www.python.org/)

↪ [How to Install Python 3.9 on Ubuntu 22.04](https://vegastack.com/tutorials/how-to-install-python-3-9-on-ubuntu-22-04/)

## [pyenv](https://github.com/pyenv/pyenv)

<!-- --8<-- [start:ubuntu-22-arm] -->
```sh
sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev
```

```sh
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
```

```sh
vim ~/.zshrc
```

```
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
```

```sh
pyenv install 3.9.13
```

↪ [ubuntu에서 pyenv 설치하기](https://jinmay.github.io/2019/03/16/linux/ubuntu-install-pyenv-1/)

```sh
sudo apt update
sudo apt install build-essential curl libbz2-dev libffi-dev liblzma-dev libncursesw5-dev libreadline-dev libsqlite3-dev libssl-dev libxml2-dev libxmlsec1-dev llvm make tk-dev wget xz-utils zlib1g-dev
```

```sh
pyenv install 3.9.13
pyenv global 3.9.13
```

↪ [pyenv install: 3.x BUILD FAILED (Ubuntu 20.04 using python-build 20180424)](https://stackoverflow.com/questions/67807596/pyenv-install-3-x-build-failed-ubuntu-20-04-using-python-build-20180424)
<!-- --8<-- [end:ubuntu-22-arm] -->

<!-- --8<-- [start:termux] -->
↪ [Build older python package - 3.9](https://github.com/termux/termux-packages/discussions/9498)
<!-- --8<-- [end:termux] -->

## [Jupyter](https://github.com/jupyter/jupyter)

```sh
pip install --user ipykernel
ipython kernel install
jupyter-lab
```

## [MSYS2](https://www.msys2.org/)

↪ [Install gcc compiler on Windows with MSYS2 for C/C++](https://www.devdungeon.com/content/install-gcc-compiler-windows-msys2-cc)  
↪ [Using CMake in MSYS2](https://www.msys2.org/docs/cmake/)

↪ [How to Install GCC in Termux for C++ Programming](https://www.samgalope.dev/2024/09/03/how-to-install-gcc-in-termux-for-c-programming/)

## [Cargo](https://doc.rust-lang.org/cargo/)

<!-- --8<-- [start:ubuntu-22-arm] -->
```sh
sudo apt install rustc cargo
```

↪ [How to Install Rust on Ubuntu](https://phoenixnap.com/kb/install-rust-ubuntu)
<!-- --8<-- [end:ubuntu-22-arm] -->

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

## [GCC](https://gcc.gnu.org/)

↪ [How to Install GCC Compiler on Ubuntu](https://phoenixnap.com/kb/install-gcc-ubuntu)

## [LLVM](https://llvm.org/)

Get `clang+llvm-*-x86_64-pc-windows-msvc.tar.xz` from [LLVM - Releases](https://github.com/llvm/llvm-project/releases).

## [lxml](https://lxml.de/)

↪ [[Bug]: Lxml](https://github.com/termux/termux-packages/issues/18552)