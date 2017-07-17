---
layout: post
title: 一部分前端面试题（未完）
author: Wplay
---

本博客用来记录随手搜集的前端面试题（高端版）
<!-- wplay -->

### 前端高级面试题总结

- prototype和 __proto__ 的关系是什么
	+ [解释](https://www.zhihu.com/question/34183746)
	+ `__proto__`: 隐式原型  构成原型链
	+ `prototype`: 显式原型  用来实现基于原型的继承与属性的共享
	+ `__proto__`指向创建这个对象的 `函数(construtor)` 的`prototype`

- meta viewport原理
	- [解释](http://www.cnblogs.com/pigtail/archive/2013/03/15/2961631.html)
	- 手机浏览器是没有自己的窗口宽度的（通俗的将，没有兼容去适合手机的宽高的浏览器）
	- viewport是一个虚拟的窗口，默认是比手机屏幕宽很多的，设置缩放就能够适应手机屏幕
	- `<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, minimum-scale=1, user-scalabel=no">`
	- 让dpi和设备的真实分辨率相同

- 域名收敛是什么
	+ [解释](https://segmentfault.com/a/1190000004641599) `里面也讲述了白屏事件的原理`
	+ **这个问题属于前端优化**  
	+ 域名收敛(`domain of convergence`)属于`DNS优化`
	+ 具体操作，在手机端的域名数不要超过5个，html，css，js，img，fonts，这五个即可，img用sprite图
	+ 其余的，尽量使用DNS，这样减少了向本地的服务器的请求数量，防止堵塞（我是这么理解的）

- float和display: inline-block的区别
	+ [传送门1](http://www.cnblogs.com/scot/p/5501669.html)
	+ [传送门2](http://www.cnblogs.com/zyh-club/p/4702994.html)
	+ [传送门3](http://blog.163.com/zx_1258/blog/static/1332337992012111184519374/) : inline-block的优点：垂直对其，文字环绕
	+ `float`它脱离了文档流，所以和它紧挨着的元素会跑到它的前面
	+ `inline-block`在`小于ie8`的情况下需要兼容，并且它需要`vertical-align: top;` 对其，并且标签之间的空格会有影响

- 前端优化策略
	+ [传送门1](http://blog.csdn.net/mahoking/article/details/51472697)


- 首屏，白屏时间如何计算
	- 白屏时间计算 `redirect > app cache > 	DNS > TCP > request > response`
	- [强大的传送门](http://www.cnblogs.com/littlelittlecat/p/6810294.html)

- 闭包
	> ```
	> function foo(x) {
	>     var tmp = 3;
	>     return function (y) {
	>         console.log(x * 2 + y + (++tmp));
	>     }
	> }
	> var bar = foo(2); // bar 现在是一个闭包
	> bar(10);  //18
	> ```
	
	- 答案 18,解释：foo(2)代表这个函数的执行结果，也就是说它指向return出来的这个函数，所以`x = 2`, `y = 10`

	```
	function foo(x) {
	var tmp = 3;
	return function (y) {
	    console.log(x + y + tmp);
	    x.memb = x.memb ? x.memb + 1 : 1;
	    console.log(x.memb);
	    }
	}
	var age = new Number(2);
	var bar = foo(age); // bar 现在是一个引用了age的闭包
	bar(10);  // 15 1
	bar(10);  // 15 2
	bar(10);  // 15 3
	bar(10);  // 15 4
	console.log(age.memb)  // 窝草，竟然是4！！！
	```

	- 解释，虽然foo被销毁了，但是`内存常驻`了，所以x从此有了一个子,x.memb从此被定义了。。。（不知道可以不可以这样理解）
	- 虽然不懂，但是age.memb被改变这个就叫`内存泄露`

	- [闭包传送门](http://kb.cnblogs.com/page/110782/)


- 作用域链
- ajax的实现(全过程)

- jsonp的实现
- 怎么处理跨域
- restful和method的解释
- get和post的区别
- 事件模型解释
- 编写一个元素拖拽插件
- 编写一个`contextmenu`的插件
- 编写web端cookie的设置和获取方法
- 兼容ie6的水平垂直居中
- 兼容ie的事件封装
- h5和原生android的优缺点
- 编写h5需要注意什么
- xss和crsf的原理以及如何预防
- css优先级（高级到底是啥意思？高级是权重高还是低？）
- 如何实现radio的文字描述控制radio的状态(通过label实现)
- delegate如何实现
- 


- 如何说服对方使用jsBridge

### http协议
- accept是什么，怎么用？
- http协议状态码，302和303的区别
- 前端缓存如何实现，etag如何实现，etag和cache-control的max-age的优先级哪个比较高，为什么，cache-control和expire优先级哪个比较高以及为什么