---
author: yshhuang
pubDatetime: 2024-11-05
title: 在Windows上搭建开发环境
featured: false
draft: false
tags:
  - 开发环境
description:
  开发机器的选择以及在win10上搭建好用的开发环境
---
“工欲善其事，必先利其器”，对于软件开发来说，好的开发环境能提升开发者的效率和开发体验。开发环境包括外在环境，硬件设备和软件，这篇博文主要是记录一下我自己在Windows上搭建开发环境的过程和一些注意事项，以后如果换电脑了可以依据这边文章来重新配置。
至于为什么选Windows?三大主流系统（Windows，macOS，Linux）我都用过，Linux开放、自由、有好用的命令行工具，但是生态太差，比如我在开发中可能会用到一些工具软件，如vpn、网盘，有些在Linux上找不到好的替代品；macOS有好用的命令行和相对丰富的软件，颜值也很高，缺点主要是太贵了以及封闭性太强了。

所以我最后选择了Windows，Windows系统毫无疑问是软件生态最丰富的，不仅如此，它还可以通过`WSL`来使用Linux的命令行，通过[Docker-OSX](https://github.com/sickcodes/Docker-OSX)来体验macOS系统。其实，操作系统的选择还要考虑开发软件的类型，如果只开发服务端并且很少使用除开发之外的其他软件，Linux非常适合。如果要开发桌面端软件，则需要对应的操作系统，而Linux的用户群体很小，通常不作为优先考虑。总而言之，三大系统各有其优势和使用场景，但是如果手上只能有一个主力设备，考虑到价格和灵活性，Windows电脑才是最优选。它虽然在某些方面做的不如Linux或者macOS好，但是胜在能力全面，什么都能做。

## 本地开发环境
Windows本地开发环境主要是为了开发Windows桌面端程序，如果没有此类需求，也可以直接使用WSL。

### Git Bash
Windows上的命令行软件，不管是自带的`命令提示符/cmd.exe`、`Windows PowerShell`，还是微软强推的[PowerShell](https://apps.microsoft.com/detail/9mz1snwt0n5d)，都不符合我的使用习惯。[^1]为了获得接近Linux和Mac上命令行的使用体验，我选择了[Git Bash](https://git-scm.com/downloads/win)作为Windows上的默认shell。

`Git Bash`默认的提示符太长了，显示用户名和主机名完全没有必要，我个人更喜欢简短一些的。修改家目录下的`.bash_profile`，写入如下内容
```bash
 export PS1="\[\033[01;34m\]\W\[\033[00m\]👉 "
```
提示符就改为仅显示当前目录名加一个表情符号。

### Windows Terminal
`Git Bash`本身自带一个终端，但是这个终端只支持`Git Bash`一种命令行解释器，而且功能比较简单。Windows上的终端模拟器，最好用的当属微软自家的[Windows Terminal](https://www.microsoft.com/store/productId/9N0DX20HK701)，它的特点有：多标签页支持，自定义外观，丰富的扩展性。从微软应用商店下载安装即可。

安装好之后，在**设置->启动->默认配置文件**那里选择`Git Bash`,以后打开`Windows Terminal`标签页，即默认使用`Git Bash`命令行。[^2]为了使用更加方便,可以在家目录下的`.inputrc`加入以下2行配置:
```bash
set bell-style none
set completion-ignore-case on
```
前者可以避免没有输入内容按退格键的时候终端窗口闪烁；后者是按tab键自动补全的时候忽略大小写。
### VSCode

### 微信输入法

### 系统字体

## WSL开发环境



[^1]:[Shell、Bash、CMD、PowerShell 的区别](https://blog.csdn.net/qq_33154343/article/details/123366377)

[^2]:[Windows下的Git Bash配置，提升你的终端操作体验](https://zhuanlan.zhihu.com/p/418321777)