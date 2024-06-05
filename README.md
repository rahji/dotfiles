# My Helix Configuration

## Installing Configuration Files

```bash
cd ~/.config/helix
git clone https://github.com/rahji/helix-config .
```

## Getting Themes to Work in WSL

Add `export COLORTERM=truecolor` to the bottom of `~/.bashrc`, then run `source ~/.bashrc` to reload the file.

## Installing Language Servers

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
