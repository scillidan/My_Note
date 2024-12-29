## [Xfce](https://www.xfce.org/)

- Screensaver → Enable Screensaver (Off)
- Lock Screen → Enable Lock Screen (Off)
- Storage → Removable Storage
  - Mount removable drives when hot-plugged (On)
  - Mount removable media when inserted (On)

## [Ubuntu Desktop](https://ubuntu.com/download/desktop)

Settings → Power → Power Saving Options → Automatic Suspend

## Andriod / Galaxy S23

三星键盘 → 样式和布局 → 自定义符号

### [Amaze](https://github.com/TeamAmaze/AmazeFileManager)

- 新建 → 网盘 → SMB共享连接 → 使用自定义IP → 服务器IP地址(.ipv4) → 用户名() → 密码() → 新建
- 新建 → 网盘 → SCP/SFTP链接

### [App Manager](https://github.com/MuntashirAkon/AppManager)

- 长按应用 → 点击其他应用 → 备份/还原 → APK文件... → 备份
- 设置 → 备份/还原 → 备份位置 → 添加 → 前往 → `.../0/Download/rclone_andriod/opt` → 勾选新位置 → 保存

### [Round Sync](https://github.com/newhinton/Round-Sync)

- Setting → Remotes → Add → Webdav → Next ...
- Setting → Export config → `/0/Download/<Flold>` → 保存
- <WebDav> → <SyncFolder> → 更多 → Sync → Sync local to remote

## Windows 10

1. 现在安装 → 我没有产品密钥 → Windows 10 专业版 → 自定义：仅安装Windows（高级） → 选择目标驱动器 → 格式化 → 新建
2. 我没有Internet连接
3. 继续执行有线设置
4. 使用脱机账户 → 不填写密码
5. 运行 → `control userpasswords2` → 属性 → 要使用本计算机，用户必须输入用户名和密码(Off)

- `Win+Q`
  - 搜索权限和历史记录 → (All Off)
  - Windows Search设置 → 高级搜索索引器设置 → 经典 → 在此自定义搜索位置 → 修改 → 包含的位置/用户 Off → 确定
- 鼠标
  - 鼠标设置 → 其他鼠标选项 → 指针 → Grey Tango
  - 自定义 → 文本选择 → 浏览 → `cursor_white/Text.cur` → 应用
- SMB
  - 启用或关闭Windows功能 → SMB1.0/CIFS文件共享支持(On) → SMB直通(On)
  - 网络和共享中心 → 高级共享设置 → 专用 → 启用网络发现(On) → 启用网络连接设备的自动设置(On) → 启用文件和打印机共享(On)
  - 计算机管理 → 本地用户和组 → 用户 → 右键 → 新用户 → 用户名() → 用户不能更改密码(On) → 密码永不过期(On) → 新建
  - 文件夹 → 右键 → 属性 → 共享 → 共享 → 选择要与其共享的用户 ... 权限级别(读取/写入) → 共享 → 完成
- 查询本机IP
  - CMD → `ipconfig | findstr /i "ipv4"`
  - 网络状态 → 更改适配器选项 → 以太网 → 属性 → Internet协议版本4 → IPv4
- 添加网络位置
  - 此电脑 → 右键 → 添加一个网络位置 → 下一页 → 选择自定义网络位置 → 查看示例 ... 用户名() → 下一步 ... 保存密码(On) → 登录 → 完成
- 新建防火墙规则
  - 管理Windows防火墙规则 → 创建新规则 → 新增空白规则 ... 此程序 → 浏览名称 → 方向 → 出站
- 资源管理器
  - 查看 → 选项 → 常规 → 打开文件资源管理器时打开(此电脑) → 在"快速访问"中显示常用文件夹(Off)
  - ... 查看 → 显示隐藏的文件、文件夹和驱动器 (On) → 隐藏已知文件类型的扩展名 (Off)
- 自动播放CD或其他媒体
  - 可移动驱动器 → 不执行操作
