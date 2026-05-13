# open_ide

`open_ide` provides a tiny macOS terminal command:

```sh
o [file-or-folder]
```

It opens a file or folder in your preferred local IDE. If no path is provided,
it opens the current directory.

## Install

Clone this repo, then link the executable into a directory on your `PATH`:

```sh
git clone https://github.com/0xyanyan/open_ide.git
cd open_ide
chmod +x o
ln -sf "$PWD/o" ~/.local/bin/o
```

Make sure `~/.local/bin` is on your `PATH`:

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

Paths are resolved to absolute paths before opening.

## IDE Selection

Resolution order:

1. `O_IDE_CMD`, for a CLI command such as `code` or `cursor`.
2. `O_IDE_APP`, for a macOS app name such as `Antigravity`.
3. Installed apps, preferring `Antigravity`.
4. macOS `open` fallback.

Examples:

```sh
O_IDE_CMD="code" o .
O_IDE_APP="Visual Studio Code" o ~/code/project
```

The built-in app lookup currently prefers:

```text
Antigravity
Cursor
Visual Studio Code
Zed
Windsurf
Trae
IntelliJ IDEA
```

If none of those apps are found, `o` falls back to macOS `open`.

## Output

After a successful IDE open, `o` prints:

```text
✅ 已用 Antigravity 打开: /path/to/target
```

If no known IDE is found:

```text
⚠️ 没找到默认 IDE，已用 macOS 默认应用打开: /path/to/target
```

If the target path does not exist, it exits with an error:

```text
o: path does not exist: missing-path
```

## Uninstall

Remove the command link:

```sh
rm ~/.local/bin/o
```

Then delete the cloned repo if you no longer need it.
