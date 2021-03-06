# Software I use on Linux

- [Neovim](https://neovim.io/)  
  Together with [NerdTree](https://github.com/preservim/nerdtree) and [CtrlP](https://github.com/ctrlpvim/ctrlp.vim) an awesome editor.



### Installation

[Download plug.vim](https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim) and put it in the "autoload" directory.

#### Vim

###### Windows (PowerShell)

```
iwr -useb https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim |`
    ni $HOME/vimfiles/autoload/plug.vim -Force
```

#### Neovim

###### Unix, Linux

```
sh -c 'curl -fLo "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/autoload/plug.vim --create-dirs \
       https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'
```

### Neovim configuration

On first launch the `~/.local/share/nvim/{shada,swap}` directories are auto-generated. Manually create a new `~/.config/nvim` directory and a `init.vim` configuration file.

```
$ mkdir ~/.config/nvim
$ touch ~/.config/nvim/init.vim
```

#### My init.vim

```
set nocompatible            " disable compatibility to old-time vi
set showmatch               " show matching brackets.
set ignorecase              " case insensitive matching
set mouse=v                 " middle-click paste with mouse
set hlsearch                " highlight search results
set tabstop=4               " number of columns occupied by a tab character
set softtabstop=4           " see multiple spaces as tabstops so <BS> does the right thing
set expandtab               " converts tabs to white space
set shiftwidth=4            " width for autoindents
set autoindent              " indent a new line the same amount as the line just typed
set number                  " add line numbers
set wildmode=longest,list   " get bash-like tab completions
set cc=80                   " set an 80 column border for good coding style
filetype plugin indent on   " allows auto-indenting depending on file type
syntax on                   " syntax highlighting

let g:mapleader = ','
nnoremap <leader>s :set invspell<CR>

" Plugins will be downloaded under the specified directory.
call plug#begin('~/.vim/plugged')

" Declare the list of plugins.
Plug 'tpope/vim-sensible'
Plug 'junegunn/seoul256.vim'
Plug 'scrooloose/nerdtree'
Plug 'ctrlpvim/ctrlp.vim'

" List ends here. Plugins become visible to Vim after this call.
call plug#end()

" Open NerdTreeToggle with CTRL-k CTRL-b
nnoremap <silent> <C-k><C-B> :NERDTreeToggle<CR>
```
