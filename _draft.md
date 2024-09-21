## Directory Opus

Open With:

format  | opt
:-      | :-
`.jpg`  | JPEGView-fork, IrfanView
`.psd`  | IrfanView
`.svg`  | qView
`.gif`  | mpv
`.epub` | ePubViewer
`.pdf`  | PDF.js

## Scoop

Windows Registry:

package      | register
:-           | :-
sublime-text | `install-context.reg`
everything   | `install-context.reg`
lockhunter   | `install-context.reg`
vim (gvim)   | `install-context.reg`
zlib         | `register.reg`
git          | `install-file-associations.reg`

Package Version:

```
nodejs18
pnpm
fnm
python39
openjdk11
php72
postgresql14
```

Setup File:

package  | file
:-       | :-
vb-cable | `VBCABLE_Setup_x64.exe`

## Komga

```
如何编目
需要引入书籍封装的概念
倾向于在软件中处理跨页
```

Tools:

- Directory_Opus
- Xnconvert
- FastStone
- Advanced_Renamer
- ki-cli-hyphen
- Mkdirs
- To_CBZ
- Komga_Cover_Extractor

Batch:

```sh
for /d %%X in (*) do arenc.exe -e "v01.aren" -t folders -p . -m rename
for /d %%X in (*) do arenc.exe -e "001.aren" -t files -p %%X -m rename
for /d %%X in (*) do cp %%X/001.jpg %%X/cover.jpg
for /d %%X in (*) do python to-cbz/to_cbz.py %%X
python komga-cover-extractor/komga_cover_extractor.py -c "True" -cq "70" -p .
```

```sh
cook c 1001-1188 | sd c1 "\55 c" > _.md && mkdirs _.md && trash _.md
```

## PM2

我搜到了一段描述，去了解`yarn dev`和`yarn start`的区别：

> **TL;DR:** In Next.js, `next dev` is used to run the app in development mode. On the other hand, `next start` is used to run the app in production mode, but requires `next build` to be run first to generate an optimized production build.
>
> （机翻）太长不看：在Next.js中，`Next dev`命令用于在开发模式下运行应用程序。另一方面，`Next start`命令用于在生产模式下运行应用程序，但需要首先运行`Next Build`命令以生成优化的生产版本。

↪ [What's the difference between npm run dev and npm run start in Next.js?](https://stackoverflow.com/questions/69400243/whats-the-difference-between-npm-run-dev-and-npm-run-start-in-next-js)

Development和Production的区别：

> The development build is used - as the name suggests - for development reasons. You have Source Maps, debugging and often times hot reloading ability in those builds.
> The production build, on the other hand, runs in production mode which means this is the code running on your client's machine. The production build runs uglify and builds your source files into one or multiple minimized files. It also extracts CSS and images and of course any other sources you're loading with Webpack. There's also no hot reloading included. Source Maps might be included as separate files depending on your webpack `devtool` [settings](https://webpack.js.org/configuration/devtool/).
>
> （机翻）使用开发构建--顾名思义--是出于开发原因。在这些版本中，您拥有源代码映射、调试和经常热重新加载的能力。
  另一方面，生产构建在生产模式下运行，这意味着这是在您的客户端机器上运行的代码。生产构建运行uglify并将源文件构建到一个或多个最小化文件中。它还提取css和图像，当然还有你用webpack加载的任何其他来源。此外，还不包括热重装。根据您的webpack开发工具设置，源地图可能会作为单独的文件包含在内。

↪ [Difference between production and development build in ReactJS](https://stackoverflow.com/questions/48151128/difference-between-production-and-development-build-in-reactjs)

## Cumaean

Tools:

- CUETools
- XMedia_Recode
- MP3TAG
- renamer
- Advanced_Renamer
- AudioShell
- TagScanner
- Lidarr

## PDF

Tools:

- [mkcert](https://github.com/FiloSottile/mkcert)：Golang包，用来生成自信任的为PCCS（Public-Key Cryptography Standards）\#12格式、扩展名为`.p12`或`.pfx`的证书文件证书
- [BatchPDFSign](https://github.com/jmarxuach/BatchPDFSign)：Java应用，使用`.pfx`给`.pdf`写入自签名数字ID，进行数字签名（Digital Signature）
- [markpdf](https://github.com/ajaxray/markpdf)：Golang包，给`.pdf`的每页添加水印。这里用来铺一层很浅的装饰底纹

## PDF.js

Tools:

- Pdfalyzer
- Sublime_Text
  - Insert_Nums
- pdf-toc

Attribution:

The [pinouts_v0.3_toc.pdf](https://github.com/scillidan/Cos_Cache/blob/master/pdf/pinouts_v0.3_toc.pdf) edit from [The Pinouts Book](https://pinouts.org) by [NODE](https://n-o-d-e.net/index.html) & Baptiste / [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).