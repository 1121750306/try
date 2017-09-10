[标题1](#标题1)
# 标题1
  ```HTML
    .item{
        top: 50%;
        margin-top: -50px;  /* margin-top值为自身高度的一半 */
        position: absolute;
        padding:0;
    }
 ```
* HTML和CSS
	* [opacity,display,visibility](#html1)
	* [文字超出用...](#html2)
	* [渐进增强和优雅降级](#html3)
	* [link 和 @import 的区别](#html4)
	* [对position属性的理解](#html5)
	* [行内元素和块级元素](#html6)
	* [水平居中，垂直居中，水平垂直居中](#html7)
	* [flex布局](#html8)
* JAVASCRIPT
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
 <pre><code>
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
  ```CSS
    .item{
        top: 50%;
        margin-top: -50px;  /* margin-top值为自身高度的一半 */
        position: absolute;
        padding:0;
    }
 ```
 </code></pre>

 > 水平垂直居中
 
 <pre><code>
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
 </code></pre>

#### html8

 > flex布局

	`flex-direction`    主轴方向 row,row-reverse,column,column-reverse
```
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

