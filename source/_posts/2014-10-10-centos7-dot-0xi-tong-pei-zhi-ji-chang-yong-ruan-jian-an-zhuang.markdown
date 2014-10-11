---
layout: post
title: "CentOS7.0系统配置及常用软件安装"
date: 2014-10-10 14:21:29 +0800
comments: true
categories: 
---
## 概述

CentOS 7.0安装完成之后系统还比较裸, 需要修改一些配置, 安装一些常用软件之后才能方便的使用. 本文简单记录这些配置方法及如何安装常用的软件.

<!-- more -->
## 系统配置

1. 执行`ip addr`命令查看网络是分配了ip地址, 如果没有, 修改网卡配置文件. 网卡的配置文件为`/etc/sysconfig/network-script/ifcfg-网卡名`, 网卡名通过`ip addr`命令可以看到, 例如我的系统网卡配置文件为:`/etc/sysconfig/network-scripts/ifcfg-enp2s0`, 用vi打开它, 找到`ONBOOT=no`行, 将其修改为`ONBOOT=yes`, 修改完成后重启系统.

2. 修改yum源	
由于默认的yum源在境外, 网络状况不佳, 需要修改为国内科大镜像. 

		cd /etc/yum.repos.d/
		mv CentOS-Base.repo CentOS-Base.repo.bak
下载[科大镜像yum源配置文件](https://lug.ustc.edu.cn/wiki/\_export/code/mirrors/help/centos?codeblock=3), 上传到`/etc/yum.repos.d/`目录, 执行如下命令:    

		yum clean all
		yum makecache

3. 安装常用软件

		yum install wget lrzsz vim gcc gcc-c++ net-tools mlocate java autoconf openssl man-pages cmake unzip gdb ctags git telnet ntpdate zip 

4. 更新locate数据库

		updatedb

5. 查看当前时区

		date -R
如果不是+0800, 编辑`/etc/profile`, 在文件最后一行添加`TZ='Asia/Shanghai';export TZ`执行命令:

		source /etc/profile

6. 如果当前系统时间不准确, 执行同步时间命令:

		ntpdate asia.pool.ntp.org

7. 添加用户

		useradd username
		password username
根据提示设置密码

## vim环境配置

1. 下载bundle插件

		git clone  https://github.com/gmarik/vundle.git ~/.vim/bundle/vundle

2. 编辑~/.vimrc文件, 输入如下脚本:

		set nu
		set autoindent
		set tabstop=4
		set softtabstop=4
		set cindent
		set shiftwidth=4
		set enc=utf-8
		"set fenc=utf-8,ucs-bom,shift-jis,gb18030,gbk,gb2312,cp936
		syntax on

		"设置nerdtree
		map <F3> :NERDTreeMirror<CR>
		map <F3> :NERDTreeToggle<CR>

		"设置Ctrl+]
		map <F12> <C-]>

		"设置Taglist \{\{\{
		let Tlist_Show_One_File = 1	"不同时显示多个文件的tag,只显示当前文件的
		let Tlist_Exit_OnlyWindow = 1 "如果taglist是最后一个窗口,则退出
		let Tlist_Use_Right_Window = 1 "Taglist窗口显示在右边
		map <F9> :Tlist<CR>

		"\}\}\}

		"设置F7执行make
		map <F7> :make<CR>

		"vundle设置 \{\{\{
		set nocompatible "be iMproved
		filetype off

		set rtp+=~/.vim/bundle/vundle
		call vundle#rc()

		Bundle 'gmarik/vundle'
		"可以通过4种方式指定插件来源
		"a)
		"指定GitHub中vim-scripts仓库中的插件,直接指定插件名称即可,插件名中的空格使用"-"代替.
		Bundle 'L9'
		Bundle 'taglist.vim'
		Bundle 'scrooloose/nerdtree'
		Bundle 'xml.vim'
		Bundle 'FuzzyFinder'
		Bundle 'json.vim'
		Bundle 'pyflakes'
		Bundle 'Snipmate'
		Bundle 'AutoComplPop'

		filetype plugin indent on
		"\}\}\}

3. 打开vim，输入`:BundleInstall`,等待插件安装完毕

