## Vercel Settings

Some repositoryie, Refer to running on local to edit project's settings, for example:

1. When deploy [Calcutext](https://github.com/jaredreich/calcutext) with [Vercel](https://vercel.com).
2. The Project → Settings → General → Node.js Version → `16.x`
3. Deployment → More → Redeploy

And:

1. When deploy [QR code designer](https://github.com/kochrt/qr-designer) with [Github Pages](https://pages.github.com/):
2. Visit [source](https://github.com/kochrt/qr-designer) → Fork → Don't select `Copy the main branch only`
3. Fork Repository → Settings → Pages → Build and development
  1. Source → Deploy from a branch
  2. Branch → `gh-pages`, `/(root)`
4. Visit `https://<user>.github.io/qr-designer/`

## [Pic Smaller](https://github.com/joye61/pic-smaller)

![](https://img.shields.io/github/license/joye61/pic-smaller?label=&style=flat-square) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

## [IT-TOOLS](https://github.com/CorentinTh/it-tools)

![](https://img.shields.io/github/license/CorentinTh/it-tools?label=&style=flat-square) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

## [altium.js](https://github.com/gsuberland/altium_js)

![](https://img.shields.io/github/license/gsuberland/altium_js?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/altium_js/main?label=&style=flat-square)](https://github.com/scillidan/altium_js) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

Open `altium_sch.html`.

## [Calcutext](https://github.com/jaredreich/calcutext)

![](https://img.shields.io/github/license/jaredreich/calcutext?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/calcutext/master?label=&style=flat-square)](https://github.com/scillidan/calcutext) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

```sh
nvm install 16.13.2
nvm use 16.13.2
npm install
npm run build
serve -s build -p 4321
```

## [Cheatsheet Generator](https://github.com/nathanlesage/cheatsheet-generator)

![](https://img.shields.io/github/license/nathanlesage/cheatsheet-generator?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/cheatsheet-generator/master?label=&style=flat-square)](https://github.com/scillidan/cheatsheet-generator)

Copy `examples/<the>.config.yml` to `config.yml`

```sh
nvm install 16.20.0
nvm use 16.20.0
npm install
npm run build
```

Open `dist/<the>.htm`.

## [CL Calc](https://github.com/ovk/clcalc)

[![](https://img.shields.io/github/last-commit/scillidan/clcalc/master?label=&style=flat-square)](https://github.com/scillidan/clcalc) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

```sh
npm install
node node_modules/gulp/bin/gulp.js
serve -s dist -p 4321
```

If app take up `4321` port, open `chrome://serviceworker-internals/?devtools` and unregister it.

1. When deploy with [Vercel](https://vercel.com).
2. The Project → Settings → General → Build & Development Settings
  ```
  Build Command `npm run dist`
  Output Directory `dist`
  ```

## [cnvrt](https://github.com/gregermendle/cnvrt)

![](https://img.shields.io/github/license/gregermendle/cnvrt?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/cnvrt/main?label=&style=flat-square)](https://github.com/scillidan/cnvrt)

```sh
pnpm install
pnpm build
pnpm start
```

## [Codi.link](https://github.com/midudev/codi.link)

![](https://img.shields.io/github/license/midudev/codi.link?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/codi.link/main?label=&style=flat-square)](https://github.com/scillidan/codi.link) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

```sh
npm install
npm run build
serve -s dist -p 4321
```

## [DGM.js](https://github.com/dgmjs/dgmjs)

![](https://img.shields.io/github/license/dgmjs/dgmjs?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/dgmjs/main?label=&style=flat-square)](https://github.com/scillidan/dgmjs)

```sh
npm install
npm build
npm run dev
```

## [diceRoller](https://github.com/zombieFox/diceRoller)

![](https://img.shields.io/github/license/zombieFox/diceRoller?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/diceRoller/main?label=&style=flat-square)](https://github.com/scillidan/diceRoller) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

```sh
nvm install 16.20.0
nvm use 16.20.0
npm install
npm run build
npm run start
```

## [Drawflow](https://github.com/jerosoler/Drawflow)

[](https://img.shields.io/github/license/jerosoler/Drawflow?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/Drawflow/main?label=&style=flat-square)](https://github.com/scillidan/Drawflow)

```sh
npm install
npm run build
```

Open `docs/index.html`.

## [SvgPathEditor](https://github.com/Yqnn/svg-path-editor)

![](https://img.shields.io/github/license/Yqnn/svg-path-editor?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/svg-path-editor/master?label=&style=flat-square)](https://github.com/scillidan/svg-path-editor) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

```sh
serve -s . -p 4321
```

## [EPUB Manga Creator](https://github.com/wing-kai/epub-manga-creator)

![](https://img.shields.io/github/license/wing-kai/epub-manga-creator?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/epub-manga-creator/master?label=&style=flat-square)](https://github.com/scillidan/epub-manga-creator) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

```sh
npm install
npm run build
serve -s build -p 4321
```

## [ePubViewer](https://github.com/pgaskin/ePubViewer)

![](https://img.shields.io/github/license/agmmnn/etytree?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/pgaskin/ePubViewer/main?label=&style=flat-square)](https://github.com/scillidan/ePubViewer) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

```sh
serve -s . -p 4321
```

Visit `localhost:4000` or `localhost:4000#book.epub`.

If app take up `4321` port, open `chrome://serviceworker-internals/?devtools` and unregister it.

With PM2:

```sh
pm2 serve . 4321 --name epubvidewer --spa
```

## [etytree](https://github.com/agmmnn/etytree)

![](https://img.shields.io/github/license/agmmnn/etytree?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/etytree/main?label=&style=flat-square)](https://github.com/scillidan/etytree) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

```sh
yarn
yarn build
yarn dev
```

## [Excalidraw](https://github.com/excalidraw/excalidraw)

![](https://img.shields.io/github/license/excalidraw/excalidraw?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/excalidraw/master?label=&style=flat-square)](https://github.com/scillidan/excalidraw)

```sh
yarn
yarn build
yarn start
```

## [ASCIIFlow](https://github.com/lewish/asciiflow)

![](https://img.shields.io/github/license/lewish/asciiflow?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/asciiflow/master?label=&style=flat-square)](https://github.com/scillidan/asciiflow) ![](https://img.shields.io/badge/GitHub%20Pages-121013?logo=github&logoColor=white)

## [Excalith Start Page](https://github.com/excalith/excalith-start-page)

![](https://img.shields.io/github/license/excalith/excalith-start-page?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/excalith-start-page/main?label=&style=flat-square)](https://github.com/scillidan/excalith-start-page) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

With PM2:

```sh
yarn
pm2 start yarn --watch --name "excalith-start-page" -- dev
```

Visit the site:

```sh
config import <config.json>
```

## [Favycon](https://github.com/ruisaraiva19/favycon)

![](https://img.shields.io/github/license/ruisaraiva19/favycon?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/favycon/main?label=&style=flat-square)](https://github.com/scillidan/favycon) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

Edit near line `13` of `.eslintrc.json`:

```json title=".eslintrc.json"
  "rules": {
    "prettier/prettier": ["error", {'endOfLine': 'auto'} ]
```

```sh
yarn install
yarn build
yarn start -- -p 4321
```

## [finetuneas](https://github.com/ozdefir/finetuneas)

![](https://img.shields.io/github/license/ozdefir/finetuneas?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/finetuneas/main?label=&style=flat-square)](https://github.com/scillidan/finetuneas) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

```sh
serve -s . -p 4321
```

## [Flatdraw](https://github.com/diogocapela/flatdraw)

![](https://img.shields.io/github/license/diogocapela/flatdraw?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/flatdraw/main?label=&style=flat-square)](https://github.com/scillidan/flatdraw)

```sh
npm install
npm run build
npm run dev
```

## [Flowchart Fun](https://github.com/tone-row/flowchart-fun)

![](https://img.shields.io/github/license/tone-row/flowchart-fun?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/flowchart-fun/main?label=&style=flat-square)](https://github.com/scillidan/flowchart-fun) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

```sh
pnpm install
pnpm build
serve -s app/build -p 4321
```

With PM2:

```sh
pm2 serve app\build\ 4321 --name flowchart-fun --spa
```

## [FocusTide](https://github.com/scillidan/FocusTide)

![](https://img.shields.io/github/license/Hanziness/FocusTide?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/FocusTide/main?label=&style=flat-square)](https://github.com/scillidan/FocusTide) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

```sh
yarn install
yarn generate
serve dist -p 4321
```

With PM2:

```sh
pm2 serve dist 4321 --name focustide --spa
```

If app take up `4321` port, open `chrome://serviceworker-internals/?devtools` and unregister it.

## [gifconverter](https://github.com/marshallku/gifconverter)

![](https://img.shields.io/github/license/marshallku/gifconverter?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/gifconverter/main?label=&style=flat-square)](https://github.com/scillidan/gifconverter) ![](https://img.shields.io/badge/GitHub%20Pages-121013?logo=github&logoColor=white)

```sh
npm install
npm run build
npm run dev
```

## [Gifsicle Wasm Browser](https://github.com/renzhezhilu/gifsicle-wasm-browser)

![](https://img.shields.io/github/license/renzhezhilu/gifsicle-wasm-browser?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/gifsicle-wasm-browser/main?label=&style=flat-square)](https://github.com/scillidan/gifsicle-wasm-browser)

```sh
npm install
serve -s docs -p 4321
```

With PM2:

```sh
pm2 serve docs 4321 --name gifsicle-wasm-browser --spa
```

If app take up `4321` port, open `chrome://serviceworker-internals/?devtools` and unregister it.

## [GIT.RAWify](https://github.com/emmanpbarrameda/GIT.RAWify)

![](https://img.shields.io/github/license/emmanpbarrameda/GIT.RAWify?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/GIT.RAWify/main?label=&style=flat-square)](https://github.com/scillidan/GIT.RAWify) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

```sh
serve -s . -p 4321
```

With PM2:

```sh
pm2 serve . 4321 --name git-rawify --spa
```

## [Guitar Editor](https://github.com/haixiangyan/guitar-tabs-editor)

![](https://img.shields.io/github/license/haixiangyan/guitar-tabs-editor?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/guitar-tabs-editor/master?label=&style=flat-square)](https://github.com/scillidan/guitar-tabs-editor) ![](https://img.shields.io/badge/GitHub%20Pages-121013?logo=github&logoColor=white)

```sh
npm install
npm run build
npm start
```

Change port by editing near line `15` of `package.json`:

```json title="package.json"
  "scripts": {
    "start": "set PORT=4321 && react-scripts start",
```

## [h2m](https://github.com/island205/h2m)

![](https://img.shields.io/github/license/island205/h2m?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/h2m/main?label=&style=flat-square)](https://github.com/scillidan/h2m) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

Open `index.html`.

## [hot-chain-svg](https://github.com/w1nt3r-eth/hot-chain-svg)

![](https://img.shields.io/github/license/w1nt3r-eth/hot-chain-svg?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/hot-chain-svg/main?label=&style=flat-square)](https://github.com/scillidan/hot-chain-svg)

```sh
yarn
yarn start
```

## [image-editor](https://github.com/andrepv/image-editor)

![](https://img.shields.io/github/license/andrepv/image-editor?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/image-editor/master?label=&style=flat-square)](https://github.com/scillidan/image-editor)

```sh
nvm install 16.20.0
nvm use 16.20.0
npm install
npm run build
serve -s build -l 4321
```

With PM2:

```sh
pm2 serve build 4321 --name image-editor --watch --spa
```

## [JS IMAGE CARVER](https://github.com/trekhleb/js-image-carver)

![](https://img.shields.io/github/license/trekhleb/js-image-carver?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/js-image-carver/main?label=&style=flat-square)](https://github.com/scillidan/js-image-carver) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

Edit near line `6` of `package.json`:

```json title="package.json"
  "homepage": "",
```

```sh
nvm install 16.20.0
nvm use 16.20.0
npm install
npm run build
serve -s build -l 4321
```

## [jsetymology](https://github.com/myrriad/jsetymology)

![](https://img.shields.io/github/license/myrriad/jsetymology?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/jsetymology/main?label=&style=flat-square)](https://github.com/scillidan/jsetymology) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

```sh
serve -s . -p 4321
```

## [Kiwix JS](https://github.com/kiwix/kiwix-js-pwa)

![](https://img.shields.io/github/license/kiwix/kiwix-js-pwa?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/kiwix-js-pwa/main?label=&style=flat-square)](https://github.com/scillidan/kiwix-js-pwa) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

```sh
npm i
npm run build
npm run serve
```

With PM2:

```sh
pm2 serve dist 5173 --name kiwix-js-pwa --spa --env production
```

Visit `localhost:5173`.

Setting → Use Private File System → Add file(s) → Add to OPFS → Select your `.zim` → Wait for it to complete → Install PWA (Optional).

If you clean up the cache of browser, you need to do it again.

## [Localpdf.tech](https://github.com/julianfbeck/localpdfmerger)

![](https://img.shields.io/github/license/julianfbeck/localpdfmerger?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/localpdfmerger/main?label=&style=flat-square)](https://github.com/scillidan/localpdfmerger) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

```sh
yarn
yarn build
yarn start
```

Change port by editing near line `4` of `package.json`:

```json title="package.json"
  "scripts": {
    "start": "next start -p 4321"
}
```

## [Look Scanned](https://github.com/rwv/lookscanned.io)

![](https://img.shields.io/github/license/rwv/lookscanned.io?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/lookscanned.io/main?label=&style=flat-square)](https://github.com/scillidan/lookscanned.io) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

```sh
npm install
npm run build
serve -s dist -p 4321
```

If app take up `4321` port, open `chrome://serviceworker-internals/?devtools` and unregister it.

## [lrc_editor](https://github.com/yiyizym/lrc_editor)

![](https://img.shields.io/github/license/yiyizym/lrc_editor?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/lrc_editor/master?label=&style=flat-square)](https://github.com/scillidan/lrc_editor)


```sh
npm install
npm audit fix --force
npm run build
serve -s docs -p 4321
```

## [Manga Repack](https://github.com/Aeroblast/MangaRepack)

![](https://img.shields.io/github/license/Aeroblast/MangaRepack?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/MangaRepack/main?label=&style=flat-square)](https://github.com/scillidan/MangaRepack)

```sh
npm
npm audit fix --force
npm run build
serve -s dist -p 4321
```

## [markdownlint](https://github.com/DavidAnson/markdownlint)

![](https://img.shields.io/github/license/DavidAnson/markdownlint?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/markdownlint/main?label=&style=flat-square)](https://github.com/scillidan/markdownlint) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

```sh
npm install
npm run build-demo
```

Open `demo/default.htm`.

## [Mermaidv Live Editor](https://github.com/mermaid-js/mermaid-live-editor)

![](https://img.shields.io/github/license/mermaid-js/mermaid-live-editor?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/mermaid-live-editor/master?label=&style=flat-square)](https://github.com/scillidan/mermaid-live-editor) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

```sh
yarn install
yarn build
serve -s docs -l 4321
```

## [miniPaint](https://github.com/viliusle/miniPaint)

![](https://img.shields.io/github/license/viliusle/miniPaint?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/miniPaint/main?label=&style=flat-square)](https://github.com/scillidan/miniPaint) ![](https://img.shields.io/badge/GitHub%20Pages-121013?logo=github&logoColor=white)

```sh
npm install
npm run build
serve -s . -p 4321
```

With PM2:

```sh
pm2 serve . 4321 --name minipaint --spa
```

## [NoiseCraft](https://github.com/maximecb/noisecraft)

![](https://img.shields.io/github/license/maximecb/noisecraft?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/noisecraft/main?label=&style=flat-square)](https://github.com/scillidan/noisecraft)

```sh
npm install
npm run build
npm run watch
```

## [NoteCalc](https://github.com/bbodi/notecalc3)

![](https://img.shields.io/github/license/bbodi/notecalc3?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/notecalc3/develop?label=&style=flat-square)](https://github.com/scillidan/notecalc3) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

Try:

```sh
rustup override set nightly-2020-11-17
cargo install wasm-pack
wasm-pack build --release --target no-modules frontend-web
```

But it didn't work. So just:

```sh
serve -s . -p 4321
```

## [Notepad Calculator Prototype](https://github.com/SteveRidout/notepad-calculator)

![](https://img.shields.io/github/license/SteveRidout/notepad-calculator?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/notepad-calculator/master?label=&style=flat-square)](https://github.com/scillidan/notepad-calculator) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

Open `index.html`.

## [ordered-dither-maker](https://github.com/seleb/ordered-dither-maker)

![](https://img.shields.io/github/license/seleb/ordered-dither-maker?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/ordered-dither-maker/main?label=&style=flat-square)](https://github.com/scillidan/ordered-dither-maker) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

```sh
npm install
npm run build
serve -s docs -p 4321
```

If app take up `4321` port, open `chrome://serviceworker-internals/?devtools` and unregister it.

## [Rearrange PDF as Duplex Scan](https://github.com/clemensheithecker/pdf-duplex-scan)

![](https://img.shields.io/github/license/clemensheithecker/pdf-duplex-scan?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/pdf-duplex-scan/main?label=&style=flat-square)](https://github.com/scillidan/pdf-duplex-scan) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

```sh
npm install
npm audit fix --force
npm run build
serve -s dist -p 4321
```

## [pdf-margins](https://github.com/ToyVo/pdf-margins)

![](https://img.shields.io/github/license/ToyVo/pdf-margins?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/pdf-margins/main?label=&style=flat-square)](https://github.com/scillidan/pdf-margins) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

```sh
npm install
npm run build
serve -s build -p 4321
```

## [PDF.js](https://github.com/mozilla/pdf.js)

![](https://img.shields.io/github/license/mozilla/pdf.js?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/pdf.js/main?label=&style=flat-square)](https://github.com/scillidan/pdf.js)

1. Get `dufs-v*-x86_64-pc-windows-msvc.zip` from [dufs - Releases](https://github.com/sigoden/dufs/releases). Decompress it.
2. Download `pdfjs-*-dist.zip` from [Releases](https://github.com/mozilla/pdf.js/releases). Decompress it to `pdfjs-dist/`.

```sh
cd pdfjs-dist
dufs.exe
```

Visit `localhost:5000/web/viewer.html`, or open `localhost:4007/web/viewer.html?file=book.pdf`.

Or build from source:

Install [GTK 2](https://github.com/Automattic/node-canvas/wiki/Installation:-Windows#2-installing-gtk-2).

```sh
pnpm install node-pre-gyp
git clone --depth=1 https://github.com/mozilla/pdf.js
cd pdf.js
npm install
npm install -g gulp-cli
gulp generic
dufs build/generic
```

↪ [Error on npm install](https://github.com/mozilla/pdf.js/issues/15112).

With PM2:

```sh
pm2 serve -s build/generic -p 4321 --name pdfjs --spa
```

Visit `localhost:4321/web/viewer.html`.

## [PDFME](https://github.com/pdfme/pdfme)

![](https://img.shields.io/github/license//pdfme/pdfme?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/pdfme/main?label=&style=flat-square)](https://github.com/scillidan/pdfme)

```sh
npm install
npm run build
serve -s build -p 4321
```

## [Potluck](https://github.com/inkandswitch/potluck)

![](https://img.shields.io/github/license//inkandswitch/potluck?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/potluck/main?label=&style=flat-square)](https://github.com/scillidan/potluck) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

```sh
yarn
yarn build
serve -s dist -p 4321
```

## [Programming Fonts](https://github.com/braver/programmingfonts)

![](https://img.shields.io/github/license/braver/programmingfonts?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/programmingfonts/gh-pages?label=&style=flat-square)](https://github.com/scillidan/programmingfonts) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)
```sh
npm install
serve -s . -p 4321
```

## [QR code designer](https://github.com/kochrt/qr-designer)

![](https://img.shields.io/github/license/kochrt/qr-designer?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/qr-designer/main?label=&style=flat-square)](https://github.com/scillidan/qr-designer) ![](https://img.shields.io/badge/GitHub%20Pages-121013?logo=github&logoColor=white)

```sh
nvm install 16.20.0
nvm use 16.20.0
npm install
npm run generate
npm run start
```

Change port by editing near line `5` of `nuxt.config.js`:

```json title="nuxt.config.js"
  server: {
    host: "localhost",
    port: 3003
  },
```

With PM2:

```sh
pm2 start npm --name "qr-designer" -- run start
```

## [quiver](https://github.com/varkor/quiver)

![](https://img.shields.io/github/license/varkor/quiver?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/quiver/master?label=&style=flat-square)](https://github.com/scillidan/quiver) ![](https://img.shields.io/badge/GitHub%20Pages-121013?logo=github&logoColor=white)

```sh
git clone --depth=1 https://github.com/varkor/quiver
```

1. Download `zip` form [KaTeX - Releases] (https://github.com/KaTeX/KaTeX/releases).
2. Decompress and move `katex/` into `src/`

```sh
serve -s src -p 4321
```

## [REAFLOW](https://github.com/reaviz/reaflow)

![](https://img.shields.io/github/license/reaviz/reaflow?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/reaflow/master?label=&style=flat-square)](https://github.com/scillidan/reaflow) ![](https://img.shields.io/badge/GitHub%20Pages-121013?logo=github&logoColor=white)

```sh
npm install
npm run start
```

## [recoded](https://github.com/siddharthroy12/recoded)

![](https://img.shields.io/github/license/siddharthroy12/recoded?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan//main?label=&style=flat-squarerecoded)](https://github.com/scillidan/recoded) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

```sh
npm install --legacy-peer-deps
npm run build
serve -s build -p 4321
```

With PM2:

```sh
pm2 serve build 4321 --name recoded --spa
```

## [Reference](https://github.com/Fechin/reference)

![](https://img.shields.io/github/license/Fechin/reference?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/reference/main?label=&style=flat-square)](https://github.com/scillidan/reference) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

```sh
npm install
npm run build
npm run dev
```

Optional command:

```sh
pnpm add pug -g
pnpm add katex -g
```

With PM2:

Change host by editing near line `16` of `_config.yml`:

```yml title="_config.yml"
url: http://localhost
```

```sh
hexo g
pm2 serve public 4321 --name reference --watch --spa
```

If need watch dir, you can use [Watchexec](https://github.com/watchexec/watchexec):

```sh
watchexec -w source\_posts -- hexo g
```

## [RegExr](https://github.com/gskinner/regexr)

![](https://img.shields.io/github/license/gskinner/regexr?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/regexr/master?label=&style=flat-square)](https://github.com/scillidan/regexr)

```sh
git clone --depth=1 https://github.com/gskinner/regexr
cd regexr
nvm install 10.21.0
nvm use 10.21.0
npm install
gulp
```

With PM2 (On Windows 10):

Edit near line `62` of `./gulpfile.babel.js`:

```js title="gulpfile.babel.js"
gulp.task("serve", () => {
	browser({
		server: { baseDir: "./deploy/" },
		port: 4321,
	});
});
```

```sh
pm2 start "C:\Users\<User>\AppData\Roaming\pnpm\node_modules\gulp-cli\bin\gulp.js" --interpreter "C:\Users\<User>\.nvm\v10.21.0\node.exe" -n regexr
``` 

Visit `localhost:4321`.

## [reminiflux](https://github.com/reminiflux/reminiflux)

![](https://img.shields.io/github/license/reminiflux/reminiflux?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/reminiflux/source?label=&style=flat-square)](https://github.com/scillidan/reminiflux) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

On Windows 10, edit near line `23` of `package.json`:

```json title="package.json"
  "scripts": {
    "build": "set GENERATE_SOURCEMAP=false && react-scripts build",
```

```sh
npm install
npm run build
serve -s build -p 4321
```

1. Miniflux → Settings → API Keys → Create a new API key → `reminiflux` → Copy the Token
2. Visit `localhost:4321`
  ```
  Host `<Host>:<Port>`
  API key `<Token>`
  ```

With PM2:

```sh
pm2 serve build 4321 --name reminiflux --spa
```

## [ReportBro Designer](https://github.com/jobsta/reportbro-designer)

![](https://img.shields.io/github/license/jobsta/reportbro-designer?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/reportbro-designer/master?label=&style=flat-square)](https://github.com/scillidan/reportbro-designer)

```sh
npm install
npm run build-prod
```

Open `demos/default.html`

## [Satori](https://github.com/vercel/satori)

![](https://img.shields.io/github/license/vercel/satori?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/satori/main?label=&style=flat-square)](https://github.com/scillidan/satori)

```sh
nvm install 16.20.0
nvm use 16.20.0
pnpm install
pnpm dev:playground -- -p 4321
```

With PM2:

```sh
set PORT=4321
pm2 start -n "satori" --cwd "./" "./node_modules/turbo/bin/turbo" -- dev --filter=satori-playground...
```

## [Signature Pad](https://github.com/szimek/signature_pad)

![](https://img.shields.io/github/license/szimek/signature_pad?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/signature_pad/main?label=&style=flat-square)](https://github.com/scillidan/signature_pad) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

```sh
npm install
npm run serve
```

1. When deploy with [Vercel](https://vercel.com).
2. The Project → Settings → General → Build & Development Settings → Output Directory → `docs`

## [sketch-to-lineart](https://github.com/seleb/sketch-to-lineart)

![](https://img.shields.io/github/license/seleb/sketch-to-lineart?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/sketch-to-lineart/main?label=&style=flat-square)](https://github.com/scillidan/sketch-to-lineart) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

```sh
npm install
npm run build
serve -s docs -p 4321
```

If app take up `4321` port, open `chrome://serviceworker-internals/?devtools` and unregister it.

## [Snippet Box](https://github.com/pawelmalak/snippet-box)

![](https://img.shields.io/github/license/pawelmalak/snippet-box?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/snippet-box/master?label=&style=flat-square)](https://github.com/scillidan/snippet-box)

```sh
nvm install 16.20.0
nvm use 16.20.0
cd client
npm install
cd ..
```

Edit near line `30` of `package.json`:

```json title="package.json"
  "dependencies": {
    "babel-jest": "^26.6.0",
    "babel-loader": "8.1.0",
    "eslint": "^7.11.0",
    "jest": "26.6.0",
    "webpack": "4.44.2",
    "webpack-dev-server": "3.11.1",
```

```sh
npm install
npm run build
cd build
node server.js
```

Visit `localhost:5000`.

## [sreadium](https://github.com/suisuyy/sreadium)

![](https://img.shields.io/github/license/suisuyy/sreadium?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/sreadium/main?label=&style=flat-square)](https://github.com/scillidan/sreadium) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

Put your books into `epub_content/`

```sh
serve -s . -p 4321
```

If app take up `4321` port, open `chrome://serviceworker-internals/?devtools` and unregister it.


With PM2:

```sh
pm2 serve -s . -p 4321 --name sreadium --spa
```

## [SvgPathEditor](https://github.com/Yqnn/svg-path-editor)

![](https://img.shields.io/github/license/Yqnn/svg-path-editor?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/svg-path-editor/master?label=&style=flat-square)](https://github.com/scillidan/svg-path-editor) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

```sh
npm install
npm run build
serve -s dist/svg-path-editor -l 4321
```

If app take up `4321` port, open `chrome://serviceworker-internals/?devtools` and unregister it.

## [SVGEdit](https://github.com/SVG-Edit/svgedit)

![](https://img.shields.io/github/license/SVG-Edit/svgedit?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/svgedit/master?label=&style=flat-square)](https://github.com/scillidan/svgedit) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

```sh
npm install
npm run build
serve -s dist/editor -l 4321
```

1. When deploy with [Vercel](https://vercel.com).
2. The Project → Settings → General → Build & Development Settings → Output Directory → `dist/editor`

## [SVGOMG](https://github.com/jakearchibald/svgomg)

![](https://img.shields.io/github/license/jakearchibald/svgomg?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/svgomg/main?label=&style=flat-square)](https://github.com/scillidan/svgomg)

```sh
npm install
npm run build
serve -s build -p 4321
```

## [Guitar Tab Editor](https://github.com/calesce/tab-editor)

![](https://img.shields.io/github/license/calesce/tab-editor?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/tab-editor/master?label=&style=flat-square)](https://github.com/scillidan/tab-editor) ![](https://img.shields.io/badge/GitHub%20Pages-121013?logo=github&logoColor=white)

```sh
npm install
npm start
```

Change port by editing near line `33` of `server.js`:

```js title="server.js"
app.listen(4321, 'localhost', function(err) {
  if (err) {
    return console.log(err);
  }

  console.log('Listening at http://localhost:4321');
});
```

## [tikzcd-editor](https://github.com/yishn/tikzcd-editor)

![](https://img.shields.io/github/license/yishn/tikzcd-editor?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/tikzcd-editor/master?label=&style=flat-square)](https://github.com/scillidan/tikzcd-editor)

```sh
npm install
npm audit fix --force
npx prettier --write .
npm run dist
```

Open `dist/tikzcd-editor-v0.9.0/index.html`

## [tldraw](https://github.com/tldraw/tldraw)

![](https://img.shields.io/github/license/tldraw/tldraw?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/tldraw/main?label=&style=flat-square)](https://github.com/scillidan/tldraw)

```sh
yarn
yarn dev
```

Visit `localhost:5420/develop`.

## [Url encoder for SVG](https://github.com/yoksel/url-encoder)

![](https://img.shields.io/github/license/yoksel/url-encoder?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/url-encoder/main?label=&style=flat-square)](https://github.com/scillidan/url-encoder) ![](https://img.shields.io/badge/GitHub%20Pages-121013?logo=github&logoColor=white)

```sh
npm install
npm run start
npm run start
```

With PM2:

```sh
pm2 serve build 4321 --name url-encoder --spa
```

Visit `localhost:4321`.

## [video-gif-web-converter](https://github.com/nabigraphics/video-gif-web-converter)

![](https://img.shields.io/github/license/nabigraphics/video-gif-web-converter?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/video-gif-web-converter/main?label=&style=flat-square)](https://github.com/scillidan/video-gif-web-converter)

```sh
npm install
npm audit fix --force
npm run build
npm start
```

## [visionmagic](https://github.com/visioncortex/visionmagic)

![](https://img.shields.io/github/license/visioncortex/visionmagic?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/visionmagic/master?label=&style=flat-square)](https://github.com/scillidan/visionmagic) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

```sh
nvm install 16.20.0
nvm use 16.20.0
cd webapp/app
npm install
cargo install wasm-pack
wasm-pack build
npm start
```

## [Vivliostyle Viewer](https://github.com/vivliostyle/vivliostyle.js/tree/master/packages/viewer)

![](https://img.shields.io/github/license/vivliostyle/vivliostyle.js?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/vivliostyle.js/main?label=&style=flat-square)](https://github.com/scillidan/vivliostyle.js)

1. Get `Stable release` from [Vivliostyle.js Releases](https://vivliostyle.github.io/).
2. Decompress it to `vivliostyle-viewer`.

```sh
cd vivliostyle-viewer
serve -s viewer -p 4321
```

With PM2:

```sh
pm2 serve viewer 4321 --name vivliostyle-viewer --spa
```

## [Vtracer Web App](https://github.com/visioncortex/vtracer)

![](https://img.shields.io/github/license/visioncortex/vtracer?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/vtracer/master?label=&style=flat-square)](https://github.com/scillidan/vtracer) ![](https://img.shields.io/badge/GitHub%20Pages-121013?logo=github&logoColor=white)

```sh
nvm install 16.20.0
nvm use 16.20.0
cd webapp/app
npm install
cargo install wasm-pack
wasm-pack build
npm run build
serve -s . -p 4321
```

## [woah!](https://github.com/pabueco/woah)

![](https://img.shields.io/github/license/pabueco/woah?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/woah/main?label=&style=flat-square)](https://github.com/scillidan/woah) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

```sh
pnpm i
pnpm build
serve -s dist -p 4321
```

If app take up `4321` port, open `chrome://serviceworker-internals/?devtools` and unregister it.

## [readium-js-viewer](https://github.com/readium/readium-js-viewer)

![](https://img.shields.io/github/license/readium/readium-js-viewer?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/readium-js-viewer/master?label=&style=flat-square)](https://github.com/scillidan/readium-js-viewer) ![](https://img.shields.io/badge/GitHub%20Pages-121013?logo=github&logoColor=white)

## [Mokuro reader](https://github.com/ZXY101/mokuro-reader)

![](https://img.shields.io/github/license/ZXY101/mokuro-reader?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/mokuro-reader/main?label=&style=flat-square)](https://github.com/scillidan/mokuro-reader) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

## [Ebook Reader](https://github.com/ttu-ttu/ebook-reader)

![](https://img.shields.io/github/license/ttu-ttu/ebook-reader?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/ebook-reader/main?label=&style=flat-square)](https://github.com/scillidan/ebook-reader) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

1. When deploy with [Vercel](https://vercel.com).
2. The Project → Settings
  - General → Build & Development Settings
    ```
    Build Command `pnpm build`
    Output Directory `build`
    Install Command `pnpm install --frozen-lockfile && pnpm svelte-kit sync`
    ```
  - Root Directory → `apps/web`

## [foliate-js](https://github.com/johnfactotum/foliate-js)

![](https://img.shields.io/github/license/johnfactotum/foliate-js?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/foliate-js/main?label=&style=flat-square)](https://github.com/scillidan/foliate-js) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

## [drawDB](https://github.com/drawdb-io/drawdb)

![](https://img.shields.io/github/license/drawdb-io/drawdb?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/drawdb/main?label=&style=flat-square)](https://github.com/scillidan/drawdb) ![](https://img.shields.io/badge/Vercel-black?style=flat&logo=Vercel&logoColor=white)

## [CyberChef](https://github.com/gchq/CyberChef)

![](https://img.shields.io/github/license/gchq/CyberChef?label=&style=flat-square) [![](https://img.shields.io/github/last-commit/scillidan/CyberChef/main?label=&style=flat-square)](https://github.com/scillidan/CyberChef) ![](https://img.shields.io/badge/GitHub%20Pages-121013?logo=github&logoColor=white)

## [Bukubrow](https://github.com/samhh/bukubrow-webext) (Cache)

![](https://img.shields.io/github/license/samhh/bukubrow-webext?label=&style=flat-square)

Install `Bukubrow` browser extension.

```sh
pipx install "buku[server]"
bukuserver run --host 127.0.0.1 --port 5001
```

↪ [Bukuserver](https://github.com/jarun/buku/tree/master/bukuserver)

```sh
git clone https://github.com/samhh/bukubrow-host
cd bukubrow-host
cargo build --release
./target/release/bukubrow --install-chrome
```

## [changedetection.io](https://github.com/dgtlmoon/changedetection.io)

![](https://img.shields.io/github/license/dgtlmoon/changedetection.io?label=&style=flat-square)

```sh
git clone --depth=1 https://github.com/dgtlmoon/changedetection.io
cd changedetection.io
python -m venv venv
venv/Scripts/activate.bat
pip install .
python changedetection.py
```

Visit `localhost:5000`.

With PM2:

```sh
pm2 start changedetection.py --name changedetection --interpreter "venv/Scripts/python.exe" --cwd "changedetection.io"
```

## [Album App for Django](https://github.com/jobsta/albumapp-django)

![](https://img.shields.io/github/license/jobsta/albumapp-django?label=&style=flat-square)

```sh
git clone --depth=1 https://github.com/jobsta/albumapp-django
cd albumapp-django
python -m venv venv
venv\Scripts\activate.bat
pip install django reportbro-lib
python manage.py makemigrations albums
python manage.py migrate
python manage.py compilemessages
```

```sh
python manage.py runserver localhost:8010
```

Visit `localhost:8010/albums`.

## [Streamlit Image Crop](https://github.com/mitsuse/streamlit-image-crop)

![](https://img.shields.io/github/license/mitsuse/streamlit-image-crop?label=&style=flat-square)

I should have tested it on `python38` and take a [screenshot](https://raw.githubusercontent.com/scillidan/Cos_Asset/main/screenshot/streamlit-image-crop_cache.png):

```sh
git clone --depth=1 https://github.com/mitsuse/streamlit-image-crop
cd streamlit-image-crop
python38 -m pip install poetry
poetry install
C:\Users\<User>\AppData\Local\pypoetry\Cache\virtualenvs\streamlit-image-crop-*-py3.8\Scripts\activate.bat
```

```sh
cd streamlit_image_crop/frontend
nvm install 16.20.0
nvm use 16.20.0
npm i
npm run build
serve -s build -l 4321
```

At the same time:

```sh
pip install -U click==8
streamlit run example.py
```

↪ [click.get_os_args is deprecated on module 'click 8.1.0'](https://github.com/streamlit/streamlit/issues/4555)

## [Calibre](https://calibre-ebook.com/)

1. Calibre → Preferences → Sharing/Sharing over ht net → The port on which to listen for connections `<Port>`
2. Calibre → Connect/share → Start Content server

But can't add books with `calibredb add <Book> --with-library <CalibreData>` when `calibre-server.exe --port <Port> <CalibreData>` running.

## [Calibre-Web](https://github.com/janeczku/calibre-web)

```sh
git clone --depth=1 https://github.com/janeczku/calibre-web
cd calibre-web
python -m venv venv
venv\Scripts\activate.bat
pip install calibreweb[metadata]
cps
```

1. Visit `localhost:8083`. If your want to shotdown the process, `Ctrl+C` and refresh the web-page.
2. Login with default Username `admin` and Password `admin123`. If you want to edit account:
  - admin → Edit `Username`, `Email`, `Password`
3. Calibre → Add books. You should get `Calibre Library\` now.
4. Calibre-Web → Admin → Edit Cabibre Database Configuration → Select folder contains the `metadata.db`.

## [SQLite Web](https://github.com/coleifer/sqlite-web)

```sh
git clone --depth=1 https://github.com/coleifer/sqlite-web
cd sqlite-web
pipx install sqlite-web
sqlite_web <database.db>
```

Or:

```sh
python -m venv venv
venv\Scripts\activate.bat
pip install .
venv\Scripts\sqlite_web.exe <database.db>
```

## [DevDocs](https://github.com/freeCodeCamp/devdocs)

<!-- --8<-- [start:windows10] -->
```sh
git clone --depth=1 https://github.com/freeCodeCamp/devdocs
cd devdocs
cp Gemfile Gemfile.bak
```

Edit `Gemfile`:

```
ruby '3.3.4'
```

In `pwsh.exe`:

```pwsh
rbenv install 3.3.4
rbenv shell 3.3.4
gem install bundler
bundle install
```

1. Get `curl-*-win64-mingw.zip` from [curl for Windows](https://curl.se/windows/).
2. Decompress it to `curl\`.
3. `cp curl\bin\libcurl-x64.dll <RBENV_ROOT>\3.3.4-1\bin\libcurl.dll`

↪ [Any pod command fails for lack of libcurl.dll on a Windows machine.](https://github.com/CocoaPods/CocoaPods/issues/9955)

1. Get `Binaries` from [Gzip for Windows](https://gnuwin32.sourceforge.net/packages/gzip.htm).
2. Decompress it to `gzip\`.
3. Add `gzip\bin` into `PATH`.
4. `mklink gzip\bin\gunzip.exe gzip\bin\gzip.exe`

↪ [Not installable on Windows](https://github.com/freeCodeCamp/devdocs/issues/1152)

```pwsh
bundle exec thor docs:download bash
bundle exec rackup
```

The data is on `public\docs`.

<!-- --8<-- [end:windows10] -->

## [Trilium](https://github.com/zadam/trilium)

↪ [Packaged server installation](https://github.com/zadam/trilium/wiki/Packaged-server-installation)

<!-- 
## [DGM.js](https://github.com/dgmjs/dgmjs)
## [Excalibur](https://github.com/camelot-dev/excalibur)
## [Super Productivity](https://github.com/johannesjo/super-productivity)
## [Instant Recipe Search](https://github.com/typesense/showcase-recipe-search)
## [MyIP](https://github.com/jason5ng32/MyIP)
## [Web-Check](https://github.com/Lissy93/web-check)
## [OpenCTI](https://github.com/OpenCTI-Platform/opencti)
## [freshermeat](https://github.com/cedricbonhomme/freshermeat)
## [Torrents.csv](https://github.com/emtee40/torrents-csv-server)
## [kitsunekko-tools](https://github.com/Ajatt-Tools/kitsunekko-tools)
## [Zeal User Contributions & Cheat Sheets](https://github.com/xantiagoma/zealusercontributions)
## [Monkeytype](https://github.com/monkeytypegame/monkeytype)
```sh
yarn
yarn build
yarn dev
```
## [Rclone-Webui-Angular](https://github.com/yuudi/rclone-webui-angular)
↪ [Using embed build of this project](https://github.com/yuudi/rclone-webui-angular/blob/master/docs/embed.md).
## [books](https://github.com/frappe/books)
 -->