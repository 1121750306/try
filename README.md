[标题1](#标题1)
[标题3](#标题3)

# 标题1
### 标题3

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
