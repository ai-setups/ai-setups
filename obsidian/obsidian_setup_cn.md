# Obsidian 安装配置

Obsidian 没有全局配置这一层，主题、快捷键、插件全都存在各自 vault 的 `.obsidian/` 目录里。
换个仓库就得从头再配一遍，索性把这套东西记下来。

```bash
brew install --cask obsidian
```

用 "Open folder as vault" 直接打开已有的 Git 仓库目录就行，Obsidian 只会往里加一个 `.obsidian/`。

## 开启官方 CLI

Obsidian 从 1.12 起自带 [命令行工具](https://obsidian.md/help/cli)，装插件不用再去点界面。
开一次就够了：Settings → General → Advanced → Command line interface，按提示完成注册
（macOS 上会在 `/usr/local/bin/obsidian` 建个软链，要输管理员密码），然后重开终端。

```bash
obsidian plugins filter=community versions
```

CLI 是连到正在运行的 Obsidian 上的，命令作用于当前打开的那个 vault。

## 不要提交 `.obsidian/`

`workspace.json` 光标一动就会被重写，`plugins/` 里装的是各插件自己仓库的构建产物，
剩下的设置也只对本机有意义。整个目录忽略掉：

```gitignore
.obsidian/
```

## 插件

| 插件 | 为什么装 |
| --- | --- |
| [Heading Level Indent](https://github.com/svonjoi/obsidian-heading-level-indent) | 正文按标题层级缩进，长文档的结构在正文里就能看出来，不用一直盯着 outline 面板找位置。 |
| [Portable Folds](https://github.com/ai-setups/obsidian-portable-folds) | Obsidian 自带的折叠状态是按绝对行号存在 localStorage 里的，上文一改位置就对不上，换台设备更是直接丢失。这个插件把折叠状态以 `%% fold %%` 注释写进笔记正文，跟着笔记走。 |

商店里有的插件，一条命令就装好：

```bash
obsidian plugins:restrict off
obsidian plugin:install id=heading-level-indent enable
```

Portable Folds 还没上架商店，也还没发 GitHub Release，BRAT 认不了，只能手动把文件拷过去：

```bash
mkdir -p .obsidian/plugins/portable-folds
cp <build>/main.js <build>/manifest.json .obsidian/plugins/portable-folds/
obsidian plugin:enable id=portable-folds
```

等那个仓库发出带 `main.js` 和 `manifest.json` 的 Release，就可以换成
[BRAT](https://github.com/TfTHacker/obsidian42-brat) 来装，顺带自动更新。

## 快捷键

CLI 只能查快捷键、改不了，这两个得去 Settings → Hotkeys 手动设。读长文档时折叠是按得最多的操作：

| 命令 | 快捷键 |
| --- | --- |
| Fold all | `Cmd+Opt+[` |
| Unfold all | `Cmd+Opt+]` |

## 核心插件

基本保持默认，只把几个根本用不到的关掉，免得命令面板里全是干扰项：

```bash
for id in slides audio-recorder webviewer zk-prefixer random-note markdown-importer; do
  obsidian plugin:disable id=$id filter=core
done
```
