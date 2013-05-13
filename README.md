9 可视化格式模型
===
## 9.1 可视化格式模型介绍
本章和下章描述可视化格式模型：用户代理为视觉媒体处理文档树的方式。

在可视化格式模型中，文档树中的每一个元素按照盒模型生成0个或多个盒。这些盒的布局由以下定义决定：

* 盒子的尺寸和类型
* 定位方案（正常流，浮动和绝对定位）
* 文档树中的元素之间的关系
* 外部信息（例如，视窗大小，图片元素的本身尺寸等）

本章和下章定义的属性应用于页面媒体和延伸媒体，然而，在页面媒体中，margin属性有不同的意义（详见页面模型）。

可视化格式模型没有明确说明格式模型的所有特征（例如，它没有明确letter-spacing算法）。因此，用户代理对这些规范没有覆盖到的格式化问题可能有不同的实现。


### 9.1.1 视窗

延展媒体的用户代理通常提供一个视窗（屏幕上一个窗口或者其他显示区域）供用户翻阅文档。当视窗大小改变的时候用户代理会改变文档布局（见初始化包含块）。

当视窗比文档渲染完后的画布区域小时，用户代理应该提供一个滚动机制。每个画布至少应该有一个视窗，但用户代理可以渲染出多个画布（例如：给同一个文档提供不同的显示）。

### 9.1.2 包含块（containing blocks）

延展媒体的用户代理通常提供一个视窗（屏幕上一个窗口或者其他显示区域）供用户翻阅文档。当视窗大小改变的时候用户代理会改变文档布局（见初始化包含块）。

当视窗比文档渲染完后的画布区域小时，用户代理应该提供一个滚动机制。每个画布至少应该有一个视窗，但用户代理可以渲染出多个画布（例如：给同一个文档提供不同的显示）。


## 9.2 控制盒的产生

延展媒体的用户代理通常提供一个视窗（屏幕上一个窗口或者其他显示区域）供用户翻阅文档。当视窗大小改变的时候用户代理会改变文档布局（见初始化包含块）。

当视窗比文档渲染完后的画布区域小时，用户代理应该提供一个滚动机制。每个画布至少应该有一个视窗，但用户代理可以渲染出多个画布（例如：给同一个文档提供不同的显示）。


### 9.2.1 块级元素（block-level elements）和块盒（block boxes）

块级元素（block-level elements）是指那些在源文档中以块方式来格式化视觉样式的元素（例如，paragraphs）。下面的这些display属性的值使得一个元素变成块级元素：’block’，’list-item’和’table’。

块级盒（block-level boxes）是指那些作用在一个块格式化上下文中的盒。每个块级元素生成一个主要块级盒，这个块级盒包含了块级元素的子孙盒以及它们生成的内容，并且同时参与了所有的定位方案。除了主要块级盒外，有些块级元素还可能会生成额外的盒子：比如’list-item’元素。这些额外的盒子与主要块级盒有同样的行为。

除了table盒之外，其他的盒将在下面的章节进行描述，而抛开元素来说，一个块级盒也是一个块容器(盒)（block container box）。一个块容器(盒)只能包含块级盒或者建立一个只能包含行内盒的行内格式化上下文。不是所有的块容器(盒)都是块级盒：non-replaced 行内盒和non-relaced table cell是块容器(盒)但不是块级盒。同时是块容器的块级盒称为块盒。

“块级盒block-level box”, “块容器(盒)block container box ”，”块盒block box”这三个术语有时候被明确的简写成”块block”。


#### 9.2.1.1 匿名块盒（anonymous block boxes）

文档中这样的代码：
```html
<div>
some text
<p>more test
</div>
```
（并且假设div和p都有属性“display：block”），div看起来有行内内容跟块内容。为了把定义格式化变得简单，我们假设这里存在一个匿名块盒包围“some text”。


换句话说：如果一个块容器（盒）（就像上面div生成的那个）内部有一个块级盒（就像上面的P），那么我们强制它的内部必须只能有块级盒。

当一个行内盒包含一个流内的块级盒时，该行内盒（和它的行内祖先）
