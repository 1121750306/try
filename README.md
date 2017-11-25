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
	* [多条注释判断浏览器版本](#html23)
	* [Web Worker , Web Socket](#html24)
	* [web storage和cookie的区别](#html25)
	* [cookie的优缺点](#html26)
	* [保证session的安全](#html27)
	* [浏览器会话机制是？](#html28)
	* [iframe的缺点](#html29)
	* [script标签的defer、async的区别](#html30)
	* [HTML5 应用程序缓存和浏览器缓存有什么区别](#html31)
	* [常见浏览器兼容性问题与解决方案](#html32)
* JAVASCRIPT
	* [数据类型 , typeof](#js1)
	* [与或非操作符 ， == 的强制转换类型规则](#js2)
	* [垃圾回收机制 ， 内存泄漏情况](#js3)
	* [ new 操作符具体做了什么](#js4)
	* [String 类型的方法](#js5)
	* [Array 类型的方法](#js6)
	* [获取链接到该节点的所有样式（包括外联）](#js7)
	* [两种立即执行函数的区别](#js8)
	* [ call() , apply() , bind()](#js9)
	* [闭包的特性，理解](#js10)
	* [正则对象的exec方法和string对象的match方法](#js11)
	* [slice() , subString() , subStr() 的比较](#js12)
* ES6
	* [函数赋值的默认值与解构赋值默认值](#es6_1)
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
```css
data- 为H5新增的为前端开发者提供自定义的属性，这些属性集可以通过对象的  dataset  属性获取，不支持该属性的浏览器可以通过 getAttribute 方法获取 :

需要注意的是： data- 之后的以连字符分割的多个单词组成的属性，获取的时候使用驼峰风格。 所有主流浏览器都支持 data-* 属性。

即：当没有合适的属性和元素时，自定义的 data 属性是能够存储页面或 App 的私有的自定义数据。
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

#### html24
 > Web Worker
```html
    1.通过 worker = new Worker( url ) 加载一个JS文件来创建一个worker，同时返回一个worker实例。

    2.通过worker.postMessage( data ) 方法来向worker发送数据。

    3.绑定worker.onmessage方法来接收worker发送过来的数据。

    4.可以使用 worker.terminate() 来终止一个worker的执行。
```
 > Web Socket
```html
  Web Socket 是 Web 应用程序的传输协议，它提供了双向的，按序到达的数据流。

  他是一个 HTML5 协议， WebSocket 的连接是持久的，他通过在客户端和服务器之间保持双工连接，

  服务器的更新可以被及时推送给客户端，而不需要客户端以一定时间间隔去轮询。

  var socket = new WebSocket("ws://192.168.1.2:8888");
  两个方法：
       1、send() 向远程服务器发送数据
       2、close() 关闭该websocket链接
  监听函数：
       1、onopen 当网络连接建立时触发该事件
　　　　2、onerror 当网络发生错误时触发该事件
　　　　3、onclose 当websocket被关闭时触发该事件
　　　　4、onmessage 当websocket接收到服务器发来的消息的时触发的事件，也是通信中最重要的一个监听事件
```

#### html25
 > web storage和cookie的区别
```html
  1、Web Storage是为了更大容量存储设计的。 

  2、Cookie 的大小是受限的，每次请求都会发送cookie，浪费带宽，另外`cookie`还需要指定作用域，不可以跨域调用。

  3、Web Storage 拥有 setItem,getItem,removeItem,clear 等方法，
    
    cookie 需要前端开发者自己封装 setCookie，getCookie 。

  4、cookie 的作用是与服务器进行交互，作为 HTTP 规范的一部分而存在 ，
    
    而 Web Storage 仅仅是为了在本地“存储”数据而生
```

#### html26
 > cookie的优缺点
 每个特定的域名下最多生成20个cookie
```html
    1.IE6或更低版本最多20个cookie

    2.IE7和之后的版本最后可以有50个cookie。

    3.Firefox最多50个cookie

    4.chrome和Safari没有做硬性限制
```
 `IE`和`Opera` 会清理近期最少使用的`cookie`，`Firefox`会随机清理`cookie`。

 `cookie`的最大大约为4096字节，为了兼容性，一般不能超过4095字节。

 `IE` 提供了一种存储可以持久化用户数据，叫做`userdata`，从IE5.0就开始支持。每个数据最多128K，每个域名下最多1M。
 这个持久化数据放在缓存中，如果缓存没有清理，那么会一直存在。
 > 优点：极高的扩展性和可用性
```
 1.通过良好的编程，控制保存在cookie中的session对象的大小。

 2.通过加密和安全传输技术（SSL），减少cookie被破解的可能性。

 3.只在cookie中存放不敏感数据，即使被盗也不会有重大损失。

 4.控制cookie的生命期，使之不会永远有效。偷盗者很可能拿到一个过期的cookie。
```
 > 缺点：
```
 1.Cookie 数量和长度的限制。每个domain最多只能有20条cookie，每个cookie长度不能超过4KB，否则会被截掉.
 
 2.安全性问题。如果cookie被人拦截了，那人就可以取得所有的session信息。即使加密也与事无补，因为拦截者并不需要知道cookie的意义，他只要原样转发cookie就可以达到目的了。

 3.有些状态不可能保存在客户端。例如，为了防止重复提交表单，我们需要在服务器端保存一个计数器。如果我们把这个计数器保存在客户端，那么它起不到任何作用。
```

#### html27
> 保证session的安全
```
  验证用户的使用环境[浏览器和 IP 地址]。 
      
      分配给用户 Session ID 时，同时探明用户使用的浏览器和 IP 地址，作为验证依据，使非法用户不能进行 Session ID 欺骗。 
  

  正确处理 Session 变量。 
      
      当用户注销时，立即删除 Session ID 。并设置好 Session 的生存周期，过期就自动删除。 
```

#### html28
> 浏览器会话机制是？
```
    当浏览器向服务器发送URL请求，服务器会生成一个会话ID，并将浏览器端的一些信息保存在服务器端，

    然后将会话ID送到浏览器端保存到cookie里，当浏览器再次向服务器发送请求时会将cookie里的会话ID

    一并发送给服务器，服务器会将接收到的会话ID和服务器里的ID比较，如果相同服务器就认定是一次会话，

    就可以找到本次会话中保存的信息。
```

#### html29
> iframe的缺点
```
iframe会阻塞主页面的 Onload 事件；
搜索引擎的检索程序无法解读这种页面，不利于 SEO;
iframe和主页面共享连接池，而浏览器对相同域的连接有限制，所以会影响页面的并行加载。
使用iframe之前需要考虑这两个缺点。如果需要使用 iframe ，最好是通过 javascript
动态给iframe添加 src 属性值，这样可以绕开以上两个问题。
```

#### html30
 > script标签的defer、async的区别
```
  defer是在HTML解析完之后才会执行，如果是多个，按照加载的顺序依次执行
  async是在加载完成后立即执行，如果是多个，执行顺序和加载顺序无关
```

#### html31
 > HTML5 应用程序缓存和浏览器缓存有什么区别
```
应用程序缓存是 HTML5  的重要特性之一，提供了离线使用的功能，让应用程序可以获取本地的网站内容，例如 HTML 、 CSS 、图片以及 JavaScript 。这个特性可以提高网站性能，它的实现借助于 manifest 文件，如下：
<!doctype html>
<html manifest=”example.appcache”>
…..
</html>
 
与传统浏览器缓存相比，它不强制用户访问的网站内容被缓存。
```

#### html32
> 常见浏览器兼容性问题与解决方案
```
(1)浏览器兼容问题一：不同浏览器的标签默认的外补丁和内补丁不同 
问题症状：随便写几个标签，不加样式控制的情况下，各自的margin 和padding差异较大。
碰到频率:100%
解决方案：CSS里 *{margin:0;padding:0;}
备注：这个是最常见的也是最易解决的一个浏览器兼容性问题，几乎所有的CSS文件开头都会用通配符*来设置各个标签的内外补丁是0。


(2)浏览器兼容问题二：块属性标签float后，又有横行的margin情况下，在IE6显示margin比设置的大 
问题症状:常见症状是IE6中后面的一块被顶到下一行
碰到频率：90%（稍微复杂点的页面都会碰到，float布局最常见的浏览器兼容问题）
解决方案：在float的标签样式控制中加入 display:inline;将其转化为行内属性
备注：我们最常用的就是div+CSS布局了，而div就是一个典型的块属性标签，横向布局的时候我们通常都是用div float实现的，横向的间距设置如果用margin实现，这就是一个必然会碰到的兼容性问题。


(3)浏览器兼容问题三：设置较小高度标签（一般小于10px），在IE6，IE7，遨游中高度超出自己设置高度 
问题症状：IE6、7和遨游里这个标签的高度不受控制，超出自己设置的高度
碰到频率：60%
解决方案：给超出高度的标签设置overflow:hidden;或者设置行高line-height 小于你设置的高度。
备注：这种情况一般出现在我们设置小圆角背景的标签里。出现这个问题的原因是IE8之前的浏览器都会给标签一个最小默认的行高的高度。即使你的标签是空的，这个标签的高度还是会达到默认的行高。


(4)浏览器兼容问题四：行内属性标签，设置display:block后采用float布局，又有横行的margin的情况，IE6间距bug 
问题症状：IE6里的间距比超过设置的间距
碰到几率：20%
解决方案 ： 在display:block;后面加入display:inline;display:table;
备注：行内属性标签，为了设置宽高，我们需要设置display:block;(除了input标签比较特殊)。在用float布局并有横向的margin后，在IE6下，他就具有了块属性float后的横向margin的bug。不过因为它本身就是行内属性标签，所以我们再加上display:inline的话，它的高宽就不可设了。这时候我们还需要在display:inline后面加入display:talbe。


(5) 浏览器兼容问题五：图片默认有间距 
问题症状：几个img标签放在一起的时候，有些浏览器会有默认的间距，加了问题一中提到的通配符也不起作用。
碰到几率：20%
解决方案：使用float属性为img布局
备注 ： 因为img标签是行内属性标签，所以只要不超出容器宽度，img标签都会排在一行里，但是部分浏览器的img标签之间会有个间距。去掉这个间距使用float是正道。（我的一个学生使用负margin，虽然能解决，但负margin本身就是容易引起浏览器兼容问题的用法，所以我禁止他们使用）


(6) 浏览器兼容问题六：标签最低高度设置min-height不兼容 
问题症状：因为min-height本身就是一个不兼容的CSS属性，所以设置min-height时不能很好的被各个浏览器兼容
碰到几率：5%
解决方案：如果我们要设置一个标签的最小高度200px，需要进行的设置为：{min-height:200px; height:auto !important; height:200px; overflow:visible;}
备注：在B/S系统前端开时，有很多情况下我们又这种需求。当内容小于一个值（如300px）时。容器的高度为300px；当内容高度大于这个值时，容器高度被撑高，而不是出现滚动条。这时候我们就会面临这个兼容性问题。
(7)浏览器兼容问题七：透明度的兼容CSS设置 
一般在ie中用的是filter:alpha(opacity=0);这个属性来设置div或者是块级元素的透明度，而在firefox中，一般就是直接使用opacity:0,对于兼容的，一般的做法就是在书写css样式的将2个都写上就行，就能实现兼容
```


# JavaScript

#### js1
 > 数据类型
```javascript
  数值（number）  字符串（string）   布尔值（boolean）   undefined    null

  对象（object）
  
  Symbol (ES6新增)
```
 > typeOf
```javascript
   number、string、boolean、undefined、function、object( {}、[]、null )
```

#### js2
> 与或非操作符
```javascript
   ~  非操作符 ：二进制0001，~的话则为1110。“&”位and操作符，用法显然。
   |  或操作符。
   ^  异或操作符，只能有一个为1。
   左移操作符： << ,即换为二进制之后向左移，右边补充添零。
   有符号的右移操作符： >> ,用符号位的数值来补充。
   无符号的右移操作符： >>> ，用0补充
```
> == 强制转换类型规则
```javascript
  1. 若有一个操作数是布尔值，则先转换为数值： false -> 0,true -> 1。
  2. 字符串和数值 ：将字符串转为数值。
  3. 若一个为对象，另一个不是对象，则对象调用valueof。
  4. null == undefined。
  5. 比较之前不能将null和undefined转为其他值。
  6. 只要其中一个操作数为NaN，==的值为false；！=的值为true。
      故而：NaN == NaN的值为false ； NaN != NaN的值为true。
  7. 两个对象（数组等）的比较，比较的是其引用值，只有他们引用的是同一个对象时才会相等。
  8. 空数组转为数字为0
  
  附：null转为数值为0  ；  undefined转为数值为NaN
```

#### js3
 > 垃圾回收机制
```
  这是JavaScript最常见的垃圾回收方式，当变量进入执行环境的时候，比如函数中声明一个变量，

  垃圾回收器将其标记为“进入环境”，当变量离开环境的时候（函数执行结束）将其标记为“离开环境”。

  垃圾回收器会在运行的时候给存储在内存中的所有变量加上标记，然后去掉环境中的变量以及被环境中变量

  所引用的变量（闭包），在这些完成之后仍存在标记的就是要删除的变量了
```
 > 内存泄漏
```
    内存泄漏指任何对象在您不再拥有或需要它之后仍然存在。

    垃圾回收器定期扫描对象，并计算引用了每个对象的其他对象的数量。如果一个对象的引用数量为 

    0（没有其他对象引用过该对象），或对该对象的惟一引用是循环的，那么该对象的内存即可回收。

    setTimeout 的第一个参数使用字符串而非函数的话，会引发内存泄漏。

    闭包、控制台日志、循环（在两个对象彼此引用且彼此保留时，就会产生一个循环）
```

#### js4
 >  new 操作符具体做了什么
```javascript
   1、创建一个空对象，并且 this 变量引用该对象，同时还继承了该函数的原型。

   2、属性和方法被加入到 this 引用的对象中。

   3、新创建的对象由 this 所引用，并且最后隐式的返回 this 。


    var obj  = {};

    obj.__proto__ = Base.prototype;

    Base.call(obj);
```

#### js5
> string 类型的方法
```javascript
   var str = "this is a string";
  1. 字符方法：alert(str.charAt(1)),返回str的第二个字符，即h;   str.charCodeAt(1),返回的是h的字符编码。

  2. var newStr = str.concat("first string","second string"),同数组的concat一样连接，且原字符串的值不变。

  3. str.slice(1,2)：两参数为始末位置			当参数为负数时，运算时会加上str的长度。
     str.substring(1,2)：两参数为始末位置			所有负数变为0
     str.substr(1,2)：前者为初始位置，后者为项数。	   第一个参数为负数：加上str长度；第二个参数为负数时变为0
     由于slice和substring的参数为索引值，若参数为(3，1)，则slice为空，substring实际变为（1，3）

  4. str.split(  ,  )，将字符串以第一个参数的字符串或正则表达式分割为数组，第二个参数为数组的长度（不可超过）。

  5. 字符串位置方法：str.indexOf()和str.lastIndexOf()，返回值为索引值

  6. str.trim(),返回一个去掉了前后空格的新字符串

  7. str.match()和str.search()，前者返回所有匹配的值的数组，后者为匹配到第一项。

  8. str.replace(  ，  )，两个参数，第一个参数为匹配的字符串或者正则表达式，第二个是替换成的字符段。

  9. str.localeCompare(str2),返回值为：1--str2在字母表中排在str前面；0--两个相同；-1--str2排在str后面。

  10. str.fromCharCode(101,104,106);根据字符编码得到对应的字符组成的字符串。
```

#### js6
 > Array 类型的方法
```javascript
  1. var arr = new Array()
     var arr = new Array(3)
     var arr = new Array("first","second","third");
     var arr = ["first","second","third"];
     arr[arr.length] = "fourth";可直接在数组末尾添加一项
     检测是否是数组的通用办法：Array.isArray(arr);

  2. var arr = ["first","second","third"];
     alert(arr.toString());
     alert(arr.valueOf());
     alert(arr);三个的输出结果都是first,second,third;
     toString()将数组返回为字符串，用逗号连接。而valueOf返回的还是数组。第三个是alert接收字符串，故在后台自动调用toStirng.

     toString和toLocalString的调用结果相同，都是用逗号连接，不过在给对象定义了各自的toString 和toLocalStirng后结果就不同了。

  3. arr.push("fifth")；类似栈方法，将该项添加到数组末尾。
     var str = arr.pop();出栈数组末尾的值。
     var str = arr.shift()得到并去除数组的第一项，并且数组依次前移。shift：去掉
     arr.unshift("first")推入第一项，其他后移一位。

  4. arr.sort(function(value1,value2){
      return value1 - value2;//当返回值大于0，则换位置....此处为升序
     })
     arr.reverse()数组反转

  5. var newArray = arr.concat("fourth",["fifth","sixth"]);新建一个数组，值为arr加上括号里面的值。。不改变arr的值
  
     var newArray = arr.slice(1,2);新建一个数组，其值只有一项为为arr[1]的值。参数为始末位置
    
     var removeArr = arr.splice(1,2,"new","newtwo");
     原数组删除arr[1]和arr[2],并在删除的位置插入第三个参数之后的所有参数，removeArr的值为删除的数组

     slice的参数为始末位置，splice的参数是起始位置和项数.

  6. IE9+,Fire2+,safari3+,opera9.5+,chrome:
   {
     arr.indexOf("first"，0);查找数组中有无该项，从第二个参数的位置开始查找。没找到则返回-1。
     arr.lastIndexOf("first",0);从数组的末尾开始找，具体从倒数第几项，此处为倒数第0项，即最后一项。

     var result = arr.every(function(item,index,arr){//值，位置，数组本身
       return -----
     })
     every()和some()用法类似，every是所有返回值为true才为true；some是只要一个true则返回true。
     forEach()，对每一项都进行函数体的运算，没有返回值,即result的值为空
     filter(),将TRUE的值写入result，即筛选出满足条件的数组的项。
     map(),也返回数组，比如return item*2,则返回数组每一项为原数组的两倍。
   }
  
  7. IE9+,Fire3+,safari4+,opera10.5+,chrome:{
       归并数组reduce()和reduceright():
       var value = [1,2,3,4,5];
       var sum = value.reduce(function(prev,cur,index,array){//前一项值(前一次sum的值)，当前值，当前索引，当前数组
         return prev+cur;
       })//sum = 15
     }

```

#### js7
> 获取链接到该节点的所有样式（包括外联）
```javascript
  非IE ： css2.0提供document.defaultView.getComputedStyle("节点","属性名")
  IE ： 节点.currentStyle.属性名
```

#### js8
 > 两种立即执行函数的区别
```javascript
1. (function(){
     ...
   }()) , 相当于函数表达式立即执行  表达式
2. (function(){
       ...
   })() , 相当于声明函数的立即执行
```

#### js9
>  call() , apply() , bind()
```javascript
   作用：动态改变某个类的某个方法的运行环境（执行上下文）。
   
   apply()函数有两个参数：第一个参数是上下文，第二个参数是参数组成的数组。如果上下文是null，则使用全局对象代替。例如：

   function.apply(this,[1,2,3])

   call()的第一个参数是上下文，后续是实例传入的参数序列，例如：
 
   function.call(this,1,2,3);
   
   bind()只有一个参数，即上下文，其返回值就是改变呢上下文的原函数，不包括运行的步骤
   ---bind(this)(1,2,3)  彩盒之前两种效果相同
```

#### js10
> 闭包的特性
```javascript
    1.函数嵌套函数

    2.函数内部可以引用外部的参数和变量

    3.参数和变量不会被垃圾回收机制回收
```
> 闭包的理解
```
   使用闭包主要是为了设计私有的方法和变量。闭包的优点是可以避免全局变量的污染，缺点是闭包会常驻内存，

   会增大内存使用量，使用不当很容易造成内存泄露。在js中，函数即闭包，只有函数才会产生作用域的概念
   
   https://segmentfault.com/a/1190000000652891
```

#### js11
> 正则对象的exec方法和string对象的match方法
```javascript
1. reg.exec(),只会返回第一个匹配到的串，所以正则对象的gim对其无效
   string.match()，会根据正则表达式中的gim等，查询到所有结果
2. 在正则表达式有匹配组的情况下
    reg.exec()返回第一个匹配到的串，并且返回数组之后会保存每个匹配组的值
    string.match()在只有一个匹配字符串的情况下，返回值与exec一样
    
    var str= "cat2,hat8" ;
    var p=/c(at)\d/;
    alert(p.exec(str))
    alert(str.match(p))    //结果都为"cat,at"

    string.match()在有多个匹配结果的情况下，不会保存匹配组的值
    
    var str= "cat,hat" ;
    var p=/a(t)/g; // g:全局 ， i:忽略大小写 ， m:多行
    alert(p.exec(str))     //"at,t"
    alert(str.match(p))    //"at,at"

```

#### js12
 > slice() , subString() , subStr() 的比较
```javascript
  1. slice() 和 subString() 的两个参数都是位置；
     subStr() 的两个参数分别是位置和项数
    
  2. slice()参数有负数 ： 都会加上length变为正数；
     subString()参数有负数 ： 第一个参数加上length来变为正数 ， 第二个参数直接当做0
     subStr()参数有负数 ： 两个参数都当做0
    
  3. slice()第一个参数大于第二个参数 ， 结果为空串""
     subString()第一个参数大于第二个参数 ， 如(2,1),会当做(1,2)来进行计算
```

# ES6
 
#### es6_1
 > * [函数赋值的默认值与解构赋值默认值](#es6_1)
 ```javascript
	// 写法一
	function m1({x = 0, y = 0} = {}) {
 	 return [x, y];
	}

	// 写法二
	function m2({x, y} = { x: 0, y: 0 }) {
  	 return [x, y];
	}
	
	
