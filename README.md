# open_ide

一个极小的 macOS 终端命令，用来从任意目录快速打开本地 IDE。

A tiny macOS terminal command for opening files or folders in your local IDE.

```sh
o [file-or-folder]
```

如果不传路径，`o` 会打开当前目录。

If no path is provided, `o` opens the current directory.

## 安装 / Install

推荐使用 Homebrew 安装：

The recommended installation method is Homebrew:

```sh
brew install 0xyanyan/open_ide/open-ide
```

安装完成后，命令名仍然是 `o`：

After installation, the command name is still `o`:

```sh
o .
```

也可以先添加 tap，再安装：

You can also tap first, then install:

```sh
brew tap 0xyanyan/open_ide
brew install open-ide
```

### 手动安装 / Manual Install

如果不使用 Homebrew，可以克隆仓库，并把 `o` 链接到你的 `PATH` 目录里：

If you do not use Homebrew, clone this repo and link `o` into a directory on
your `PATH`:

```sh
git clone https://github.com/0xyanyan/open_ide.git
cd open_ide
chmod +x o
ln -sf "$PWD/o" ~/.local/bin/o
```

确认 `~/.local/bin` 已经在 `PATH` 中：

Make sure `~/.local/bin` is already on your `PATH`:

```sh
echo $PATH
```

## 使用 / Usage

打开当前目录：

Open the current directory:

```sh
o
```

打开指定文件夹：

Open a specific folder:

```sh
o ~/code/my-project
```

打开指定文件：

Open a specific file:

```sh
o README.md
```

传入的路径会先解析成绝对路径，再交给 IDE 打开。

The given path is resolved to an absolute path before being opened.

## IDE 选择顺序 / IDE Selection

`o` 会按下面的顺序选择打开方式：

`o` chooses an opener in this order:

1. `O_IDE_CMD`：IDE 的命令行工具，例如 `code` 或 `cursor`。
2. `O_IDE_APP`：macOS 应用名，例如 `Antigravity`。
3. 本机已安装的常见 IDE，默认优先 `Antigravity`。
4. macOS 自带的 `open` 回退。

1. `O_IDE_CMD`: an IDE CLI command, such as `code` or `cursor`.
2. `O_IDE_APP`: a macOS app name, such as `Antigravity`.
3. Common installed IDE apps, preferring `Antigravity`.
4. The macOS `open` fallback.

示例 / Examples:

```sh
O_IDE_CMD="code" o .
O_IDE_APP="Visual Studio Code" o ~/code/project
```

当前内置识别这些 IDE：

The built-in app lookup currently checks:

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

If none of these IDE apps are found, `o` falls back to the default macOS opener.

## 输出提示 / Output

成功用 IDE 打开后：

After opening with an IDE:

```text
✅ 已用 Antigravity 打开: /path/to/target
```

没有找到默认 IDE，使用 macOS 默认方式打开后：

If no known IDE is found and macOS `open` is used:

```text
⚠️ 没找到默认 IDE，已用 macOS 默认应用打开: /path/to/target
```

如果目标路径不存在：

If the target path does not exist:

```text
o: path does not exist: missing-path
```

## 卸载 / Uninstall

如果使用 Homebrew 安装：

If installed with Homebrew:

```sh
brew uninstall open-ide
brew untap 0xyanyan/open_ide
```

如果手动安装，删除命令链接：

If installed manually, remove the command link:

```sh
rm ~/.local/bin/o
```

如果不再需要，也可以删除克隆下来的仓库。

You can also delete the cloned repo if you no longer need it.

## 许可证 / License

MIT
