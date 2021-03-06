---
date: 2020-10-28T20:02:11+08:00  # 创建日期
author: "Rustle Karl"  # 作者

# 文章
title: "C++ 命名空间"  # 文章标题
url:  "posts/cpp/tutorial/namespace"  # 设置网页永久链接
tags: [ "cpp" ]  # 标签
series: [ "C/C++ 学习笔记"]  # 文章主题/文章系列
categories: [ "学习笔记"]  # 文章分类

# 章节
weight: 20 # 排序优先级
chapter: false  # 设置为章节

index: true  # 是否可以被索引
toc: true  # 是否自动生成目录
draft: false  # 草稿
---

## 标准名空间

命名空间是类、函数、对象、类型和其他名字声明的集合。std 是 C++ 语言的标准名空间，包含了标准头文件中各种名字的声明。

C++ 语言标准头文件有：

```c++
iostream iomanip limit fstream string typeinfo stdexcept
```

C++ 语言标准头文件没有扩展名。使用标准类库的组件时，需要指定名空间。

```c++
#include <iostream>
using namespace std;
```

其中，namespace 是 C++ 的关键字，用于说明命名空间（或称为名字作用域）。声明之后，程序中就可以直接使用 iostream 中的元素（组件名），例如，cin、cout 等。

如果不用 using 声明名空间，则需要在使用时指定组件的名空间。

若包含标准名空间没有定义的头文件，则不能省略扩展名。

### 定义命名空间

C++ 可以识别不同作用域的名字。例如，一个文件中的全局量和局部量可能有相同的名字，或不同类有同名的成员，系统可以根据作用域明确地区分开来。
开发一个应用程序常常需要多个库，它们源自不同的文件，这些文件通常用 include 指令包含进来，而不同的文件可能定义了相同名字的类或函数。

```c++

```



```c++

```

```c++

```


```c++

```






