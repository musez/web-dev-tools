# 算法(es6)

## js 统计一个字符串出现频率最高的字母/数字
``` javascript
let str = 'asdfghjklaqwertyuiopiaia';
const strChar = str => {
    let string = [...str],
        maxValue = '',
        obj = {},
        max = 0;
    string.forEach(value => {
        obj[value] = obj[value] == undefined ? 1 : obj[value] + 1
        if (obj[value] > max) {
            max = obj[value]
            maxValue = value
        }
    })
return maxValue;
}
console.log(strChar(str))    // a
```

## 数组去重
1. forEach
    ``` javascript
    let arr = ['1', '2', '3', '1', 'a', 'b', 'b']
    const unique = arr => {
        let obj = {}
        arr.forEach(value => {
            obj[value] = 0
        })
        return Object.keys(obj)
    }
    console.log(unique(arr))  // ['1','2','3','a','b']
    ```
2. filter
    ``` javascript
    let arr = ['1', '2', '3', '1', 'a', 'b', 'b']
    const unique = arr => {
        return arr.filter((ele, index, array) => {
            return index === array.indexOf(ele)
        })
    }
    console.log(unique(arr))  // ['1','2','3','a','b']
    ```
3. set
    ``` javascript
    let arr = ['1', '2', '3', '1', 'a', 'b', 'b']
    const unique = arr => {
        return [...new Set(arr)]
    }
    console.log(unique(arr))  // ['1','2','3','a','b']
    ```

## 翻转字符串
``` javascript
let str ="Hello Dog";
const reverseString = str =>{
    return [...str].reverse().join("");
}
console.log(reverseString(str))   // goD olleH
```

## 数组中最大差值
1. forEach
    ``` javascript
    let arr = [23, 4, 5, 2, 4, 5, 6, 6, 71, -3];
    const difference = arr => {
        let min = arr[0],
            max = 0;
        arr.forEach(value => {
            if (value < min) min = value
            if (value > max) max = value
        })
        return max - min ;
    }
    console.log(difference(arr))  // 74
    ```

2. max、min
    ``` javascript
    let arr = [23, 4, 5, 2, 4, 5, 6, 6, 71, -3];
    const difference = arr => {
        let max = Math.max(...arr),
            min = Math.min(...arr);
        return max - min ;
    }
    console.log(difference(arr)) // 74
    ```

## 不借助临时变量，进行两个整数的交换
1. 数组解构
    ``` javascript
    let a = 2,
        b = 3;
        [b,a] = [a,b]
        console.log(a,b)   // 3 2
    ```
2. 算术运算（加减）
    输入a = 2,b = 3,输出 a = 3,b = 2
    ``` javascript
    let a = 2,
        b = 3;
    const swop = (a, b) => {
        b = b - a;
        a = a + b;
        b = a - b;
        return [a,b];
    }
    console.log(swop(2,3)) // [3,2]
    ```
3. 逻辑运算（异或）
    ``` javascript
    let a = 2,
        b = 3;
    const swop = (a, b) => {
        a ^= b; //x先存x和y两者的信息
        b ^= a; //保持x不变，利用x异或反转y的原始值使其等于x的原始值
        a ^= b; //保持y不变，利用x异或反转y的原始值使其等于y的原始值
        return [a,b];
    }
    console.log(swop(2,3)) // [3,2]
    ```

## 排序 (从小到大)
1. 冒泡排序
``` javascript
let arr = [43, 32, 1, 5, 9, 22];
const sort = arr => {
    let res = []
    arr.forEach((v, i) => {
        for (let j = i + 1; j < arr.length; j++) {
            if (arr[i] > arr[j]) {
                [arr[i],arr[j]] = [arr[j],arr[i]]
            }
        }
    })
    return arr
}
console.log(sort(arr))  // [1, 5, 9, 22, 32, 43]
```

### 比较两个数组的内容是否相同
``` javascript
// Warn if overriding existing method
if (Array.prototype.equals)
    console.warn(
        "Overriding existing Array.prototype.equals. Possible causes: New API defines the method, there's a framework conflict or you've got double inclusions in your code.");
// attach the .equals method to Array's prototype to call it on any array
Array.prototype.equals = function (array) {
    // if the other array is a falsy value, return
    if (!array)
        return false;

    // compare lengths - can save a lot of time
    if (this.length != array.length)
        return false;

    for (var i = 0, l = this.length; i < l; i++) {
        // Check if we have nested arrays
        if (this[i] instanceof Array && array[i] instanceof Array) {
            // recurse into the nested arrays
            if (!this[i].equals(array[i]))
                return false;
        } else if (this[i] != array[i]) {
            // Warning - two different object instances will never be equal: {x:20} != {x:20}
            return false;
        }
    }
    return true;
}
// Hide method from for-in loops
Object.defineProperty(Array.prototype, "equals", {
    enumerable: false
});
```

## 比较Object
``` javascript
Object.prototype.equals = function (object2) {
    //For the first loop, we only check for types
    for (propName in this) {
        //Check for inherited methods and properties - like .equals itself
        //https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty
        //Return false if the return value is different
        if (this.hasOwnProperty(propName) != object2.hasOwnProperty(propName)) {
            return false;
        }
        //Check instance type
        else if (typeof this[propName] != typeof object2[propName]) {
            //Different types => not equal
            return false;
        }
    }
    //Now a deeper check using other objects property names
    for (propName in object2) {
        //We must check instances anyway, there may be a property that only exists in object2
        //I wonder, if remembering the checked values from the first loop would be faster or not
        if (this.hasOwnProperty(propName) != object2.hasOwnProperty(propName)) {
            return false;
        } else if (typeof this[propName] != typeof object2[propName]) {
            return false;
        }
        //If the property is inherited, do not check any more (it must be equa if both objects inherit it)
        if (!this.hasOwnProperty(propName))
            continue;

        //Now the detail check and recursion

        //This returns the script back to the array comparing
        /**REQUIRES Array.equals**/
        if (this[propName] instanceof Array && object2[propName] instanceof Array) {
            // recurse into the nested arrays
            if (!this[propName].equals(object2[propName]))
                return false;
        } else if (this[propName] instanceof Object && object2[propName] instanceof Object) {
            // recurse into another objects
            //console.log("Recursing to compare ", this[propName],"with",object2[propName], " both named \""+propName+"\"");
            if (!this[propName].equals(object2[propName]))
                return false;
        }
        //Normal value comparison for strings and numbers
        else if (this[propName] != object2[propName]) {
            return false;
        }
    }
    //If everything passed, let's say YES
    return true;
}
```
