# front-end-interview-questions
前端面试题整理

## Questions
* [Describe CSS Positions](#describe-css-positions)
* [Describe CSS Box Models](#describe-css-box-models)
* [Describe `apply` And `call`](#describe-apply-and-call)
* [Describe `JSONP`](#describe-jsonp)
* [Describe Event Delegation](#describe-event-delegation)
* [How to Achieve Vertical Align Center](#how-to-achieve-vertical-align-center)
* [Describe two modes of `vue-router`](#describe-two-modes-of-vue-router)

## Answers

### Describe css positions
CSS 定位方式有 static, fixed, relative, absolute, inherit，以及 CSS3 新增的 sticky.
* static - 默认值，元素位于正常文档流中
* fixed - 固定定位，相对于浏览器窗口进行定位
* relative - 相对定位，相对于元素其自身正常位置进行定位
* absolute - 绝对定位，相对于最近一个非 static 定位的父元素进行定位
* sticky - 粘性定位

易错点：绝大多数人都以为 absolute 仅仅是相对于有 relative 的父级节点定位（实际工作中会经常这么用）。

考察：侧面考察求职者对基础知识的积累以及从官方文档学习的能力

### Describe css box models
CSS 盒模型由内容区(Content)、内边距(Padding)、边框(Border)和外边距(Margin)组成.

有两种常用的盒模型：IE 和 W3C
* IE - 元素实际宽度/高度 = 声明的 width/height ; 元素内容区向内挤压
* W3C - 元素实际宽度/高度 = 声明的 width/height + padding + border ; 元素的内容区即为声明的 width/height 尺寸。

CSS box-sizing 属性的两个值可以控制对元素应用哪种盒模型：
* box-sizing: border-box - IE
* box-sizing: content-box - W3C

实际开发中，IE 的盒模型(border-box)应用的更广泛。

考察方式：可以结合盒模型及 offsetWidth 对此知识点进行综合应用考察，防止死记硬背

### Describe `apply` and `call`
Javascript 中的每个函数都有 apply 和 call 方法，用于在函数执行时改变函数内部 this 的指向。第一个参数为替代 this 的对象。
* call - 从第二个参数起，使用逗号分隔的方式为方法传参
* apply - 第二个参数为数组，数组的每个元素作为方法的参数传递

举例考察：Math.max(1, 5, 2, 4, 3) 可以求出一堆参数列表中的最大值。如何利用 apply 实现从一个数组中求出最大值。
```javascript
Math.max.apply(null, arr);
```
也可以利用 ES6 的数组解构实现：
```javascript
Math.max(...arr);
```

考察 JS 基本功，同时出一道应用题以确认求职者会用，而不是背题。

### Describe `JSONP`
JSONP 是实现跨域的一种方式，它是通过动态创建 script 标签赋值 src，并在 URL 中传递 callback 回调函数名称，并配合服务端返回 callback(objects) 的脚本形式触发前端回调函数调用以实现跨域。
注意点：JSONP 只能发起 GET 请求。

考察：如果求职者可以顺利的描述 JSONP 的基本原理，则可以让其尝试简单写一个 JSONP 的实现。

### Describe event delegation
事件代理(或事件委托)，可以为父元素绑定事件，利用事件冒泡机制，可以监听到所有子元素冒泡上来的事件，这样做的好处有两点：
* 无需为每一个子元素都绑定事件，节约资源
* 可以监听到当前的子元素以及将来创建出来的子元素所触发的事件

### How to achieve vertical align center
CSS 实现垂直居中有多种方式：
* 使用 Flex 布局并设置 align-items: center. (如果是纵向排列则 justify-content: center)
* 使用 display: table-cell; vertical-align: middle; 实现
* 将子元素宽高固定，则设置 position:absolute，设置 width 和 height，四个定位都是0, margin:auto
* 如果子元素高度不固定，则设置 top:50%,  transform: translateY(-50%);
* 如果子元素是文字，则可以设置 line-height 与父元素高度相同（仅适用于单行文字）
* 如果父元素高度可变，则可以设置 padding-top 和 padding-bottom 为相同的值实现

### Describe two modes of vue router
Vue Router 有两种路由模式，hash 和 history，默认为 hash
* Hash - 使用 URL Hash 作为路由路径，在 URL 中会出现 # 字样，底层基于 hashchange 事件
* History - 基于 History API 实现，底层基于 history.pushState 和 popstate 事件实现。但由于 URL 是正常形式，通常需要服务端配置支持。