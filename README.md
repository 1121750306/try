[标题1](#标题1)
# 标题1
* HTML和CSS
	* [opacity,display,visibility](#html1)
	* [文字超出用...](#html2)
	* [渐进增强和优雅降级](#html3)
	* [link 和 @import 的区别](#html4)
	* [对position属性的理解](#html5)
	* [行内元素和块级元素](#html6)
	* [水平居中，垂直居中，水平垂直居中](#html7)
	* [flex布局](#html8)
	* [box-sizing属性](#html9)
	* [CSS选择器](#html10)
	* [哪些属性可以继承](#html11)
	* [CSS3新增伪类选择器，以及伪类有哪些](#html12)
	* [对语义化的理解](#html13)
	* [Doctype作用? 严格模式与混杂模式如何区分？它们有何意义?](#html14)
	* [HTML与XHTML——二者有什么区别](#html15)
	* [回流（Reflow）和重绘（Repaint）](#html16)
	* [浮动造成的结果，以及清除浮动的方法](#html17)
	* [W3C标准都有什么](#html18)
	* [对BFC的理解，BFC的触发条件都有哪些](#html19)
	* [部分属性的百分比，是相对于什么的](#html20)
	* [窗口和元素的各种宽高距离](#html21)
	* [HTML5新增标签](#html22)
	* [多条注释判断浏览器版本]（#html23）
* JAVASCRIPT
* [常见兼容性问题]
 </br>

# HTML和CSS
#### html1

 >`display:none`,`opacity=0`和`visibility:hidden`的区别？ 说出6种隐藏元素的方法？

	display:none  隐藏对应的元素，在文档布局中不再给它分配空间，它各边的元素会合拢，就当他从来不存在。
	opacity=0  透明度为0，子元素不能通过改变透明度来反隐藏。。。只有这个可以触发绑定事件。
	visibility:hidden  隐藏对应的元素，但是在文档布局中仍保留原来的空间，子元素可以visibility:visible来反隐藏。
	
#### html2

 > 文字超出部分用...来表示
 
 	overflow: hidden; 
 	text-overflow:ellipsis; 
	white-space: nowrap;
	/*上面仅支持单行文本,多行呢？*/

	display: -webkit-box; 
	-webkit-box-orient: vertical; 
	-webkit-line-clamp: 3; 
	overflow: hidden;

	使用了WebKit的CSS扩展属性，该方法适用于WebKit浏览器及移动端；
 
 #### html3
 
  > 渐进增强和优雅降级
  
  	渐进增强 ：针对低版本浏览器进行构建页面，保证最基本的功能，然后再针对高级浏览器进行效果、交互等改进和追加功能达到更好的用户体验。
	
	优雅降级 ：一开始就构建完整的功能，然后再针对低版本浏览器进行兼容。

#### html4

 > link 和 @import 的区别
 
	1.link属于HTML标签，而@import( CSS2.1 )是CSS提供的;

	2.页面被加载的时，link会同时被加载，而@import被引用的CSS会等到引用它的CSS文件被加载完再加载;

	3.import只在IE5以上才能识别，而link是HTML标签，无兼容问题;

	4.link方式的样式的权重 高于@import的权重.

#### html5

 > 对position的理解
 <pre><code>
 position：static | relative | absolute | fixed | center | page | sticky
 默认值：static，center、page、sticky是CSS3中新增加的值。
(1)、static 
可以认为静态的，默认元素都是静态的定位，对象遵循常规流。此时4个定位偏移属性不会被应用，也就是使用left，right，bottom，top将不会生效。

(2)、relative 
相对定位，对象遵循常规流，并且参照自身在常规流中的位置通过top，right，bottom，left这4个定位偏移属性进行偏移时不会影响常规流中的其他元素。

(3)、absolute 
a、绝对定位，对象脱离常规流，此时偏移属性参照的是离自身最近的定位祖先元素，如果没有定位的祖先元素，则一直回溯到body元素。盒子的偏移位置不影响常规流中的任何元素，其margin不与其他任何margin折叠。
b、元素定位参考的是离自身最近的定位祖先元素，要满足两个条件，第一个是自己的祖先元素，可以是父元素也可以是父元素的父元素，一直找，如果没有则选择body为对照对象。第二个条件是要求祖先元素必须定位，通俗说就是position的属性值为非static都行。

(4)、fixed 
固定定位，与absolute一致，但偏移定位是以窗口为参考。当出现滚动条时，对象不会随着滚动。

(5)、center 
与absolute一致，但偏移定位是以定位祖先元素的中心点为参考。盒子在其包含容器垂直水平居中。（CSS3）

(6)、page 
与absolute一致。元素在分页媒体或者区域块内，元素的包含块始终是初始包含块，否则取决于每个absolute模式。（CSS3）

(7)、sticky 
对象在常态时遵循常规流。它就像是relative和fixed的合体，当在屏幕中时按常规流排版，当卷动到屏幕外时则表现如fixed。该属性的表现是现实中你见到的吸附效果。（CSS3）
</code></pre>

#### html6

 > 行内元素和块级元素
<pre><code>
 块级元素可以包含块级元素和行内元素，行内元素只能包含行内元素。
 块级元素可以设置宽高，行内元素不能设置宽高。
 块级元素的margin和padding四周都有效，行内元素的margin和padding只在水平方向（left和right）有效
 
 常见块级元素： div , p , form , ul , li , ol , dl , form , address , fieldset , hr , menu , table
 常见行内元素： span, strong , em , br , label , select , textarea , cite （注：img和input属于特殊的行内元素，又叫行内可替代元素）
</code></pre>

#### html7

 > 水平居中
 <pre><code>
 变为inline或者inline-block，给其父元素text-align:center。
 
 定宽和块级元素，使用margin：0 auto。
 
 使用flex布局。
 
 通过给父元素设置 float，然后给父元素设置 position:relative 和 left:50%，子元素设置 position:relative 和 left:-50% 来实现水平居中
 </code></pre>
 
 > 垂直居中
 ```css
 	单行文本使用height和line-height实现。
 
	vertical-align：middle。只在父元素为th和td有效。
 
 	垂直居中：多行的行内元素解决方案
  	组合使用display:table-cell和vertical-align:middle属性来定义需要居中的元素的父容器元素生成效果，如下：
  	.parent {
   	  background: #222;
   	  width: 300px;
    	  height: 300px;
      
   	  /* 以下属性垂直居中 */
    	  display: table-cell;
    	  vertical-align:middle;
   	 }
 	 垂直居中：已知高度的块状元素解决方案
 	 .item{
      	  top: 50%;
      	  margin-top: -50px;  /* margin-top值为自身高度的一半 */
      	  position: absolute;
      	  padding:0;
   	 }
 ```
#
 > 水平垂直居中
 
 ```css
 水平垂直居中：未知高度和宽度元素解决方案

   .item{
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);  /* 使用css3的transform来实现 */
   }

 使用flex
   .parent{
        display: flex;
        justify-content:center;
        align-items: center;

        /* 注意这里需要设置高度来查看垂直居中效果 */
        background: #AAA;
        height: 300px;
    }
 ```

#### html8

 > flex布局
```css
	`flex-direction`    主轴方向 row,row-reverse,column,column-reverse

	`flex-wrap`     是否换行  wrap，nowrap,wrap-reverse

	`flex-flow` :<direction> <wrap>
	
	`justify-content` :主轴对齐方式 flex-start,flex-end,center,space-between,space-around

	`align-item` :交叉轴对其方式 flex-start,flex-end,center,baseline,strench(占满)

	`align-content` :多跟轴线的对齐方式 属性值同上

	`order` :先后排序，由小到大

	`flex-grow`  默认0，都不放大。如果所有项目的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍

	`flex-shrink`   默认1，空间不足时该项目缩小。如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。负值对该属性无效

	`flex` 属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。该属性有两个快捷值：auto (1 1 auto) 和 none (0 0 auto)

	`align-self`   自定义当前项目的对齐方式，属性为baseline和strench
```

#### html9
 > box-sizing属性
 
 ```css
 content-box (W3C模型)   Width = width + padding-left + padding-right + border-left + border-right
 padding-box             Width = width(包含padding-left + padding-right) + border-top + border-bottom
 border-box (IE)         Width = width(包含padding-left + padding-right + border-left + border-right)
 
 ```

#### html10
 > CSS选择器
 ```css
    1.id选择器（ # myid）

    2.类选择器（.myclassname）

    3.标签选择器（div, h1, p）

    4.相邻选择器（h1 + p）

    5.子选择器（ul > li）

    6.后代选择器（li a）

    7.通配符选择器（ * ）

    8.属性选择器（a[rel = "external"]）

    9.伪类选择器（a: hover, li:nth-child）
 ```

#### html11
 > 哪些属性可以继承
 ```css
  不可继承的：
    display、margin、border、padding、background、height、min-height、max-height、width、min-width、max-width、overflow、position、left、right、top、bottom、z-index、float、clear、table-layout、vertical-align、page-break-after、page-bread-before和unicode-bidi

  所有元素可继承：visibility和cursor

  内联元素可继承：
    letter-spacing、word-spacing、white-space、line-height、color、font、font-family、font-size、font-style、font-variant、font-weight、text-decoration、text-transform、direction

  终端块状元素可继承：text-indent和text-align

  列表元素可继承：list-style、list-style-type、list-style-position、list-style-image

  表格元素可继承：border-collapse
 ```

#### html12
 > CSS3新增选择器
 ```CSS
    p:first-of-type 选择属于其父元素的首个 <p> 元素的每个 <p> 元素。

    p:last-of-type  选择属于其父元素的最后 <p> 元素的每个 <p> 元素。

    p:only-of-type  选择属于其父元素唯一的 <p> 元素的每个 <p> 元素。

    p:only-child    选择属于其父元素的唯一子元素的每个 <p> 元素。

    p:nth-child(2)  选择属于其父元素的第二个子元素的每个 <p> 元素。

    :enabled  :disabled 控制表单控件的禁用状态。

    :checked        单选框或复选框被选中。
 ```
 > 伪类选择器有哪些
 ```css
first-child()
last-child()
link
visited
hover
active
focus
after
before
first-letter
first-line
lang(language)

 ```

#### html13
 > 对语义化的理解
 ```css
    1.去掉或者丢失样式的时候能够让页面呈现出清晰的结构

    2.有利于SEO：和搜索引擎建立良好沟通，有助于爬虫抓取更多的有效信息：爬虫依赖于标签来确定上下文和各个关键字的权重；

    3.方便其他设备解析（如屏幕阅读器、盲人阅读器、移动设备）以意义的方式来渲染网页；

    4.便于团队开发和维护，语义化更具可读性，是下一步吧网页的重要动向，遵循W3C标准的团队都遵循这个标准，可以减少差异化。
 ```

#### html14
 > Doctype作用? 严格模式与混杂模式如何区分？它们有何意义?
 ```css
    1.<!DOCTYPE> 声明位于文档中的最前面，处于 <html> 标签之前。告知浏览器以何种模式来渲染文档。

    2.严格模式的排版和 JS 运作模式是  以该浏览器支持的最高标准运行。

    3.在混杂模式中，页面以宽松的向后兼容的方式显示。模拟老式浏览器的行为以防止站点无法工作。

    4.<!DOCTYPE> 不存在或格式不正确会导致文档以混杂模式呈现。
 ```
 
 #### html15
  > HTML与XHTML——二者有什么区别
  ```css
   XHTML中：区别：

    1.所有的标记都必须要有一个相应的结束标记

    2.所有标签的元素和属性的名字都必须使用小写

    3.所有的XML标记都必须合理嵌套

    4.所有的属性必须用引号""括起来

    5.把所有<和&特殊符号用编码表示

    6.给所有属性赋一个值

    7.不要在注释内容中使“--”

  ```
  
  #### html16
   > 回流（Reflow）和重绘（Repaint）
   ```css
  
  回流 
  当render树的一部分或者全部因为大小边距等问题发生改变而需要重建的过程，叫做回流。（回流相当于给人做了一次抽脂手术）
      发生情况：
       1、页面渲染初始化。
       2、DOM结构变化，比如删除了某个节点。（骨头都被打断了，肯定比抽脂更严重，所以会引发回流）
       3、render树变化，比如减少了padding。（也就是进行抽脂手术）
       4、窗口resize事件触发。
       5、字体大小
  重绘 
  当诸如颜色背景等不会引起页面布局变化，而只需要重新渲染的过程叫做重绘。（重绘就好像给人染了一个头发）
      发生情况：
       1、字体颜色、元素背景

  重绘的代价要比回流小，毕竟重绘只涉及样式的改变，不涉及到布局。
  回流一定触发重绘，但是重绘不一定触发回流。
  ```
  ```css
  避免回流发生的方法：
  1、避免逐项更改样式。最好一次性更改style属性，或者将样式列表定义为class并一次性更改class属性。
  2、避免循环操作DOM。创建一个documentFragment或div，在它上面应用所有DOM操作，最后再把它添加到window.document。
  3、避免多次读取offsetLeft等属性。无法避免则将它们缓存到变量。
  4、将复杂的元素绝对定位或固定定位，使它脱离文档流。否则回流代价十分高

  ```
  
#### html17
   > 浮动造成的结果，以及清除浮动的方法
   ```
   造成的现象：
   1.父元素的高度无法被撑开，影响与父元素同级的元素

   2.与浮动元素同级的非浮动元素（内联元素）会跟随其后

   3.若非第一个元素浮动，则该元素之前的元素也需要浮动，否则会影响页面显示的结构
   ```
   ```css
   清除浮动的方法 
   1.父元素浮动 
   2.父元素设置overflow:hidden
   3.浮动元素后面添加额外div清除浮动
   4. #parent:after{}
   ```
   
#### html18
   > W3C标准都有什么
   ```
   要有doctype声明；
   标签闭合、标签小写、不乱嵌套、提高搜索机器人搜索几率；
   使用外链css和 js 脚本；
   结构行为表现的分离；
   属性要用""括起来，属性值不能为空；
   注释中不要使用--；
   < , &等要使用编码表示&gl；
   图片要加alt，form表单应该有对应的label；
   文件下载与页面速度更快、内容能被更多的用户所访问、内容能被更广泛的设备所访问、更少的代码和组件，
   容易维护、改版方便，不需要变动页面内容、提供打印版本而不需要复制内容、提高网站易用性。
   ```

#### html19
   > 对BFC的理解
   ```css
    BFC，块级格式化上下文，一个创建了新的BFC的盒子是独立布局的，盒子里面的子元素的样式不会影响到外面的元素。

    在同一个BFC中的两个毗邻的块级盒在垂直方向（和布局方向有关系）的margin会发生折叠。

    W3C CSS 2.1 规范中的一个概念，它决定了元素如何对其内容进行布局，以及与其他元素的关系和相互作用。
   ```
   
 > 哪些可以触发BFC
 ```css
    float: left;
    overflow: auto;
    display: table;
    display: table-cell;
    display: table-caption;
    display: inline-block;
    position: fixed;
    position: absolute;
    ……
 ```

#### html20
 > 部分属性的百分比，是相对于什么的
 ```css
 1.margin 和padding 都是相对于块级父元素的width
 2.设置了定位，在left和right有效的情况下相对于父元素的width  ；
   top和bottom是相对于父元素的height
 3.transform:translate(50%,50%)是相对于自身宽高的50%
 ```

#### html21
 > 元素的属性：
 ```JavaScript
 1. clientWidth和clientHeight，返回该元素的可视宽高，不包括滚动条
 2. scrollWidth和scrollHeight，滚动大小，指的是包含滚动内容的元素大小（元素内容的总高度）
 3. offsetWidth和offsetHeight，返回元素实际大小，包含边框、内边距和滚动条
 
 在浏览器中的区别在于：
 IE6、IE7 认为scrollHeight 是网页内容实际高度，可以小于clientHeight。
 FF、Chrome 认为scrollHeight 是网页内容高度，不过最小值是clientHeight。
 
 返回视图大小：
 function getViewPort () {
    if(document.compatMode == "BackCompat") {   //浏览器嗅探，混杂模式
        return {
            width: document.body.clientWidth,
            height: document.body.clientHeight
        };
    } else {
        return {
            width: document.documentElement.clientWidth,
            height: document.documentElement.clientHeight
        };
    }
}
返回文档大小：
function getDocumentPort () {
    if(document.compatMode == "BackCompat") {
        return {
            width: document.body.scrollWidth,
            height: document.body.scrollHeight
        };
    } else {
        return {
            width: Math.max(document.documentElement.scrollWidth,document.documentElement.clientWidth),
            height: Math.max(document.documentElement.scrollHeight,document.documentElement.clientHeight)
        }
    }
}
 ```
> 元素周边长度
 ```javascript
 1. clientLeft和clientTop 获取边框大小,返回值即为左边框和上边框宽度
 2. offsetLeft和offsetTop 相对于父元素的左上距离
 3. scrollTop和scrollLeft 滚动条被卷入的长度，也可以直接赋值使滚动条调到该位置
 ```
 
#### html22
```css
一丶结构标签
  （1）section：独立内容区块，可以用h1~h6组成大纲，表示文档结构，也可以有章节、页眉、页脚或页眉的其他部分；
  （2）article：特殊独立区块，表示这篇页眉中的核心内容；
  （3）aside：标签内容之外与标签内容相关的辅助信息；
  （4）header：某个区块的头部信息/标题；
  （5）hgroup：头部信息/标题的补充内容；
  （6）footer：底部信息；
  （7）nav：导航条部分信息
  （8）figure：独立的单元，例如某个有图片与内容的新闻块。 

二丶表单的type
   （1）email：必须输入邮件；
   （2）url：必须输入url地址；
   （3）number：必须输入数值；
   （4）range：必须输入一定范围内的数值；
   （5）Date Pickers：日期选择器；
      a.date：选取日、月、年
      b.month：选取月、年
      c.week：选取周和年
      d.time：选取时间（小时和分钟）
      e.datetime：选取时间、日、月、年（UTC时间）
      f.datetime-local：选取时间、日、月、年（本地时间）
   （6）search：搜索常规的文本域；
   （7）color：颜色

三丶媒体标签
   （1）video：视频
   （2）audio：音频
   （3）embed：嵌入内容（包括各种媒体），Midi、Wav、AU、MP3、Flash、AIFF等。
   （4）source：在video和audio中定义原文件路径
四丶表单元素
   （1）datalist 定义下拉列表，内部的项，用option标签
   （2）keygen 用于表单的密钥对生成器字段
   （3）output
五丶其他标签
   （1）mark：标注（像荧光笔做笔记）
   （2）progress：进度条；<progress max="最大进度条的值" value="当前进度条的值">
   （3）time：数据标签，给搜索引擎使用；发布日期<time datetime="2014-12-25T09:00">9：00</time>更新日期<time datetime="2015-
01-23T04:00" pubdate>4:00</time>
   （4）ruby和rt：对某一个字进行注释；<ruby><rt>注释内容</rt><rp>浏览器不支持时如何显示</rp></ruby>
   （5）wbr：软换行，页面宽度到需要换行时换行；
   （6）canvas：使用JS代码做内容进行图像绘制；
   （7）command：按钮；
   （8）deteils ：展开菜单；
	
六丶移除的标签
    纯表现的元素：basefont，big，center，font, s，strike，tt，u；

    对可用性产生负面影响的元素：frame，frameset，noframes；
```

#### html23
 > 多条注释判断浏览器版本IE
```HTML
<!--[if !IE]><!--> 除IE外都可识别 <!--<![endif]-->
<!--[if IE]> 所有的IE可识别 <![endif]-->
<!--[if IE 6]> 仅IE6可识别 <![endif]-->
<!--[if lt IE 6]> IE6以及IE6以下版本可识别 <![endif]-->
<!--[if gte IE 6]> IE6以及IE6以上版本可识别 <![endif]-->
<!--[if IE 7]> 仅IE7可识别 <![endif]-->
<!--[if lt IE 7]> IE7以及IE7以下版本可识别 <![endif]-->
<!--[if gte IE 7]> IE7以及IE7以上版本可识别 <![endif]-->
<!--[if IE 8]> 仅IE8可识别 <![endif]-->
<!--[if IE 9]> 仅IE9可识别 <![endif]-->
```
