---
layout: post
title: "UEFI+GPT+Clover macOS原版单、双系统双版教程(正式版)"
date: 2017-05-07 20:05:22 
description: "安装系统教程"
tag: 教程
---

## **阅前须知**
> 首要条件：本教程仅针对UEFI主板 如果你主板支持UEFI但现在用的是BIOS（Legacy/Launch CSM）+MBR的，

> MBR分区表等下要转GPT，主板的launch CSM/Legacy要关掉，请按照实际情况修改。（不知道什么意思的请百度）

### 一、Windows下制作macOS原版安装U盘

用到的正式版自修改镜像：<a href="http://pan.baidu.com/s/1kV0WHTl" target="_blank">macOS Sierra 10.12.4(16E195)原版镜像</a>

下下来后用Transmac写入就行，Tramsmac在镜像链接里面

写入占用大概5-6G，准备8G以上U盘即可。



### 二、OS X下制作macOS原版安装U盘

#### **1.准备工作：**

(1).准备一个 8GB 或以上容量的 U 盘，确保里面的数据已经妥善备份好（该过程会抹掉 U 盘全部数据）

(2).首先，在 MAS 下载 macOS 10.12 原版安装包。

或者通过其他途径下载，拖动至自己的 **应用程序（Applications）**文件夹。

确定应用程序名字为「**Install macOS Sierra.app**」
![cmd-镜像地址-镜像](/images/posts/tutorial/Install macOS Sierra.app.png)

#### **2.格式化优盘**

(1).插入你的 U 盘，然后在「**应用程序**」->「**实用工具**」里面找到并打开「**磁盘工具**」

(2).在左方列表中找到 U 盘的名称并点击

(3).右边顶部选择「**分区**」，然后在「**分区布局**」选择「**1个分区**」

(4).在分区信息中的 「**名称**」输入「**ABCD**」 (由于后面的命令中会用到此名称，如果你要修改成其他(英文)，请务必对应修改后面的命令)

(5).在「**格式**」中选择 「**Mac OS 扩展 (日志式)**」

(6).这时，先别急着点“应用”，还要先在 「**选项**」里面，选择「**GUID 分区表**」

(7).开始格式化

![cmd-DG-格式化](/images/posts/tutorial/Disk Utility.png)

#### **3.输入终端命令开始制作启动盘**

(1).请再次确保安装文件是保存在「**应用程序**」的目录中

(2).在「**应用程序**」->「**实用工具**」里面找到「**终端**」并打开。也可以直接通过 Spotlight 搜索「**终端**」打开

(3).复制下面的命令，并粘贴到「**终端**」里，按回车运行：

    sudo /Applications/Install\ macOS\ Sierra.app/Contents/Resources/createinstallmedia --volume /Volumes/ABCD --applicationpath /Applications/Install\ macOS\ Sierra.app --nointeraction

> 命令说明：

> Install\ macOS\ Sierra.app 这个是正式版的“安装 macOS Sierra” 正确位置

> ABCD 这个是优盘的名字

回车后，系统会提示你输入管理员密码，接下来就是等待系统开始制作启动盘了。这时，命令执行中你会陆续看到类似以下的信息：

![cmd-DG-终端1](/images/posts/tutorial/CMD1.png)

![cmd-DG-终端2](/images/posts/tutorial/CMD2.png)

当你看到最后有 「**Copy complete**」和「**Done**」 字样出现就是表示启动盘已经制作完成了！

#### **4.在EFI分区放入Clover**

最后打开Clover Configurator，点击Mount EFI，选择你的U盘，点击Mount Partition ，然后点击Open Partition ，弹出EFI分区，在里面放入EFI文件夹，至此，U盘安装盘制作而成。使用方法同上！
![cmd-DG-Clover Configurator](/images/posts/tutorial/Snip1.png)

### 三、Windows+macOS(同一硬盘内同时存在NTFS/HFS+分区)

> 适用于以下情况： 

> I.  Windows和macOS安装到同一个硬盘； 

> II. OSX安装到另外的硬盘，但Windows要在macOS所在硬盘划分NTFS分区当做仓储。（此情况下，建议每个硬盘都建一个EFI和MSR分区）


#### **1.硬盘分区情况**

进入PE，打开DiskGenius，这里推荐使用的PE是<a href="http://www.wepe.com.cn/download.html" target="_blank">微PE</a>

(1).选中要操作的硬盘，点击快速分区
![cmd-DG-快速分区](/images/posts/tutorial/sshot-1.png)

