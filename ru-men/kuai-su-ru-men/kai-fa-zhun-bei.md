# 开发准备

#### 安装依赖

必须安装的依赖有：Node、JDK 和 Android Studio。

#### Node, JDK

使用搜索引擎搜索下载Node和Java SE Development Kit (JDK)，注意Node的版本应大于等于14。

React Native需要Java Development Kit \[JDK] 11。你可以在命令行中输入javac -version来查看你当前安装的JDK版本。

#### Yarn

Yarn是Facebook提供的替代npm的工具，可以加速node模块的下载。安装完yarn之后就可以用yarn代替npm了，例如用yarn代替npm install命令。

#### Android开发环境

* 安装Android Studio

首先下载和安装Android Studio。安装界面中选择“Custom”选项，确保选中Android SDK、Android SDK Platform及Android Virtual Device三项。

* 安装Android SDK

Android Studio默认会安装最新版本的Android SDK。目前编译React Native应用需要Android 13版本的SDK。你可以在Android Studio的SDK Manager中选择安装各版本的SDK。

在SDK Manager中选择“SDK Platforms”选项卡，然后在右下角勾选“Show Package Details”。展开Android 13选项，确保勾选了Android SDK Platform 33及Intel x86 Atom\_64 System Image，然后点击“SDK Tools”选项卡，同样勾中右下角的“Show Package Details”。展开“Android SDK Build-Tools”选项，确保选中了React Native所必须的33.0.0版本。你可以同时安装多个其他版本。最后点击"Apply"来下载和安装这些组件。

* 配置ANDROID\_HOME环境变量

打开控制面板->系统和安全->系统->高级系统设置->高级->环境变量->新建，创建一个名为ANDROID\_HOME的环境变量（系统或用户变量均可），指向你的Android SDK所在的目录。你需要关闭现有的命令符提示窗口然后重新打开，新的环境变量才能生效。

* 把一些工具目录添加到环境变量Path

打开控制面板->系统和安全->系统->高级系统设置->高级->环境变量，选中Path变量，然后点击编辑。点击新建然后把这些工具目录路径添加进去：platform-tools、emulator、tools、tools/bin。

#### 创建新项目

使用React Native内建的命令行工具来创建一个名为“AwesomeProject”的新项目。

```
npx react-native init AwesomeProject
```

#### 准备Android设备

* 使用Android真机

你可以使用Android真机来代替模拟器进行开发，只需用usb数据线连接到电脑，然后遵照文档的说明操作即可。

* 使用Android模拟器

你可以使用Android Studio打开项目下的“android”目录，然后可以使用“AVD Manager”来查看可用的虚拟设备。

#### 编译并运行React Native应用

确保你先运行了模拟器或者连接了真机，然后在你的项目目录中运行yarn android或者yarn react-native run-android。
