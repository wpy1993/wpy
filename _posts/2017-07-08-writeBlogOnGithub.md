---
layout: post
title: 我的搭建github的blog全程
author: wplay
---

全程记录我如何搭建自己的github博客
<!-- wplay -->

***

[TOC]

***

## Set Github Pages
- 什么是GitHub Pages?
 
> [官网](https://pages.github.com/)说明: 
> `Websites for you and your projects` `hosted directly from your GitHub repository. Just edit, push, and your change are live`
> **翻译**: `把你的仓库变成一个可直接展示的网页` `直接为你的仓库构建服务器，你只需要在仓库修改内容，页面就会变化`
> **说明**: github page简单的理解为为你的项目提供服务器和网址，默认加载index.html文件
 
**操作**
 - 进入你的某一个仓库，点击上方的`settings`
 - `Option > GitHub Pages`，找到这个选项，source默认选中为none，点击更改为`master branch`，save，即看到为你提供的url
 - `master branch/docs folder`不知道是干嘛的，毕竟不可选中，可能是因为我没有符合的文件吧
 - 保存之后，你会看到github pages选项上面有一行提示`your site is ready to be published at xxx`，`xxx`即为默认为你提供的`域名`，进入这个域名即打开了项目的`index.html`文件
 - 如果你不喜欢官方为你提供的域名，`Custom domain`（定制域名）允许你提供自己的域名，它会将仓库指向这个网址，（前提是你掏钱购买了这个域名）
 - 一般情况下我们的代码放在git仓库中的都是源码，也就是不可运行（缺胳膊少腿）的代码，所以`GitHub Pages`并不适合当做我们私人项目的服务器，更适合当做一个写博客的简单网站

## Clone Jekyll
>开启了github pages，我们如何搭建一个可用来写博客的仓库呢？
> 自己写一个框架？好吧，我还没这个能力。。。尴尬，还是网上找模板吧
>推荐[Jekyll](http://jekyll.com.cn/)作为我们的博客框架

> 可能有人进网址去看doc了，其实，上面讲述的是如何依赖`jekyll`开发一套自定义的模板，但是呢，看了下安装，头都大了，嗯，去github上`clone一个现成的模板`当做自己的呗，简单方便

- 首先github，自己搜索关键字`jekyll`，立刻就出来一大堆了好不好！
- 我使用是的这一套模板，[Jekyll-Mono](https://github.com/AkshayAgarwal007/Jekyll-Mono)
- 最快clone方式：`Fork`，没错，点击一下右上角的fork，就把它偷到自己的仓库里面去了，然后`settings`里面修改一下`respository name`，直接就变成自己的了（臭不要脸）

## Change Detail
> 如果英文水平可以的话，跟着fork下来的仓库里面的readme走一遍就能够熟悉了
> 我这里只说一下我自己fork的`Jekyll-Mono`遇到的问题和进行的操作哈（当然大部分是和Jekyll文档匹配的）

- 项目结构一览
	- `_config.yml`就是配置咯，可以说，每一个html文件需要的数据都来自于这里，比如`个人信息` name, discription之类的
	- `index.html`就是`默认主页的框架`(ps，并不一定所有的内容都在里面，它只是个外壳放置了header和footer)
	- `_layouts/`里面就是一个组件页面了，default就是默认的content显示内容
	- `_includes/`提供了默认的一些东西，基本来说，只有这个文件夹不要乱动
	- `_sass/`就是这个框架的样式了，如果你有很好的UI，可以自由修改哦
	- 头像位置，默认在`_sass/_jekyll-mono.scss`里面`.ch-info-wrap`有个`background`，所以说，你把images文件夹下面的`avatar.jpg`替换掉即可（注意咯，最好的220*220尺寸，不然你就去修改scss，添加一个`background-size`属性）
	- `博客的摘要(excerpt)`，也就是博客列表中标题下面的摘要
		- 这个折腾了我好久啊，不舍得不要，但是我写的markdown，作者提供的excerpt解析方式我没有找到
		- 我明明按照模板上面的格式写得，但是就是没有办法解析excerpt成功，它总是把我所有内容全都解析为摘要!
		- 只知道在index.html里面作者如下写到，但是没找到他怎么解析这个excerpt的
		
			```

			<div class="entry">
				\{{ post.excerpt }\}
			</div>
			
			```

		- 还好我机智，谷歌了好久，找到一种方式，就是自己在该处手写一个解析不就行了嘛！[解决方案传送门](https://gist.github.com/benbalter/5555369)
		- 修改后的内容为下，也就是说，我的博客里，从上面开始读，但凡读取到`<!-- wplay -->`这个字段就停止读取，截取已读取的内容作为摘要
		
			```		
			<div class="entry">
				\{{ post.content | split:'<!-- wplay -->' | first \}}
			</div>
			```

## Write Blog
> 好了，可以开始写博客了，所有的博客放置在`_posts/`里面，必须按照格式`year-month-day-title`来书写，（ps：记得之前找到了，现在又找不到了，尴尬），反正就是需要提取出来`year-month-day`以此来给博客列表进行排序并且记录时间的
> 最后，在`_posts/`里面新建一个markdown文件开始blog的撰写吧！

## Q&A
我发现了，sublime写markdown保存后页面无法刷新的原因很可能是因为没有使用服务器！窝草。。。

- Q: 为啥要在这里写博客？
- A: 尝试过，
	- 有道云笔记里面写md，支持的功能太少，最主要的图片支持功能很差
	- 博客园等网站写博客，无人问津，写了一篇总是很快被移除，那么，既然没人看，就更彻底一点吧
	- 买个自己的域名，买个自己的云端，但是我特么没钱更重要的是，我不会啊！以后吧

