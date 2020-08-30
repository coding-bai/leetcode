# `JS`剑指*offer*19--表示数值的字符串

> 请实现一个函数用来判断字符串是否表示数值（包括整数和小数）。例如，字符串"+100"、"5e2"、"-123"、"3.1416"、"-1E-16"、"0123"都表示数值，但"12e"、"1a3.14"、"1.2.3"、"+-5"及"12e+5.4"都不是。
>
> 来源：力扣（LeetCode）
> 链接：https://leetcode-cn.com/problems/biao-shi-shu-zhi-de-zi-fu-chuan-lcof
> 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

1. 正则大法好

   ```js
   var isNumber = function(s) {
       let result = s.match(/\s*[+-]?((\d+(\.\d*)?)|\.\d+)([e][+-]?\d+)?\s*/g);
       return s !== '.' && result ? result[0] === s : false;
   };
   ```

2. `isNaN`

   ```js
   /**
    * @param {string} s
    * @return {boolean}
    */
   var isNumber = function(s) {
     s = s.trim()
     if (s == '') return false
     return !Number.isNaN(Number(s))
   };
   ```

3. 穷举法

   首先去掉字符串前后的空格，因为中间出现空格，就不合法，前后出现合法
   `e` 只能出现一次，前边必须出现数字，这个出现以后，将数字标记置为false，因为后边如果没有数字还是`false`,`.` 出现过`e` 和 `.`以后就不能再出现`.` 了这种，只能出现在最前边，或者 `e`的后边（表示是不是变成分数）

   ```js
   /**
    * @param {string} s
    * @return {boolean}
    */
   var isNumber = function(s) {
       let isNum = false, isDot = false, isSymbol = false, isE = false
       let s1 = s.trim()
       for(let v = 0; v < s1.length; v++) {
           if (0 <= s1[v] && s1[v] <= 9 && s1[v] != ' ') {
               isNum = true
           }else if (s1[v] == 'e' || s1[v] == 'E') {
               if (!isNum || isE) {
                   return false
               }
               isE = true
               isNum = false
           }else if (s1[v] == '.') {
               if(isDot || isE){
                   return false
               }
               isDot = true
           }else if (s1[v] == '-' || s1[v] == '+') {
               if (v != 0 && (s1[v - 1] != 'e' || s1[v - 1] != 'e')) {
                   return false
               }
           }else {
               return false
           }
       }
       return isNum
   };
   ```

   