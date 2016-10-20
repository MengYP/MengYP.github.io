---
title:          "React Native - Button"
description:    "使用React Native创建按钮，封装按钮"
image:          "http://placehold.it/400x200"
author:         "GeekMeng"
---

一、React Native 按钮的创建
===============

1.项目介绍
-------------

### 1.1 项目创建 ###

在命令行中，目标文件下：

(1).创建项目：

`react-native init 项目的名字`

(2).运行项目：

`cd 项目目录`

`react-native run-ios`

### 1.2 项目文件 ###

* 开发iOS应用：编写`index.ios.js`文件（入口文件）。
(使用`WebSorm` 或者 其他Web开发工具`Sublime`等)

* 开发Android应用：编写`index.android.js`文件（入口文件）。

### 1.3 index.ios.js文件 ###

文件分为四部分，第一部分：导入用到的组件

```JavaScript
import React, { Component } from 'react';
import {   //导入组件
  AppRegistry,
  StyleSheet,
  Text,
  View,
  TouchableOpacity    
} from 'react-native';
```

第二部分：添加组件

* 定义一个名字为`AwesomeProject`的新的组件（`Component`）.
* 编写`React Native`应用时，会写出很多的组件，而一个App的最终界面，其实也就是各式各样的组件的组合。
* 组件本身结构非常简单，唯一必须的就是在`render`方法中返回一些用于渲染的JSX语句。

```JavaScript
export default class AwesomeProject extends Component {
  render() {
    return (
      <View style={styles.container}>
      </View>
    );
  }
}
```

第三部分：样式

```JavaScript
const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  instructions: {
    textAlign: 'center',
    color: '#333333',
    marginBottom: 5,
  },
});
```

第四部分：

> 注册应用(registerComponent)后才能正确渲染
> 注意：只把应用作为一个整体注册一次，而不是每个组件/模块都注册

* 使用`AppRegistry`内置模块进行“注册”操作。
* 用来告诉`React Native`哪一个组件被注册为整个应用的根容器。
* 一般在一个应用里面，`AppRegistry.registerComponent`方法只会调用一次。
  有点像Foundation框架中设置App的根控制器。
* `AwesomeProject`必须和`init`创建的项目名一致。

```JavaScript
AppRegistry.registerComponent('AwesomeProject', () => AwesomeProject);
```

2.Button的创建
-------------

* 第一步：导入组件 `TouchableOpacity`    

在**项目文件**的第一部分，导入`TouchableOpacity`组件

* 第二步：添加组件 `TouchableOpacity`

在**项目文件**的第二部分，在`render`方法中返回一些用于渲染`TouchableOpacity`的JSX语句，并设置一些样式、监听方法。

```JavaScript
  {/*
    监听方法：
   onPress={this.customPressHandler}   :点击按钮时调用此属性方法
   onPress={this.customPressHandler()} :初始化时，就直接调用此属性方法，点击按钮不会调用此方法
    注意：所以一定不能带小括号

    样式：组件的Props（属性）
    style={styles.button}
  */}
  <TouchableOpacity
      style={styles.button}
      onPress={this.customPressHandler}>
    <Text style={styles.buttonText}>确定</Text>
  </TouchableOpacity>
```

* 第三步：样式

在**项目文件**的第三部分，添加`TouchableOpacity`组件的样式

```JavaScript
button:{
     height:40,
     width:100,
     borderRadius:20,
     backgroundColor:'green',
     justifyContent:'center'
 },
 buttonText:{
   textAlign:'center',
   color:'white'
 }
```

二、Button的封装
===============

>问题：
  1、如果所有的组件都写在`index.ios.js`文件中，势必会造成`index.ios.js`文件的庞大，不利于项目的维护和编写。
  2、如果项目中需要多个按钮组件，并且样式相同，可能只有很少的地方不同，比如文字，颜色，这样如果都重复编写在`index.ios.js`文件，是不合适的。
>
>解决：封装专门的Button组件。
可以在不同的页面中使用同样样式的按钮，达到代码的复用。


1、封装文件介绍
-------------

在项目根目录中创建目录`src/component`（个人习惯，在此目录下存放自定义组件）。

创建自定义的`Button.js`组件。

`Button.js`文件包含`index.ios.js`文件的前三部分。

* 第一部分：

```JavaScript
import React, { Component } from 'react';
import {  //导入组件
    AppRegistry,
    StyleSheet,
    Text,
    TouchableOpacity    
} from 'react-native';
```

* 第二部分：

```JavaScript
/*
自定义组件：
 关键字 export default 不能缺少: 有这个关键字，把自定义的Button组件标记为导出组件，这样Button组件才可以被其它文件所引用。
 */
export default class Button extends Component {
    //此处构造的函数属性外部都能调用
    //构造函数
    constructor(props){
        super(props);
        //初始化状态
    }
    //render: 渲染
    render() {
        //{} ：解构。 解构的好处：可以一次性取出多个属性， 也可以取出方法。
        const { text, bgColor} = this.props; //const表示是一个不可修改的量
        //基本上等同于： const text = this.props.text;
        return (
            //添加组件
        );
    }
}
```

* 第三部分：

```JavaScript
const styles = StyleSheet.create({
    //设置组件Props（属性）   (位置、颜色、文字等)
});
```

* 注意点：

(1).使用自定义组件，必须引入自定义组件

`import Button from './src/component/Button';`

(2).构造函数中初始化状态
```
//构造函数
constructor(props){
    super(props);
    //初始化状态
}
```

(3).对属性进行解构

```JavaScript
//解构 （对属性进行解构）
const {text, bgColor} = this.props;
```




## 完 ##
