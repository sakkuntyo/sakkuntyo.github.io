---
layout: post
title: Neovim + vim-plug + vim-lspでLanguage Server Protocolを利用
date: 2020-02-02 23:59:14
tags: [vim,Neovim,vim-plug,vim-lsp]
---

vim-lspをインストールする所まで
この手順では、python3.7.2をインストールするためにpyenvを入れています

# 環境

- Ubuntu18.04

# 手順

## Pythonとpipをインストールする

~/.bashrcに以下を追記する

```bash
## pyenv init and install
PYENV_ROOT="${HOME}/.pyenv/bin"
PATH="${PATH}:${PYENV_ROOT}"
pyenv --version > /dev/null || {
  git clone https://github.com/pyenv/pyenv ${HOME}/.pyenv
  sudo ${HOME}/.pyenv/plugins/python-build/install.sh
  pyenv install 3.7.2
  pyenv rehash
  pyenv global 3.7.2
}
eval "$(pyenv init -)"
```

~/.bashrcを読み込み直す

```bash
$ source ~/.bashrc
```

## Neovimをインストールする

~/.bashrcに以下を追記する

```bash
## neovim init and install
XDG_CONFIG_HOME="${HOME}/.config"
XDG_CACHE_HOME="${HOME}/.cache"
nvim --version > /dev/null || {
  sudo add-apt-repository ppa:neovim-ppa/stable -y
  sudo apt-get update
  sudo apt-get install neovim -y
  mkdir -p ${XDG_CONFIG_HOME}/nvim
  touch ${XDG_CONFIG_HOME}/nvim/init.vim
}
pip install neovim
```

~/.bashrcを読み込みなおす
```bash
$ source ~/.bashrc
```

## vim-lspをインストールする

~/.config/nvim/init.vimを以下の内容にする

```vimscript
if has('vim_starting')
  set rtp+=~/.vim/plugged/vim-plug
  if !isdirectory(expand('~/.vim/plugged/vim-plug'))
    echo 'install vim-plug...'
    call system('mkdir -p ~/.vim/plugged/vim-plug')
    call system('git clone https://github.com/junegunn/vim-plug.git ~/.vim/plugged/vim-plug/autoload')
  end
endif

call plug#begin('~/.vim/plugged')
  Plug 'junegunn/vim-plug',{'dir': '~/.vim/plugged/vim-plug/autoload'}
  Plug 'prabirshrestha/async.vim'
  Plug 'prabirshrestha/vim-lsp'
  Plug 'mattn/vim-lsp-settings'
call plug#end()
```

上記設定ではNeovim起動時にvim-plugが無ければインストール、
その後async.vim,vim-lsp,vim-lsp-settingsをインストールしています。

Neovimを起動

```bash
$ nvim
```

コマンド「:PlugInstall」を実行し、上記プラグインをインストールする

その後「:PlugStatus」を実行し、全てOKになっていれば問題なし、qキーでステータス画面を抜ける

nodejsやgolang、pythonのlspをインストールする場合は、
init.vimに設定を追記、必要なモジュールをインストールするなど、それぞれlspに合わせた設定が必要となる
