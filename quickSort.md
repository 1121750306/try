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
