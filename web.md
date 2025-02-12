## [Material for MkDocs](https://github.com/squidfunk/mkdocs-material)

```sh
mkdir <site>
cd <site>
uv venv
.venv\Scripts\activate.bat
uv pip install mkdocs-material
mkdocs new .
```

```yaml
theme:
  name: material
```

## [Sphinx](https://www.sphinx-doc.org/en/master/)

```sh
mkdir <site>
cd <site>
uv venv
.venv\Scripts\activate.bat
uv pip install furo sphinx-copybutton sphinxcontrib-mermaid
# uv pip install sphinxcontrib-asciinema sphinx-autobuild
sphinx-quickstart
# make clean
make html
```

↪ [Furo](https://github.com/pradyunsg/furo)  
↪ [sphinx-copybutton](https://github.com/executablebooks/sphinx-copybutton)  
↪ [sphinxcontrib-mermaid](https://github.com/mgaitan/sphinxcontrib-mermaid)  
↪ [sphinxcontrib-asciinema](https://github.com/divi255/sphinxcontrib.asciinema)  
↪ [sphinx-autobuild](https://github.com/sphinx-doc/sphinx-autobuild)

## [Vivliostyle CLI](https://github.com/vivliostyle/vivliostyle-cli)

```sh
mkdir <dir>
cd <dir>
pnpm add -g @vivliostyle/cli
vivliostyle init
```

Edit `vivliostyle.config.js` by yourself.

```sh
vivliostyle preview
```

You can refer to `.css` files in [vivliostyle_doc/samples](https://github.com/vivliostyle/vivliostyle_doc/tree/gh-pages/samples) or [kaigainotabi1](https://github.com/MurakamiShinyu/kaigainotabi1) to create your `style.css`.

PS: I don't know why, but sometimes after you use "vivliostyle preview", you need to used `Task Manager` to find and stop the (multi-) `chromium` process.

Build `html`, `epub`, `pdf`:

```sh
vivliostyle build
vivliostyle build --format epub -o <file>.epub
```

Build with Github Action, host on Github Pages:

1. Repository → Settings → Pages → Build and deployment → Github Actions
2. Edit `./github/workflows/action.yml`:

```
name: vivliostyle_gh-page

on:
  push:
    branches: ["gh-page"]
  workflow_dispatch:
permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '18.x'
      - name: Install Vivliostyle CLI
        run: npm install -g @vivliostyle/cli
      - name: Build Project
        run: vivliostyle build
      - name: Setup Pages
        uses: actions/configure-pages@v3
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v2
        with:
          path: ./
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v2
```

Visit [Vivliostyle Viewer](https://vivliostyle.org/viewer/). Enter your `gh-pages` URL. liked `https://<User>.github.io/<Repository>`.

PS: You can refer to [web-app.md - Vercel Settings](https://github.com/scillidan/My_Note/blob/main/web-app.md#vercel-settings), [web-app.md - Vivliostyle Viewer](https://github.com/scillidan/My_Note/blob/main/web-app.md#vivliostyle-viewer) to host `Vivliostyle Viewer` on local, [Vercel](https://vercel.com/), Github Pages.

## [stagit](https://git.codemadness.org/stagit)

```sh
git clone git://git.codemadness.org/stagit
cd stagit
sudo apt install libgit2-dev
make
ln -s stagit ~/.local/bin/
ln -s stagit-index ~/.local/bin/
```

```sh
mkdir <dir>
cd <dir>
cp <path_to_stagit>/style.css ./
mkdir <subdir1>
mkdir <subdir2>
mkdir source
git clone <repo1> source/<subdir1>
git clone <repo2> source/<subdir2>
cd <subdir1>
stagit ../source/<subdir1>
cd ../<subdir2>
stagit ../source/<subdir2>
cd ..
stagit-index source/<subdir1> source/<subdir2> > index.html
```

```sh
magick convert image.png -resize 96x96 favicon.png
magick convert image.png -resize 96x96 logo.png
ln -s favicon.png <subdir1>/
ln -s favicon.png <subdir2>/
ln -s logo.png <subdir1>/
ln -s logo.png <subdir2>/
```