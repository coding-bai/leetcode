# `JS`剑指*offer2*--二维数组中的查找

>二维数组的查找:
>
>在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。
>
>示例:
>
>现有矩阵 matrix 如下：
>
>[
>  [1,   4,  7, 11, 15],
>  [2,   5,  8, 12, 19],
>  [3,   6,  9, 16, 22],
>  [10, 13, 14, 17, 24],
>  [18, 21, 23, 26, 30]
>]
>给定 target = 5，返回 true。
>
>给定 target = 20，返回 false。
>
>限制：
>
>0 <= n <= 1000
>
>0 <= m <= 1000
>
>来源：力扣（LeetCode）
>链接：https://leetcode-cn.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof

1. 一行代码的骚气解法

   通过`flat`给数组进行降维打击，直接化成一位数组查找值

   ```js
   /**
    * @param {number[][]} matrix
    * @param {number} target
    * @return {boolean}
    */
   var findNumberIn2DArray = function(matrix, target) {
       return matrix.flat(Infinity).includes(target)
   };
   ```

   

2. 根据二维数组的数据特点查找

   根据题中所给，这个二维数组有**每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序**的特点，那么我们可以先逆序遍历每一行：

   - 只要该行首元素大于`target`跳过该行
   - 该行首元素小于`target`，则判断该行是否有`target`
   - 该行首元素等于`target`

   ```js
   /**
    * @param {number[][]} matrix
    * @param {number} target
    * @return {boolean}
    */
   var findNumberIn2DArray = function(matrix, target) {
       for(let row = matrix.length-1; row > -1; --row) {
           if(matrix[row][0] < target) {
               if(matrix[row].indexOf(target) > 0) {
                   return true
               }
           } else if(matrix[row][0] === target) {
               return true
           }
       }
       return false
   };
   ```

   