大家好我是lemon，上次推送的文章，虽然不是技术文，但热度非常高，刚来的小伙伴可以点击这里「链接」，仅一天时间阅读数就达到 1000+ ，目前为止有 16 位土豪朋友赞赏，这也是写公众号这半年来收获点赞最多、赞赏最多的文章（作为一个技术号主，高赞竟然不是技术文，哭死）。

![](https://github.com/lemonchann/images/raw/master/tools/vscode_cpp_env/赞赏截图.jpg)

大家一定是知道我要开始还房贷了，压力太大想帮 lemon 分担一把，鞠躬感谢各位小伙伴的支持与认可，lemon 会坚持输出技术文章让自己和读者们都有收获。

话不多说，马上进入我们今天的主题吧。

## 又见VsCode

之前写过一篇文章详细介绍如何使用 VsCode 进行远程开发，VsCode 远程开发环境相对其他 IDE 的远程开发环境，实现了真正的远程开发，在本地主机（一般是Windows或MAC）上的操作的对象直接就是远程机（Linux），所有本地主机上的修改直接基于远端文件，摆脱了传统开发流程在本地编辑文件，利用FTP工具上传到远程编译机调试编译，这一套繁琐的操作，因此非常的方便。

那篇文章得到了各位读者的广泛好评，也被各大号转载 15 次之多，感兴趣的朋友看我原来这篇文章： [手把手教你配置VS Code远程开发工具，工作效率提升N倍](https://mp.weixin.qq.com/s?__biz=MzIwMjM4NDE1Nw==&mid=2247486006&idx=1&sn=f7953a700f32eefe16e5dfd8d3a9be26&chksm=96de3c44a1a9b552825bc90c3cd3c90f661d40dace0e19328b2cf77d06fcc522f6d898bd1f9d&token=240311464&lang=zh_CN#rd)。

这篇文章我会结合日常工作使用经验，教你打造一个体验流畅的 C/C++ 开发环境，这份配置指南可能不是面面俱到，也不会详细的教你一步步怎么配置插件，这些太细节的工作留给你自己去完成，实际上插件下载页都会有详细的说明。

不少新手可能会觉得 VsCode 编辑文本还好，看代码和写代码太难用，那是没有掌握正确的打开方式，VsCode 精髓是丰富的插件体系，相信看完这篇文章配置好环境之后，就只剩一句「真香」能形容。

  ![img](https://sorry.xuty.tk/cache/54574df0fb11c33586cdd011d1e9ed35.gif)  

为了有个直观的印象，先来看下我的 VsCode 插件列表，因为我用VsCode 开发 C/C++/Go/Python 程序，插件比较多，有些可能和本文无关的插件可以忽略掉。

![已安装插件](https://github.com/lemonchann/images/raw/master/tools/vscode_cpp_env/%E5%B7%B2%E5%AE%89%E8%A3%85%E6%8F%92%E4%BB%B6.png)

## 基础开发插件

既然是配置支持C/C++环境下开发，那首先推荐的基础 C/C++ 开发插件，以下两个是必须要装的插件，主要提供一些基础的代码调试和查看功能，安装以后 VsCode 就能支持智能化代码补全、类型填充和联想、符号和函数定义跳转、引用查找等 C/C++ 程序开发和源码管理必备能力，让你的 VsCode 从编辑器进化成 IDE 的基础插件。

![c_cpp_ext](https://github.com/lemonchann/images/raw/master/tools/vscode_cpp_env/c_cpp_ext.png)

![cpp_intellisense_ext](https://github.com/lemonchann/images/raw/master/tools/vscode_cpp_env/cpp_intellisense_ext.png)



## 源码阅读

程序员日常工作有两大内容，一个是写自己的代码，一个是阅读别人写的代码，下面这两个插件让你在 VsCode 优雅看代码。

**首先推荐的是下面的这个懒人神器 TODO Tree，自己写的 TODO 哭着也要补充实现。**

![TODO_tree_ext](https://github.com/lemonchann/images/raw/master/tools/vscode_cpp_env/TODO_tree_ext.png)

这个插件的使用场景是，你看完代码加了下面这个注释 ：`// TODO 以后会扩展这部分功能` 当然，不知道这个「以后」是什么时候，一不小心以后变成遥遥无期，一部分原因是不想改，另一部分原因是写下这段注释的人时间久了就忘记了，这时候你需要「 TODO Tree 插件」，我们可以更方便的管理代码中的此类注释。

这个插件能帮你组织和管理TODO 注释，你在代码中注释的带 TODO 的标签会统一在侧边栏显示出来，当然不限于 TODO 注释，可以自定义管理标签比如 `FIXME` 等，可以基于标签过滤和筛选。

**另一个推荐的源码阅读插件是 Bookmarks**

![bookmark_ext](https://github.com/lemonchann/images/raw/master/tools/vscode_cpp_env/bookmark_ext.png)

「书签」这个插件的功能就和它名字一样直接，没错它就是一个你的源码书签，当我们看大工程源码的时候，往往需要在成千上万个源文件之间跳转，此时 Bookmarks 能帮你方便的创建和管理书签，看到哪个位置想加个书签就按快捷键 `Ctrl + Alt + K` ，多按一次就是删除，不仅如此他还提供了在书签之前跳跃和查看管理的功能，更多功能可以自己体验，反正我看大工程源码用这个很爽。



## 代码管理

下面介绍两个 Git 版本控制相关的插件，项目中我们用的最多的版本控制工具是 Git ，当然 VsCode 自身提供了比较丰富的 Git 版本控制功能，基本上可以通过在界面点点点完成一些了Git 操作，但我今天要介绍的这两个插件能让你的 Git 更惊艳，算是对功能的增强，让你的 Git 操作更直观好用，好看的东西谁不喜欢呢？

**第一个出场的是Git Graph 插件，可视化Git仓库，让你的提交记录看起来美观大方，并且基于图中提交点提供了丰富的Git 操作。**

![git_graph_ext](https://github.com/lemonchann/images/raw/master/tools/vscode_cpp_env/git_graph_ext.png)

如图中你所见到的样子，提交记录变成一条条时间线，分支也能清晰的用不同颜色时间线区分出来，并且点开提交线上的提交点可以查看当时的提交动作，可以在提交动作上查看做了哪些改动，也可以方便的跳转到改动文件，更多功能自行体验，这个插件 lemon 强烈推荐！

**下面介绍的这个GitLens 插件也是Git功能增强工具。**

![gitLens_ext](https://github.com/lemonchann/images/raw/master/tools/vscode_cpp_env/gitLens_ext.png)

我最喜欢它的一个功能是，它可以在文件中改动的位置后面直接显示出本次改动的提交信息，然后你可以直接通过显示的提交信息跳转到提交文件对比，其实还有其他丰富的功能，不过这个功能我用的最多。



## 小而美的工具

下面这几个插件是我在日常使用中积累的工具插件，非必须，但是拥有了之后编码幸福感倍增，下面一一介绍给大家。

**第一个是下面这个Bracket Pair Colorizer插件，我管它叫彩虹括号插件。**

![color_bracket](https://github.com/lemonchann/images/raw/master/tools/vscode_cpp_env/color_bracket.png)

你是否为经常为写的大括号、花括号、小括号没有匹配而烦恼？是否经常找匹配括号看瞎了眼？现在不要 888 也不要 998，只需一键下载安装这个插件就再也不用担心啦。这个插件让你写的每一个括号都能找到他自己的颜色，成双成对，点一下其中一半括号自动匹配另一半，拯救了广大程序员的近视眼睛度数。

**再来介绍下面这个koroFileHeader插件，这个插件主要用于自动的插入头文件开头的说明和函数的说明。**

![koroFileHeader_ext](https://github.com/lemonchann/images/raw/master/tools/vscode_cpp_env/koroFileHeader_ext.png)

比如我们经常看到别人的头文件开头是这样的模板：

```c
/******************************************************************************
*  FILENAME:    niu_bi_head_file.h
*  DESCRIPTION: 非常厉害的头文件
*  HISTORY:     Date        Author      Comment
*               2020/09/05  lemon
*******************************************************************************/
```

这个可不是别人一个个字打出来的，安装插件之后你只需要简单配置想要的格式，然后按下快捷键`Ctrl + Alt +i` 即可自动即可自动生成这样一个模板。

类似的对函数的说明注释模板，只需按下快捷键`Ctrl + Alt +t` 即可完成，非常的方便。

**下面这个插件Switcher，这个插件能在头文件和 C/C++ 文件之间跳转。**

![switcher](https://github.com/lemonchann/images/raw/master/tools/vscode_cpp_env/switcher.png)

这个插件完全是因为我太懒想省力，才找的一个辅助工具，我们经常需要通过头文件跳到对应的源文件，或者从源文件跳转到对应的头文件，当然可以在侧边栏的文件管理器中选择打开，但是多了一个步骤有点繁琐，所以我找了这个插件，其实按插件的说明文档，它是能在不同的文件类型之间跳转，不仅仅局限于头文件和源文件，懒人福音，你值得拥有。



## 实用工具

下面这几个插件是比较实用的工具插件，各取所需。

**第一个是官方提供的 VsCode 中文汉化包**。虽然lemon提倡并鼓励大家多多实用英语，但若你不想折腾，那咱们家汉语博大精深，好优美的中国话，那就让VsCode也来说汉语吧，Microsoft 官方直供，兼容性好，放心食用。

![chinese_pack_ext](https://github.com/lemonchann/images/raw/master/tools/vscode_cpp_env/chinese_pack_ext.png)

**下面这个是 Markdown 预览增强插件**。对于经常写博客或文章的人来说，Markdown 肯定是少不了的，这个插件支持分屏预览，各种丰富的Markdwon 增强功能。

![markdown_enhance](https://github.com/lemonchann/images/raw/master/tools/vscode_cpp_env/markdown_enhance.png)

最后这个 shellman 插件是 Linux shell 脚本辅助工具。在 Linux 下工作难免随手写一个脚本，这个插件能提供了便捷的shell script 自动补全和联想等功能，提高你的脚本编写速度和准确性。

![shell_man](https://github.com/lemonchann/images/raw/master/tools/vscode_cpp_env/shell_man.png)



## 部分插件配置

### 生成头文件防重复引用宏

利用代码片段生成如下的头文件宏定义

```c
#ifndef _MY_TEST_FILE_H_
#define _MY_TEST_FILE_H_

// here is you code...

#endif // _REDIS_FREQ_WRITE_ACTION_H_
```

**设置步骤：**

![image-20200510003826796](C:\Users\linlongchen\AppData\Roaming\Typora\typora-user-images\image-20200510003826796.png)

![image-20200510004021821](C:\Users\linlongchen\AppData\Roaming\Typora\typora-user-images\image-20200510004021821.png)

格式可自定义，完成设置之后在输入 header 的时候选择设置好的代码块即可根据文件名自动生成宏定义。

```
{
	"C C++ Header": {
		"scope": "c, cpp",
		"prefix": "header", //代码片段名称
		"description": "Add #ifndef, #define and #endif",

		"body": [
			"#ifndef _${TM_FILENAME_BASE/(.*)/${1:/upcase}/}_H_",
			"#define _${TM_FILENAME_BASE/(.*)/${1:/upcase}/}_H_",
			"",
			"$0",
			"",
			"#endif // _${TM_FILENAME_BASE/(.*)/${1:/upcase}/}_H_"
		]
	}
}
```



### 文件和函数注释

安装插件 `koroFileHeader`可以自定义文件头部注释和函数注释。

![image-20200510001900009](C:\Users\linlongchen\AppData\Roaming\Typora\typora-user-images\image-20200510001900009.png)

搜索 `filehead` 点击编辑 `settings.json` 打开配置编辑界面。

```json
// 文件头部注释
    "fileheader.customMade": {

        "Description":  "",
        "version":      "1.0",
        "Author":       "lemon",
        "Copyright":    "(C) BAT",
        "Date":         "Do not edit",
        "History":      "Date        Author      Comment"
    },

    // 函数注释
    "fileheader.cursorMode": {
    

        "name":       "",
        "description":"",
        "param":      "",
        "return":     ""
    },
    "fileheader.configObj": {
        // 自定义语言注释符号，覆盖插件的注释格式
        "language": { 
            "java": {
                "head": "/$$",
                "middle": " $ @",
                "end": " $/"
            },
        // 一次匹配多种文件后缀文件 不用重复设置
        	"h/hpp/cpp": {
            "head": "/**************************************************", // 注释开头 多个*
            "middle": " * @",                                              // 注释中间 *
            "end": " ***************************************************/" // 注释结尾 多个*
            },
            // 针对有特殊要求的文件如：test.blade.php
            "blade.php":{
            "head": "<!--",
            "middle": " * @",
            "end": "-->",
            }
        }   
    }
```



### 格式化代码

一般代码格式有Visual Studio 和Google 代码格式，最大的区别是花括号要不要换行。

现在可以随意切换了，先按如下方式，打开VsCode 设置，搜索clang 关键字，选择：` C_Cpp: Clang_format_fallback Style`  配置完成，选中需要格式化的代码块，按快捷键：Shift+Alt+F 完成格式化。

![image-20200509231323363](C:\Users\linlongchen\AppData\Roaming\Typora\typora-user-images\image-20200509231323363.png)

可以选择的代码格式化方式是： `Visual Studio, LLVM, Google, Chromium, Mozilla, WebKit`



## 最常用快捷键

快捷键太多，没必要完全记下来，只需记住一些常用的快捷键即可，一些不常用的快捷键在使用的时候加强记忆就好。列举出我自己常用的快捷键，不多，但够用！应付日常开发工作绰绰有余。

`Ctrl + Shift + P `  这个必须要放在第一位，这个命令是所有「命令之母」。这么说一点也不过分，它会打开 VsCode 命令窗口，在这个窗口下输入上述的插件名称就能知道这个插件支持哪些特性了，顺带还会说明特性快捷键。

下面举个例子，输入 `bookmarks` 就能知道这个插件的所有特性。

![](https://github.com/lemonchann/images/raw/master/tools/vscode_cpp_env/bookmarks_shili.png)



`Ctrl + P` 文件查找。快速打开文件列表，输入关键字匹配文件，优先显示最新打开过的文件，方便的在指定文件之间跳转。

`F12` 跳转到定义，这个没啥好说的，跳转到函数或符号的定义，这是高频操作。

`Alt + F12` 以预览方式在当前页面显示定义，都是查看定义，相对 `F12` 的优点是不会跳出当前文件到定义文件，而是在当前文件打开一个小窗口预览，如下图：

![](https://github.com/lemonchann/images/raw/master/tools/vscode_cpp_env/f12_yulan.png)

`Shift + F12` 查看光标所在函数或变量的引用，就像 `Alt +F12` 一样以预览方式在当前文件打开引用的文件列表。如下图： 

![](https://github.com/lemonchann/images/raw/master/tools/vscode_cpp_env/yinyong.png)

`Alt + 左/右箭头` 前进或者后退到光标所在源码的上一个位置。

`Ctrl + Shift + O` 查看当前文件的符号，可以用关键字过滤符号，当然你也可以在左侧的大纲视图中查找符号，不过大纲视图不能查找匹配符号，所以我更习惯用快捷键方式查找符号。 

![](https://github.com/lemonchann/images/raw/master/tools/vscode_cpp_env/chazhao_fuhao.png)

快捷键讲完了吗？没有，太多快捷键了；其他的快捷键不重要吗？因人而异吧，高频使用的快捷键就是重要的，而上面我说的这几个是超高频使用，记住这几个差不多就行了，剩下快捷键你如果用的多了自然就记住了，但是我说的这几个请务必先记在脑子里，这会大大降低你的使用成本，尽早享受 VsCode Coding 的乐趣！



## 最后说几句

想起我上大学的时候，大一学习C语言课必须安装VC++ 6.0才行，那时候也有 Visual studio 这样的 IDE，不过老师没推荐其他 IDE，都是凭借自己对编程的兴趣发现了更多比VC++ 6.0 更加 '现代化' 的 IDE，比如Jetbrain 系列和Visual studio系列，爱不释手各种尝试。
![jetbrain_cpp.png](https://upload-images.jianshu.io/upload_images/7842464-d3b1c04b7f331035.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


现在主流的 IDE 已经非常丰富，其实编辑器或者 IDE 只是一个工具，没有最好自己用的顺手就行，就像 Vim 党和 Emacs 党谁也说服不了谁一样，有的人喜欢。

大家更应该关注编程这件事本身，提高自身硬实力才是最紧要的，不过好的工具能让你事半功倍，这点 lemon 也是完全赞成的，希望这篇文章也能够让你事半功倍。 

我是lemon，热爱技术，也爱生活，坚持分享输出，让自己和读者都有收获！关注我来跟我一起变强吧。 如果文章对你有帮助，请不吝「点赞、分享、在看」激励我持续创作。

文章首发个人技术公众号「**后端技术学堂**」，**目标是成为技术人的充电学堂**。

**欢迎扫码关注，分享、记录、成长！**

<p align="center">
<img src="https://github.com/lemonchann/images/raw/master/gzh/公众号二维码.png" width="300" height="300"/>
</p>