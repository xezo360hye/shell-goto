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

## Shell-specific instructions

For this tool to work you need to save your history to file dynamically, before each command execution. Methods differ from shell to shell

### Zsh

You need to add `setopt incappendhistory` to your Zsh config (e.g. `~/.zshrc`)

### Bash

For Bash you need to add the following code to your Bash config (e.g. `~/.bashrc`)

```
PROMPT_COMMAND='__prompt__=1'
trap '__cmd__="$BASH_COMMAND"; [[ "$__prompt__" && "$__cmd___" != "$PROMPT_COMMAND" ]] && history -a; unset __prompt__' DEBUG
```

If you already use `$PROMPT_COMMAND` variable, you can use `+=` instead of `=`. Sometimes the variable is set but replacing it doesn't break anything

### Other shells

Many shells can support Bash variant. If it doesn't work in your case, you can search on the internet and if you find something useful please let me know by open new issue or sending a pull request

# Usage

1. Type `: label TEXT` before the command(s) you want to repeat

2. Continue using your shells

3. Type `goto TEXT` and press Y or Enter

# How this works?

This is pretty simple tho tricky

The thing is that `:` in shells is mostly the same as `true` (there are some differences, but they are offtopic). Because of this, in fact shell ignores `: label TEXT` but saves it in history

When you call `goto TEXT`, it simply 'scrolls' your history file until it finds `: label TEXT`

After that it shows you the commands and executes them if you confirm

# TODOs

- [] Add support for `: unlabel TEXT`
- [] Add `-y` / `--yes` and `-s` / `--silent` options
- [] Figure out how to make it for Bash and other shells
