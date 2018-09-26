# VUE
 
 > vue.js异步更新dom
 

 vuejs的watch检测到数据变化时，会调用queueWatcher检查观察者id是否存放在了观察者队列，存在的话就不push进去，不存在再放进去。
 在下一个tick执行的时候才执行观察者队列来更新一堆需要更新的视图。
 下一个tick其实就是nextTick方法，当该方法能够执行的时候，变进行视图的更新，所以可能出现以下代码的发生：
  ```
 <div ref="test">{{test}}</div>
 handleClick () {
    this.test = 'end';
    console.log(this.$refs.test.innerText);//打印的不是end
 }
  
 ```
 这个时候贯彻着队列还没有执行，所以视图并没有更新
 
 异步更新的优点：如果短时间修改了很多次数据，同步更新的话就会对dom操作很多次，消耗太大，异步更新则会减少更新次数

	
	
	
	
 
 > 不要在选项属性或者回调上使用箭头函数

```
  比如：
  created: () => console.log(this.a) 
  vm.$watch('a', newValue => this.myMethod())
  因为箭头函数是和父级上下文绑定在一起的，this 不会是如你所预期的 Vue 实例，
  经常导致 Uncaught TypeError: Cannot read property of undefined 
	或 Uncaught TypeError: this.myMethod is not a function 之类的错误
```

> 组件和混合对象合并规则

```
  当组件和混合对象含有同名选项时，这些选项将以恰当的方式混合：  
     同名钩子函数将混合为一个数组，因此都将被调用。fix钩子先被调用
     值为对象的选项，例如 methods, components将被混合为同一个对象。两个对象键名冲突时，取组件对象的键值对
    
    即：值为函数的选项会被合并为函数数组，值为对象的则会合并为对象，键名冲突以组件为准
```
> 全局混合函数会影响到之后创建的所有VUE实例，甚至影响到第三方模板

> 计算属性computed和方法methods的某些区别

```
 methods明明可以完成computed的任务，那conputed存在的价值在哪：
  计算属性基于它们的依赖进行缓存的。计算属性只有在它的相关依赖发生改变时才会重新求值
  即： 如计算属性依赖与data的size，则conputed只有在size改变时才会重新计算，而methods每次调用都会计算
  下面代码的Date.now不是响应式依赖，所以也只会计算一次
	computed: {
  	now: function () {
    	return Date.now()
  	}
	}
```

 > 数值的传递
 
 ```
 	<comp some-prop="1"></comp>
	此处传递的1是字符串，若需要传递数值的1,需要加上v-model进行绑定
 ```
 
