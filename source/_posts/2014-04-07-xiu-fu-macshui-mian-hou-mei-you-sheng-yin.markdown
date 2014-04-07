---
layout: post
title: "修复mac睡眠后没有声音"
date: 2014-04-07 19:55
comments: true
categories: 
---

电脑没关的习惯，所以出去有事也是不关机的，很多时候电脑就睡眠了，可是mac有个问题就是睡眠后唤醒就没有声音了，以前都是重启就解决，可是开了很多东西又不想关，后来上网去搜索了一下，找到了一个帖子

在贴吧找到的这个方法，还算不错，我自己记录一下原帖在这里[〔技术向〕Mac唤醒后无声的终极解决方法——脚本大法][1]

[1]:http://tieba.baidu.com/p/2865826102

具体命令是这几个
```
➜  ~  sudo kextunload /System/Library/Extensions/AppleHDA.kext
Password:
➜  ~  sudo kextload /System/Library/Extensions/AppleHDA.kext 
```
这样我的电脑就有声音了，我没有按照贴吧的说。。。我就直接写了一个两行脚本。。。本人比较懒

如果有兴趣可以按照贴吧里的方法试试，我自己执行了那两条命令成功修复，不过不知道苹果啥时候修复这bug。
