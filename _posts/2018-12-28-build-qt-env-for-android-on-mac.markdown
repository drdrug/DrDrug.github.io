---
layout: post
title:  "build QT env for android on MacOS"
date:   2018-12-28 21:00:37 -0800
categories: code
tags: qt android mac
excerpt: 环境搭建。
---

* content
{:toc}

## 1. 安装准备
* [Qt](http://download.qt.io/archive/qt/)安装包，当前使用版本为5.11.2
* [Java SDK](https://www.oracle.com/technetwork/java/javase/downloads/index.html)，下载最新的即可
* [Android Studio](https://developer.android.com/studio/#downloads)，一般被墙，当然科学上网的手段是必不可少的了。
* [Android NDK](https://developer.android.com/ndk/)，同上。
* 下载完后，最好检查下SHA，防止植入。

## 2. 安装Qt开发环境
1. QT安装包直接安装即可，在选择安装配置的时候，为了后期开放方便，还是全都选上吧。其中：
    * armv7a：真机的交叉编译环境，编译生成的APP可以部署上Android设备运行。
    * x86：本机的交叉编译环境，主要用于模拟APP运行场景。尽管模拟器能模拟armv7a的环境，但会巨慢。
    * clang：Mac的编译环境，想在Mac/IOS上玩耍的，可以试试。

2. 安装的过程会要求安装XCode，这个当然最好从App Store下载安装了，会比较安全。
3. 安装结束后，将安装路径下的：Qt Creator.app拷贝到Application目录，方便日常使用。
    
## 3. 安装Java SDK
1. 安装也是傻瓜式的安装了，一路狂点。
2. 配置环境变量：
    * export JAVA_HOME=Java安装路径
    * export CLASSPATH=.:\$JAVA_HOME/lib/tools.jar:\$JAVA_HOME/lib/dt.jar
    * export PATH=\$JAVA_HOME/bin:\$PATH
3. 自行java -version；能输出安装的版本号即为安装完成。

## 4. 安装Android Studio
1. 安装也是与JAVA SDK一样啦，狂点(可能需要科学上网更新相关组件)
2. 配置环境变量：
    * export ANDORID_NDK_ROOT=/xxxx #NDK安装路径
    * export ANDROID_SDK_ROOT=/xxxx #SDK安装路径，一般为Android Studio安装的SDK路径
3. 安装开发用的SDK版本：
    * Preference -> Appearance & Behavior -> System Settings -> Android SDK(Tool -> SDK Manager)
    * 勾选需要安装的API Level,等待安装完成
4. 创建AVD(Android Virtual Device)
    * Tool -> AVD Manager 
    * Create Virtual Device
    * 选择需要仿真的平台类型，或New Hardware Profile..
    * 选择硬件类型后，需要选择该类型使用的System Image，这里选择x86架构的ABI，如果选择armv7a，运行起来可能巨慢无比。
    * 对于未安装的System Image，安装即可

## 5. 使用Qt开发Android
1. 配置QCreator环境
    * Preference -> Devices
    * 配置JAVA SDK、Android SDK、Android NDK路径
    * 确保各个Kits的警告消除，能正常使用
2. 新建项目
    * 新建支持Android平台的项目
    * 配置项目选择x86或armv7a，前者在本地模拟，后者在真机运行
    * 编译通过后，最后调试运行：开始调试后，选择对应的ABI即可。

## 结语
随手笔记，至于图文并茂的效果，再说了。
                    


