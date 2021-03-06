---
date: 2020-10-29T22:00:25+08:00  # 创建日期
author: "Rustle Karl"  # 作者

# 文章
title: "C/C++ 结构体"  # 文章标题
url:  "posts/cpp/tutorial/struct"  # 设置网页永久链接
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

## 概述

在C语言中，结构体（struct）指的是一种数据结构，是C语言中复合数据类型（aggregate data type）的一类。结构体可以被声明为变量、指针或数组等，用以实现较复杂的数据结构。结构体同时也是一些元素的集合，这些元素称为结构体的成员（member），且这些成员可以为不同的类型，成员一般用名字访问。

结构由数目固定的成员（又称域、项目或元素）构成，各成员可以具有不同的数据类型，包括基本类型和非基本类型。一个结构变量在内存占有一片连续的存储空间，但是，因为各数据成员的类型不相同，所以具有特定的定义和访问形式。

## 定义结构

结构体的定义如下所示，struct 为结构体关键字，tag 为结构体的标志，member-list 为结构体成员列表，其必须列出其所有成员； variable-list 为此结构体声明的变量。

```c++
struct tag { member-list } variable-list;
```

在一般情况下，tag、member-list、variable-list 这 3 部分至少要出现 2 个。

### 三种方式示例

```c++
// 此声明声明了拥有 3 个成员的结构体，分别为整型的 a，字符型的 b 和双精度的 c
// 同时又声明了结构体变量 s1，这个结构体并没有标明其标签
struct 
{
    int a;
    char b;
    double c;
} s1;
```

```c++
// 此声明声明了拥有 3 个成员的结构体，分别为整型的 a，字符型的 b 和双精度的 c
// 结构体的标签被命名为 SIMPLE，没有声明变量
struct SIMPLE
{
    int a;
    char b;
    double c;
};
//用 SIMPLE 标签的结构体声明变量 t1、t2、t3
struct SIMPLE t1, t2[20], *t3;
```

```c++
// 用 typedef 创建新类型
typedef struct
{
    int a;
    char b;
    double c; 
} Simple2;
// 可以用 Simple2 作为类型声明新的结构体变量
Simple2 u1, u2[20], *u3;
```

在上面的声明中，第一个和第二声明被编译器当作两个完全不同的类型，即使他们的成员列表是一样的，如果令 t3 =& s1，则是非法的。

结构体的成员可以包含其他结构体，也可以包含指向自己结构体类型的指针，而通常这种指针的应用是为了实现一些更高级的数据结构如链表和树等。

```c++
//此结构体的声明包含了其他的结构体
struct COMPLEX
{
    char string[100];
    struct SIMPLE a;
};

//此结构体的声明包含了指向自己类型的指针
struct NODE
{
    char string[100];
    struct NODE *next_node;
};
```

如果两个结构体互相包含，则需要对其中一个结构体进行不完整声明，如下所示：

```c++
struct B;    //对结构体 B 进行不完整声明

//结构体 A 中包含指向结构体 B 的指针
struct A
{
    struct B *partner;
    //other members;
};

//结构体 B 中包含指向结构体 A 的指针，在 A 声明完后，B 也随之进行声明
struct B
{
    struct A *partner;
    //other members;
};
```

## 结构体变量存储

在内存中，编译器按照成员列表顺序分别为每个结构体变量成员分配内存，当存储过程中需要满足边界对齐的要求时，编译器会在成员之间留下额外的内存空间。如果想确认结构体占多少存储空间，则使用关键字 sizeof，如果想得知结构体的某个特定成员在结构体的位置，则使用 offsetof 宏 ( 定义于 stddef.h)。

```c++
struct SIMPLE
{
    int a;
    char b;
};

//获得SIMPLE类型结构体所占内存大小
int size_simple = sizeof( struct SIMPLE );

#define offsetof(structName, memName) (int)&((structName*) 0)->memName

//获得成员b相对于SIMPLE储存地址的偏移量
int offset_b = offsetof( struct SIMPLE, b );
```

## 匿名结构体

匿名 struct、匿名 union 以及 C ++的匿名 class，是指既没有类型名，也没有直接用这种类型定义了对象；如果紧随类型定义之后，又定义了该类型的对象，就不算是匿名类型，与普通情形的使用是一样的。

匿名类型作为嵌套定义，即在一个外部类（这里的类是指 struct、union、class ）的内部定义，则编译器就在匿名类型定义之后定义一个无名变量，并把该匿名类型的数据成员的名字提升到匿名类的外部类的作用域内。如果匿名类型是连续嵌套，则最内部的匿名类型的成员名字被提升到最外部的可用变量名字访问的类的作用域内。

```c++
    struct sn{
        struct { int i;};  /* 匿名 struct */
    } v1;

   v1.i=101;
```

## 声明结构体类型变量

可以用两种方式说明结构变量：在定义类型的同时说明变量；或者，在类型定义之后说明变量。

```c++
struct Book {
    int code;
    double price;
} book, *pBook;
```

在结构定义之后，使用类型标识符说明变量：

```c++
struct Book {
    int code;
    double price;
};

Book book, *pBook;
```

语法原则是首先定义类型，然后说明变量。通常可以把类型定义放在一个头文件中，使用时用 include 指令嵌入。

说明结构变量的同时可以进行初始化，例如：

```c++
Book book = {1000, 36.5};
```

## 访问结构体

普通变量说明时就开辟内存空间，而结构类型中说明的数据成员仅仅描述了数据的组织形式，这就是“类型”的概念。当说明结构变量之后，系统为变量建立各自的存储空间。所以，把结构的数据成员看做普通变量是错误的。数据成员必须在结构变量说明后才有存储意义

访问结构变量成员使用圆点运算符：

```c++
int main() {
    Book book = {1000, 36.5};
    cout << book.code << endl;
    cout << book.price << endl;
}
```

访问结构指针变量：

```c++
int main() {
    Book book = {1000, 36.5};
    Book *pBook = &book;
    cout << pBook->code << endl;
    cout << (*pBook).price << endl;
}
```

pBook 是结构类型的指针，若执行 pBook++，则偏移量是一个结构的长度。而结构的各数据成员具有不同的类型，因此，要访问结构变量里的各成员不能用指针偏移方式而只能用“.”运算符。这与数组元素操作不同。

类型相同的结构变量可以使用赋值运算。所谓“类型相同的变量”，是指用同一个类型标识符说明的变量。

## 结构数组

数组元素类型可以是基本类型，也可以是已经定义的构造类型。当数组的元素类型为结构类型时，称为结构数组。其定义和访问方式遵循数组和结构的语法规则。
