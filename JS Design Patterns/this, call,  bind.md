#### 除去不常用的 with 和 eval 的情况,具体到实际应用中, this 的指向大致可以分为以下 4 种。
1. 作为对象的方法调用。
  this指向该对象
  
2. 作为普通函数调用。
  当作为普通函数调用时，this指向全局对象。在浏览器JavaScript中，全局对象为window。
  es5的严格模式下，普通函数的this不再指向全局对象window，而是undefined。
  es6的语法声明的变量，不再指向全局对象（顶层对象）
  
3. 构造器调用。
  通常情况下，构造器内部的this指向放回的对象，当构造函数显式反悔了一个对象时，this则不指向它（看代码显然如此）
  
4. Function.prototype.call 或 Function.prototype.apply 调用
  call，apply等，改变了this的指向，指向了传入的第一个参数
  
#### call,apply的用途
1. 改变this的指向
2. 实现bind方法
```JavaScript
  Function.prototype.bind = function(content) {
    let self = this;
    return self.apply(content, arguments)
  }
```

3. 借用其他对象的方法
  * 借用构造函数调用
  * Array.prototype.push.apply(DOM, newDom)
