---
layout: post
title: 奔驰抽奖项目开发总结
author: Wplay 
---

### 关于select标签

- 设置默认的，隐藏的option
	- 在option标签中设置hidden属性,并且selected(否则默认选中非hidden吧?还是默认选中有value的第一个)
- value和text不一样,但是当没有在标签中写value="xxx"属性的时候,text则被拿来顶上了
- 手机h5的option有些不是很一样，并非pc的下拉，android和ios也不同

- 原生js获取被选中的值

```
var mySelect = document.getElementById('mySelect');
var selectedIndex = mySelect.selectedIndex;   // 获取被选中option的下标
var selectedValue = mySelect.options[selectedIndex].value;  // 获取被选中的option的value
var selectedText = mySelect.options[selectedIndex].text;  // 获取被选中的option的text
```

### 关于如何动态的绑定class
```

<div :class="{'prizeNum-tip-blank': prizeNum.length == 0, 'prizeNum-tip-non-blank': prizeNum.length != 0, 'prizeNum-tip': true}"></div>
// 形式 'className': Boolen, ...

```

### 关于华为虚拟按键碍事&&调出键盘事件改变屏幕尺寸

> 处理方式是锁住屏幕的高度，让body由100%变成具体的数据
> 取消所有的fixed定位
> [预备知识](http://blog.csdn.net/woxueliuyun/article/details/8638427)

``` 
window.onload = function () {
	var clientHeight  = document.documentElement.clientHeight;
	document.body.style.height = clientHeight + 'px';

// 记录一下浏览器的高度，因为键盘事件会改变它的高度
window.addEventListener('resize', function () {
	var newHeight = document.documentElement.clientHeight;
	// 如果是类似华为的底部的虚拟按钮，这种小的地方，改变一下body的高度也无妨
	if (Math.abs(newHeight - clientHeight) < 50) {
		document.body.style.height = newHeight + 'px';
	}
		
	/*alert(document.body.style.height);
	alert(document.body.clientHeight);
	alert(document.documentElement.clientHeight);*/
})
```

- 注意上面的几个要点：
	- html <==> document.documentElement
	- body <==> document.body
	- html高度是恒定不变的，body的高度是可能会变化的(臆测的，不可全信)
	