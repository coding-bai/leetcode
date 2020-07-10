#  `JS`剑指*offer*7--斐波那契数列

> 斐波那契数列：
>
> 写一个函数，输入 n ，求斐波那契（Fibonacci）数列的第 n 项。斐波那契数列的定义如下：
>
> F(0) = 0,   F(1) = 1
> F(N) = F(N - 1) + F(N - 2), 其中 N > 1.
> 斐波那契数列由 0 和 1 开始，之后的斐波那契数就是由之前的两数相加而得出。
>
> **答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。**
>
> 示例 1：
>
> 输入：n = 2
> 输出：1
> 示例 2：
>
> 输入：n = 5
> 输出：5
>
>
> 提示：
>
> 0 <= n <= 100
>
> 来源：力扣（LeetCode）
> 链接：https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof

这道题需要注意的是答案一定要**取模1e9+7**

1. 普通法

   ```js
   /**
    * @param {number} n
    * @return {number}
    */
   var fib = function(n) {
       if(n < 2) {
           return n?1:0
       }
       let res1 = 0
       let res2 = 1
       for(let i = 1;i<n;i++){
           let t = res1
           res1 = res2
           res2 = (t + res2) % 1000000007
       }
       return res2
   };
   ```

2. 备忘录（**缓存法**）

   通过使用缓存来解决斐波那契数列中重复的计算过程

   ```js
   /**
    * @param {number} n
    * @return {number}
    */
   var fib = function(n) {
       //js的bigint类型
       const cache = {
           0: 0n,
           1: 1n
       };
       return Fibonacci(n) % 1000000007n;
   
       /**
        * @param {number} n
        * @return {number}
        */
       function Fibonacci(n) {
           if (cache[n] !== undefined) {
               return cache[n];
           }
   
           cache[n] = Fibonacci(n - 1) + Fibonacci(n - 2);
           return cache[n];
       }
   };
   
   ```

   这里的好处是通过备忘录对之前已经计算出的值通过键值对的方法存储，在后面使用的时候通过取值便可直接进行计算，相比之前的方法每一次都要对之前的值进行再一次计算。

3. 数组备忘录

   这里的思想和上面的大同小异

   ```js
   /**
    * @param {number} n
    * @return {number}
    */
   var fib = function(n) {
       let fibonacci = [0,1];
       for(let i = 2; i <= n; i ++) {
           fibonacci[i] = (fibonacci[i - 1] + fibonacci[i - 2]) % (1e9 +7);
       }
       return fibonacci[n];
   };
   
   ```

4. 也可以通过哈希表进行缓存，因为方法大同小异，这里就不再赘述

