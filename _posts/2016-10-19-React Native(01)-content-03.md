---
title:          "React Native"
description:    "React Native使你能够在Javascript和React的基础上获得完全一致的开发体验，构建世界一流的原生APP。React Native着力于提高多平台开发的开发效率 —— 仅需学习一次，编写任何平台(Learn once, write anywhere)。Facebook已经在多项产品中使用了React Native，并且将持续地投入建设React Native。"
image:          "http://placehold.it/400x200"
author:         "GeekMeng"
---

一、React Native环境搭建
===============

1.packager
-------------

### 1.1 介绍 ###
* 开发环境：`React Native packager`
* 默认在8081端口运行
* 一个微型的HTTP服务器
* 把已经写的所有js 以及 依赖的第三方js文件收集起来打包在一起，通过HTTP服务提供给`React Native`应用。

### 1.2 启动packager ###
* 方法一：在mac下点击项目run按钮，会自动弹出packager。
* 方法二：命令行，cd到项目文件夹下，启动命令：

  `npm start`  或  `react-native start`  两个命令等效

2.构架
-------------

* 在开发模式下，分为两部分，一部分是原生代码写成的部分，相当于壳子CD机，我们写的js代码就是CD

* 开发模式下，在iPhone模拟器中直接`Cmd+R`刷新

3.package.json文件
-------------------

* `package.json`文件中的`devDependencies`下可以查看`React Native`的版本号，以及相关依赖模块。


4.node_modules文件夹
-------------------

* `项目文件夹/node_modules`：通过`npm install`命令，下载的模块（包括官方和第三方）。

`React Native`的命令行工具（`react-native-cli`）

`React Native`的命令行工具用于执行创建、初始化、更新项目、运行打包服务（packager）等任务。

`npm install -g react-native-cli`

* 在当前目录下运行上面命令的作用是：从项目路径下的`package.json`文件中，读取`devDependencies`信息，来下载模块到`node_modules`文件夹下。

* 无论是下载查看别人的写的项目、还是自己创建项目都需要执行该命令。


二、React Native使用
===============

* ES6标准的JavaScript
* `JSX`是一种在`JavaScript中嵌入XML`结构的语法。

很多传统的应用框架会设计自有的模板语法，让你在结构标记中嵌入代码。

React反其道而行之，设计的`JSX语法`却是让你`在代码中嵌入结构标记`。

`<Text>Hello world!</Text>`初看起来，这种写法很像web上的HTML，只不过使用的并不是web上常见的标签如<div>或是<span>等，这里我们使用的是`React Native的组件`。上面的示例代码中，使用的是`内置的<Text>组件`，它专门用来显示文本。


三、React Native项目规范代码
===============

代码规范的一个插件：
[eslint-config-airbnb](https://www.npmjs.com/package/eslint-config-airbnb)

WebStorm的Terminal中输入命令安装：

```
(
  export PKG=eslint-config-airbnb;
  npm info "$PKG" peerDependencies --json | command sed 's/[\{\},]//g ; s/: /@/g' | xargs npm install --save-dev "$PKG"
)
```

### WebStorm 常用快捷键 ###

`Cmd + D` ：复制当前行

`Alt + Shift + 向上键/向下键` ：向 上/下 移动代码块 一行

`Cmd + Shift + 向上键/向下键` ：向 上/下 移动代码块 到上/下一个方法块位置

`Tab` ：向后移动代码块

`Tab + Shift` ：向前移动代码块

`Ctrl + tab` ：切换已经打开的文件

WebStorm的Terminal中输入命令： `react-native run-ios` 直接自动编译项目、运行项目在模拟器。

### 注 ###

[React Native文档](http://reactnative.cn/docs/0.31/getting-started.html#content)






## 完 ##
