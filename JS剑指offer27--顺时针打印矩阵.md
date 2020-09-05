# `JS`剑指*offer*27--顺时针打印矩阵

> 输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。
>
> 示例 1：
>
> 输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
> 输出：[1,2,3,6,9,8,7,4,5]
> 示例 2：
>
> 输入：matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
> 输出：[1,2,3,4,8,12,11,10,9,5,6,7]
>
>
> 限制：
>
> 0 <= matrix.length <= 100
> 0 <= matrix[i].length <= 100
>
> 来源：力扣（LeetCode）
> 链接：https://leetcode-cn.com/problems/shun-shi-zhen-da-yin-ju-zhen-lcof
> 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

1. 模拟路径

   根据直觉，当遍历的过程中，遇到超出边界 / 元素已经被访问过的情况时，应该按照顺时针转变方向。

   假设给定的矩阵的形状是 `m*n`，那么一共要遍历 `m*n` 次。要准备一个长度为 `m*n` 的哈希表，来保存元素是否被遍历过。要准备一个记录方向的数组，里面方向的排列顺序是顺时针。

   ```js
   /**
    * @param {number} i
    * @param {number} j
    */
   function hash(i, j) {
       return `${i}-${j}`;
   }
   
   /**
    * @param {number[][]} matrix
    * @return {number[]}
    */
   var spiralOrder = function(matrix) {
       const m = matrix.length;
       if (!m) {
           return [];
       }
   
       const n = matrix[0].length;
       if (!n) {
           return [];
       }
   
       const results = []; // 遍历结果
       const visited = {}; // 记录元素是否被访问过
       const directions = [
           [0, 1],
           [1, 0],
           [0, -1],
           [-1, 0]
       ]; // 顺时针方向数组
   
       for (let step = 0, row = 0, col = 0, dIdx = 0; step < m * n; ++step) {
           results.push(matrix[row][col]);
           visited[hash(row, col)] = true;
           // 最巧妙的地方：借助方向数组来进行row、col的更新
           const newR = row + directions[dIdx][0];
           const newC = col + directions[dIdx][1];
   
           if (
               !visited[hash(newR, newC)] &&
               newR >= 0 &&
               newR < m &&
               newC >= 0 &&
               newC < n
           ) {
               row = newR;
               col = newC;
           } else {
               // 转变方向
               dIdx = (dIdx + 1) % 4;
               row += directions[dIdx][0];
               col += directions[dIdx][1];
           }
       }
   
       return results;
   };
   ```

   

2. 按层遍历

   这种方法的思路是从外到内，一层层打印。难点在于怎么找到标记点，以及防止重复遍历。

   怎么找到标记点？对于每一层来说，设左上角的元素坐标为 (i, j)，那么右上角的元素坐标为 (i, n - j - 1)，右下角的元素坐标是 (m - i - 1 ,n - j - 1)，左下角的元素坐标是 (m - i - 1, j)。找到标记点后，就是对行/列进行+/-的过程。

   ![img](https://pic.leetcode-cn.com/dfdfa1be4e547f8a171379e7bf99654885de50c444284bae901a8b803e9bcb01.jpg)

   第一种拆分方法会有例外，比较难处理，无法避免重复遍历。因此使用第二种。

   ```js
   /**
    * @param {number[][]} matrix
    * @return {number[]}
    */
   var spiralOrder = function(matrix) {
       const m = matrix.length;
       if (!m) {
           return [];
       }
   
       const n = matrix[0].length;
       if (!n) {
           return [];
       }
   
       const results = [];
       let i = 0,
           j = 0;
       // 这里的终止条件是： i <= (m - 1) / 2 与 j <= (n - j) / 2
       // 即最里面的那层左上角元素的坐标
       while (i <= m - i - 1 && j <= n - j - 1) {
           for (let col = j; col <= n - j - 1; ++col) {
               results.push(matrix[i][col]);
           }
   
           for (let row = i + 1; row <= m - i - 1; ++row) {
               results.push(matrix[row][n - j - 1]);
           }
   
           if (i < m - i - 1 && j < n - j - 1) {
               for (let col = n - j - 2; col > j; --col) {
                   results.push(matrix[m - i - 1][col]);
               }
   
               for (let row = m - i - 1; row > i; --row) {
                   results.push(matrix[row][j]);
               }
           }
   
           i++;
           j++;
       }
   
       return results;
   };
   ```

   