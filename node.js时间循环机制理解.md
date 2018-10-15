* 任务队列分为宏任务macro-task和微任务micro-task，也被称为task和job

* macro-task 包括script(整体的代码),setTimeout,setInterval,setImmediate,I/O,UI-rendering

* micro-task 包括process.nextTick,Promise,Object.observe(已废弃),MutationObserve(html5新特性)

* 事件循环的调用顺序：从自身script(整体的代码)开始，进行第一次循环。之后全局上下文进入函数调用栈。调用栈全部执行完之后，执行所有的micro-task，清空micro-task之后，调用macro-task队列的第一个，之后执行micro-task，完成后再是下一个macro-task以此循环。

* 注意点：setTimeout会比setImmediate先执行，mextTick会比promise.then先执行，而promise内部将直接执行

* 各种任务分发器，管理各自的部分，录入先后遇到了setTimeout1，setImmediate，setTimeout2，则执行顺序是setTimeout1，setTimeout2，setImmediate，因为setTimeout属于同一个任务分发器

```node.js
setTimeout(function() {
    console.log('timeout1');
    process.nextTick(function() {
        console.log('timeout1_nextTick');
    })
    new Promise(function(resolve) {
        console.log('timeout1_promise');
        resolve();
    }).then(function() {
        console.log('timeout1_then')
    })
})

setImmediate(function() {
    console.log('immediate1');
    process.nextTick(function() {
        console.log('immediate1_nextTick');
    })
    new Promise(function(resolve) {
        console.log('immediate1_promise');
        resolve();
    }).then(function() {
        console.log('immediate1_then')
    })
})

process.nextTick(function() {
    console.log('glob1_nextTick');
})
new Promise(function(resolve) {
    console.log('glob1_promise');
    resolve();
}).then(function() {
    console.log('glob1_then')
})

setTimeout(function() {
    console.log('timeout2');
    process.nextTick(function() {
        console.log('timeout2_nextTick');
    })
    new Promise(function(resolve) {
        console.log('timeout2_promise');
        resolve();
    }).then(function() {
        console.log('timeout2_then')
    })
})

process.nextTick(function() {
    console.log('glob2_nextTick');
})
new Promise(function(resolve) {
    console.log('glob2_promise');
    resolve();
}).then(function() {
    console.log('glob2_then')
})
```
