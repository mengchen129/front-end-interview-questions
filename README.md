# front-end-interview-questions
前端面试题整理

## Questions
* [Describe CSS Positions](#describe-css-positions)
* [Describe CSS Box Models](#describe-css-box-models)

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

