[TOC]



## プラグイン

#### endwise.vim

This is a simple plugin that helps to end certain structures automatically. In Ruby, this means adding end after if, do, def and several other keywords. In Vimscript, this amounts to appropriately adding endfunction, endif, etc. There's also Bourne shell, Z shell, VB (don't ask), C/C++ preprocessor, Lua, Elixir, Haskell, Objective-C, Matlab, Crystal, Make, Verilog and Jinja templates support.

A primary guiding principle in designing this plugin was that an erroneous insertion is never acceptable. **The behavior is only triggered once pressing enter on the end of the line.** When this happens, endwise searches for a matching end structure and only adds one if none is found.

While the goal was to make it customizable, this turned out to be a tall order. Every language has vastly different requirements. Nonetheless, for those bold enough to attempt it, you can follow the model of the autocmds in the plugin to set the three magic variables governing endwise's behavior.

https://zenn.dev/takuya/articles/2570f1f2025ce2298991#denite.nvim---ファイル検索



#### denite.vim

<kbd>;f</kbd>でファイル検索

<kbd>;r</kbd>でファイル内の単語を検索



#### defx.vim

open file <kbd>ctrl-f</kbd>

Create new file: <kbd>shift-N</kbd>
Delete file: <kbd>D</kbd>
Rename file: <kbd>R</kbd>



#### coc.nvim

vim環境にてインテリセンスを実現するためのプラグイン

オートコンプリーション、オートインポート、タイプ定義といった、IDEがよく備えている補助系機能を提供

カーソル下のタイプ定義を調べたい場合は、<kbd>shift-K</kbd>

定義元へとジャンプ<kbd>gd</kbd>

<kbd>ctrl-o</kbd>で前に戻



#### vim-fugitive

```
nnoremap [fugitive]  <Nop>
nmap <space>g [fugitive]
nnoremap <silent> [fugitive]s :Gstatus<CR><C-w>T
nnoremap <silent> [fugitive]a :Gwrite<CR>
nnoremap <silent> [fugitive]c :Gcommit-v<CR>
nnoremap <silent> [fugitive]b :Gblame<CR>
nnoremap <silent> [fugitive]d :Gdiff<CR>
nnoremap <silent> [fugitive]m :Gmerge<CR>
```

<kbd>gs</kbd> git status <kbd>gw</kbd> git write <kbd>gc</kbd> git commit

<kbd>gb</kbd> git blame <kbd>gd</kbd> git diff <kbd>gm</kbd> git merge



#### vim-react-snipets

https://github.com/mlaursen/vim-react-snippets#usestate

### 移動

ctrlT + HJKL

### NVIM

dw => delete the word + blank

de -> delete the only word

d$ => delete after the word



Ctrl v => tankei senntaku



r -> change the word

cw -> change the word 書き換え。置き換え。カーソルの後ろの文字は単語単位で消える。

c$

:! command => shell command available

### search and replace

:s/foo/bar/g

Find each occurrence of 'foo' (in the current line only), and replace it with 'bar'.

### vim-prettier

control + p -> prettier run

### lightline.vim

```
let g:lightline = {
      \ 'colorscheme': 'wombat',
      \ 'active': {
      \   'left': [ [ 'mode', 'paste' ],
      \             [ 'gitbranch', 'readonly', 'filename', 'modified' ] ]
      \ },
      \ 'component_function': {
      \   'gitbranch': 'FugitiveHead'
      \ },
      \ }
```

in case of using with describing error





cannot update nvim version due to the effect of other packages

to solve this issue, it needs some process. 

1. uninstall neovim

2. install neovim with below command

   ```
   sudo apt-add-repository ppa:neovim-ppa/stable
   sudo apt update // the version of neovim must the latest version. Check that.
   apt show neovim
   sudo apt -y install neovim
   ```

   ### Toml
   
   #### コメント
   
   ハッシュ記号（#）に続けて改行までをコメントとします。