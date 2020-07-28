# `JS`剑指*offer*13--剪绳子2

> 给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 k[0],k[1]...k[m - 1] 。请问 k[0]*k[1]*...*k[m - 1] 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。
>
> 答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。
>
> 来源：力扣（LeetCode）
> 链接：https://leetcode-cn.com/problems/jian-sheng-zi-ii-lcof
> 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

1. 数学规律合理取模

   ```js
   /**
    * @param {number} n
    * @return {number}
    */
   var cuttingRope = function(n) {
     let arr=[0,0,1,2,4];
     if(n<5) return arr[n];
     const max=1e9+7;
     let res=1;
     while(n>=5){
         res=res%max*3;
         n=n-3;
     }
     return  res*n%max;
   };
   ```

2. `bigint`无脑

```js
/**
 * 我们要将n拆成尽可能多的3，剩下的余数若为1，则加入3变成4，若为2，则直接相乘
 * @param {number} n
 * @return {number}
 */
const cuttingRope = function(m) {
    let n = BigInt(m)
    const modNum = 1000000007n
    if (n === 1n || n === 2n) {
        return 1n
    }
    if (n === 3n) {
        return 2n
    }

    const mod = n % 3n
    const time = n / 3n
    if (mod === 0n) {
        return (3n ** time) % modNum
    } else if (mod === 1n) {
        return 4n * (3n ** (time - 1n)) % modNum
    } else {
        return 2n * (3n ** time) % modNum
    }
}
```

