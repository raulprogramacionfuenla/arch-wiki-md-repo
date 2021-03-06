[Powerline](https://powerline.readthedocs.io/en/master/index.html) is a statusline plugin for Vim, and provides statuslines and prompts for several other applications, including zsh, bash, tmux, IPython, Awesome, i3 and Qtile.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Bash](#Bash)
    *   [2.2 Zsh](#Zsh)
    *   [2.3 Tmux](#Tmux)
    *   [2.4 Vim](#Vim)
    *   [2.5 Detailed Usage](#Detailed_Usage)
*   [3 Customizing](#Customizing)
*   [4 Miscellaneous](#Miscellaneous)
    *   [4.1 Alternative Installation](#Alternative_Installation)
        *   [4.1.1 Using python-pip](#Using_python-pip)
        *   [4.1.2 Using a vim plugin manager](#Using_a_vim_plugin_manager)
    *   [4.2 Alternative Fonts](#Alternative_Fonts)
    *   [4.3 Alternative Package](#Alternative_Package)

## Installation

[Install](/index.php/Install "Install") [powerline](https://www.archlinux.org/packages/?name=powerline) and [powerline-fonts](https://www.archlinux.org/packages/?name=powerline-fonts) from the [official repositories](/index.php/Official_repositories "Official repositories")

**Note:** Installing [powerline-fonts](https://www.archlinux.org/packages/?name=powerline-fonts) does not provide any of the patched fonts from [powerline-fonts-git](https://aur.archlinux.org/packages/powerline-fonts-git/)

## Usage

### Bash

Add the following to your **~/.bashrc**:

```
powerline-daemon -q
POWERLINE_BASH_CONTINUATION=1
POWERLINE_BASH_SELECT=1
. /usr/share/powerline/bindings/bash/powerline.sh

```

Close and reopen your terminal and it should be working. If not, check the [Powerline bash prompt](https://powerline.readthedocs.io/en/latest/usage/shell-prompts.html#bash-prompt) usage instructions to ensure that it has not changed.

You can also enter:

```
source ~/.bashrc

```

if you don't want to close and re-open your terminal.

### Zsh

Add the following to your **~/.zshrc**:

```
powerline-daemon -q
. /usr/lib/python3.7/site-packages/powerline/bindings/zsh/powerline.zsh

```

### Tmux

**Note:** Watch out for interfering styles in .tmux.conf (i.e. window-status-format)
Add the following to your **~/.tmux.conf**:
```
source /usr/lib/python3.7/site-packages/powerline/bindings/tmux/powerline.conf

```

**Note:** It is sufficient to just add this to .tmux.conf (adding anything zshrc or bashrc isn't neccessary).

### Vim

Install [powerline-vim](https://www.archlinux.org/packages/?name=powerline-vim)

**Note:** If you have more than one version of python installed, add `let g:powerline_pycmd="py3"` or `let g:powerline_pycmd="py"` to your `.vimrc`.

**Tip:** By default, the statusline (and therefore Powerline) only appears when there are multiple windows open. To show it all the time, use `:set laststatus=2`

**Tip:** This package installs Powerline to `/usr/share/vim/vimfiles/plugin`, which vim is configured to check by default, meaning this will install Powerline in vim for all users and may require additional configuration. If this is not intended, consider either using a vim plugin manager, or installing the [powerline](https://www.archlinux.org/packages/?name=powerline) package and adding `set rtp+=/usr/lib/python3.7/site-packages/powerline/bindings/vim` to your `.vimrc`.

### Detailed Usage

For detailed usage instructions, such as configuring your system to use Powerline with other shells, window manager widgets, etc., please refer to the [Usage section](https://powerline.readthedocs.io/en/latest/usage.html#usage) of the [Powerline documentation](https://powerline.readthedocs.io/en/latest/index.html).

## Customizing

The official [Powerline docs](https://powerline.readthedocs.io/en/master/) refer to "powerline_root", which for Arch Linux is the following:

```
/usr/lib/python3.7/site-packages/powerline

```

To customize powerline, copy a default config to $XDG_CONFIG_HOME/powerline/... Then edit the file to your liking.

Example to customize powerline for tmux:

```
cp /usr/lib/python3.7/site-packages/powerline/config_files/themes/tmux/default.json ~/.config/powerline/themes/tmux/default.json

```

## Miscellaneous

### Alternative Installation

#### Using python-pip

*   [Install](/index.php/Install "Install") [python-pip](https://www.archlinux.org/packages/?name=python-pip) from the [official repositories](/index.php/Official_repositories "Official repositories")
*   Please refer to the [Powerline installation guide](https://powerline.readthedocs.io/en/master/installation.html) for additional python-pip instructions

#### Using a vim plugin manager

There are many vim plugin managers available which are able to install and update Powerline, assuming you are using a version of vim with Python support or you install [python](https://www.archlinux.org/packages/?name=python). For example, using [vim-plug](https://aur.archlinux.org/packages/vim-plug/) from the [AUR](/index.php/AUR "AUR"), add the following to your `.vimrc` file:

 `~/.vimrc` 
```
call plug#begin('*path/to/vim/plugins/directory*')

Plug 'powerline/powerline'

call plug#end()

```

Substitute `*path/to/vim/plugins/directory*` with the actual directory, such as `~/.vim/plugged`, or `~/.local/share/nvim/plugged` for Neovim, and run the vim-plug command `:PlugInstall` within vim. This will download Powerline from the [Powerline GitHub page](https://github.com/powerline/powerline) to the specified plugin directory and add it to vim.

### Alternative Fonts

A reduced set of fonts for the text console are available in [powerline-console-fonts](https://aur.archlinux.org/packages/powerline-console-fonts/).

### Alternative Package

There is currently one known alternative to Powerline - [Vim-airline](https://github.com/vim-airline). It is a part of [vim-plugins](https://www.archlinux.org/groups/x86_64/vim-plugins/) and can be installed separately as [vim-airline](https://www.archlinux.org/packages/?name=vim-airline). Optionally, install [vim-airline-themes](https://www.archlinux.org/packages/?name=vim-airline-themes).

**Note:** In [vim-airline](https://www.archlinux.org/packages/?name=vim-airline), showing the current git branch relies on [vim-fugitive](https://www.archlinux.org/packages/?name=vim-fugitive). vim-fugitive v2.4 made a change that broke this feature. [Upstream will not tag a new release](https://github.com/vim-airline/vim-airline/issues/1815) with the single commit that fixes compatibility with vim-fugitive v2.4\. Until then, if you want to see the current git branch, you have to: use [vim-airline-git](https://aur.archlinux.org/packages/vim-airline-git/); downgrade vim-fugitive to v2.3; or make your own vim-airline v0.9.0, cherry-picking [upstream's fixing commit](https://github.com/vim-airline/vim-airline/commit/30a3c4f54948bc2692a6e218a600d1ebea42f94d). If you decide to cherry-pick, it doesn't apply cleanly, so you'll need to fix that too.