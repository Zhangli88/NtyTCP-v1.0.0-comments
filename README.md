NtyTCP 注释版，仅供学习使用。
原仓库地址：https://github.com/wangbojing/NtyTcp

NtyTCP-v1.0.0-comments
===========================
****
	
|Author|徐昌隆|
|---|---
|E-mail|xclsoftware@163.com

****
### 零、前言
#### 1、NtyTCP 介绍
    NtyTCP 是王博靖前辈开发的单线程用户态TCP/IP协议栈，包含epoll实现代码、服务器案例、并发测试案例。原仓库地址：https://github.com/wangbojing/NtyTcp
#### 2、本仓库的说明
    在工作中，由于要解决很多棘手问题，阅读源代码了解原理是开发人员的必修课。为了记录我的学习过程，并且也为了和他人分享我的成果，本仓库会保存我对 NtyTCP 的详细的注释，
内容会不断的更新，如果我的分享能够帮助大家进步，请告诉我，我会非常开心的。😊

    感谢王博靖前辈的开源精神，让我对epoll实现原理有了深刻的理解，在这里对他表示非常的感谢！
### 一、目录介绍
（后期补充）
### 一、整体框架
（后期补充）
### 三、更细日志
#### 1、2019-10-25
    截至到今天，已完成对 epoll_create()、epoll_ctl()、epoll_wait()、epoll_event_callback()、epoll_destroy()等接口函数的初步注释，具体内容如下：
   * epoll_create()：申请 _nty_socket 的详细过程、红黑树和双向链表初始化。
   * epoll_ctl()：向 epoll 中增加、删除、修改监控的 sokcet 及其对应的事件。【实际上就是在红黑树上对节点（包含 socket 和待监控的事件的结构体的指针）进行增删改操作】
   * epoll_wait()：从 epoll 中获取就绪事件的过程，即：循环遍历 epoll 的双向链表，若双向链表中有了节点，说明有了事件发生，将最多返回指定数目的节点内容。
   * epoll_event_callback()：该函数是回调函数，由网卡驱动调用。当事件来临时会先检查红黑树中是否存在该 socket，若存在则将发生的事件放到节点中，最后将该节点放入双向链表中，供 epoll_wait() 调用。
   * epoll_destroy()：遍历双向链表，去掉所有节点。遍历红黑树，free 所有节点。

（ 完 ）