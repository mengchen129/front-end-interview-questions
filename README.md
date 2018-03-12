# front-end-interview-questions
前端面试题整理

## Questions
* [Describe CSS Positions](#describe-css-position)


## Answers

### describe-css-position
CSS 定位方式有 static, fixed, relative, absolute, inherit，以及 CSS3 新增的 sticky.
* static - 默认值，元素位于正常文档流中
* fixed - 固定定位，相对于浏览器窗口进行定位
* relative - 相对定位，相对于元素其自身正常位置进行定位
* absolute - 绝对定位，相对于最近一个非 static 定位的父元素进行定位
* sticky - 粘性定位

易错点：绝大多数人都以为 absolute 仅仅是相对于有 relative 的父级节点定位（实际工作中会经常这么用）。
考察：侧面考察求职者对基础知识的积累以及从官方文档学习的能力


