title: 浅谈字符串编码
date: 2014-07-19 22:54:32
tags:
- 编程
categories: 
- 常识

---
#### 1. 字符串的编码是个即简单又麻烦的话题，主要涉及两个不同的概念：字节(byte)和字符(character)


***字节*** 是计算机软件系统的最小存储单位，任何对象最终都是通过字节组合来完成存储的。
***字符*** 也是一种对象，它和具体的语言有关,比如在中文里，“我”是一个字符，不能生生将其当坐几个字节的拼接

#### 2. 历史原因

早期的计算机技术主要是处理英文等字母语言体系，ASCII编码方案足以容纳所有要表达的字符，于是每个字符占一个字节被固定下来，这也为后来造成了一定程度的误解(***将字符和字节等同起来***),随着计算机技术的普及，像东亚语言体系的字符数量就无法用ASCII容纳，人们只好用2个或者更多的字节来表达一个字符，于是就有了像GB2312/GBK/BIG5等种类繁多且不兼容的编码方案

#### 3. 标准化

随着计算机技术的国际化，以往的字符编码方案已经不适应现代软件开发，ISO在参考很多现有方案的基础上统一制定了一种可以容纳世界上所有文字和符号的字符编码方案，这就是Unicode编码方案

#### 4. Unicode

Unicode本质上就是通过特定的算法将不同国家不同语言的字符都映射到数字上。Unicode字符集（UCS）有UCS－2，UCS－4两种标准。UCS－2最多可以表达U+FFFF个字符，而UCS－4则使用4字节编码，首位固定为0，也就是说最多可以有2^31个字符，几乎容纳了全世界所有的字符。

#### 5. UTF

Unicode只是将字符和数字建立了映射关系，但对于计算机而言，要存储和操作任何数据，都得用字节来表示，这就涉及到不同计算机架构得大小端问题（Big Endian,Little Endian）,于是有了几种将Unicode字符数字转换成字节得方法:Unicode字符集转换格式(UCS Transformation Format) ,缩写 UTF

#### 6. UTF-8/16/32

***UTF-8*** 1到4字节不等长方案，西文字符通常只用一个字节，而东亚字符(CJK)则需要三到四个字节

***UTF-16*** 用2个字节无符号整数存储Unicode字符，与UCS-2对应，适合处理中文

***UTF-32*** 用4个字节无符号整数存储Unicode字符，与UCS-4对应，多数时候有点浪费内存空间

UTF－8具有非常良好得平台适应性和交互能力，因此已经成为很多操作系统平台的默认存储编码方案。而UTF-16因为等长，浪费空间较少，拥有更好的处理性能，包括.NET /JVM等都使用2字节的Unicode Char

#### 7. BOM头信息

按照大小端划分，UTF又有BE和LE两种格式，比如UTF-16BE/UTF-16LE等.为了让系统自动识别出BE和LE,通常在头部添加BOM信息，“FE FF” 表示BE,“FF FE”表示LE. 后面还会有一两个字符用来表示UTF-8或UTF-32.
