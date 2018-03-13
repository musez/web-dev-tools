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