# `JS`剑指*offer*20--调整数组顺序使奇数位于偶数前面

> 输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有奇数位于数组的前半部分，所有偶数位于数组的后半部分。
>
>  
>
> 示例：
>
> 输入：`nums` = `[1,2,3,4]`
> 输出：`[1,3,2,4] `
> 注：`[3,1,2,4]` 也是正确的答案之一。
>
>
> 提示：
>
> 1 <= `nums.length` <= 50000
> 1 <= `nums[i]` <= 10000
>
> 来源：力扣（LeetCode）
> 链接：https://leetcode-cn.com/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof
> 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

1. 开辟新数组（`push` &`unshift` ）

   ```js
   /**
    * @param {number[]} nums
    * @return {number[]}
    */
   var exchange = function(nums) {
       const arr = []
       for(let item of nums) {
           item%2 == 0 ? arr.push(item):arr.unshift(item)
       }
       return arr
   };
   ```

2. 双指针交换

   ```js
   /**
    * @param {number[]} nums
    * @return {number[]}
    */
   var exchange = function(nums) {
       const len = nums.length
       if(!len) return [];
       for(let i = 0, j = len -1;i < len, j>=0 , i< j;i = nums[i] % 2 + i, j = j - (nums[j] +1) % 2) {
           [nums[i], nums[j]] = [nums[j], nums[i]];
       }
       return nums
   };
   ```

