[标题1](#标题1)

# 标题1

* HTML和CSS
	* [opacity,display,visibility](#html1)
	* [文字超出用...](#html2)
	* [渐进增强和优雅降级](#html3)
	* [link 和 @import 的区别](#html4)
	* [对position属性的理解](#html5)
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
 <pre>
 <code>
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
</code>
</pre>
