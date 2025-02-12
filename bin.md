## [git](https://git-scm.com/)

Set:

```sh
git config --global user.email "your_email"
git config --global user.name "your_name"
```

Undo and re-push:

```sh
git fetch --all
git reset --hard <commit-hash>
# git reset --hard HEAD~1
git push --force origin <branch>
````

## [chezmoi](https://www.chezmoi.io)

<!-- --8<-- [start:ubuntu-server-arm-22] -->
Get `chezmoi_*_linux_arm64.deb` from [chezmoi - Releases](https://github.com/twpayne/chezmoi).

```sh
sudo dpkg -i chezmoi_*_linux_arm64.deb
```

<!-- --8<-- [end:ubuntu-server-arm-22] -->

```sh
chezmoi init
vim ~/.local/share/chezmoi/.chezmoiignore
```

```
**/zjframes.wasm # Example
**/zjstatus.wasm
lazy-lock.json
```

↪ [Chezmoi: ignore files and subdirectories](https://stackoverflow.com/questions/75519055/chezmoi-ignore-files-and-subdirectories)

```sh
chezmoi add <files>
chezmoi diff
chezmoi apply -v
chezmoi cd
git add .
git commit -m "<commit>"
```

```sh
git remote add origin https://github.com/<user>/dotfiles.git
git branch -M main
git push -u origin main
```

On another PC:

```sh
chezmoi init https://github.com/<user>/<dotfiles>
chezmoi diff
chezmoi apply -v
```

Or:

```sh
chezmoi edit <file>
```

Or:

```sh
chezmoi merge <file>
```

```sh
chezmoi update -v
```

For new PC:

```sh
chezmoi init --apply https://github.com/<user>/dotfiles.git
```

↪ [Dotfiles with Chezmoi](https://blog.lazkani.io/posts/dotfiles-with-chezmoi/)

## [Dolt](https://www.dolthub.com/) (Cache)

1. Get `dolt-windows-amd64.zip` from [Dolt - Releases](https://github.com/dolthub/dolt/releases).
2. Decompress it to `dolt\`.

<!-- --8<-- [start:ubuntu-server-arm-22] -->
Get `dolt-linux-arm64.tar.gz` from [Dolt - Releases](https://github.com/dolthub/dolt/releases).

```sh
tar -xzvf dolt-linux-arm64.tar.gz
chmod +x dolt-linux-arm64/bin/dolt
ln -s ~/dolt-linux-arm64/bin/dolt ~/.local/bin/dolt
```
<!-- --8<-- [end:ubuntu-server-arm-22] -->

```sh
dolt config --global --add user.email "you@example.com"
dolt config --global --add user.name "your_name"
dolt init
```

## [Ansible](https://www.ansible.com/)

↪ [使用 Ansible 管理 Linux 系统的配置文件](https://sspai.com/post/91932)

## [portable-python-maker](https://github.com/dreamsavior/portable-python-maker) (BUG)

```sh
git clone https://github.com/dreamsavior/portable-python-maker
cd portable-python-maker
```

For example:

```sh
pwsh.exe portablepy.ps1 -source "https://www.python.org/ftp/python/3.7.0/python-3.7.0-embed-win32.zip" -destination "C:\Users\User\Lib\python-3.7-32"
pwsh.exe portablepy.ps1 -source "https://www.python.org/ftp/python/3.9.13/python-3.9.13-embed-amd64.zip" -destination "C:\Users\User\Lib\python-3.9"
```

If it fails, run again.

## [PyGlossary](https://github.com/ilius/pyglossary)

```sh
pip install pyglossary
pip install lxml beautifulsoup4
```

For `DICT.org`:

```sh
pyglossary <stardict.ifo> <dictionary.index> --write-options=dictzip=true --remove-html-all
```

```sh
pyglossary <mdict.mdx> <mdict.txt>
pyglossary <mdict.txt> <dictionary.index> --write-options=dictzip=true
```

## [MDict Tool](https://github.com/liuyug/mdict-utils) (Cache)

```sh
mdict.exe -x "汉语大词典(简体精排).mdx"  -d ./mdx
```

Find all `` → 
Replace `\n`1`` → `\t`

```sh
pyglossary <mdict.txt> <dictionary.index> --write-options=dictzip=true
```

## [marker](https://github.com/VikParuchuri/marker)

1. Get `Ghostscript 10.* for Windows (64 bit) form [ghostscript - Downloads](https://ghostscript.com/releases/gsdnld.html)
2. Get `tesseract-ocr-w64-setup-5.*.exe` from [Tesseract at UB Mannheim](https://github.com/UB-Mannheim/tesseract/wiki)

```sh
python.exe -m venv venv
venv\Scripts\activate.bat
pip install torch  --index-url https://download.pytorch.org/whl/cu121
pip install ocrmypdf
pip install -e .
```

Use with command:

```sh
marker_single <file.pdf> <OutputFolder> --batch_multiplier 2 --max_pages 10 
```

With GUI:

```sh
pip install streamlit
marker_gui
```

↪ [marker - install_ocrmypdf.md](https://github.com/VikParuchuri/marker/blob/master/docs/install_ocrmypdf.md)  
↪ [PermissionError: [Errno 13] Permission denied: 'C:\\Users\\schor\\AppData\\Local\\Temp\\tmpoaply4el.pdf'](https://github.com/VikParuchuri/marker/issues/267)

## [NSZ](https://github.com/nicoboss/nsz)

```sh
python -m venv venv
venv\Scripts\activate.bat
pip install -r requirements-gui.txt 
python nsz.py
```

## [syncabook](https://github.com/r4victor/syncabook) (Cache)

Get `aeneas-win64-setup-*.exe` [Aeneas Tools - Releases](https://github.com/sillsdev/aeneas-installer/releases).

↪ [Installing and using Aeneas](https://lingtran.net/Installing-and-using-Aeneas)

```sh
mkdir syncabook
cd syncabook
pvthon -m venv venv
venv\Scripts\activate.bat
```

```sh
git clone --depth=1 https://github.com/r4victor/afaligner
cd afaligner
pip install -e .
edit setup.py
cd ..
```

```sh
git clone --depth=1 https://github.com/r4victor/syncabook
cd syncabook
pip install beautifulsoup4 lxml numpy aeneas
```

See [Check out this ShareGPT conversation](https://sharegpt.com/c/97thh2m)

```sh
pip install pytest epubcheck
python -m pytest -s tests/
```

```sh
syncabook download_files theurl thebook
```

```sh
syncabook split_text --mode opening --p theindex thebook\text.txt thebook\plaintext
syncabook split_text --mode delimeter --p theindex thebook\text.txt thebook\plaintext
syncabook split_text --mode equal --n 2 thebook\text.txt thebook\plaintext
```

```sh
syncabook to_xhtml thebook/plaintext/ thebook/sync_text/
syncabook sync thebook/
```

```sh
syncabook create thebook
```

```sh
cd _synclibrivox\books\_little_prince\ // Cache
syncabook.exe split_text --m opening --p 第一章 text.txt plaintext
iconv -f gbk -t utf-8 plaintext\1.txt > plaintext\_1.txt && trash plaintext\1.txt && move plaintext\_1.txt plaintext\1.txt
syncabook.exe to_xhtml plaintext sync_text\
iconv -f gbk -t utf-8 sync_text\1.xhtml > sync_text\_1.xhtml && trash sync_text\1.xhtml && move sync_text\_1.xhtml  sync_text\1.xhtml
syncabook sync _synclibrivox\books\_little_prince
syncabook create thebook
```

... calibre-web → Apphabetical Books → ALL → `The Black Cat` → Import (EPUB)
My Books → `The Black Cat` → ButtonOfPlayAudio

↪ [Audio Ebook ID Inserter](https://github.com/Audun97/audio-ebook-id-inserter)

## syncabook-like (TBD)

↪ [Package aeneas - language](https://www.readbeyond.it/aeneas/docs/language.html)

## [Av1an](https://github.com/master-of-zen/Av1an)

Install `vapoursynth`, `vmaf`.

```sh
python vsrepo.py update
python vsrepo.py install lsmas ffms2
```

Install `nasm`, `emscripten`.

```sh
emsdk install latest
emsdk activate latest
```

```sh
venv/Scripts/streamlit.exe run web_demo2.py
```

## [spongebob-cli](https://github.com/trakBan/spongebob-cli)

```sh
git clone https://github.com/trakBan/spongebob-cli
cd spongebob-cli
python -m venv venv
venv/Scripts/activate.bat
python setup.py install
python spongebob-cli
```

## [Warcraft Font Merger](https://github.com/nowar-fonts/Warcraft-Font-Merger)

1. Get `WarFontMerger-SC-*-windows-x64.7z` from [Warcraft-Font-Merger - Releases](https://github.com/nowar-fonts/Warcraft-Font-Merger/releases).
2. Decompress and rename it to `Warcraft-Font-Merger\`.
3. Create `fonts\`.
4. Copy fonts into `fonts\`.
5. Run `合并补全.bat fonts/<font1> fonts/<font2>`.
6. Rename `out.ttf`.

## [FFmpeg](https://www.ffmpeg.org/)

1. Get `ffmpeg-master-latest-win64-gpl-shared.zip` from [FFmpeg Static Auto-Builds - Releases](https://github.com/BtbN/FFmpeg-Builds/releases).
2. Add `ffmpeg-gpl-shared\bin` into PATH.

## [ShellGPT](https://github.com/TheR1D/shell_gpt) (Cache)

```sh
pip install shell-gpt
```

## [Jackett Search Cli](https://github.com/rodrigo-sys/jsc)

```sh
sudo apt install jq fzf
git clone depth=1 https://github.com/rodrigo-sys/jsc
cd jsc
chmod +x jsc
```

1. jackett → Open Web UI → Copy API Key.
2. Edit `jsc`.

```
api_key='<api_key>'
url="http://<jackett_host>:9117/api/v2.0/indexers/all/results?apikey=$api_key"
```

```sh
jsc -t nyaa-si -s "chainsaw man"
jsc -t nyaa-si -s "chainsaw man" | xargs -n 1 -r aria2
```

## [MinIO Client](https://min.io/docs/minio/linux/reference/minio-mc.html)

<!-- --8<-- [start:ubuntu-server-arm-22] -->
```sh
wget https://dl.min.io/client/mc/release/linux-arm64/mc
chmod +x mc
mv mc ~/.local/bin/
```

```sh
mkdir -p ~/minio_recursive
mc alias set <database_name> http://<your_host>:9000 <MINIO_ROOT_USER> <MINIO_ROOT_PASSWORD>
mc list <database_name>
mc cp --recursive <database_name>/ ~/minio_recursive/
```
<!-- --8<-- [end:ubuntu-server-arm-22] -->

## [BeatPrints](https://github.com/TrueMyst/BeatPrints)

1. Visit [Spotify Developer Dashboard](https://developer.spotify.com/dashboard/).
2. Create app `BeatPrints`, add `http://localhost` on `Redirect URIs (required)`.
3. Go `Settings`, get `Client ID`, `Client secret`.
4. Add `SPOTIFY_CLIENT_ID`, `SPOTIFY_CLIENT_SECRET` into PATH.

```sh
git clone --depth=1 https://github.com/TrueMyst/BeatPrints
cd BeatPrints
uv.exe venv --python cpython-3.10.11-windows-x86_64-none
.venv\Scripts\activate.bat
uv pip install -e .
# uv pip install python-dotenv
```

```sh
beatprints
```

Optional:

```sh
mkdir C:\Users\User\AppData\Roaming\BeatPrints
subl C:\Users\User\AppData\Roaming\BeatPrints\config.toml
```

```toml
[general]
search_limit = 7
output_directory = "C:\\Users\\User\\Downloads"

[credentials]
client_id = "SPOTIFY_CLIENT_ID"
client_secret = "SPOTIFY_CLIENT_SECRET"
```

↪ [CLI Setup](https://beatprints.readthedocs.io/en/latest/guidebook/cli.html)

## [SeaGOAT](https://github.com/kantord/SeaGOAT) (Cache)

```sh
uvpipx install seagoat
seagoat-server start <your_repo>
```

## [mkcert](https://github.com/FiloSottile/mkcert)

```sh
sudo apt install libnss3-tools
mkcert -install
mkcert example.com "*.example.com" example.test localhost
```

## [shot-scraper](https://github.com/simonw/shot-scraper) (Cache)

```sh
pipx install shot-scraper playwright
playwright install
shot-scraper <url>
```

## [MarkItDown](https://github.com/microsoft/markitdown)

```sh
git clone --depth=1 https://github.com/microsoft/markitdown
cd markitdown
uv venv
.venv\Scripts\activate.bat
uv pip install -e packages/markitdown
```