- 关闭Windows键热键
  - 编辑组策略 → 用户配置 → 管理模板 → Windows组件 → 文件资源管理器 → 关闭Windows键热键 → 右键 → 编辑 → 已启用 → 确定
- 键盘
  - Windows
    - 编辑语言和键盘选项
      - 拼写、键入和键盘设置 → 全部关闭
      - 添加语言 → 英语(美国)
      - 添加语言 → 中文(简体，中国)/选项 → 微软拼音 → 删除
    - 高级键盘设置
      - 语言栏选项 → 语言栏/语言栏 隐藏 → (可选)高级键设置 → 选择操作 → 更改按键顺序 → 全部未分配
      - 替代默认输入法 → 英语(美国) - 美式键盘 → 允许我为每个应用窗口使用不同的输入法 Off
  - KBLAutoSwith → 设置
    - 基础设置1 → 输入法切换设置
      - 自动切换 → 禁止
      - 默认输入法 → 英文
    - 基础设置2 → 特殊热键 → 右Shift → 切换中英文输入法
  - Rime
    - 迁移: 复制用户资料夹到新目录 → 小狼毫 安装选项 → 新目录 → 小狼毫 重新部署 → 小狼毫算法服务
    - 小狼毫安装选项 → 用户文件夹 → 使用默认默认位置 → 修改文件夹
    - 小狼毫重新部署
      - 小狼毫输入法设定 → 检查配置
    - 崩溃时运行小狼毫算法服务
- 声音
  - 声音 → 声音控制面板 → 声音 → 声音方案 → 无声
- Game bar
  - 游戏 → Game Bar (Off) → 允许控制器打开Game Bar (Off)
- 更改DNS服务器
  - 查看网络连接 → 以太网 → 属性 → 网络 → Internet协议版本4 → 属性 → 自动获得DNS服务器地址
  - 命令提示符 → `ipconfig /flushdns`
- 打印机
  - 属性 → 共享 → 共享这台打印机 (On) → 在客户端计算机上呈现打印作业 (On)

## Windows Environment

tag        | variable         | value
:-         | :-               | :-
windows10  | `%HOME%`         | `C:\Users\%USERNAME%`
windows10  | `%APPDATA%`      | `%HOME%\AppData\Roaming`
windows10  | `%LOCALAPPDATA%` | `%HOME%\AppData\Local`
pnpm       | `PNPM_HOME%`     | `%LOCALAPPDATA%\pnpm`
pip        | -                | `%HOME%\pip.ini`
rust       | -                | `%HOME%\.cargo\config`
neovim     | -                | `%LOCALAPPDATA%\nvim`
neovim     | -                | `%LOCALAPPDATA%\nvim-data`
neovim     | packer.nvim      | `%LOCALAPPDATA%\nvim-data\site\autoload\pack\packer\start\packer.nvim`
neovim     | packer.nvim      | `%LOCALAPPDATA%\nvim\lua\lsp\plugins.lua`
vim        | -                | `%HOME%\.vimrc`
vim        | vim-plug         | `<OPT_DIR>\autoload\plug.vim`
vim        | vim-plug         | `%LOCALAPPDATA%\nvim\init.vim`
vim        | vim-plug         | `%LOCALAPPDATA%\nvim-data\site\autoload\plug.vim`
vim        | gvim             | `%HOME%\.gvimrc`
pm2        | `PM2_HOME`       | `C:\ProgramData\pm2\home`
lazygit    | -                | `%APPDATA%\lazygit\config.yml`
qutebrower | -                | `%APPDATA%\qutebrowser\config`

## [ReviOS](https://revi.cc)

Revision Tool → Security → Windows Defender (On)

## [WSL](https://ubuntu.com/desktop/wsl)

