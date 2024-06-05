# My Dot Files

These are the really minimal dot files that I am using at the moment on WSL2. It's basically
just to get some sane, comfortable defaults for [helix](https://helix-editor.com/) and [tmux](https://github.com/tmux/tmux/wiki).

## Installation

```bash
cd && git clone https://github.com/rahji/dotfiles .
```
tmux should be installed, but you will want to install helix (probably by using the [AppImage](https://docs.helix-editor.com/install.html#appimage) if you're using WSL)

## Getting True Color Themes to Work in WSL

Add `export COLORTERM=truecolor` to the bottom of `~/.bashrc`, then run `source ~/.bashrc` to reload the file.

## Installing Catppuccin Theme for Tmux

I really don't mind the tmux defaults, but I do want it to look nicer.

1. Install [tmux-plugins](https://github.com/tmux-plugins/tpm) by typing `git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm`
2. Run tmux and press `prefix` (ctrl+b by default) + `I` (capital letter i) to install the all plugins listed in `~./tmux.conf` (which is just the catppuccin plugin at the moment)

## Installing Helix Language Servers

1. Check to see what is needed for the languages you intend to use: `hx --health`
2. Look at https://github.com/helix-editor/helix/wiki/Language-Server-Configurations to see how to install what's missing

When I'm using WSL, I will need to do the following to get my preferred languages set up:

1. Before installing Go stuff, make sure that `$HOME/go/bin` is in the PATH
2. For markdown, install [marksman](https://github.com/artempyanykh/marksman/releases) and [ltex-ls](https://github.com/valentjn/ltex-ls/releases/tag/16.0.0) (for spelling and grammar checking)
3. Install each of the following language servers...

```bash
go install golang.org/x/tools/gopls@latest            # Go LSP
go install github.com/go-delve/delve/cmd/dlv@latest   # Go Debugger
go install golang.org/x/tools/cmd/goimports@latest    # Go Formatter
npm i -g vscode-langservers-extracted                 # HTML, JSON, et al
npm install -g typescript typescript-language-server  # javascript
npm i -g yaml-language-server@next                    # YAML
npm i -g bash-language-server                         # bash
npm install -g dockerfile-language-server-nodejs      # docker files
```
