---
title: "CSS"
---


层叠: 当多个规则作用于同一元素时，我们会使用一系列的规则来决定生效的样式，这一系列的规则便叫做层叠。

1. 样式表的来源: 作者样式表、用户样式表、用户代理样式表（浏览器的默认样式）（优先级左 → 右由高到低）
2. 是否是内联样式: 优先采用内联样式
3. 选择器优先级
4. 样式在样式表中的书写顺序

要想在样式表中覆盖行内样式，在属性值的后面加上 !important:

```css
.feature {
  color: red !important;
}
```
但如果行内样式中也有!important的话，以上代码则不会覆盖行内样式，所以最好的方式就是永远不要在行内样式里加!important。

伪类选择器和属性选择器相当于一个类选择器，*选择器没有任何作用，选择器的优先级是ID > 类 > 标签选择器，一个ID选择器的优先级大于N个类选择器，同理可知，一个类选择器的优先级大于N个标签选择器。

一直以为如果一个样式后面加了!important就无法被覆盖了，刚刚发现，如果两个规则集都选中了这个元素，并且都有!important，这时候就会比较选择优先级...

尽量让选择器的优先级低，这样的话想覆盖也是很容易的事情。

a标签的书写顺序: `a:link → a:visited → a:hover → a:active。`

### Problem

存在一个按钮，它始终固定在视口底部，且点击它会发送请求。关于固定位置可以通过让它的position为fixed来实现，点击事件直接绑定即可。
```css
.btn {
	position: fixed;
	bottom: 0;
	left: 0;
}
```

但是这个按钮存在一个不可点击的可能性（当它点击过一次以后），这个功能也可以使用CSS来实现，当这个按钮不可点击，给它添加disabled类名。

```scss
.btn {
	position: fixed;
	bottom: 0;
	left: 0;
	
	&.disabled {
		pointer-events: none;
	}
}
```

会存在一个隐患，如果这个按钮下方的元素有可点击的事件或者是a标签，当fixed和pointer-events:none同时作用时，会穿透，即按钮下方的元素被触发点击事件。解决方法也很简单，将这两个属性分散在两个元素，父 - 子元素，父元素负责定位，子元素负责点击事件:

```scss
.btn {
	position: fixed;
	bottom: 0;
	left: 0;
	
  // 注意这里&和.disabled中间的空格，代表父 - 子关系
	& .disabled {
		pointer-events: none;
	}
}
```

`flex: 1;`是简写属性，完整的写法:

```css
.flex-1 {
  flex-grow: 1;
  flex-shrink: 1;
  flex-basis: 0;
}
```

em是相对单位，计算方式是当前元素的字号乘以当前的em数：

```css
/* 计算出来box的padding为32px */
.box {
  font-size: 16px;
  padding: 2em;
}
```