1. 启用或关闭Windows功能 → Hyper-V, 用于Linux的Windows子系统
2. PowerShell(管理员):
  ```sh
  wsl --list --online
  wsl --install -d Ubuntu-22.04
  wsl -l -v
  wsl --set-version Ubuntu-22.04 2
  wsl --shutdown
  ```
3. `wsl.exe`:
  ```sh
  sudo apt update && sudo apt upgrade
  sudo apt install wget curl git
  ```

## [Paspberry Pi Imager](https://www.raspberrypi.com/software/)

1. Choose Device
2. 选择操作系统 → Other general-purpose OS → Ubuntu → `Ubuntu Server 22.04.4 LTS (64-bit)` → 编辑设置:
    1. General
    ```
    设置主机名 `ubuntu22`
    Username `User`
    Password `Password`
    热点名 `SSID`
    Password `WifiPassword`
    Wifi国家 `CN`
    ```
    2. Services → 开启SSH服务 (On) → 只允许使用公匙登录 (On)
    3. Options → 完成后弹出磁盘 (On)
3. Next

## [MiniTool Partition Wizard](https://minitool.com/partition-manager/partition-wizard-home.html)

Disk → Copy

## [Thunderbird](https://www.thunderbird.net/)

1. For [outlook](https://outlook.live.com) email
2. Settings → Mail → Forwarding and IMAP → POP and IMAP
3. Enable `POP`, `IMAP`

Or:

1. For [yandex](https://mail.yandex.com) email
2. Settings → All settings → Email clients
3. Enable `IMAP`, `POP`

## [Chrome](https://www.google.com/intl/en/chrome/) / [Brave](https://github.com/brave/brave-browser)
  
`brave://flags/#enable-parallel-downloading` → Parallel downloading → Enabled

### [floccus bookmarks sync](https://github.com/floccusAddon)

1. 打开 → ... →  新建账户 → WebDav分享
  ```
  WebDAV URL `URL`
  用户名 `User`
  密码 `Password`
  ```
2. 下一步
  ```
  服务器详细信息 → 书签路径 `floccus/bookmarks.xbel`
  文件夹映射 → 本地文件夹 `/书签栏/`
  同步间隔 `1d`
  嵌套账户 `在其他帐户同步中包括此帐户的本地`
  文件夹 → 保存
  ```
3. 打开 ... WEBDAV → 行为(推送) → 自动同步(On)

### [Cookie AutoDelete](https://github.com/Cookie-AutoDelete/Cookie-AutoDelete)

设置 → CAD设置 → 扩展选项 → 启用上下文菜单(右键菜单) (Off)

### [Saladict](https://saladict.crimx.com/)

设置 → 右键菜单 → All Off

### [uBlock Origin](https://github.com/gorhill/uBlock)

设置 → 添加“屏蔽元素”到右键菜单 (Off)

### [Imagus](https://github.com/TheFantasticWarrior/chrome-extension-imagus)

选项 → (禁用)此项功能的方式 → (启用)此项功能的方式

## [Directory Opus](https://gpsoft.com.au)

- 设置 → 选项 → 工具栏 → 图标 → 导入
- 设置 → 自定义工具栏 → 快捷键
- 设置 → 文件类型 → 文件类型群组 → Archives → `SmartZip.exe x {allfilepath}`

## [HiBit Uninstaller](https://hibitsoft.ir/Uninstaller.html)

- 工具 → 垃圾文件清理程序 → 忽略列表 → 右键 → 添加文件夹
  - `C:\Users\<User>\AppData\Roaming\fnm\node-versions`
  - `C:\ProgramData\pm2\home`
- 工具 → 空文件夹清理程序 → 忽略列表 → 右键 → 添加文件夹
  - `PostgresData`

## [BleachBit](https://bleachbit.org/)

Windows Explorer → 缩略图(On) → 清空

## [Ditto](https://ditto-cp.sourceforge.io)

- 选项 → 显示字体 → 字体 → `Sarasa Term SC Nerd` → 字形/常规 → 小五
- 选项 → Advanced → Text lines per clip → `1`

## [Everything](https://voidtools.com)

- 选项 → 索引/排除列表 → 启用排除列表 → 添加筛选器 → `node_modules\`, `public\`, `site\`, `Rubbish\`
  - 添加文件夹 → 文件夹 → `C:\$Recycle.Bin` → 确定
- 选项 → 常规 → 结果 → 双击路径列打开目录 On
- 索引 → 索引最近变化 Off
- 索引 → NTFS → 自动... Off → 不搜索的本地磁盘 → 包含到数据库 Off, 启用USN日志 Off

## [EverythingToolbar](https://github.com/srwi/EverythingToolbar)

EverythingToolbar → 更多:

- 视图 → 紧凑 (详细)
- 选项 → 修改快捷键 → Win+Alt+S
- 选项 → 隐藏空搜索, 选择第一个结果, 双击打开, 显示快速开关, 禁用动画, 自动检查更新 On
- 选项 → 规则 → 添加
  ```
  名称 `Open with Sublime`
  命令 `subl %filename%`
  ```

EverythingToolbar → 调整窗口大小 → 全高, 1/3宽

## [clawPDF](https://github.com/clawsoftware/clawPDF)

PDF阅读器 → 打印 → clawPDF → 属性 → 页面设置 → 方向(横向) → 确定 → 缩放类型(每张纸多页面) → 每张页面数(2)

## [Krita](https://krita.org/en/)

↪ [Hexagonal maps with Inkscape and Krita](https://vladar.bearblog.dev/hexagonal-maps-with-inkscape-and-krita/)  
↪ [Public Domain art preparation: monochrome](https://vladar.bearblog.dev/public-domain-art-preparation-monochrome/)  
↪ [Public Domain art preparation: in color](https://vladar.bearblog.dev/public-domain-art-preparation-in-color/)

## [GIMP](https://gimp.org)

- 复制图层 → 选中新图层 → 颜色 → 去色 → 去色 → 模式 → luma
- 添加图层模板 → 选区工具 → 填充黑色
- 模式 → 点光/叠加/色相

## [Photoshop]

导入选项 → 选择文件 → `file.csv` → 替换先有的数据组 → 确定
储存选项 → 选择文件夹 → `output\`, 文件命名 → `文档名称+下划线+数据组编号` → 确定

## [IrfanView](https://irfanview.com)

Options → Properties/Settings:

- Start / Exit options → Exit options
  - Close viewer only on ESC, if Thumbnails window displayed (On)
  - Others (Off)
- File Handing
  - Delete
    - Delete to Recycle Bin (On)
    - Jump to the next file after deleting/moving (On)
    - Others (Off)
  - Save / Rename
    - Ask to rename if incorrect extension (On)
    - Others (Off)

Open a image → `Ctrl-s` → Save quality → 100 → Profiles → Save
1. 按住左键拖拽 → `Shift+ArrowKey` → `Alt+ArrowKey` → `Ctrl+y`剪裁
2. `F12`
3. `Ctrl+s`保存

## [JPEGView](https://github.com/sylikc/jpegview)

JPEGView → 右键:

- 显示导航面板 (Off)
- 显示顺序 → 文件名
- 设定/管理 → 编辑用户设置
  ```
  ShowFullScreen=false
  DefaultSaveFormat=png
  ```
- 设定/管理 →
  - 设置当前参数为默认值
  - 管理"打开图片方式"菜单 → 新增
    ```
    标题 `Fast Stone Viewer`
    快捷键 `Shift+o`
    应用程序 → 浏览 → `FSViewer.exe`
    ```

## [FastStone Image Viewer](https://faststone.org/FSViewerDetail.htm)

设置 → 设置:

- 视图
  ```
  关联文件打开方式 `浏览模式`
  循环 (On)
  退出时提示确认 (Off)
  覆盖文件时提示确认 (On)
  单个文件删除到 `回收站，不提示`
  ```
- JPEG文件
  ```
  默认JPEG质量 → 100
  如果可能，使用原始JPEG文件的质量值 (Off)
  颜色缩减取样 → 无（图像品质最好）
  ```
- 外部程序 → 增加 → 目标程序 → 显示名称 `IrfanView` → 确定

## [PureRef](https://pureref.com)

`Ctrl+Right` → `Ctrl+Down` → `Ctrl+f` → Resize by mouse wheel → `Ctrl+Shift+r`

## [ShareX](https://getsharex.com) (Bug)

- 快捷键设置 → 添加 → 屏幕截图 → 滚动截图
  1. 滚动截图 → 设置 → 覆盖"截图后"设置 → 捕捉后：保存图像文件，在资源管理器中显示文件
  2. 快捷键 → `Ctrl+Shift+Alt+s`
- 任务设置 → 图像 → JPEG质量 `100`

## [XnConvert](https://xnview.com/en/xnconvert)

设置 → 读取格式设置 → 写入 → JPEG:

```
质量 `100`
渐进 (On)
优化哈夫曼表 (On)
DCT方式 `浮点（慢速高品质）`
二次采样系数 `2x2, 1x1, 1x1（默认）`
使用预估质量（如果可能） (Off)
```

## [Audacity](https://audacityteam.org/)

- 改变音高 → 半阶F → -3.00
- 效果 → 增幅 → 允许振幅失真

## [CUETools](https://cue.tools/wiki/Main_Page)

导出 → `[%directoryname%\]%artist% - %album%\%filename%-new[%unique%].cue`

## [FFmpeg Batch AV Converter](https://github.com/eibol/ffmpeg_batch)

流多路复用 → 字幕轨 → 保存轨道

## [HandBrake](https://handbrake.fr/)

首选项 → 输出文件 → 自动命名输出文件 → 文件格式 → `{source}.{preset}`

## [Kdenlive](https://kdenlive.org)

导出 → 导出项目 → Generic → Matroska-H264/AAC → 嵌入字幕而不是合成到画面

## [mpv](https://mpv.io)

`mpv.exe` → 新建快捷方式 → 属性 → 快捷方式:

```
目标 `mpv.exe`
起始位置 `mpv_config_dir_for_stream\`
```

## [Lively](https://github.com/rocksdanister/lively)

设置 → 壁纸 → 壁纸输入 → 键盘 → 应用聚焦时的鼠标交互

## [Wallpaper Engine](https://wallpaperengine.io/)

1. 新建 → ... → 关闭
2. 编辑 → 在资源管理器中打开 → .json
3. 文件 → 打开最近的项目 → .json
4. 创意工坊 → 在创意工坊上分享壁纸 → 预览图片 → 导入文件 → 发布更新 → 关闭

## [qBittorrent](https://github.com/c0re100/qBittorrent-Enhanced-Edition)

选项 → BitTorrent → 自动将以下Tracker添加到新的任务 → `udp://tracker.sbsub.com:2710/announce`

## [QtScrcpy](https://github.com/barry-ran/QtScrcpy)

1. 设置 → 连接 → WLAN → 当前网络 → IP地址
2. 设置 → 关于手机 → 版本号(x7)
3. 系统 → 开发者选项 → USB调试(On) → 网络ADB调试(On) → 无线调试(On) → 是否允许USB调试(确定) →  一律允许使用这台计算机进行调试(允许)

## [Fluent Reader](https://github.com/yang991178/fluent-reader)

Fluent Reader → View:

```
View `List view`
Filtering `Unread only`
Search `Show hidden articles`
```

## [LaTeX](https://www.latex-project.org/)

↪ [Choosing a LaTeX Compiler](https://www.overleaf.com/learn/latex/Choosing_a_LaTeX_Compiler)  
↪ [Paragraphs and new lines](https://www.overleaf.com/learn/latex/Paragraphs_and_new_lines)  
↪ [Bold, italics and underlining](https://www.overleaf.com/learn/latex/Bold%2C_italics_and_underlining)  

↪ [LaTeX for tabletop](https://vladar.bearblog.dev/latex-for-tabletop/)  
↪ [LaTeX images](https://vladar.bearblog.dev/latex-images/)  
↪ [LaTeX and its fancy fonts](https://vladar.bearblog.dev/latex-and-its-fancy-fonts/)  
↪ [LaTeX: text spacing and decoration](https://vladar.bearblog.dev/latex-text-spacing-and-decoration/)  
↪ [LaTeX tables: Basics](https://vladar.bearblog.dev/latex-tables-basics/)  
↪ [LaTeX tables: Advanced features](https://vladar.bearblog.dev/latex-tables-advanced-features/)  
↪ [LaTeX page geometry and layout](https://vladar.bearblog.dev/latex-page-geometry-and-layout/)  
↪ [LaTeX document structure](https://vladar.bearblog.dev/latex-document-structure/)  
↪ [Screenplay template](https://www.overleaf.com/latex/templates/screenplay-template/grqmtrnytdhj)  
↪ [Retrotype](https://github.com/Vladar4/retrotype)

## [Godot](https://godotengine.org/)

↪ [Godot Recipes](https://kidscancode.org/godot_recipes/4.x/)  
↪ [Dialogic 2](https://docs.dialogic.pro/introduction.html)  
↪ [Configuring neovim's LSP to work with Godot](https://ericlathrop.com/2024/02/configuring-neovim-s-lsp-to-work-with-godot/)

## [Renpy](https://www.renpy.org/)

Build Distributions:

1. Download `SDK.zip` from [Download Ren'Py](https://www.renpy.org/latest.html)
2. Decompress it to `renpy-*-sdk\`
3. Run `renpy-*-sdk\renpy.exe`
4. preferences → General → Projects Directory → `C:\Users\<User>\Project\renpy` → Return
5. Go to `C:\Users\<User>\Project\renpy`，`git clone --depth=1 https://codeberg.org/fhs/katawa-shoujo-re-engineered`
6. Renpy → PROJECTS → refresh → Select `katawa-shoujo-re-engineered`
7. Build Distributions → Build

Build Android:

1. Renpy → Android → Build
  1. Install SDK
  2. Generate Keys
  3. Build Package
2. 这个步骤会检测环境要求，需要JDK和Gradle
  1. 这里会涉及到Library文件的存放位置。我个人没分CDEF盘，只有C盘，也优先使用软件的便携版，一般就是压缩包。下面步骤就根据你的实际情况做修改
  2. 按照提示下载JDK和Gradle的文件。解压`OpenJDK21U-jdk_x64_windows_hotspot_21.0.4_7.zip`到`C:\Users\User\Lib\jdk-21.04`
  3. 解压`gradle-8.5-bin.zip`到`C:\Users\User\Lib\gradle-8.5`。
  4. Windows设置 → 查看高级系统设置 → 环境变量 → 用户变量 → 选中Path → 编辑 → 新建 → `C:\Users\User\Lib\jdk-21.04\bin` → 再新建 → `C:\Users\User\Lib\gradle-8.5\bin`
  5. 重启`renpy.exe` → Andriod → Build Package
3. 如果在gradle相关的步骤提示`需要下载gradle`，这可能是个bug。可以把`gradle-8.5-bin.zip`放进`C:\Users\User\.gradle\wrapper\dists\gradle-8.5-bin\<一串字符>\`下。重启renpy.exe，再试一次
4. 如果出现未知错误，可尝试关闭梯子。重启renpy.exe再试

## KOReader

Search → OPDS catalog → Add:

```
Catalog name `dir2opds`
Catalog URL `<host>:8080`
```

dir2opds → <epub> → Download → Read now

## Readium

Catalogs → Add:

```
Title `dir2opds`
Enter `<host>:8080`
```