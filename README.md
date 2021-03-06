<h1 align="center"> Vector's VIMRC memo </h1>


## Table of contexts

<!-- TOC GFM -->

* [Pre-requirements](#pre-requirements)
* [spell check usage](#spell-check-usage)
* [fzf in terminal](#fzf-in-terminal)
* [Plugins](#plugins)
  * [Markdown & Editor enhancement](#markdown--editor-enhancement)
    * [markdown-preview.nvim](#markdown-previewnvim)
    * [vim-markdown-toc](#vim-markdown-toc)
    * [vim-table-model](#vim-table-model)
    * [vim-surround](#vim-surround)
    * [vim-visual-multi](#vim-visual-multi)
    * [tabular](#tabular)
    * [bullets.vim](#bulletsvim)
    * [vim-move](#vim-move)
    * [auto-pairs](#auto-pairs)
  * [Visual enhancement](#visual-enhancement)
    * [vim-airline](#vim-airline)
    * [vim-deus](#vim-deus)
    * [vim-devicons](#vim-devicons)
    * [vim-xtabline](#vim-xtabline)
    * [rainbow](#rainbow)
    * [vim-illuminate](#vim-illuminate)
  * [Auto completion](#auto-completion)
    * [coc.nvim](#cocnvim)
    * [coc-snippets](#coc-snippets)
    * [vim-snippets](#vim-snippets)
  * [File navigation](#file-navigation)
    * [fzf.vim](#fzfvim)
    * [nerdtree](#nerdtree)
  * [vimtex](#vimtex)
  * [vista.vim -- TagList](#vistavim----taglist)
  * [Golang T.B.A](#golang-tba)
  * [Python T.B.A](#python-tba)
  * [Others](#others)
    * [coc-translator](#coc-translator)
    * [figlet](#figlet)
* [Some issues you may meet](#some-issues-you-may-meet)
  * [Build VIM from source via brew](#build-vim-from-source-via-brew)
* [To-do](#to-do)

<!-- /TOC -->

## Pre-requirements

1. `nodejs` - For coc.nvim.
    >curl -sL install-node.vercel.app/lts | bash

## spell check usage

- `<LEADER>sc` : enable spell check
- `C-x` : replace the bad word
- `<LEADER>-` : jump to the previous bad word
- `<LEADER>=` : jump to the next bad word

Auto enable spell check for `markdown` files.

>autocmd BufRead,BufNewFile *.md call SetSpell()

## fzf in terminal

The following command will install `fzf` binary and key bindings for MacOS.

```bash
brew install fzf
(brew --prefix)/opt/fzf/install
```
Here I just list some of my most commonly used usages.

- `C-t` : open interactive fzf in the current directory. Then insert some keywords for searching, `C-p`, `C-n` for moving and `<CR>` for selecting.

    ![fzf-C-T-example](https://image.i-ll.cc//uPic/20220123/kwOBDZ.png?imageMogr2/auto-orient/blur/1x0/quality/75|watermark/2/text/WmhhbyBDaGnigJhzIEJsb2c=/font/dGltZXMgbmV3IHJvbWFu/fontsize/240/fill/IzAwMDAwMA==/dissolve/75/gravity/SouthEast/dx/10/dy/10|imageslim)

- `C-r` : open interactive fzf for history commands with the same selection logic as `C-t`.
- **shell completion** : fzf use keyword `**` instead of `<TAB>` for shell completion.

  ![fzf-shell-completion-example](https://image.i-ll.cc//uPic/20220123/gs5lbL.png?imageMogr2/auto-orient/blur/1x0/quality/75|watermark/2/text/WmhhbyBDaGnigJhzIEJsb2c=/font/dGltZXMgbmV3IHJvbWFu/fontsize/240/fill/IzAwMDAwMA==/dissolve/75/gravity/SouthEast/dx/10/dy/10|imageslim)


## Plugins


### Markdown & Editor enhancement

Some snippets can be found at `./markdown-snippets.vim`. The following part show the usage of other markdown related plugins.

#### [markdown-preview.nvim](https://github.com/iamcco/markdown-preview.nvim)


- `<LEADER>b` : preview in a browser.
- You can add `toc` by one of the following flag.

  ```text
  ${toc}
  [[toc]]
  [toc]
  [[_toc_]]
  ```
- More example can be found in [doc](https://github.com/iamcco/markdown-preview.nvim).

Use [markdown-preview.nvim](https://github.com/iamcco/markdown-preview.nvim) instead of ~~[vim-instant-markdown](https://github.com/instant-markdown/vim-instant-markdown)~~.

I met some problems when I use [vim-instant-markdown](https://github.com/instant-markdown/vim-instant-markdown).

1. Auto scroll not work on `MacOS` and `WSL(Ubuntu 20.04)`.
2. `<LEADER>b` on `WSL` will cause a very weird problem -- everything in the current vim editor disappears inexplicably and when you move the cursor the contents will recover. Upgrading vim to 8.2 didn't make sense for this problem.
3. Cross reference can not work. (can not go to section from table of contents)

#### [vim-markdown-toc](https://github.com/mzlogin/vim-markdown-toc)

- `GenTocGFM` : Generate table of contents in GFM link style under the cursor.

`GenTocGFM` can be changed to `GenTocGitLab`.

#### [vim-table-model](https://github.com/dhruvasagar/vim-table-mode)

- `<LEADER>tm` : enable table model;
- `<LEADER>tdd` : delete row;
- `<LEADER>tdc` : delete column;
- `<LEADER>tic` : insert column;
- `[|` : move to the previous cell;
- `]|` : move to the next cell;
- `{|` : move to the left top corner of table;
- `}|` : move to the right bottom corner of table.
- `<LEADER>tt` : convert select part to table(only available in visual model)


#### [vim-surround](https://github.com/tpope/vim-surround)

- `ysiw'` : change `word` to `'word'`
- `ds'` : change `'word'` to `word`
- `cs"'` : change `"word"` to `'word'`

#### [vim-visual-multi](https://github.com/mg979/vim-visual-multi)

`<LEADER>` in my vimrc is `,`.
- `u` : undo
- `C-r` : redo
- `C-n` : select the next key
- `q` : skip and go to next
- `Q` : remove region under cursor
- `<Tab>` : switch between `Cursor Model` and `Extend Model`
- `C-Up` : add cursors up
- `C-Down` : ad cursors down
- `<LEADER>A` : select all words under cursor.

#### [tabular](https://github.com/godlygeek/tabular)

Simple usage: line up at `=`.

```text
:Tabularize /=
```
`=` can be changed to any signs.

More complex usage can be found at [tabular-doc](https://github.com/godlygeek/tabular/blob/master/doc/Tabular.txt).

#### [bullets.vim](https://github.com/dkarter/bullets.vim)

- `<leader>x` : set the current checkbox as completion.

#### [vim-move](https://github.com/matze/vim-move)

- `C-j` : move the current line down

#### [auto-pairs](https://github.com/jiangmiao/auto-pairs)

Auto pair for the following signs.
>\`\`, {}, [], (), '', ""

More complex usage please refer the [doc](https://github.com/jiangmiao/auto-pairs).


### Visual enhancement

#### [vim-airline](https://github.com/vim-airline/vim-airline)

Just install it without any extra configuration. When the plugin is loaded correctly, the status line should looks like this.

![vim-airline](https://image.i-ll.cc/uPic/20220122/NzrP33.gif)

#### [vim-deus](https://github.com/ajmwagar/vim-deus)

Need some configuration for pretty looking. Which can be found in `vimrc`.

![vim-deus](https://image.i-ll.cc//uPic/20220122/tgY4Yx.jpg)

#### [vim-devicons](https://github.com/ryanoasis/vim-devicons)

Need some pre-requirements

* [nerd-fonts](https://github.com/ryanoasis/nerd-fonts)
  ```shell
  brew tap homebrew/cask-fonts
  brew install --cask font-hack-nerd-font
  ```
Set your terminal font to `Hack Nerd Font Mono` or `Hack Nerd Font`. The following figure show the comparison between proportional font and monospaced font.

![comparison between proportional font and monospaced font](https://image.i-ll.cc//uPic/20220122/phEM1j.jpg)

#### [vim-xtabline](https://github.com/mg979/vim-xtabline)

Pretty the tab line;

![vim-xtabline](https://image.i-ll.cc//uPic/20220122/8QoT8A.png?imageMogr2/auto-orient/blur/1x0/quality/75|watermark/2/text/WmhhbyBDaGnigJhzIEJsb2c=/font/dGltZXMgbmV3IHJvbWFu/fontsize/240/fill/IzAwMDAwMA==/dissolve/75/gravity/SouthEast/dx/10/dy/10|imageslim)

- `to` : switch among the modes in the list ['tabs', 'buffers']
- `\p` : show the path of current file
- `N<BS>` : go to N-th tab, `N` is a number.

#### [rainbow](https://github.com/luochen1990/rainbow)

Show different level of brackets in different color!

![rainbow](https://image.i-ll.cc//uPic/20220122/YFLVjW.jpg)

**Note** : This plugin will cause some confliction with *Nerdtree*. We should add the following configuration to disable rainbow for nerdtree.
```vim
let g:rainbow_conf = {
\	'separately': {
\		'nerdtree': 0,
\	}
\}
```

#### [vim-illuminate](https://github.com/RRethy/vim-illuminate)

Highligh others words automatically under the current cursor.

```vim
" time in milliseconds
let g:Illuminate_delay = 500
```

### Auto completion

#### [coc.nvim](https://github.com/neoclide/coc.nvim)

The base of `coc.*` extensions. Requires [nodejs](https://nodejs.org/en/download/) >=12.12.

```bash
curl -sL install-node.vercel.app/lts | bash
```

- `<TAB>` : trigger completion, select next and jump to next like VSCode
- `<S-TAB>` : select previous and jump to previous like VSCode
- `<CR>` : select the first item in the candidate list
- `[g` : go to the previous diagnostic
- `]g` : go the the next diagnostic
- `gd` : go to the definition
- `gD` : go to the definition in a separate tab
- `dy` : go to type definition
- `gi` : go to implementation
- `gr` : go to reference
- `gh` : show documentation in preview window
- `<LEADER>rn` : rename the variable name
- `<LEADER>a` : do code action of selected region

#### [coc-snippets](https://github.com/neoclide/coc-snippets)

- `<TAB>` : trigger completion, select next and jump to next like VSCode
- `<S-TAB>` : select previous and jump to previous like VSCode.
- `C-e` : trigger snippet expand in `insert` mode.
- `C-s` : select the text under the visual placeholder of snippet in `visual` mode.
- `C-s` : expand snippet or jump(expand has higher priority).
- `<LEADER>x` : convert visual selected code to snippet.

#### [vim-snippets](https://github.com/honza/vim-snippets)

This repository contains snippets files for various programming languages. No extra configuration.

### File navigation

#### [fzf.vim](https://github.com/junegunn/fzf.vim)

The following shortcuts are working on **normal** mode.

- `C-p` : Show the files in current directory. By the way, you can use `:File [path]` to show the files in `[path]`.
- `<BS>` : Open the buffer list. (Because I set `<BS>` in **xtabline**, for someone don't want to set `<BS>` in **xtabline**, you can use `:Buffers` instead.
- `C-f` : Searching text in files under the current directory via [ripgrep](https://github.com/BurntSushi/ripgrep).

    ![ripgrep-search-example](https://image.i-ll.cc//uPic/20220123/260o2G.png?imageMogr2/auto-orient/blur/1x0/quality/75|watermark/2/text/WmhhbyBDaGnigJhzIEJsb2c=/font/dGltZXMgbmV3IHJvbWFu/fontsize/240/fill/IzAwMDAwMA==/dissolve/75/gravity/SouthEast/dx/10/dy/10|imageslim)

- `<LEADER>;` : Which is the simplification for command `:History`. **Note: no \<CR\> after :History**. Three cases here, [`<CR>`, `:<CR>`, `/<CR>`].
  - `<LEADER>;<CR>` : `:oldfiles` and open buffers.
  - `<LEADER>;:<CR>` : Command history.
  - `<LEADER>;/<CR>` : Searching history.

#### [nerdtree](https://github.com/preservim/nerdtree)

- `tt` : open the Nerdtree of current working directory.

    ![nerdtree-example](https://image.i-ll.cc//uPic/20220124/nCQB4L.png?imageMogr2/auto-orient/blur/1x0/quality/75|watermark/2/text/WmhhbyBDaGnigJhzIEJsb2c=/font/dGltZXMgbmV3IHJvbWFu/fontsize/240/fill/IzAwMDAwMA==/dissolve/75/gravity/SouthEast/dx/10/dy/10|imageslim)

- `o` : open the selected file in new tab.
- `?` : show/close the nerdtree help documentation.

### [vimtex](https://github.com/lervag/vimtex)

- `localLeader` : `,`
- `<localLeader>ll` : start or stop compiling the document
- `<localLeader>lk` : stop the compilation process
- `<localLeader>lv` : forward search, view the compiled PDF
- `<localLeader>lc` : clean the auxiliary files
- `<localLeader>le` : toggle the QuickFix menu
- `<localLeader>lt` : show table of contents, also show labels, can be used to jump to sections, labels, references and TODOs.
- `dse` : delete surrounding environment
- `cse` : change surrounding environment
- `tse` : toggle surrounding environment(toggle between `environment*` and `environment`)
- `<LEADER>c` : set conceallevel=1 -- better view for latex documents

    ![concealment-latex-code-example](https://image.i-ll.cc//uPic/20220205/eF21Gq.gif)

Note: If you use VIM and want to use `vimtex-synctex-inverse-search`, you should be aware that one may need to ensure that the server is really running. For OSX user, you should make sure you already install `XQuartz` and it is running and make sure your vim is support `clientserver` and `X11`.

### [vista.vim](https://github.com/liuchengxu/vista.vim) -- TagList

- `T` : toggle vista view window

### Golang T.B.A

### Python T.B.A

### Others

#### [coc-translator](https://github.com/voldikss/coc-translator)

- `ts` : translate the words under cursor or in the selected region.

#### figlet

**Installation**

```bash
brew install figlet
```

- `tx words` : insert the following lines to current buffer, `words` can be changed by yourself.

```text
                       _     
__      _____  _ __ __| |___ 
\ \ /\ / / _ \| '__/ _` / __|
 \ V  V / (_) | | | (_| \__ \
  \_/\_/ \___/|_|  \__,_|___/
                             
```


## Some issues you may meet

- [X] `bullets.vim` will cause selecting the first item in the candidate list via `<CR>` not work.
    >Using `<TAB>` instead of `<CR>`.
- [X] `cmd.exe` and `clip.exe` not work(i.e. can not access windows file system from WSL), which causes `<leader>b` not properly on WSL.
    >wsl.exe --shutdown
- [X] can not use `vimtex-synctex-inverse-search` with `zathura` and `vimTex`.
    >brew  install xquartz --cask # and build VIM from source via brew

### Build VIM from source via brew

```bash
brew edit vim
```
Change brew formula of vim like this.

```bash
system "./configure", "--prefix=#{HOMEBREW_PREFIX}",
                      "--mandir=#{man}",
                      "--enable-gui=gtk2",
                      "--with-features=huge",
                      "--with-client-server",
                      "--enable-multibyte",
                      "--with-tlib=ncurses",
                      "--with-compiledby=Homebrew",
                      "--enable-cscope",
                      "--enable-terminal",
                      "--enable-perlinterp",
                      "--enable-rubyinterp",
                      "--enable-python3interp",
                      #"--without-x",
                      "--enable-luainterp",
                      "--with-lua-prefix=#{Formula["lua"].opt_prefix}"
```


```base
brew install --build-from-source --formula /path/to/your/brew/formula/of/vim
```


## To-do

- [ ] windows/tabs management
- [ ] md-img-paste.vim
- [ ] pandoc with vim
- [ ] vim with tex (brew install --build-from-source --formula /path/to/your/formula) **need vim enable client-server**
- [ ] file navigation
  - [X] fzf
  - [ ] nerdtree

--------
- [ ] ranger
- [ ] git related
- [ ] vim-go
- [ ] python