(2).分区表类型选择GUID，分区数目不用管，然后点击确定
![cmd-DG-快速分区](/images/posts/tutorial/sshot-2.png)

(3).到DiskGenius主界面，还是点击要操作的硬盘，右键选择删除所有分区，删除完后，点击左上角的保存更改
![cmd-DG-删除所有分区](/images/posts/tutorial/sshot-3.png)

(4).还是点击该硬盘，并且点击该硬盘的空白分区，然后点击新建分区，出来选项，打勾建立ESP分区，ESP分区的大小改为300MB，然后点击确定
![cmd-DG-新建分区](/images/posts/tutorial/sshot-4.png)

![cmd-DG-新建分区](/images/posts/tutorial/sshot-5.png)

(5).接下来就是建立C盘，D盘，E盘等等（点击该硬盘的空白分区选择建立新分区即可），macOS的分区建议放在硬盘的最后一个分区，建立完成以后，点击左上角的保存更改
![cmd-DG-分区完成](/images/posts/tutorial/sshot-6.png)

***注：可以不需要按照这样来分，这里给出的只是建议，具体随便你们***

#### **2.Windows的安装**

Windows安装的方法很多（这里建议安装Windows10），这里就不细说了，详情百度：<a href="https://www.baidu.com/s?ie=UTF-8&wd=UEFI+GPT%E5%AE%89%E8%A3%85Windows10" target="_blank">UEFI+GPT安装Windows10</a>

#### **3.macOS的安装**

(1).启动电脑，按下启动快捷热键，选择**UEFI 你的U盘启动**，进入Clover界面
![cmd-DG-华硕笔记本U盘启动](/images/posts/tutorial/Snip2.png)


> **注：每个型号的笔记本或主板的启动快捷热键并不一定相同，具体请自己百度搜索：你的笔记本或主板怎么选择U盘启动**

(2).进入Clover界面后，选择镜像盘，按空格，勾选**Verbose(-v)**后，选择**Return**，会返回Clover主界面，然后还是选择镜像盘回车，出现滚码
![cmd-Clover-界面](/images/posts/tutorial/Snip3.png)

![cmd-Clover—界面](/images/posts/tutorial/Snip4.png)

![cmd-Clover-V图](/images/posts/tutorial/Snip5.png)

(3).进入安装界面后，选择磁盘工具
![cmd-macOS-安装界面](/images/posts/tutorial/Snip6.png)

(4).点击你要安装的分区，选择抹掉，名称自己填，格式选择Mac OS 扩展（日志式），然后点击抹掉
![cmd-macOS-安装界面](/images/posts/tutorial/Snip7.png)

(5).抹掉以后，关闭磁盘工具，选择mac OS安装，点击继续
![cmd-macOS-安装界面](/images/posts/tutorial/Snip8.png)

![cmd-macOS-安装界面](/images/posts/tutorial/Snip9.png)

![cmd-macOS-安装界面](/images/posts/tutorial/Snip10.png)

(6).选择刚刚抹掉的那个分区，点击继续
![cmd-macOS-安装界面](/images/posts/tutorial/Snip11.png)

(7).等待安装结束，会自动重启
![cmd-macOS-安装界面](/images/posts/tutorial/Snip12.png)

(8).重启后，还是和第一阶段一样，进入后会自动安装
![cmd-Clover-界面](/images/posts/tutorial/Snip3.png)

![cmd-Clover-界面](/images/posts/tutorial/Snip13.png)


**注：有可能会出现重复进入第一阶段，或者进入第二阶段出现以下错误**
![cmd-Clover-出错](/images/posts/tutorial/Snip14.png)

**出现这种情况的话，进入Windows，打开Tramsmac，下载<a href="https://pan.baidu.com/s/1hsBUzm0" target="_blank">IAProductInfo.zip</a>，解压缩，里面为一个隐藏文件，使用方法为**
![cmd-Clover-出错](/images/posts/tutorial/IAProductInfo.png)


### 三、macOS单系统安装(macOS所在硬盘没有NTFS分区)




转载请注明：[淡忘的博客](http://alansachin.github.io) » [点击阅读原文](https://alansachin.github.io/2017/05/UEFI+GPT+Clover-macOS%E5%8E%9F%E7%89%88%E5%8D%95-%E5%8F%8C%E7%B3%BB%E7%BB%9F%E5%8F%8C%E7%89%88%E6%95%99%E7%A8%8B(%E6%AD%A3%E5%BC%8F%E7%89%88)/)

