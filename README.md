# open_ide

[English](./README.en.md)

一个极小的 macOS 终端命令，用来从任意目录快速打开本地 IDE。

```sh
o [文件或文件夹]
```

如果不传路径，`o` 会打开当前目录。

## 安装

推荐使用 Homebrew 安装：

```sh
brew install 0xyanyan/open_ide/open-ide
```

安装完成后，命令名仍然是 `o`：

```sh
o .
```

也可以先添加 tap，再安装：

```sh
brew tap 0xyanyan/open_ide
brew install open-ide
```

### 手动安装

如果不使用 Homebrew，可以克隆仓库，并把 `o` 链接到你的 `PATH` 目录里：

```sh
git clone https://github.com/0xyanyan/open_ide.git
cd open_ide
chmod +x o
ln -sf "$PWD/o" ~/.local/bin/o
```

确认 `~/.local/bin` 已经在 `PATH` 中：

```sh
echo $PATH
```

## 使用

打开当前目录：

```sh
o
```

打开指定文件夹：

```sh
o ~/code/my-project
```

打开指定文件：

```sh
o README.md
```

传入的路径会先解析成绝对路径，再交给 IDE 打开。

## IDE 选择顺序

`o` 会按下面的顺序选择打开方式：

1. `O_IDE_CMD`：IDE 的命令行工具，例如 `code` 或 `cursor`。
2. `O_IDE_APP`：macOS 应用名，例如 `Antigravity`。
3. 本机已安装的常见 IDE，默认优先 `Antigravity`。
4. macOS 自带的 `open` 回退。

示例：

```sh
O_IDE_CMD="code" o .
O_IDE_APP="Visual Studio Code" o ~/code/project
```

当前内置识别这些 IDE：

```text
Antigravity
Cursor
Visual Studio Code
Zed
Windsurf
Trae
IntelliJ IDEA
```

如果没有找到这些 IDE，`o` 会回退到 macOS 默认打开方式。

## 输出提示

成功用 IDE 打开后：

```text
✅ 已用 Antigravity 打开: /path/to/target
```

没有找到默认 IDE，使用 macOS 默认方式打开后：

```text
⚠️ 没找到默认 IDE，已用 macOS 默认应用打开: /path/to/target
```

如果目标路径不存在：

```text
o: path does not exist: missing-path
```

## 卸载

如果使用 Homebrew 安装：

```sh
brew uninstall open-ide
brew untap 0xyanyan/open_ide
```

如果手动安装，删除命令链接：

```sh
rm ~/.local/bin/o
```

如果不再需要，也可以删除克隆下来的仓库。

## 许可证

MIT
