---
title:        "Runtime"
description:  "Runtime简称运行时。Object-C就是运行时机制，主要是消息机制。"
image:        "http://placehold.it/400x200"
author:       "GeekMeng"
---

一、综述
============

RunTime简称运行时。OC就是运行时机制，也就是在运行时候的一些机制，其中最主要的是消息机。

* OC & C 比较

对于C语言，函数的调用在编译的时候会决定调用哪个函数，编译完成之后直接顺序执行，没有任何二义性。

对于OC的函数调用称为消息发送，属于动态调用过程，在编译的时候并不能决定真正调用哪个函数，只有在真正运行的时候才会根据函数的名称找到对应的函数来调用。

在编译阶段，OC可以调用任何函数，即使这个函数并未实现，只要声明过就不会报错。
在编译阶段，C语言调用未实现的函数就会报错。

>二义性：指的是一个东西在一种环境下会出现两种以上（包含两种）含义，导致难以清楚到底何种意思。没有二义性，就是同名覆盖。）
>
>`Runtime`基本是用C和汇编写的。
>苹果维护的开源代码： http://opensource.apple.com//source/objc4/
>苹果和GNU各自维护一个开源的runtime版本，这两个版本之间都在努力的保持一致。
>

* runtime 与OC交互

Object-C从三种不同的层级上与Runtime系统进行交互：
  * 通过Objective-C源代码；
  * 通过Foundation框架的NSObject类定义的方法；
  * 通过对runtime函数的直接调用。


* runtime用途实现：

  * 1) `Swizzie`黑魔法（拦截系统自带的方法，并替换系统的方法）
  * 2）将某些`OC`代码转为运行时代码
  * 3）实现分类也可以增加属性（通常情况`category`不能增加属性，`Extension`才可以）
  * 4）自动归档和自动解档（原理是通过遍历属性来实现）
  * 5）动态增加方法（动态的为某个类或对象增加一个方法）
  * 6）动态变量控制（动态对某个对象的变量的值进行替换）
  * 7）实现万能控制器跳转（推送过来的消息，要跳转到任意控制器。利用`runtime`动态生成对象、属性、方法这一特性）
  * 8）插件开发（通过头文件名猜测方法的作用，`swizzie`这些方法，插入自己的代码实现插件逻辑）
  * 9）`JSPath`热更新（在线修复bug，实现热更新）

Note that --- not considering the asterisk --- the actual text
content starts at 4-columns in.

> Block quotes are
> written like so.
>
> They can span multiple paragraphs,
> if you like.

Use 3 dashes for an em-dash. Use 2 dashes for ranges (ex., "it's all
in chapters 12--14"). Three dots ... will be converted to an ellipsis.
Unicode is supported. ☺



An h2 header
------------

Here's a numbered list:

 1. first item
 2. second item
 3. third item

Note again how the actual text starts at 4 columns in (4 characters
from the left side). Here's a code sample:

    # Let me re-iterate ...
    for i in 1 .. 10 { do-something(i) }

As you probably guessed, indented 4 spaces. By the way, instead of
indenting the block, you can use delimited blocks, if you like:

~~~
define foobar() {
    print "Welcome to flavor country!";
}
~~~

(which makes copying & pasting easier). You can optionally mark the
delimited block for Pandoc to syntax highlight it:

~~~python
import time
# Quick, count to ten!
for i in range(10):
    # (but not *too* quick)
    time.sleep(0.5)
    print i
~~~



### An h3 header ###

Now a nested list:

 1. First, get these ingredients:

      * carrots
      * celery
      * lentils

 2. Boil some water.

 3. Dump everything in the pot and follow
    this algorithm:

        find wooden spoon
        uncover pot
        stir
        cover pot
        balance wooden spoon precariously on pot handle
        wait 10 minutes
        goto first step (or shut off burner when done)

    Do not bump wooden spoon or it will fall.

Notice again how text always lines up on 4-space indents (including
that last line which continues item 3 above).

Here's a link to [a website](http://foo.bar), to a [local
doc](local-doc.html), and to a [section heading in the current
doc](#an-h2-header). Here's a footnote [^1].

[^1]: Footnote text goes here.

Tables can look like this:

size  material      color
----  ------------  ------------
9     leather       brown
10    hemp canvas   natural
11    glass         transparent

Table: Shoes, their sizes, and what they're made of

(The above is the caption for the table.) Pandoc also supports
multi-line tables:

--------  -----------------------
keyword   text
--------  -----------------------
red       Sunsets, apples, and
          other red or reddish
          things.

green     Leaves, grass, frogs
          and other things it's
          not easy being.
--------  -----------------------

A horizontal rule follows.

***

Here's a definition list:

apples
  : Good for making applesauce.
oranges
  : Citrus!
tomatoes
  : There's no "e" in tomatoe.

Again, text is indented 4 spaces. (Put a blank line between each
term/definition pair to spread things out more.)

Here's a "line block":

| Line one
|   Line too
| Line tree

and images can be specified like so:

![example image](http://placehold.it/800x250 "An exemplary image")


And note that you can backslash-escape any punctuation characters
which you wish to be displayed literally, ex.: \`foo\`, \*bar\*, etc.
