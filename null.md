
```javascript
typeof null === 'object';
null instanceof Object === false;

这是JavaScript的一个历史遗留问题，在 JavaScript 最初的实现中，JavaScript 中的值是由一个表示类型的标签和实际数据值表示的。对象的类型标签是 0。
由于 null 代表的是空指针（大多数平台下值为 0x00），因此，null的类型标签也成为了 0，typeof null就错误的返回了"object"
```
  ```javascript
   function quickSort(arr) {
        if (arr.length <= 1) return arr;
        var midVal = arr.splice(Math.floor(arr.length/2),1)[0];
        var left = [];
        var right = [];
        for (var i = 0; i < arr.length; i++) {
            if (arr[i] < midVal) {
                left.push(arr[i])
            } else {
                right.push(arr[i])
            }
        }
        return quickSort(left).concat([midVal], quickSort(right))
    }
  
    var arr = [86,46,97,35,12,16,3,84];
    arr = quickSort(arr)
    console.log(arr)
  ```
