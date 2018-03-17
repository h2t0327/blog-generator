---
title: Ubuntu17.10 友善6410 PC端QT开发环境搭建
date: 2018-03-17 18:10:00
tags: W3C MDN HTML Tag 空Tag 可替换Tag
categories: Embedded
---

## 下载QT

[QT各版本官方下载大全](http://download.qt.io/archive/qt/)  
这里我们下载最新的安装文件  
`qt-opensource-linux-x64-5.10.1.run`  
这个.run文件既包含了SDK也包含了IDE：QtCreator

## 安装交叉编译工具

### Step1
将光盘 Linux 目录中的 arm-linux-gcc-4.5.1-v6-vfp-20120301.tgz 复制到 Ubuntu某个
目录下如 tmp/（没有的话可以在自己的用户目录上创建）,然后进入到该目录,执行解压命令:
```
cd /tmp
tar xvzf arm-linux-gcc-4.5.1-v6-vfp-20120301.tgz –C /
```

- 注意:C 后面有个空格,并且 C 是大写的,它是英文单词“Change”的第一个字母,在此是改变目录的意思。
- 执行该命令,将把 arm-linux- gcc 安装到/opt/FriendlyARM/toolschain/4.5.1 目录。

### Step2
`#vim /root/.bashrc`  
编 辑 `/root/.bashrc` 文 件 , 注 意 “ bashrc ” 前 面 有 一 个 “ . ”, 修 改 最 后 一 行 为   
`export PATH=$PATH:/opt/FriendlyARM/toolschain/4.5.1/bin`,注意路径一定要写对,否则将不会有效。  
重启 ，其实注销就行 。你随意  
在命令行 输入  
`arm-linux-gcc –v`,会出现一堆信息，最下面一行为`gcc version 4.5.1 (ctng-1.8.1-FA)`,这说明交叉编译环境已经成功安装。

## 编译与安装QtE-4.8.5

### 解压QtE-4.8.5
```
首先创建工作目录/opt/FriendlyARM/tinyc110/linux
在命令行执行
mkdir –p /opt/FriendlyARM/tinyc110/linux
cd /opt/FriendlyARM/tinyc110/linux
tar xvzf /tmp/linux/arm-qte-4.8.5-20101105.tar.gz
```

### 编译与安装

```
cd /opt/FriendlyARM/mini210/linux/arm-qte-4.8.5
./build.sh
此处等待完成， 要很长时间 ，耐心一点
./mktarget       这一步其实可以省略，执行此文件会提取出必要的 QtE-4.8.5 库文
件 和 可 执 行 二 进 制 示 例 , 并 打 包 为 
target-qte-4.8.5-to-devboard.tgz 
target-qte-4.8.5-to-hostpc.tgz
如果省略,也可以直接使用我们编译好的二进制包,它们放在光盘的 Linux 目录下,名称
target-qte-4.8.5-to-devboard.tgz 
target-qte-4.8.5-to-hostpc.tgz
```
- 其中 `target-qte-4.8.5-to-devboard.tgz` 是用于部署在开发板上的版 本,为了节省空间该版本删
除了开发工具只保留运行程序所需的库文件,而 `target-qte-4.8.5-to-hostpc.tgz` 则是用于安装在 PC
上,用来开发和编译程序的版本,带有 qmake 等 Qt 工具以及编译所需的头文件等,可用于配置
Qt Creator 开发工具。

- 安装 QtE-4.8.5 到 PC 上的方法如下:
把 `target-qte-4.8.5-to-hostpc.tgz` 在 PC 的根目录下解压即可,如下命令
`tar xvzf target-qte-4.8.5-to-hostpc.tgz –C /`
- QtE-4.8.5 会安装到目录 `/usr/local/Trolltech/QtEmbedded-4.8.5-arm/` 下,它里面包含了运行
所需要的所有库文件和可执行程序。

- qmake路径配置 ：  
`cd /usr/lib/x86_64-linux-gnu/qt-default/qtchooser/`  
`vim default.conf` 将第一行路径替换为QTE485路径 `/usr/local/Trolltech/QtEmbedded-4.8.5-arm/lib`

## 安装QT

### Step1
进入下载好QT的目录， 一般在下载目录中 。给安装文件运行权限：  
`chmod u+x qt-opensource-linux-x64-5.10.1.run`

### Step2
运行 `./qt-opensource-linux-x64-5.10.1.run`  
一路向下，注意   那个`5.10.1`要勾选，3.6个G的样子

### Step3
QT5.10.1 安装按成后会自带QTcreator ， 打开QTcreator
- 在菜单栏处找到`工具（Tools）` -> `选项（options）` 打开options窗口 ，点击`构建和运行`   
- 点击`QT Versions` ，看auto （自动）栏是否检测到`QT 5.10.1 GCC 64bit` 以及`QT 4.8.5 in PATH(QtEmbedded-4.8.5-arm)` 如果没有检测到4.8.5 那么手动添加 路径为：`/usr/local/Trolltech/QtEmbedded-4.8.5-arm/bin/qmake`
- 点击`编译器（compilers）` -> `添加（add）` -> `GCC` -> `C++`  下方出现弹窗 ， 将一条名称改为`ARMGCC` ， 第二条路径为`/opt/FriendlyARM/toolschain/4.5.1/bin/arm-linux-gcc` ，最后点击`应用（apply）` 
- 点击`构建套件（kit）`  ，修改名称为ARM ， 然后将才编译器 c++ ： 更换成 `ARMGCC`  ，最后点击`应用（apply）` 

> 最后这就表示安装并且配置完成了， 可以开心的玩起来了。

## 新建工程

新建工程 ， 选择编译环境时把`ARM` 和 `Desktop` 都勾选起来 ，这样的话 ，我们就可以在PC上调试好， 放到开发板中运行了  。
- 编译的时候可以在左边绿色三角上方选择编译器 ，  选择Desktop可以在PC上调试 ， 选择ARM 会生成开发板需要的执行文件 。 运行之后都会在项目所在的目录生成一个目录。