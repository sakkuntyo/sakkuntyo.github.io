---
layout: post
title: minicondaでpython3をインストール
date: 2020-02-09 04:52:22
tags: [miniconda]
---

anacondaとは、データサイエンティスト向けのpythonパッケージを含んだパッケージマネージャの様な物です。

そのため、沢山のツールがインストールされてしまうため、
3GBの容量を使用してしまったり、
プラットフォームに予めインストールされている実行ファイルとの競合を起こす事があります。

minicondaとは、anacondaからそれらのパッケージを除外したパッケージマネージャが主な機能となります。

# 環境

- Ubuntu 18.04

# 手順

## minicondaをインストールする

```bash
$ wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh

$ ./Miniconda3-latest-Linux-x86_64.sh
この後、以下操作でインストールが完了します。
1.Enter
2.yesを入力後、Enter
3.Enter
4.yesを入力後、Enter

bashを再起動
$ exec $SHELL -l
```

インストール中に、以下の様なリストが表示されますが、これらのツールも同時にインストールされます。

```bash
The following NEW packages will be INSTALLED:                                           
                                                                                        
  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main                         
  asn1crypto         pkgs/main/linux-64::asn1crypto-1.2.0-py37_0                        
  ca-certificates    pkgs/main/linux-64::ca-certificates-2019.10.16-0                   
  certifi            pkgs/main/linux-64::certifi-2019.9.11-py37_0                       
  cffi               pkgs/main/linux-64::cffi-1.13.0-py37h2e261b9_0                     
  chardet            pkgs/main/linux-64::chardet-3.0.4-py37_1003                        
  conda              pkgs/main/linux-64::conda-4.7.12-py37_0                            
  conda-package-han~ pkgs/main/linux-64::conda-package-handling-1.6.0-py37h7b6447c_0    
  cryptography       pkgs/main/linux-64::cryptography-2.8-py37h1ba5d50_0                
  idna               pkgs/main/linux-64::idna-2.8-py37_0                                
  libedit            pkgs/main/linux-64::libedit-3.1.20181209-hc058e9b_0                
  libffi             pkgs/main/linux-64::libffi-3.2.1-hd88cf55_4                        
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-9.1.0-hdf63c60_0                     
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-9.1.0-hdf63c60_0                  
  ncurses            pkgs/main/linux-64::ncurses-6.1-he6710b0_1                         
  openssl            pkgs/main/linux-64::openssl-1.1.1d-h7b6447c_3                      
  pip                pkgs/main/linux-64::pip-19.3.1-py37_0                              
  pycosat            pkgs/main/linux-64::pycosat-0.6.3-py37h14c3975_0                   
  pycparser          pkgs/main/linux-64::pycparser-2.19-py37_0                          
  pyopenssl          pkgs/main/linux-64::pyopenssl-19.0.0-py37_0                        
  pysocks            pkgs/main/linux-64::pysocks-1.7.1-py37_0                           
  python             pkgs/main/linux-64::python-3.7.4-h265db76_1                        
  readline           pkgs/main/linux-64::readline-7.0-h7b6447c_5                        
  requests           pkgs/main/linux-64::requests-2.22.0-py37_0                         
  ruamel_yaml        pkgs/main/linux-64::ruamel_yaml-0.15.46-py37h14c3975_0             
  setuptools         pkgs/main/linux-64::setuptools-41.4.0-py37_0                       
  six                pkgs/main/linux-64::six-1.12.0-py37_0                              
  sqlite             pkgs/main/linux-64::sqlite-3.30.0-h7b6447c_0                       
  tk                 pkgs/main/linux-64::tk-8.6.8-hbc83047_0                            
  tqdm               pkgs/main/noarch::tqdm-4.36.1-py_0                                 
  urllib3            pkgs/main/linux-64::urllib3-1.24.2-py37_0                          
  wheel              pkgs/main/linux-64::wheel-0.33.6-py37_0                            
  xz                 pkgs/main/linux-64::xz-5.2.4-h14c3975_4                            
  yaml               pkgs/main/linux-64::yaml-0.1.7-had09818_2                          
  zlib               pkgs/main/linux-64::zlib-1.2.11-h7b6447c_3
```

## pythonがインストールされている事を確認

```bash
$ python -V
Python 3.7.4
```

## pipがインストールされている事を確認

```bash
pip -V
$ pip 19.3.1 from /root/miniconda3/lib/python3.7/site-packages/pip (python 3.7)
```

## アンインストール

~/miniconda3フォルダ以下に全てインストールされるため、以下できます。

```bash
$ rm -r ~/miniconda3

bashを再起動
$ exec $SHELL -l
```
