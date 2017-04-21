## 使用 VSCode 开发 C项目
OS: win10

VScode Version：1.11

最近在使用 VScode 开发 STM32 的项目，起因是 MDK 代码提示功能的落后。在网上看到有很多朋友都在问 VSCode 开发 C/Cpp 项目的自动补全与函数跳转，刚好我也碰到了。所以写出来供大家参考。如有错误，请指出。

#### 软件下载

现在有两个网站都可以下载到 VSCode 。

一个是 VSCode 中文网，现更新到 Version 1.8。(这个站，貌似是个人的，所以更新没那么快?)
另一个是 VScode 官方网站,现更新到 Version 1.11。(在中文 windows 系统下安装，默认显示中文菜单。)
So, 建议从 VScode 官方网站 下载最新版本的 VSCode 使用。

参考： VS Code C++不同文件夹下的函数跳转不了？ @mengdi 的回答

#### 插件安装

在这里，要介绍两种实现 C/Cpp 代码自动补全，函数跳转的实现方法。

###### 方法一：使用最新的插件，实现 代码自动补全、函数跳转

本方法使用最新的 C/C++ 插件。

按下快捷键 Ctrl+P 之后输入 ext install cpptools,可以看到，左侧第一个就是 微软自家的 C/C++ 插件。 这里我们点击安装，然后重启 VSCode ，让插件生效。再次按下快捷键 Ctrl+P, 输入 settings, 在打开的 settings.json 文件中 设置以下代码，开启 C/C++ 插件自带的代码补全功能。
"[cpp]": {
"editor.quickSuggestions": true
    },
"[c]": {
"editor.quickSuggestions": true
    }
用和上面同样的方法，我们需要安装第二个插件 C++ Intellisense ： ext install code-gnu-global, 同样重启生效。

接下来我们需要下载 gtags 来支持 C++ Intellisense 插件。gtags 是一个类似CTag的，能够创建用于实现索引和自动补全功能所需的Tag的程序。下载Gtags可以去Gtags官网下载源代码自己编译，或者直接下载它提供的Win32安装包。 由于我们是在 windows 操作系统下，所以我们在 官网下载页面 下，选择win32 下载 (可能需要梯子)。下载完成后，解压缩，可以看到里面包含 3 个文件夹。我们需要把三个文件夹统一移动到 VSCode 的安装目录下（其实，随便哪个目录都可以，不过为了方便讲解，我添加到了安装目录下）。我的具体路径为： C:\Program Files (x86)\Microsoft VS Code\glo656wb。

被'强'的可以到我的 云盘下载。
下一步我们要把 C:\Program Files (x86)\Microsoft VS Code\glo656wb\bin 添加到 系统环境变量。 具体添加方法可以看此链接. 注意:系统变量需要重启才能生效 。

重启电脑后，用 VSCode 打开你的工程文件夹(C/C++源码目录)，按下快捷键ctrl+shift+C , 输入 gtags ，运行。可以看到在工程文件夹下生成了 3 个文件，分别是： GPATH、GRTAGS、GTAGS ，这表明，我们的 gtags 开始正常工作啦。

按Ctrl键并使鼠标指向某个函数，您将看到这个函数的提示信息，您还可以跳转到定义、查找引用（shift+F12）、自动补全、列出符号等（ctrl+P，输入@）。

这时候你就会发现可以使用 Go to definition 进行跨文件跳转啦~

###### 方法二：安装旧版本的插件，以支持 代码自动补全、函数跳转

在搜索如何使用 VSCode 进行开发 C项目的时候，我发现有很多博主写的文章里，是能够实现 C/C++ 代码的自动补全与函数跳转功能的，但是我一步一步做下来，就是达不到文章里的效果。 最后我经过不断测试，发现对于微软的 C/C++ 插件， 0.9.1 版本以前，是能够原生支持这些功能的。但是不知道为什么，后面的版本，就去阉割了这些功能。 下面我就介绍如何离线下载 0.9.1 版本的插件，以支持这些功能。

我参考 简书上的这篇文章(@白水螺丝),找到了 不同版本的 C/C++ 插件，发现最后完成支持的版本是： 0.9.1。 离线下载的地址，可以点我。下载后，将下载的文件 Microsoft.VisualStudio.Services.VSIXPackage 进行重命名为 debugger-for-chrome.vsix ;文件名可以随意取，但是后缀一定要是 vsix .

下不动的可以到我的 云盘下载。
离线安装 C/C++ V0.9.1。 在拓展选项卡中选择 从 VISX 安装，然后选下载好的 *.vsix 文件安装即可。

最后一步，就是 在 c_cpp_properties.json 中配置自己的 include 文件夹了。参见本链接。

检验成功与否的方法： 如果成功了，可以发现在 工程文件夹下， .vscode 的目录中，会出现 *.VC.DB.* 的文件。我猜测，这就是关键字的索引了。

ok，本教程就到这里。

参考链接：

配置Visual Studio Code的C++开发环境
配置VSCode
Windows下VSCode便携式c/c++环境
VSCode配置C++编写环境:
C/C++Visual Studio Code介绍及部署
Visual Studio Code的C/C++扩展功能:
附： 完全卸载 VScode 的方法：

在控制面板中删除程序
删除 C:\Users\用户名\.vscode\extensions 文件夹
删除 C:\Users\用户名\AppData\Roaming\Code 文件夹


