---
layout: post
title: 从头开始一个新的vue
author: wplay
---

> 今天天气晴朗，风和日丽，扯远了，重新来一个vue-webpack

- 目标：做出一个webpack严格模式的产品模型，测试能否放在199服务器（公司）并能够运行
- 时限：一天
- 模式：vue init webpack  并且使用vue-roouter，unit test，e2e test



## 现在开始！ 
-----

- `vue init webpack vue-web`
- `cd vue-web`
- `git init`
- `git remote add origin git@github.com:wpy007/vue-web.git`
- `git add .`
- `git commit -m 'first commit'`
- `git push origin master`
	- > ps:当我这这里使用 `git pull origin master` 的时候，
	- > 报错 `fatal: Couldn't find remote ref master` , 
	- > 我想了想，发现，嗯，窝草，仓库是空的，根本就没有master分支，
	- > 所以这一步不用管它就好了
- `cnpm install`

***以上就是初始化过程，可用***



