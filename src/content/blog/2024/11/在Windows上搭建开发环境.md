---
author: yshhuang
pubDatetime: 2024-11-15
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

#### 插件

[VSCode Great Icons](https://marketplace.visualstudio.com/items?itemName=emmanuelbeziat.vscode-great-icons):我个人最喜欢的一套文件图标。

[Dracula Theme Official](https://marketplace.visualstudio.com/items?itemName=dracula-theme.theme-dracula)：鼎鼎大名的德古拉主题配色，支持多种编辑器和shell。

[Markdown Preview Enhanced](https://marketplace.visualstudio.com/items?itemName=shd101wyy.markdown-preview-enhanced):功能非常强大的Markdown增强插件,支持幻灯片、电子书、LaTeX……

[background](https://marketplace.visualstudio.com/items?itemName=shalldie.background)：自定义VSCode的背景图片。

#### 设置

Windows下的配置文件位于`~/AppData/Roaming/Code/User/settings.json`。

```json
// 编辑器字体大小
"editor.fontSize": 16,
// 终端模拟器的字体大小
"terminal.integrated.fontSize": 16,
// 整个软件的缩放,可以放大侧栏的文字
"window.zoomLevel": 0.4,
// 无障碍支持,开启后会多很多提示音,直接关掉即可
"editor.accessibilitySupport": "off",
// 如果不想关闭无障碍支持,可以通过这个设置关闭提示音
"accessibility.signalOptions.volume": 0,
// 关闭编辑器右侧的缩略图
"editor.minimap.enabled": false,
// 设置默认的shell
"terminal.integrated.defaultProfile.windows": "Git Bash",
```

### 微信输入法

之前用了好多年的搜狗输入法，非常喜欢它可以展示多行候选词的功能，后来不知道哪次更新把这个功能去掉了，而且各种乱七八糟的工具都被捆绑到输入法里面，看着十分讨厌。后来发现微信也做了一个输入法，完美满足我的需求，所以就切换到了微信输入法。

### 系统字体

Windows系统默认的字体太糟糕了，使用[MacType](https://www.mactype.net/)进行修改，可以在Windows上获得接近Mac的字体体验。

### Nodejs

以前给别人打工的时候，我没得选，只能使用公司要求的技术栈。现在灵活就业了，我终于可以自由选择自己喜欢的技术。对于个人开发者来说，JavaScript最大的优势在于，它什么都能干。最拿手的web开发自不必说，还可以使用electron开发桌面客户端；ionic或React Native开发移动端；nodejs开发服务端或者写一些脚本；cocosjs开发游戏；开发小程序、快应用；各种软件的插件大多也是使用JavaScript开发（例如chrome和Microsoft edge等浏览器，VSCode、Microsoft Office、Photoshop……）；最近几年开始流行的serverless也是默认支持nodejs。

对于个人开发者来说，一是时间精力有限，熟练掌握并主要使用一门语言，是投入产出比最高的；二是个人开发的项目相对比较简单，对性能的要求没那么高，所以也就不需要在每个领域都选择最合适的语言，JavaScript虽然在很多领域不是最好的语言，但是却能完成大多数任务，省去了配置多种开发环境和在不同语言之间切换思维模式和语法的成本，对于个人的开发效率提升有很大帮助。

#### 安装fnm

`nodejs`版本更新比较频繁，而且很多项目可能依赖不同的`nodejs`版本，所以使用版本管理工具来安装`nodejs`就很有必要。在所有的`nodejs`版本管理工具中，`fnm`（Fast Node Manager）因其快速、跨平台的特性而大受欢迎。根据[nodejs官网的指示](https://nodejs.org/en/download/package-manager)，在`PowerShell`环境中下载安装：

```bash
  1. winget install Schniz.fnm
  2. fnm env --use-on-cd | Out-String | Invoke-Expression
```

第一步下载`fnm`一般没什么问题，但是第二步在设置环境变量的时候就出现问题了，会提示无法识别`fnm`命令。其实第二步的命令不是在`PowerShell`里执行，而是要写到`PowerShell`的配置文件里:`%USERPROFILE%\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1`。具体的文件路径可以在`PowerShell`里执行 `echo $profile`查看。[^3]

修改完`PowerShell`的配置文件后再打开`PowerShell`可能会提示“*无法加载文件……profile.ps1*”，需要修改安全策略。以管理员身份打开`PowerShell`，执行命令`Set-ExecutionPolicy -ExecutionPolicy RemoteSigned`，再次打开`PowerShell`窗口，执行命令`fnm --version`，显示`fnm`的版本号，说明安装成功了

在`PowerShell`里配置`fnm`比较麻烦，还可以在`Git Bash`里使用`fnm`，配置起来比较简单，只需要在`%USERPROFILE%\.bash_profile`文件中写入如下内容即可：

```bash
# 配置fnm
eval "$(fnm env --use-on-cd)"
```

## WSL开发环境

------------
*参考资料:*
[^1]:[Shell、Bash、CMD、PowerShell 的区别](https://blog.csdn.net/qq_33154343/article/details/123366377)
[^2]:[Windows下的Git Bash配置，提升你的终端操作体验](https://zhuanlan.zhihu.com/p/418321777)
[^3]:[Node.JS 版本管理工具 Fnm 安装及配置（Windows）](https://blog.csdn.net/Y2ANGAO/article/details/142653309)
