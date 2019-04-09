---
layout: post
title:  "Target Detesction 1"
crawlertitle: "open ai lab 目标检测"
summary: "目标检测"
date:   2019-04-06 12:13:00 +0700
categories: posts
tags: 'Target Detesction'
author: 711E
---

一、c++
===

1.hpp和cpp
---
  >\*.h文件做的是类的声明，包括类成员的定义和函数的声明，而*.cpp文件做的类成员函数的具体实现（定义）。一个*.h文件和*.cpp文件一般是配对的。在*.cpp文件的第一行一般也是#include"\*.h"文件，其实也相当于把\*.h文件里的东西复到\*.cpp文件的开头。所以，你全部写在\*.cpp文件其实也是一样的。

  头文件的所有内容，都必须包含在

```
#ifndef {Filename}
#define {Filename}

//{Content of head file} 　　你的代码写在这里

#endif
```
这样才能保证头文件被多个其他文件引用(include)时，内部的数据不会被多次定义而造成错误。
2.class定义
---
```
class 类名
{
  punlic:
  //公有成员：公有成员在程序中类的外部是可访问的，可以不使用任何成员函数来设置和获取公有变量的值
  //行为或属性
  protected:
  //受保护成员：保护成员变量或函数与私有成员十分相似，但有一点不同，保护成员在派生类（即子类）中是可访问的。
  //行为或属性
  private:
  //私有成员：私有成员变量或函数在类的外部是不可访问的，甚至是不可查看的。只有类和友元函数可以访问私有成员。默认情况下，类的所有成员都是私有的。
  //行为或属性
};
```
3.struct
---
结构体
```
struct
{
  int a;
  char b;
  double c;
} s1;
//此声明声明了拥有3个成员的结构体，分别为整型的a，字符型的b和双精度的c，但没有标明其标签，声明了结构体变量s1
```
```
struct SIMPLE
{
  int a;
  char b;
  double c;
};
SIMPLE t1, t2[20], *t3;
//此声明声明了拥有3个成员的结构体，分别为整型的a，字符型的b和双精度的c，结构体的标签被命名为SIMPLE，用SIMPLE标签的结构体，另外声明了变量t1, t2[20], *t3
```
1. 默认的继承访问权限。struct是public的，class是private的。
2. struct作为数据结构的实现体，它默认的数据访问控制是public的，而class作为对象的实现体，它默认的成员变量访问控制是private的。

4.vecter
---
>vector 是向量类型，它可以容纳许多类型的数据，如若干个整数，所以称其为容器。vector 是C++ STL的一个重要成员，使用它时需要包含头文件：`include<vector>`

5.cerr
---
* cout：写到标准输出的ostream对象；
* cerr：输出到标准错误的ostream对象，常用于程序错误信息；cerr不经过缓冲而直接输出，一般用于迅速输出出错信息，是标准错误，默认情况下被关联到标准输出流，但它不被缓冲，也就说错误消息可以直接发送到显示器，而无需等到缓冲区或者新的换行符时，才被显示。
* clog：clog流也是标准错误流,作用和cerr一样,区别在于cerr不经过缓冲区,直接向显示器输出信息,而clog中的信息存放在缓冲区,缓冲区满或者遇到endl时才输出.

6.析构函数
---
析构函数是类的一个成员函数，名字由波浪号加类名构成:释放对象使用的资源，并销毁非static成员。不能带任何参数，也没有返回值（包括void类型）。



二、编译
===

1.terminal编译
---
`g++ -o mipi-demo mipi-demo.cpp`
//编译

`./ mipi-demo`
//执行

2.terminal SSH
---
1. 首先打开终端，然后输入`sudo su - `回车进入根目录
2. 然后输入：`ssh -p 端口号 服务器用户名@ip` （例如ssh -p 22 userkunyu@119.29.37.63）回车，到这会让你输入yes或者no来确认是否连接，输入yes回车
3. 然后输入在服务器上的用户密码回车
4. 到此进入的是你在服务器上的账户的目录，即为连接成功

3.FileZilla
---
略
