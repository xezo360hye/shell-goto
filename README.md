# GOTO functionality for Linux shells

Just a simple script for GOTOs for shells (currently Zsh only)

# Installation

All you need to do is to save the `goto` file in your `$PATH` and to make it executable

If you have `~/bin` in `$PATH`, run the following command. If not, replace `~/bin` to `/usr/local/bin`

```
wget -qO ~/bin/goto https://raw.githubusercontent.com/xezo360hye/shell-goto/master/goto
chmod +x ~/bin/goto
```

And that's all!

# Usage

1. Type `: label TEXT` before the command(s) you want to repeat

2. Continue using your shells

3. Type `goto TEXT` and press Y or Enter

# Shells support

Currently only Zsh is fully supported. You need to add `setopt incappendhistory` to your Zsh config (e.g. `~/.zshrc`)

Bash does not have this feature. However, there's a workaround using `trap DEBUG` — see `BASH.md` for instruction (WIP)

# How this works?

This is pretty simple tho tricky

The thing is that `:` in shells is mostly the same as `true` (there are some differences, but they are offtopic). Because of this, in fact shell ignores `: label TEXT` but saves it in history

When you call `goto TEXT`, it simply 'scrolls' your history file until it finds `: label TEXT`

After that it shows you the commands and executes them if you confirm

# TODOs

[x] Add support for `: unlabel TEXT`

[x] Add `-y` / `--yes` and `-s` / `--silent` options

[x] Figure out how to make it for Bash and other shells
