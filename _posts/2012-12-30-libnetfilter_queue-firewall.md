---
layout: post
title: 利用Netfilter打造用户态防火墙
category: linux
tag: [libnetfilter_queue, firewall]
---
{% include JB/setup %}
###前言
由于在新版内核中nfnetlink_queue已经取代了ip_queue, 所以在一些较新的发行版中无法进行老师给的实验.

这篇文章是利用nfnetlink_queue机制代替ip_queue机制完成ISDP实验`利用Netfilter构建用户态防火墙`

[实验源码](https://github.com/Blaskyy/isdpclass/tree/master/lab12)

###环境:
######设置iptables过滤规则为:所有从本机发出的icmp包全部到自己编写的应用程序
	#modprobe iptables_filter
	#modprobe nfnetlink_queue
	#iptables -A OUTPUT -p tcp -j NFQUEUE
	#iptables -A OUTPUT -p icmp -j NFQUEUE
######编写应用程序, 功能如下:
	1. 允许从本机出发, 目的地址为win xp ip的icmp包;
	2. 丢弃其他任何icmp包;
	3. 当出现错误时, 做错误处理, 能够清理占用资源, 退出程序.

###编译:
######源码自己去看哈(其实没什么看得)
	编译时遇到了点小麻烦, 我是在 OpenSUSE 12.2 libnetfilter_queue v1.0.1 环境下编译的, 编译时提示找不到 libnetfilter_queue.h 这个头文件, 后来发现libnetfilter_queue.h 这个文件在 /usr/include/libnetfilter_queue-1.0.1/libnetfilter_queue/ 目录下, 而不是在本该在的 /usr/include/libnetfilter_queue/ 目录下. 我还以为是 SUSE 的打包人员打包的时候把 _includedir 写错了, 还特意去 Bugzilla 上提交了个 Bug.
	最终结果原来是我火星了, 竟不知道有 pkg-config 这玩意.(如果你也不知道的话, 请移步维基百科: https://zh.wikipedia.org/zh/Pkg-config).

######写了个用了 pkg-config 的简单的 Makefile
{% highlight mf %}
ifeq ($(shell pkg-config --exists libipq; echo $$?), 0)
	IPQ_CFLAGS = $(shell pkg-config --cflags libipq)
		IPQ_LIBS = $(shell pkg-config --libs libipq)
else
	IPQ_CFLAGS =
		IPQ_LIBS = -lipq
endif

ifeq ($(shell pkg-config --exists libnetfilter_queue; echo $$?), 0)
	NFQ_CFLAGS = $(shell pkg-config --cflags libnetfilter_queue)
	NFQ_LIBS = $(shell pkg-config --libs libnetfilter_queue)
	else
	NFQ_CFLAGS =
	NFQ_LIBS = -lnetfilter_queue
endif

all:nfq_firewall ipq_firewall

nfq_firewall:nfq_firewall.c
	gcc -o nfq_firewall nfq_firewall.c $(NFQ_CFLAGS) $(NFQ_LIBS)

ipq_firewall:ipq_firewall.c
	gcc -o ipq_firewall ipq_firewall.c $(IPQ_CFLAGS) $(IPQ_LIBS)

clean:
	rm -f nfq_firewall ipq_firewall
{% endhighlight %}
