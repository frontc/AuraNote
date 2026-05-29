# Aura

极简、无干扰的 macOS 状态栏 Markdown 速记工具。完全本地化，即用即走。

<p align="center">
  <img src="aura-icon.svg" alt="Aura Logo" width="80" />
</p>

## ✨ 特性

- **常驻状态栏** — 不占 Dock 栏，后台静默运行
- **全局快捷键** — 默认 `Option+A` 一键唤出/隐藏，支持自定义
- **所见即所得 Markdown** — 基于 TipTap 的沉浸式编辑体验
- **CJK 友好** — 中文输入时 Markdown 语法（加粗/斜体/删除线/代码块/引用块等）通过全角符号也可正常触发
- **代码语法高亮** — 基于 Lowlight 引擎，支持 190+ 编程语言，可切换代码换行模式
- **本地优先** — 所有数据存储在本地 `.md` 文件，不依赖任何云端服务
- **自动保存** — 防抖写入本地文件，绝不丢失内容
- **图片拖拽/粘贴** — 自动存入笔记目录 `images/` 子文件夹，插入相对路径
- **笔记固定** — 侧边栏最多固定 7 个常用笔记，支持 17 种 Lucide 图标 + 首字模式，可按需排序
- **最近笔记** — 固定区下方自动展示未固定的最近笔记，快捷切换
- **首字图标** — 新固定笔记默认显示标题首字符（完美支持中文），时间标题自动取「日」字
- **禅模式 (Zen Mode)** — 点击标题栏绿色信号灯隐藏侧边栏和状态栏，纯书写沉浸体验
- **三种笔记命名策略** — 未命名 / 月日时分秒 / 命运的启示（随机句子），可在设置中选择
- **表格编辑** — 支持 Markdown 表格创建和编辑，Enter 键在表格内智能导航
- **待办列表** — 支持 `- [ ]` 和中文 `【 】` 语法，点击复选框切换完成状态
- **快捷键速查** — 长按 `Cmd` 键（800ms）查看当前所有可用快捷键
- **搜索与切换** — 底部状态栏按标题模糊搜索，按时间倒序浏览
- **浮动胶囊工具栏** — 底部毛玻璃胶囊式工具栏，悬浮渐显，集切换/固定/图标/排序/删除于一体
- **无边框美学** — 透明背景、12px 圆角窗口、macOS 风格信号灯控件
- **双主题 + 柔和模式** — 浅色 / 深色 / 柔和 / 跟随系统四种主题
- **macOS 原生体验** — 原生窗口拖拽、多桌面空间管理、安全作用域书签持久化权限
- **空间记忆** — 手动拖拽窗口后记住位置和所在屏幕，快捷键唤出时智能恢复
- **内容切换动画** — 切换笔记时平滑淡入淡出过渡
- **智能退格** — 行首退格自动将标题降级为段落，样式符号回退为 Markdown 源字符
- **大文件只读模式** — 笔记超过设定阈值（默认 5 万字）自动切换原生只读渲染，无卡顿
- **MCP 模式** — 支持以 `--mcp` 参数启动 headless 模式，作为 AI 工具的 MCP 服务端运行
- **MCP 配置复制** — 设置面板一键复制 MCP 配置 JSON，可直接粘贴至 AI 工具配置

## 🖥 系统要求

- macOS 13 (Ventura) 及以上
- Apple Silicon (M 系列) 或 Intel 芯片

## 🚀 快速开始

### 环境准备

