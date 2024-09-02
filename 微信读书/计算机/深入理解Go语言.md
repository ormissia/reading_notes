---
doc_type: weread-highlights-reviews
bookId: "3300059653"
reviewCount: 0
noteCount: 6
author: 刘丹冰
cover: https://cdn.weread.qq.com/weread/cover/77/cpplatform_nhmagh6mnyrbgfugxz55lv/t7_cpplatform_nhmagh6mnyrbgfugxz55lv1684921281.jpg
readingStatus: 读完
progress: 100%
totalReadDay: 2
readingTime: 1小时47分钟
readingDate: 2024-02-21
finishedDate: 2024-03-01
isbn: 9787302613664
category: 计算机 计算机综合
title: 深入理解Go语言
tags: 读书笔记 计算机 计算机综合 读完

---

# 深入理解Go语言

# 元数据
> [!abstract] 深入理解Go语言
> - ![ 深入理解Go语言|200](https://cdn.weread.qq.com/weread/cover/77/cpplatform_nhmagh6mnyrbgfugxz55lv/t7_cpplatform_nhmagh6mnyrbgfugxz55lv1684921281.jpg)
> - 书名： 深入理解Go语言
> - 作者： 刘丹冰
> - 简介： 本书为深入理解学习Go语言必经之路中的重点知识领域，采用大量精美详细的图文介绍，文章讲解深入浅出，极大降低了理解Golang底层精髓的学习门槛。 本书包含3篇：第一篇为深度理论篇（第1章~第4章），包含深入理解Golang中GPM模型、深入理解Golang垃圾回收GC三色标记与混合写屏障、深入理解Golang内存管理模型、网络IO复用模型等。第二篇为Golang实战中需要进阶的知识盲区介绍（第5章~第12章）。第三篇为基于Golang从0到1的实现轻量级网络服务框架Zinx及相关应用案例。 本书主要的面向读者是已经具有软件编程开发经验的工程师、系统开发工程师、期望由Python、PHP、C/C++、Ruby、Java等编程语言转职到Golang开发的后端工程师、期望深入理解Go语言特性的计算机软件学者等。
> - 出版时间 2023-04-01 00:00:00
> - ISBN： 9787302613664
> - 分类： 计算机-计算机综合
> - 出版社： 清华大学出版社

# 高亮划线

## 第3章 Go语言内存管理洗髓经


- 📌 虚拟内存的目的是解决以下几件事：
   (1)物理内存无法被最大化利用。
   (2)程序逻辑内存空间使用独立。
   (3)内存不够，继续虚拟磁盘空间。 ^16-5384-5536
    - ⏱ 2024-03-01 15:44:15 

- 📌 虚拟内存本身是通过一个叫页表(Page Table)的东西实现的 ^16-7473-7505
    - ⏱ 2024-02-29 17:57:01 

- 📌 TCMalloc则是为每个Thread预分配一块缓存，每个Thread在申请内存时首先会从这个缓存区ThreadCache申请，并且所有ThreadCache缓存区还共享一个叫作CentralCache的中心缓存。 ^16-37999-38106
    - ⏱ 2024-02-29 18:13:42 
## 第4章 深入理解Linux网络I/O复用并发模型


- 📌 开发过程中，一般给流的定义有很多种，这里我们用三个特征来描述一个流的定义：
   (1)可以进行I/O操作的内核对象。
   (2)传输媒介可以是文件、管道、套接字等。
   (3)数据的入口是通过文件描述符(fd)描述。 ^17-787-973
    - ⏱ 2024-02-29 18:22:04 

- 📌 epoll给开发者提供了两种触发模式，它们分别是水平触发与边缘触发。 ^17-12294-12328
    - ⏱ 2024-02-29 18:25:45 
## 第8章 defer践行中必备的要领


- 📌 当遇到panic时，会遍历本协程的defer链表，并执行defer。在执行defer的过程中，如果遇到recover，则停止panic，返回recover处继续往下执行。如果没有遇到recover，则遍历完本协程的defer链表后，向stderr抛出panic信息， ^22-5055-5188
    - ⏱ 2024-03-01 14:38:11 
# 读书笔记

# 本书评论
