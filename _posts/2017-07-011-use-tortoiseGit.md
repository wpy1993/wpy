---
layout: post
title: 使用tortoiseGit(小乌龟)
author: Wplay
---

安装tortoiseGit. [官网下载](https://tortoisegit.org/download/) 
<!-- wplay -->

## 安装tortoiseGit
-----

- 默认安装，除了路径改为了D盘
- 安装失败，报错2503，没有权限的意思，我想，50%可能性是因为我在安装过程中使用它在d盘新建了文件夹的原因吧，也可能就是需要管理员权限
	+ 对了，记得以管理员身份安装啊！不然报错2503
	+ 以管理员权限安装方法[见网址](http://blog.csdn.net/leedaning/article/details/53138664)
	+ 嗯，安装成功了

> 后续发展，安装中文语言补丁的时候，又报错了2503，看来真的只是必须要在管理员权限中安装啊。。。
> 
> 

- 安装完成后会有`启动向导`，它让我选择git.exe，当然由于我的git安装到了d盘，它自动识别了，所以不用在意它
- 配置用户信息，由于我在git bash中已经配置好了，所以这个也是默认
- 让我配置秘钥，我也让它默认执行了，没有修改
- push的时候报错`no suppported authentication methods`
	+ 原因：git和小乌龟冲突了呗
	+ [解决方案](http://blog.csdn.net/yym6789/article/details/53807640)
	+ ps:在哪里呢？在git安装目录下面`D:\IT\Git\usr\bin\ssh.exe`

- 安装中文语言包（以管理员身份安装）,`tortoiseGit > settings > General > language`,ok~

> 窝草？记录了半天，发现网上有详细的安装blog，详细到每一步骤都有截图，嗯，推荐一下。[传送门](http://blog.csdn.net/renfufei/article/details/41647937)