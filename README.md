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
* [A Comprehensive Question With Vue](#a-comprehensive-question-with-vue)

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
也可以利用 ES6 的扩展运算符实现：
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
* 如果子元素宽高固定，则设置 position:absolute，设置 width 和 height，四个定位都是0, margin:auto
* 如果子元素高度不固定，则设置 top:50%,  transform: translateY(-50%);
* 如果子元素是文字，则可以设置 line-height 与父元素高度相同（仅适用于单行文字）
* 如果父元素高度可变，则可以设置 padding-top 和 padding-bottom 为相同的值实现

### Describe two modes of vue router
Vue Router 有两种路由模式，hash 和 history，默认为 hash
* Hash - 使用 URL Hash 作为路由路径，在 URL 中会出现 # 字样，底层基于 hashchange 事件和 location.hash 实现
* History - 基于 History API 实现，底层基于 history.pushState 和 popstate 事件实现。但由于 URL 是正常形式，通常需要服务端配置支持。

### A comprehensive question with vue
这是一道关于 Vue.js 的综合题目
```html
<body>
<div id="app">
    <span ref="text">{{ text }}</span>
    <button @click="changeText">改变文字</button>
</div>
</body>
```

```css
body { font-size: 10px; }
#app { font-size: 2em; }
```

```javascript
new Vue({
    el: '#app',
    data: {
        text: '新年好'
    },
    methods: {
        changeText() {
            this.text = '新年快乐';
            console.log(this.$refs.text.offsetWidth);
        }
    }
});
```

问：当点击按钮时，在控制台打印的内容是什么？

本题考察的知识点有：em/px 换算关系、中文字体、offsetWidth、Vue 异步更新 DOM、nextTick。下面是详细分析：
* em 单位继承父元素字体大小，#app中的1em=10px，所以2em=20px
* 在不设置字符间距(letter-spacing)时，一个中文汉字的宽度即为字体大小(font-size)，多个汉字的宽度用 font-size 乘以个数即可
* offsetWidth 叫做偏移宽度，即元素的内容区宽度+padding+border 的宽度，单位是 px，这里 span 未设置 padding 和 border，所以 offsetWidth 就是 span 所包含文字的宽度
* 当点击 changeText 方法时，更新了模型数据 text 为"新年快乐"四个字，此时 DOM 还没有更新，所以第二行代码打印的是改变前的 span 宽度，即"新年好"的宽度，即60
* 如果想打印出80，可以将最后一行代码放置在 Vue.nextTick 回调中，此时回调将在 DOM 更新完成后得到执行。放在 setTimeout(fn, 0)中亦可。

关于 Vue 的异步更新，详见官网文档：[深入响应式原理](https://cn.vuejs.org/v2/guide/reactivity.html)