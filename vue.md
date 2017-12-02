# VUE

 > 不要在选项属性或者回调上使用箭头函数

```
  比如：
    created: () => console.log(this.a) 
    `vm.$watch('a', newValue => this.myMethod())`
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
? 全局混合函数会影响到之后创建的所有VUE实例，甚至影响到第三方模板
