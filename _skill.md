## hosts

```sh
sudo vim /etc/hosts
```

```
<ip> github.com
<ip> raw.githubusercontent.com
<ip> mirror.archlinuxarm.org
```

## Command

↪ [Linux Bash Script, Single Command But Multiple Lines?](https://superuser.com/questions/508507/linux-bash-script-single-command-but-multiple-lines)  
↪ [How to write a multiline command?](https://stackoverflow.com/questions/605686/how-to-write-a-multiline-command)  
↪ [Multiple commands in command prompt using vbscript](https://stackoverflow.com/questions/28437066/multiple-commands-in-command-prompt-using-vbscript)

## Regex

↪ [How do I find and remove duplicate lines from a file using Regular Expressions? [closed]](https://stackoverflow.com/questions/1573361/how-do-i-find-and-remove-duplicate-lines-from-a-file-using-regular-expressions)

## [LaTeX](https://www.latex-project.org/)

↪ [A Tufte Handout Example](https://rstudio.github.io/tufte/)  
↪ [How I'm able to take notes in mathematics lectures using LaTeX and Vim](https://castel.dev/post/lecture-notes-1/)  
↪ [LaTeX tables: Basics](https://vladar.bearblog.dev/latex-tables-basics/)  
↪ [LaTeX page geometry and layout](https://vladar.bearblog.dev/latex-page-geometry-and-layout/)  
↪ [LaTeX: text spacing and decoration](https://vladar.bearblog.dev/latex-text-spacing-and-decoration/)  
↪ [LaTeX and its fancy fonts](https://vladar.bearblog.dev/latex-and-its-fancy-fonts/)  
↪ [LaTeX document structure](https://vladar.bearblog.dev/latex-document-structure/)  
↪ [LaTeX for tabletop](https://vladar.bearblog.dev/latex-for-tabletop/)  
↪ [LaTeX tables: Advanced features](https://vladar.bearblog.dev/latex-tables-advanced-features/)  
↪ [LaTeX images](https://vladar.bearblog.dev/latex-images/)

## [Krita](https://krita.org/en/)

↪ [Hexagonal maps with Inkscape and Krita](https://vladar.bearblog.dev/hexagonal-maps-with-inkscape-and-krita/)  
↪ [Public Domain art preparation: monochrome](https://vladar.bearblog.dev/public-domain-art-preparation-monochrome/)  
↪ [Public Domain art preparation: in color](https://vladar.bearblog.dev/public-domain-art-preparation-in-color/)

## [Godot](https://godotengine.org/)

↪ [Godot Recipes](https://kidscancode.org/godot_recipes/4.x/)  
↪ [Dialogic 2](https://docs.dialogic.pro/introduction.html)

↪ [Configuring neovim's LSP to work with Godot](https://ericlathrop.com/2024/02/configuring-neovim-s-lsp-to-work-with-godot/)

## [Renpy](https://www.renpy.org/)

Build Distributions:

1. 下载`SDK.zip`从[Renpy latest release](https://www.renpy.org/latest.html) → 解压到`renpy-8.2.3-sdk` → 运行 `renpy.exe`
2. preferences → Projects Directory → 修改项目文件夹路径，例如`C:\Users\User\Project\renpy` → Return
3. 在`C:\Users\User\Project\renpy`文件夹下，克隆仓库，`git clone https://codeberg.org/fhs/katawa-shoujo-re-engineered`
4. renpy.exe → PROJECTS → refresh → 选中`katawa-shoujo-re-engineered`
5. Renpy → Build Distributions → 默认会构建Linux、Macintosh、Windows三个发行版 → Build

Build Android:

1. Renpy → Android → Build
  1. Install SDK
  2. Generate Keys → 全部默认即可
  3. Build Package
2. 这个步骤会检测环境要求，需要JDK和Gradle。
  1. 这里会涉及到Library文件的存放位置。我个人没分CDEF盘，只有C盘，也优先使用软件的便携版，一般就是压缩包。下面步骤就根据你的实际情况做修改
  2. 按照提示下载JDK和Gradle的文件。解压`OpenJDK21U-jdk_x64_windows_hotspot_21.0.4_7.zip`到`C:\Users\User\Lib\jdk-21.04`
  3. 解压`gradle-8.5-bin.zip`到`C:\Users\User\Lib\gradle-8.5`。
  4. Windows设置 → 查看高级系统设置 → 环境变量 → 用户变量 → 选中Path → 编辑 → 新建 → `C:\Users\User\Lib\jdk-21.04\bin` → 再新建 → `C:\Users\User\Lib\gradle-8.5\bin`
  5. 重启`renpy.exe` → Andriod → Build Package
3. 如果在gradle相关的步骤提示`需要下载gradle`，这可能是个bug。可以把`gradle-8.5-bin.zip`放进`C:\Users\User\.gradle\wrapper\dists\gradle-8.5-bin\<一串字符>\`下。重启renpy.exe，再试一次
4. 如果出现未知错误，可尝试关闭梯子。重启renpy.exe再试