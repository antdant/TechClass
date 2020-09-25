---
layout: post
title: "我给VSCode报了个bug，微软工程师竟然凌晨修复了..."
date:   2020-9-23
tags: [geek]
comments: true
author: lemonchann
---

**本文首发个人微信公众号**，[点击阅读原文](https://mp.weixin.qq.com/s?__biz=MzIwMjM4NDE1Nw==&tempkey=MTA4MF9xZTIzY1RYU3VDNnBpN1NNVFNfQnNsSVZGcW45aXRKYWozSmU2YnJ4LWpZenJjQzk2V29mR0dycktyTlJ1R0IzRmZwdkdqYnZRbU9BR2VUNGJDbTJHcmZFaERfQTR5S0tzRzl6TmVfLW5GQnV0bnNQbk1TNFN6N2NxbkxodFRNSGhySVBHT0tYVEZOdWcyNHB1QXBBYjFZeFg1cWV1WWo1OGhNUVNBfn4%3D&chksm=16de3d9d21a9b48b34bc3edab98c180e3105c5fab8495a5cc5a51eaafdb9aacc04387caee3bf&__mpa_temp_link_flag=1&token=574085929#rd)

最近遇到一个有意思的bug，是关于VSCode编辑器插件的，最近赶项目时间非常紧，说实话在这时平常用的顺手的IDE出问题非常影响心情。**这就像是你开在高速路上，吃着火锅唱着歌，突然轮胎爆了，你说气不气人**。

不过在找bug和推动修复bug的过程有点意思，**通过一系列尝试最终定位和复现了bug，并且给这个项目的微软官方仓库提了issue，最终在最新版本得到了修复，把这个有趣的过程分享给大家**。

**也给大家演示一下如何通过提 issue 的方式参与到开源项目中**，当然，参与开源项目的方式有多种，**你可以给项目贡献源码，甚至作为大使帮助推广项目，找到项目的bug进而提issue也是一种参与方式**，总之先参与进来，才能发现开源的乐趣！

## 诡异的报错

上周，又是一个在公司的夜晚，好像和平常没啥区别，柠檬哥在加班ing，飞快的敲打着自己的机械键盘，熟练的用 VSCode 浏览着项目源码，顺手按下`F12+Shift` 想看看这个函数在哪些地方被引用了，诡异的事情发生了，这VSCode它竟然不听使唤了，查不出引用的结果了，并且终端提示如下错误：

```shell
快速信息操作失败: FE: 'Compiler exited with error - No IL available'
快速信息操作失败: FE: 'Compiler exited with error - No IL available'
```

一开始我以为是单个工程解析问题，**不慌，问题不大**。

后来换了个工程尝试，**不论我如何的反复摩擦我洁白的键盘帽，始终不能出来查找引用的结果界面**，这时才发现，粗大事了。工欲善其事必先利其器，虽然进度有点赶，还是停下来康康是谁在捣鬼？

 ![](https://i02piccdn.sogoucdn.com/2a072b9c2bde3535) 

**老读者应该知道我的开发环境都是远程开发环境，之前我写过几篇介绍如何用VSCode搭建远程开发**，以及配置开发环境的文章，可以说是VSCode重度爱好者，感兴趣我是怎么远程开发的可以了解下历史文章：

[文章1](https://mp.weixin.qq.com/s?__biz=MzIwMjM4NDE1Nw==&mid=2247486237&idx=1&sn=d2e4e4f7bccbd7c84417d1e8eb7e4911&chksm=96de3d6fa1a9b4792a260433922feec563dcb5ec5dd05ddafd527e27b12c390367054c38d02d&token=1873619493&lang=zh_CN#rd)

[文章2](https://mp.weixin.qq.com/s?__biz=MzIwMjM4NDE1Nw==&mid=2247486237&idx=1&sn=d2e4e4f7bccbd7c84417d1e8eb7e4911&chksm=96de3d6fa1a9b4792a260433922feec563dcb5ec5dd05ddafd527e27b12c390367054c38d02d&token=1873619493&lang=zh_CN#rd)

继续前面说的，如果不能查找引用的话，那会对编码和阅读源码带来很大的不便，**这个功能算的上是IDE的基础功能了，如果连这功能都废了，那我要你这VSCode有何用**？如果不能修复的话我估计要跑抛弃它，用回 Visual Studio 或 CLion。

但是VSCode远程开发是真的香，并且已经习惯了VSCode操作，在放弃之前还想挣扎下，看还能不能抢救？不过如果实在不行，也没时间死磕，项目还要继续，大不了换个 IDE 继续玩，甚至都想好了以面再也不说VSCode香了。

 ![](https://i02piccdn.sogoucdn.com/a92363242e8f23f9) 



## 一起来找bug呀

虽然这个插件不是我写的，但我按照一般程序员排查bug的思路，通过下面几个步骤一步步来找到问题原因，最终并推动官方的版本更新来修复，一起来看看吧。

### 软件问题？

**首先，来看看是不是VSCode版本升级导致的问题**。按下面的操作，我检查 VSCode 的版本信息。

![](https://github.com/lemonchann/images/raw/master/tools/vscode_bug_find/查看版本.png)

仔细核对版本号和官网的区别，对比问题出现的时间前后都没有升级过新版本。

OK，**应该不是 VSCode 版本升级导致的问题**。

![](https://github.com/lemonchann/images/raw/master/tools/vscode_bug_find/VSCode版本确认.png)

### 配置问题？

既然不是 VSCode 升级版本导致的问题，那就奇了怪了，白天还好好的晚上突然咋就不行了呢？难道这插件也不想加班了？我陷入了沉思，不过马上灵机一动，**会不会小心改了C++环境配置文件出了问题**？

**这里有个知识点记下，要考**。VSCode中有一个叫`c_cpp_properties.json`的配置文件，这个文件主要用于配置C/C++工程的基础信息，比如：**预定义宏、指定编译器路径、预定义头文件搜索路径等**。

```json
{
    "configurations": [
        {
            "name": "Linux",
            "includePath": [
                "${workspaceFolder}/**",
                "/lemon/handsome/thirdparty/**",
                "/lemon/smart/inc/**"
            ],
            "defines": [], 
            "compilerPath": "/usr/bin/gcc",
            "cStandard": "c11",
            "cppStandard": "c++14",
            "intelliSenseMode": "gcc-x64"
        }
    ],
    "version": 4
}
```

机智如我，肯定是这个工程的`include` 搜索路径配置的有问题，才导致查找引用失败了，赶紧去检查一眼配置文件，于是熟练的敲下`Ctrl+Shift+P` **查找所有命令和配置**（**敲黑板！这个命令很常用，背下来**），输入关键字`c++ Edit` 果然匹配到了配置文件，打开就是上面的配置文件。

![](https://github.com/lemonchann/images/raw/master/tools/vscode_bug_find/cpp_json.png)

但是看起来文件路径好像是对的，不管了，死马当活马医，先全部删除重新配置一遍看看效果，一顿操作之后兴奋的检查有没有用，然并卵，还是那个该死的提示` FE: 'Compiler exited with error - No IL available'`，心态有点崩。


  ![img](https://i04piccdn.sogoucdn.com/837ca3f1a6b9cc9b)  



### 环境问题？

发现这个问题确实有点诡异，走到这一步，**我几乎可以断定是Linux开发环境出了问题，但是不确定是我的机器环境问题还是 Linux下 VSCode 本身问题，那怎么办呢？先来证明是Linux下才出的问题吧**！

我就尝试不开远程开发模式，把远程Linux机器上的工程直接拉到宿主机本地文件夹，然后用VSCode打开宿主机上的本地工程，**它竟然工作的很好，完全没有出现什么错误提示，到这，已经完全可以确定这个bug只在Linux环境下出现了**。

**夜已深，起来喝杯水，看了下时间，加班班车快到末班了。**

 ![img](https://i03piccdn.sogoucdn.com/19bd21cf691b2a0f)

事已至此，看来真的要关掉远程开发，在本地重新配置所有工程了，表面上还是劝自己再找找原因，没事，问题不大。

 

### 插件问题？

喝完水，我坐下来继续想，**会不会是C++扩展出了问题呢？大家都知道VSCode只能说是一个编辑器，能够让他变身C++ IDE完全是有背后的C++插件或者叫扩展的支持**。

就是下面黑黑的这货，它是VSCode能够支持C++开发背后的男人，众所周知VSCode是微软亲儿子，看看这个插件作者`Microsoft` 看来也是微软自家人开发的插件，发布之前肯定是经过严格测试的，问题不大。

![](https://github.com/lemonchann/images/raw/master/tools/vscode_bug_find/C++扩展.png)

不过现在谁也不能相信，即使是微软自家的插件也不能信任了，假装冷静分析一波。

 ![img](https://i04piccdn.sogoucdn.com/144531647594eff3) 

经过严谨的思考（然而并没有），最终决定拿出程序员必杀技：**重启试试，卸载重装**。

点击卸载，卸载完成，点击安装，重装完成，重启加载，一气呵成。

兴奋的搓小手手，准备再次见证奇迹，WTF，问题依旧没能解决，实话告诉大家，做到这个份上，柠檬哥可以说是已经非常的绝望了。

 ![img](https://i01piccdn.sogoucdn.com/466081e15ab9e449) 



## 正道的光

### 真相只有一个

不管了先回去睡一觉，梦里啥都有，没准第二天白天又有了新思路。

果然第二天我又有了新想法，虽然卸载重装插件没用，但我们程序员还有最后一招：**回退版本**！

是时候表演真正的技术了，**资深程序员肯定懂的，常在河边站哪有不湿鞋，版本发布出问题，赶紧回退保命是常规操作**。

 ![img](https://i01piccdn.sogoucdn.com/483ea665b3bf43c5) 

那我们就有理由怀疑：**微软在发布这个插件最新版本的的时候把一个重要特性搞掉了**。但是这东西发都发出去了，也不是服务端后台服务说回退就能回退的，这个插件如果真是bug也只能等下一个版本修复，还是我们自己来操作回退吧。

找到插件，按下面方法来执行回退操作：

![](https://github.com/lemonchann/images/raw/master/tools/vscode_bug_find/安装低版本.png)

柠檬当时回退的时候还没有出最新的修复版本，装的是有问题的1.0.0版本的插件，**看这个版本号应该是个较大改动的大版本，出问题也正常**。

关键是**可以看到这个版本的发布时间点刚好是我发现bug的时间**，这回感觉离真相越来越近了，至少在时间上是吻合的有底气了点，那有理由怀疑是这个插件出了问题，回退到上一个稳定版本0.29.0

![](https://github.com/lemonchann/images/raw/master/tools/vscode_bug_find/选择插件安装版本.png)

**这次奇迹真的出现了，「查找引用功能」它回来了**！而且也没有出现`FE: 'Compiler exited with error - No IL available'`的报错提示，为了进一步确认自己的判断，我又把插件升级到1.0.0版本（稳了），果然又出现了刚才的问题。

**至此，这个bug算是定位成功，并且可复现验证，暂时的解决方法是回退到上一个稳定版本**。



### 离线安装

另外提醒一下，公司其他同学也遇到这个问题，我在帮其他同学解决这个问题的时候，发现有些人直接升级可能会有网络问题，导致在线升级不了，报错：

![](https://github.com/lemonchann/images/raw/master/tools/vscode_bug_find/自动升级下载失败.png)

这时候可以去上面我发的官网下载离线版本插件安装包，下完之后，按照下面的操作升级即可，效果和在线升级一样。

![](https://github.com/lemonchann/images/raw/master/tools/vscode_bug_find/离线安装插件步骤.png)

注意了，由于一些众所周知的原因，**如果你打不开官网或者下载速度很慢，可以加文末我个人微信，备注「下载插件」我发给你已经下载好的插件**。



## 推动版本更新

### 提issue报bug

这就完了吗？当然不是。**费了我这么大功夫找出来的bug，不要再浪费其他人时间了，所以我决定去微软这个插件的官方仓库去给他们提 ` issue`**，这里给不了解 Github 开源项目的同学科普下什么是` issue` ? **上课了，看黑板**！

> Github项目的 issue 用于团队协作管理，可以把将要实现的 feature 或者要修复的 bug 通过提 issue的形式记录下来，所以我们如果发现开源项目的bug，可以通过给开源项目提issue的形式报告这个bug，提醒项目团队修复跟进。 

这里给出微软官方C/C++ 插件的github仓库地址：https://github.com/microsoft/vscode-cpptools

我去写下了下面这个issue ，虽然是英文描述的，大家应该都能看得懂我就不逐字翻译了，计算机相关的英文来回就那么几个单词，看多了就会写，大意就是描述了我遇到的bug和问题出现时的环境配置信息，方便他们定位和复现问题。

issue 标题： `C/C++ Extension 1.0.0 some feature Not working When using in Remote-SSH remote development #6176`

![issue描述](https://github.com/lemonchann/images/raw/master/tools/vscode_bug_find/issue描述.png)

并且详细描述了我遇到的问题，其实经过上面一顿操作，柠檬肯定是他们这个版本有问题，**但还要友好沟通推进问题尽快解决才是目的，写代码的何苦为难写代码的**，没有直接说他们有问题，而是委婉的问了下 `  I wonder if there is a problem with this latest Extension ? ` 哈哈

### 完美解决

我提issue的时候是中午吃饭的时候12点左右，那时美国那边应该还是凌晨，我想肯定没这么快有回复了，国外程序员小哥都还在睡觉呢，怎么也得早上上班才能看到之后回复，**但是万万没想到在下午5点左右就收到了回复，果然神速**。

![](https://github.com/lemonchann/images/raw/master/tools/vscode_bug_find/issue交流.png)

**不过，等等，好像哪里有点不对劲**，注意上面图中具体时间已经没显示了，只是显示一个 `2 days ago`，在我看到消息通知的时候有点诧异处理这么神速，好奇去翻开处理issue老哥的 github 主页介绍。

回复的这位是微软`VS Code C++ Extension`的软件开发工程师，然后定位是美国的`Redmod, WA` ，特意去查了当时的美国时间是`05:03`，这位老哥是在凌晨5点钟处理的这个bug。。。**这也太优秀了吧，果然大佬们都是半夜写代码不用睡觉的，看到凌晨五点的太阳我信了**。

![](https://github.com/lemonchann/images/raw/master/tools/vscode_bug_find/所在地区美国华盛顿雷德蒙德.png)



## 复盘一下

**到了这里，这个bug从出现在我的机子上，到定位查找，最终修复算是完美的解决**。这里附上官方的版本链接：https://github.com/microsoft/vscode-cpptools/releases ，里面有提到本次修复的bug。

![](https://github.com/lemonchann/images/raw/master/tools/vscode_bug_find/%E7%89%88%E6%9C%AC%E6%9B%B4%E6%96%B0.png)

按照最新的1.0.0 版本发布说明，**如果你使用 Linux/MAC 版本的VSCode 或者像我这样用远程开发的方式从宿主机使用Linux版本，可能会遇到我文中说的bug**，我是在0.29.0自动升级到1.0.0发现的bug，于是给1.0.0版本报了个issue，微软官方在1.0.1版本修复了上述的bug，**一张图看清时间线**。

![](https://github.com/lemonchann/images/raw/master/tools/vscode_bug_find/版本列表.png)

柠檬在这里建议：**正在使用0.29.0版本插件的同学不升也没啥大问题，但如果你用的是1.0.0版本，那就要注意了，这个版本在本文描述的场景下是有问题的，还是及时升级到最新版本为好**。



## 技术公众号

文章首发个人技术公众号「**后端技术学堂**」，**目标是成为技术人的充电学堂**。

**欢迎扫码关注，分享、记录、成长！**

<p align="center">
<img src="https://github.com/lemonchann/images/raw/master/gzh/公众号二维码.png" width="300" height="300"/>
</p>

