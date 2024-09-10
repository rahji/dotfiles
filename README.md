# My Dot Files

These are the really minimal dot files and config that I am using at the moment on WSL2 to set up 
[helix](https://helix-editor.com/) and [tmux](https://github.com/tmux/tmux/wiki). I also 
set a (mostly) matching theme (catppuccin mochiatto) for helix, tmux, micro, and bat.

## Installation

1. Back up any of the files that might get overwritten below
2. Get the files by cloning the repo: `git clone https://github.com/rahji/dotfiles`
3. Move `.tmux.conf` and the contents of `.config` to your home directory

tmux should already be installed, but you will want to install helix (probably by using the [AppImage](https://docs.helix-editor.com/install.html#appimage) if you're using WSL) or by using [snap](https://snapcraft.io/install/helix/raspbian) if you're on a raspberry pi.

## Getting True Color Themes to Work in WSL

Add the following to the bottom of `~/.bashrc`, then run `source ~/.bashrc` to reload the file.

```bash
export COLORTERM=truecolor
export "MICRO_TRUECOLOR=1"
```

## Installing Catppuccin Theme for Tmux

I really don't mind the tmux defaults, but I do want it to look nicer.

1. Install [tmux-plugins](https://github.com/tmux-plugins/tpm) by typing `git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm`
2. Run tmux and press `prefix` (ctrl+b by default) + `I` (capital letter i) to install the all plugins listed in `~/.tmux.conf` (which is just the catppuccin plugin at the moment)

## Installing Catppuccin Theme for Bat

Note that `bat` may be installed as `batcat` on linux, in which case you should probably make a shorter alias. In any case, you'll need to run the following command to get `bat` to recognize the added themes:

```bash
bat cache --build
```

## Configuring Helix

Helix is ready to go once it's installed, but you do have to install the language servers for the kinds of files you typically edit. It's still pretty simple and you only have to do it once. This is the main reason why I'm using this instead of neovim - I just want to edit some files and not spend my life dealing with config/plugins.

1. Check to see what is needed for the languages you intend to use: `hx --health`
2. Look at https://github.com/helix-editor/helix/wiki/Language-Server-Configurations to see how to install what's missing

For me, using WSL to mainly edit Markdown and Go and Javascript, that means:

1. Before installing Go stuff, make sure that `$HOME/go/bin` is in the PATH
2. For markdown, install [marksman](https://github.com/artempyanykh/marksman/releases) and [ltex-ls](https://github.com/valentjn/ltex-ls/releases/tag/16.0.0) (for spelling and grammar checking)
3. Install each of the following language servers...

```bash
go install golang.org/x/tools/gopls@latest            # Go LSP
go install github.com/go-delve/delve/cmd/dlv@latest   # Go Debugger
go install golang.org/x/tools/cmd/goimports@latest    # Go Formatter
go install github.com/nametake/golangci-lint-langserver@latest
npm i -g vscode-langservers-extracted                 # HTML, JSON, et al
npm install -g typescript typescript-language-server  # javascript
npm i -g yaml-language-server@next                    # YAML
npm i -g bash-language-server                         # bash
npm install -g dockerfile-language-server-nodejs      # docker files
```

### Setting Up dprint

`dprint` is a file formatter, ala `prettier`. Download it by running this command:

```bash
curl -fsSL https://dprint.dev/install.sh | sh
```

`dprint` doesn't work without a `dprint.json` config file in the local directory. There's no such thing as a global config file, strangely. This works for me, when working with Markdown:

```json
{
  "markdown": {
    "lineWidth":120,
    "emphasisKind":"asterisks",

  },
  "excludes": [],
  "plugins": [
    "https://plugins.dprint.dev/markdown-0.16.1.wasm"
  ]
}
```

Other possible options are in the [dprint Markdown Configuration page](https://dprint.dev/plugins/markdown/config/)

The `languages.toml` file in this repo is already set up to use `dprint` as its formatter. It's configured to format every time you save, but you can also format by typing `:format` or `:fmt`. Most of this `dprint` config info came from <https://medium.com/@CaffeineForCode/helix-setup-for-markdown-b29d9891a812>.

### Fixing Helix Issue with Slow Startup

In WSL2, Helix seems to have clipboard-related trouble that causes startup to take longer than it should. Install the following to (hopefully) resolve the issue:

```bash
sudo apt install wl-clipboard
```

> [!NOTE]  
> It's generally not recommended to edit files in Windows directories using WSL2. Everything seems slower/clunkier. It's better to just stick with the linux filesystem - especially since it even shows up in the Windows File Explorer. (Of course I still edit in Windows directories because a lot of my documents are in Dropbox. Then I have the problem of trying to work with files at the command line that haven't been downloaded locally, which causes them to appear as zero-byte files. What a mess. Someday I'll just go back to Linux without Windows. 🤷🏽‍♂️)

## Notes For Windows Command Prompt

Some of the above config works when using helix and micro in Windows (ie: without WSL2). The micro configuration should not be used since I think the status line configuration causes the editor to move really slowly. The colorschemes folder can be used for Windows, however. It will require that the following environment variable is set though. You'll need to use the "Edit system environment variables" control panel if you want the setting to stick.

```bash
set MICRO_TRUECOLOR=1
```
