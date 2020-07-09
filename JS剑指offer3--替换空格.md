# `JS`剑指*offer2*--替换空格

> 替换空格：
>
> 请实现一个函数，把字符串 s 中的每个空格替换成"%20"。
>
> 示例 1：
>
> 输入：s = "We are happy."
> 输出："We%20are%20happy."
>
>
> 限制：
>
> 0 <= s 的长度 <= 10000
>
> 来源：力扣（LeetCode）
> 链接：https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof

1. 天下无敌正则表达式

   根据正则表达式`/ /g`匹配空格然后进行替换

   ```js
   /**
    * @param {string} s
    * @return {string}
    */
   var replaceSpace = function(s) {
       return s.replace(/ /g ,'%20')
   };
   ```

2. 字符串-->数组-->字符串

   善于利用`js`针对不同数据类型的那些小技巧

   ```js
   /**
    * @param {string} s
    * @return {string}
    */
   var replaceSpace = function(s) {
         if(s === '') return ''
           return s.split(' ').join('%20');
   };
   ```

3. 迭代字符串

   这个方法看代码最好理解

   ```js
   /**
    * @param {string} s
    * @return {string}
    */
   var replaceSpace = function(s) {
   let replaceStr = '';
     for (let str of s) {
         replaceStr += str === ' ' ? '%20' : str;
     }
     return replaceStr;
   };
   ```

   