---
layout: post
title: "pkgutil的使用"
date: 2014-03-23 09:45
comments: true
categories: 
---
> 最近用pkg格式的文件安装了几个mac软件，但是这种安装方式的软件都是一些需要在root用户的文件里创建一些文件的安装包

> 网上找了一些其他的方法来管理这些文件，发现`pkgutil`这个命令还是很有用的，下面做一些简要的介绍，以作备忘

- `pkgutil` --pkgs 显示已经安装在系统上的软件包
- `pkgutil` --files PKGID 显示某个软件包安装的文件列表
- `pkgutil` --unlink PKGID 删除该软件包创建的文件（但不会从包管理数据库中移除软件包信息）
- `pkgutil` --forget PKGID 从包管理数据库中移除软件包信息（但不会删除该软件包创建的文件）



####想卸载一个软件时
    先用 `pkgutil --pkgs` 列出你所安装的软件列表，找到你要卸载的包名
    在用 `pkgutil --files PKGID` 查看此软件所产生的文件，一般在`/usr/local`里
    在用 `pkgutil --unlink PKGID` 删除所产生文件
    最后 `pkgutil --forget PKGID` 从包管理中删除此软件包信息
    
- PS 一般还会有一些配置信息，有耐心的找找吧，一般在`/etc`这个文件夹里
