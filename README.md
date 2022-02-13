# 🚀 JETPACK.vim

The lightning-fast plugin manager for Vim/Neovim.

## Benchmark

In the simple cases, JETPACK.vim is the fastest plugin manager.

|  name   | time (ms) |
| :-----: | --------: |
| jetpack |     0.095 |
|  dein   |     0.113 |
|  plug   |     0.130 |

## Installation

Download pack.vim and put it in the `autoload` directory.

```
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/tani/jetpack/master/autoload/pack.vim
```

## Supported options

|   name   | description                         |
| :------: | :---------------------------------- |
|   `do`   | Post-update hook                    |
| `branch` | git branch                          |
|  `rtp`   | subdirectory is placed a plugin     |
|   `as`   | name of plugin                      |
|  `for`   | lazy loading for the given filetype |
|  `opt`   | lazy loading for `packadd {name}`   |

## Example configuration

### vim-plug style

```vim
call pack#begin()
Pack 'junegunn/fzf.vim'
Pack 'junegunn/fzf', { 'do': 'call fzf#install()' }
Pack 'neoclide/coc.nvim', {'branch': 'release'}
Pack 'neoclide/coc.nvim', {'branch': 'master', 'do': '!yarn install --frozen-lockfile'}
Pack 'vlime/vlime', { 'rtp': 'vim' }
Pack 'dracula/vim', { 'as': 'dracula' }
Pack 'tpope/vim-fireplace', { 'for': 'clojure' }
call pack#end()
```

### dein/ minpac style

```vim
call pack#begin()
pack#add('junegunn/fzf.vim')
pack#add('junegunn/fzf', { 'do': 'call fzf#install()' })
pack#add('neoclide/coc.nvim', {'branch': 'release'})
pack#add('neoclide/coc.nvim', {'branch': 'master', 'do': '!yarn install --frozen-lockfile'})
pack#add('vlime/vlime', { 'rtp': 'vim' })
pack#add('dracula/vim', { 'as': 'dracula' })
pack#add('tpope/vim-fireplace', { 'for': 'clojure' })
call pack#end()
```

### packer style

```lua
require('pack').setup(function(use)
  use 'junegunn/fzf.vim'
  use {'junegunn/fzf', do = 'call fzf#install()' }
  use {'neoclide/coc.nvim', branch = 'release'}
  use {'neoclide/coc.nvim', branch = 'master', do = '!yarn install --frozen-lockfile'}
  use {'vlime/vlime', rtp = 'vim' }
  use {'dracula/vim', as = 'dracula' }
  use {'tpope/vim-fireplace', for = 'clojure' }
end)
```

You additionally need to download the lua extension and put it in the `lua`
directory as follows.

```
curl -fLo ~/.config/nvim/lua/pack.lua --create-dirs \
    https://raw.githubusercontent.com/tani/jetpack/master/pack.lua
```

## Q & A

### Why is this plugin so fast?

Because we bundle the all plugins as possible to reduce runtimepath, which takes
a long time at startup. This is the same algorithm of the plugin manager
dein.vim.

### Is this plugin faster than dein?

No if you are vim-wizard. Dein provides many option to tune the startup. This is
a trade-off. Dein takes milli-seconds to do many things. Our plugin do as the
same as the vim-plug, i.e., this plugin provides less feature than dein.

## Copyright and License

Copyright (c) 2022 TANIGUCHI Masaya. All rights reserved.

This software is licensed under the MIT License.
