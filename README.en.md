# open_ide

[中文](./README.md)

A tiny macOS terminal command for opening files or folders in your local IDE.

```sh
o [file-or-folder]
```

If no path is provided, `o` opens the current directory.

## Install

The recommended installation method is Homebrew:

```sh
brew install yanyansay/open_ide/open-ide
```

After installation, the command name is still `o`:

```sh
o .
```

You can also tap first, then install:

```sh
brew tap yanyansay/open_ide
brew install open-ide
```

### Manual Install

If you do not use Homebrew, clone this repo and link `o` into a directory on
your `PATH`:

```sh
git clone https://github.com/yanyansay/open_ide.git
cd open_ide
chmod +x o
ln -sf "$PWD/o" ~/.local/bin/o
```

Make sure `~/.local/bin` is already on your `PATH`:

```sh
echo $PATH
```

## Usage

Open the current directory:

```sh
o
```

Open a specific folder:

```sh
o ~/code/my-project
```

Open a specific file:

```sh
o README.md
```

The given path is resolved to an absolute path before being opened.

## IDE Selection

`o` chooses an opener in this order:

1. `O_IDE_CMD`: an IDE CLI command, such as `code` or `cursor`.
2. `O_IDE_APP`: a macOS app name or `.app` path, such as `Antigravity IDE`.
3. Common installed IDE apps, preferring `Antigravity IDE`.
4. The macOS `open` fallback.

Examples:

```sh
O_IDE_CMD="code" o .
O_IDE_APP="Visual Studio Code" o ~/code/project
O_IDE_APP="/Applications/Antigravity IDE.app" o .
```

The built-in app lookup currently checks:

```text
Antigravity IDE
Antigravity
Cursor
Visual Studio Code
Zed
Windsurf
Trae
IntelliJ IDEA
```

If none of these IDE apps are found, `o` falls back to the default macOS opener.

## Output

After opening with an IDE:

```text
✅ 已用 Antigravity 打开: /path/to/target
```

If no known IDE is found and macOS `open` is used:

```text
⚠️ 没找到默认 IDE，已用 macOS 默认应用打开: /path/to/target
```

If the target path does not exist:

```text
o: path does not exist: missing-path
```

## Uninstall

If installed with Homebrew:

```sh
brew uninstall open-ide
brew untap yanyansay/open_ide
```

If installed manually, remove the command link:

```sh
rm ~/.local/bin/o
```

You can also delete the cloned repo if you no longer need it.

## License

MIT
