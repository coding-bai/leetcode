# ` JS`剑指*offer*16--打印从1到最大的n位数

> 输入数字 n，按顺序打印出从 1 到最大的 n 位十进制数。比如输入 3，则打印出 1、2、3 一直到最大的 3 位数 999。
>
> 示例 1:
>
> 输入: n = 1
> 输出: [1,2,3,4,5,6,7,8,9]
>
>
> 说明：
>
> 用返回一个整数列表来代替打印
> n 为正整数
>
> 来源：力扣（LeetCode）
> 链接：https://leetcode-cn.com/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof
> 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

1. `Array.from()`

> `Array.from()`方法就是将一个类数组对象或者可遍历对象转换成一个真正的数组。`Array.from`有三个参数，`Array.from(arrayLike[, mapFn[, thisArg]])`，`arrayLike`：想要转换成数组的伪数组对象或可迭代对象；`mapFn`：如果指定了该参数，新数组中的每个元素会执行该回调函数；`thisArg`：可选参数，执行回调函数 `mapFn` 时 `this` 对象。该方法的返回值是一个新的数组实例（真正的数组）。

```js
/**
 * @param {number} n
 * @return {number[]}
 */
var printNumbers = function(n) {
    let len = 10**n -1 
    //let len = Math.pow(10, n)-1
    return Array.from({length:len},(item, index) => index+1)
};



//以下为精简版
/**
 * @param {number} n
 * @return {number[]}
 */
var printNumbers = function(n) {
    return Array.from({length:10**n -1 },(item, index) => index+1)
};
```

2. 快速幂

    本质还是使用快速幂求出10^n次方
   快速幂：将指数转换成二进制形式，例如a13=a2^0+2^2+2^3=a2^0a2^2a2^3 

   ```js
   var printNumbers = function(n) {
       let base = 10, sum = 1, res = [];
   
       while (n != 0) {
           if ((n & 1) == 1) {
               // 如果当前二进制最后一位为1
               sum *= base;
           }
           n >>= 1;
           base *= base;
       }
       let i = 1;
   
       while (i < sum) {
           res.push(i++);
       }
       return res;
   };
   ```

   