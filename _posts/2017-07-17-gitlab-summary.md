---
layout: post
title: 如何使用gitLab进行团队开发
author: Wplay
---

本博客并非什么gitLab详解教程，仅仅是在你学会了git以及gitHub/gitLab的基本使用`[传送门](https://wpy007.github.io/wpy/git-summary/)`之后，进行的进一步补充
<!-- wplay -->


## 多人合作理念
----- 

> 我并不是为了讲解如何进行前后台的交互，代码的结构目录。而是告诉你多个前端如何共同上传代码到同一仓库
> 


- 前端老大建立一个仓库
- 设置其他成员变为开发者
- gitLab共计四个权限 `owner` `master` `developer` `custom`

### 我所认为合作权限
- 一个`owner` 同时也是`master`
- 一个或有限个`master`
- 其余的全都是`developer`

### 分支数量
- `master` 如果不是直接将master所处的地方当做生产环境，至少应该保持生产环境的代码和master分支的代码是同步的
- `dev` 这里放置着所有的developer共同维护的代码，  


### 设置一个仓库的某分支被保护`protected`

> `project > settings > Repository > protected Branches`
> 在这里可以设置某个分支为`被保护`状态
> 也可以设置`被保护`的分支的权限，哪些人`allow to merge`，哪些人`allow to push`
> 默认的`master`分支是`protected`状态
> 
> 
> 


### 未完，那就不要完了，简简单单就这吧。以后会补充的