- [Node.js](https://nodejs.org/) >= 18
- [Rust](https://www.rust-lang.org/) 最新稳定版
- macOS 开发工具（Xcode Command Line Tools）

### 安装依赖

```bash
npm install
```

### 开发模式

```bash
npm run tauri dev
```

### 构建生产包

```bash
nvm use 22 && CI=true npm run tauri build && bash scripts/fix-dmg.sh
```

构建完成后，`.dmg` 安装包将生成在 `src-tauri/target/release/bundle/dmg/` 目录下。

> **注意**：`fix-dmg.sh` 做了两件事：
> 1. 修复 macOS 26.x 下 `hdiutil -srcfolder` 无法正确估算镜像大小的 bug
> 2. 对 `.app` 执行 `codesign --deep --force --sign -` 补全 ad-hoc 签名，避免在他人 Mac 上提示「已损坏」

### 分发给其他人安装

未签名应用首次打开时，macOS 会拦截。让对方**右键点击 `.app` → 选择「打开」**，在弹出的对话框中点击「打开」即可。

> 若右键仍报「已损坏」，让对方在终端运行：
> ```bash
> xattr -cr /Applications/Aura.app
> ```
> 然后重新右键打开。

## ⌨️ 快捷键

### 全局快捷键

| 快捷键 | 功能 |
|---|---|
| `Option+A`（默认，可自定义） | 全局唤出/隐藏主窗口 |
| `Cmd + N` | 新建笔记 |
| `Cmd + W` | 关闭窗口（隐藏） |
| `Cmd + Q` | 退出应用 |
| `Esc` | 关闭帮助 / 弹窗 / 隐藏窗口 |
| 长按 `Cmd`（800ms） | 唤出快捷键速查面板 |

### 📝 文本格式化

| 快捷键 | 功能 |
|---|---|
| `Cmd + B` | 加粗 (Bold) |
| `Cmd + I` | 斜体 (Italic) |
| `Cmd + D` | 删除线 (Strike) |
| `Cmd + E` | 行内代码 (Code) |

### 🏷️ 标题与段落

| 快捷键 | 功能 |
|---|---|
| `Cmd + Option + 0` | 切换为正文段落 |
| `Cmd + Option + 1~4` | 切换为对应级别标题 (H1~H4) |
| `Shift + Enter` | 硬换行（不产生新段落） |

### 📋 列表与引用

| 快捷键 | 功能 |
|---|---|
| `Cmd + Shift + 8` | 无序列表 (Bullet List) |
| `Cmd + Shift + 7` | 有序列表 (Ordered List) |
| `Cmd + Shift + B` | 引用块 (Blockquote) |
| `Cmd + Option + C` | 代码块 (Code Block) |
| `Cmd + T` | 插入表格 (Table) |

### ⏪ 历史记录

| 快捷键 | 功能 |
|---|---|
| `Cmd + Z` | 撤销 (Undo) |
| `Cmd + Shift + Z` / `Cmd + Y` | 重做 (Redo) |

## 🛠 技术栈

| 层 | 技术 | 用途 |
|---|---|---|
| 桌面框架 | Tauri 2 (Rust) | 窗口管理、系统托盘、全局快捷键、文件系统 |
| 前端 | React 19 + TypeScript | UI 渲染与交互逻辑 |
| 构建 | Vite 8 | 前端开发与打包 |
| 样式 | Tailwind CSS 4 + @tailwindcss/typography | 原子化样式 + 编辑器排版 |
| 编辑器 | TipTap + tiptap-markdown | WYSIWYG Markdown 编辑 |
| 语法高亮 | CodeBlockLowlight + lowlight | 代码块语法高亮（190+ 语言） |
| 图标 | lucide-react | 极简 SVG 图标库 |
| 状态管理 | Zustand | 前端全局状态 |
| 持久化 | tauri-plugin-store | 本地配置持久化 |
| 对话框 | tauri-plugin-dialog | 系统原生文件选择器 |
| 文件系统 | tauri-plugin-fs | 文件系统权限 |
| Shell | tauri-plugin-shell | Shell 命令调用 |
| CLI | tauri-plugin-cli | CLI 参数解析（MCP 模式） |
| 窗口定位 | tauri-plugin-positioner | 窗口定位辅助 |
| macOS 原生 | objc2 + foundation + app-kit | 透明窗口、圆角、多桌面空间行为 |

## 📁 项目结构

```
aura/
├── src/                        # React 前端
│   ├── assets/
│   │   └── pinned-icons.tsx    # 侧边栏 18 个图标定义 + 首字模式
│   ├── components/
│   │   ├── editor/             # TipTap 编辑器及自定义 Extension
│   │   │   ├── TipTapEditor.tsx    # 主编辑器组件
│   │   │   ├── AuraImage.ts        # 自定义图片 Extension
│   │   │   └── TableToolbar.tsx    # 表格工具栏
│   │   ├── overlay/
│   │   │   └── CheatsheetOverlay.tsx  # 快捷键速查面板
│   │   ├── layout/
│   │   │   └── Sidebar.tsx      # 侧边栏（固定 + 最近笔记）
│   │   └── statusbar/
│   │       ├── NotesPopover.tsx  # 笔记切换弹窗
│   │       └── EmojiPicker.tsx   # 图标选择器
│   ├── data/
│   │   ├── help-content.ts      # 内置帮助文档
│   │   └── shortcutData.ts      # 快捷键分组数据
│   ├── hooks/
│   │   └── useNotesWatcher.ts   # 文件系统变更监听 Hook
│   ├── lib/
│   │   ├── ipc.ts               # IPC 通信封装层
│   │   ├── search.ts            # 前端全文搜索 Hook
│   │   ├── store.ts             # 持久化存储操作
│   │   └── utils.ts             # 工具函数
│   ├── pages/
│   │   ├── MainWindow.tsx       # 主窗口（编辑界面 + 浮动状态栏 + 禅模式）
│   │   └── Settings.tsx         # 设置面板（flip 翻转）
│   ├── store/
│   │   ├── useNoteStore.ts      # 笔记状态管理
│   │   └── useSettingsStore.ts  # 设置状态管理
│   ├── types/
│   │   └── index.ts             # TypeScript 类型定义（IPC 接口）
│   ├── App.tsx                  # 根组件（配置初始化 + 翻转动效路由）
│   ├── main.tsx                 # 应用入口
│   └── index.css                # 全局样式（Tailwind、动画、编辑器主题）
├── src-tauri/                  # Tauri Rust 后端
│   ├── src/
│   │   ├── main.rs             # 应用入口
│   │   ├── lib.rs              # Tauri Builder 组装
│   │   ├── commands.rs         # IPC 命令（文件读写、笔记管理、图片、固定笔记）
│   │   ├── cache.rs            # 内存缓存系统
│   │   ├── search.rs           # 全文搜索（CJK bigram + rayon 并行）
│   │   ├── watcher.rs          # 文件系统监视器（FSEvent）
│   │   ├── shortcut.rs         # 全局快捷键管理
│   │   ├── window.rs           # 窗口生命周期与 Anchored/Floating 状态机
│   │   ├── tray.rs             # 系统托盘逻辑
│   │   ├── bookmark.rs         # macOS 安全作用域书签
│   │   ├── mcp.rs              # MCP 模式（JSON-RPC 2.0 over stdio）
│   │   └── title_generator.rs  # 新建笔记标题生成器
│   ├── capabilities/
│   │   └── default.json        # 权限配置
│   ├── Info.plist              # macOS 应用信息
│   ├── entitlements.plist      # 沙箱授权
│   └── tauri.conf.json         # Tauri 全局与打包配置
├── scripts/                    # 构建与辅助脚本
│   ├── build-all.sh
│   ├── build-appstore.sh
│   ├── build-version.mjs
│   ├── build-website.sh
│   └── fix-dmg.sh
├── title.txt                   #「命运的启示」标题库
├── package.json
└── vite.config.ts
```

## ⚙️ 设置选项

通过系统托盘右键菜单「设置」进入（或快捷键唤起窗口后，右键托盘图标 → 设置）：

| 设置项 | 可选值 | 说明 |
|---|---|---|
| 主题模式 | 跟随系统 / 浅色 / 深色 / 柔和 | 适配不同环境光照 |
| 图标大小 | 常规 / 偏大 / 大 | 侧边栏图标尺寸 |
| 默认标题 | 未命名 / 月日时分秒 / 命运的启示 | 新建笔记的命名策略 |
| 新建按钮 | 开关 | 侧边栏新建笔记按钮显隐 |
| 最近笔记 | 开关 | 侧边栏最近笔记区域显隐 |
| 窗口置顶 | 开关 | 窗口始终保持最前 |
| 代码换行 | 开关 | 代码块内容自动换行 |
| 只读模式 | 2~10 万字 | 笔记字数超过阈值时自动以原生只读模式渲染 |
| 快捷键 | 自定义 | 全局唤醒快捷键（支持 Backspace 清空） |
| 存储位置 | 自定义目录 | 笔记文件存放路径（支持安全书签持久化） |

## 🎨 设计理念

Aura 遵循三大核心原则：

- **极简主义** — 无边框、透明背景、紧凑排版、浮动胶囊 UI，完美融入 macOS 生态
- **键盘驱动** — 唤醒、创建、输入、隐藏全程键盘操作，无需鼠标切换
- **即用即走** — 呼出即写，写完即隐，自动保存，零心智负担

## 📄 许可

MIT License
