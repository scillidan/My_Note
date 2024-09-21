## [neofetch](https://github.com/dylanaraps/neofetch)

```sh
pkg install neofetch
```

```sh
neofetch
```

## [chezmoi](https://www.chezmoi.io)

```sh
pkg install chezmoi
```

```sh
chezmoi init
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
chezmoi init https://github.com/<user>/dotfiles.git
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

## [sdcv](https://github.com/Dushistov/sdcv)

```sh
pkg install sdcv
```

1. Get [ecdict-stardict-28.zip](https://github.com/skywind3000/ECDICT/releases) form [ECDICT](https://github.com/skywind3000/ECDICT).
2. Depress it into `/storage/emulated/0/Download/sdcv/`

```sh
vim /storage/emulated/0/Download/sdcv/stardict-ecdict-2.4.2/stardict-ecdict-2.4.2.ifo
```

```
bookname=ecdict
```

```sh
sdcv <word>
```

↪ [A command line dictionary.](https://nchrs.xyz/stardict.html)

## [Newsboat](https://github.com/newsboat/newsboat)

```sh
pacman -S newsboat
pkg install newsboat
```

```sh
vim ~/.newsboat/urls
```

```
<Url1>
<Url2>
...
```

```sh
mkdir ~/.config/newsboat
vim ~/.config/newsboat/config
```

```sh
include /usr/share/doc/newsboat/contrib/colorschemes/plain
include /data/data/com.termux/files/usr/share/doc/newsboat/contrib/colorschemes/plain
```

```sh
vim ~/.config/newsboat/urls
```

```
https://hnrss.org/newest
...
```

```sh
newsboat
```

↪ [ArchWiki - Newsboat](https://wiki.archlinux.org/title/Newsboat)

## [cmus](https://cmus.github.io/)

```sh
pkg install cmus
```

```sh
cmus
:a storage/Download
```

↪ [A command line music player.](https://nchrs.xyz/cmus.html)  
↪ [How can I create a playlist and add songs to it in cmus?](https://unix.stackexchange.com/questions/593727/how-can-i-create-a-playlist-and-add-songs-to-it-in-cmus)

## [tldr](https://github.com/tldr-pages/tldr)

```sh
tldr -c
```

```sh
mklink /J `C:/Users/<User>/.cache/tldr/pages.en` `C:/Users/<User>/AppData/Roaming/tldr/pages.en`
```

## [broot](https://dystroy.org/broot)

↪ [edit a text file](https://dystroy.org/broot/file-operations/#edit-a-text-file)  
↪ [Launching movie playback via "am start"](https://stackoverflow.com/questions/8207548/launching-movie-playback-via-am-start)

## [asciinema](https://github.com/asciinema/asciinema)

```sh
pkg install asciinema
```

↪ [Recording & Sharing Terminal Sessions](https://weblog.masukomi.org/2022/10/11/recording_and_sharing_terminal_sessions/)

## [marker](https://github.com/VikParuchuri/marker)

1. Get `Ghostscript 10.* for Windows (64 bit) form [ghostscript - Downloads](https://ghostscript.com/releases/gsdnld.html)
2. Get `tesseract-ocr-w64-setup-5.*.exe` from [Tesseract at UB Mannheim](https://github.com/UB-Mannheim/tesseract/wiki)

↪ [marker - install_ocrmypdf.md](https://github.com/VikParuchuri/marker/blob/master/docs/install_ocrmypdf.md)

## [syncabook](https://github.com/r4victor/syncabook)

Full → Language(Chinese) → Upload Files → VAD(silero-vad-skip-gaps) → Initial Prompt(对于普通话句子，以中文简体输出) → Diarization - Speakers(), Min Speakers(1), Max Speakers() → Submit

```sh
git clone https://github.com/r4victor/syncabook
cd syncabook
pvthon37 -m venv venv
venv\Scripts\activate.bat
git clone afaligner https://github.com/r4victor/afaligner _afaligner
cd _afaligner
pip install -e .
edit setup.py
cd ..
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

↪ 0 [Installing and using Aeneas](https://lingtran.net/Installing-and-using-Aeneas)

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

```sh
av1an -i %1 ^
	-v "--cpu-used=3 --end-usage=q --cq-level=30 --threads=8" ^
	-w 10 ^
	--target-quality 95 ^
	-a "-c:a libopus -b:a 192k -ac 2" -l _log_%1 -o _%1"
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

## [starfetch](https://github.com/Haruno19/starfetch)

```sh
git clone https://github.com/Haruno19/starfetch
cd starfetch/res/constellations
```

```sh
git clone https://github.com/K1ngst0m/starfetch
cd starfetch
make
./starfetch.exe -r
```

Or:

Install and use MSYS2.

```sh
git clone https://github.com/CoderCharmander/starfetch
cargo build
cd target/debug
starfetch.exe -d
starfetch.exe -l
```