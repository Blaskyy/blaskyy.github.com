---
layout: post
title: 离开OpenSUSE, 来到Chakra
category: linux
tags: [linux, chakra]
---
{% include JB/setup %}
如果不是经过百般失败后终于成功装上了Archlinux，如果没有体验到pacman以及AUR的便捷，可能OpenSUSE现在依然还是我最喜欢的发行版～

前几天在虚拟机下各种折腾了下Arch，那可是真折腾啊！不过收获还是很大的～用了pacman+AUR之后真的觉得以前的各种包管理就跟屎一样， 这也是我投奔Chakra的直接原因。不得不说，确实有点受够了OpenSUSE安个软件前refresh半天以及各个repo中重复的不同版本的packages。编程时还要装各种各样的devel包。

Chakra提供类似于yaourt的ccr来使用社区软件仓库（Chakra Community Repository）

桌面环境的话个人比较倾向于功能强大且稳定的KDE，Chakra提供了最纯净的KDE环境，常用GTK软件都以Bundle的形式安装，个人觉得Bundle的好处就是不污染，无残留。（对于强迫症，完美主义，以及系统洁癖的人来说这点很重要！）这也就是我不用Arch+KDE而用Chakra的原因之一。

关于为何选择了Chakra而不是Arch+KDE的另一个原因就是Chakra的半滚动无痛更新，虽说OpenSUSE也有Tumbleweed版，但是每当新版本发布时zypper dup之后总是各种疼～和Arch的滚动发行比区别在于Chakra GNU/Linux 的核心包的更新至少经过数周至数月的测试，才会升级到最新版。目的就是让系统更加稳定。相反地，软件和桌面组件会在发布新版本第一时间，更新到最新版。目的就是让用户能用到最新的桌面与软件。这一点很符合我个人的取向。

`额外收获：N卡手工安装驱动with dkms成功且没折腾一点~`
桌面截图一张(其实跟在OpenSUSE下没啥区别)
http://ww1.sinaimg.cn/large/719bb945jw1e0z3p6t8k0j.jpg
