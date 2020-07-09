# `JS`剑指*offer*1--找出数组中重复的数字

> 找出数组中重复的数字。
>
> 在一个长度为 n 的数组 `nums` 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。
>
> 示例 1：
>
> 输入：
> [2, 3, 1, 0, 2, 5, 3]
> 输出：2 或 3 
>
> 限制：
>
> 2 <= n <= 100000
>
> 来源：力扣（`LeetCode`）
> 链接：https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof

1. `hash`表

   通过哈希表键值对的存储特点，使用`number`-`boolean`的结构，遍历数组中的数字，未出现就存入哈希表并将值改为`true`，一旦出现过，就可以通过`boolean`的值进行判断。

   ```js
   /**
    * @param {number[]} nums
    * @return {number}
    */
   var findRepeatNumber = function(nums) {
       const hash = {}
       for(const num of hash) {
           if(!hash[num]) {
               hash[num] = true
           } else {
               return num
           }
       }
   };
   ```

2. 自身`hash`

   由题可知，数字的范围是0~n-1，而数组的长度是n，所以就是一个萝卜一个坑的道理，每个元素都应该在自己的位置上。首先通过遍历检查当前元素是否放在了正确的位置上（`i`应在`nums`下标为`i`的位置上）

   例如：

   - `nums[num]`的元素和`num`相等，说明`num`元素重复，返回`num`

     - 比如数组`[1,3,2,4,3]`，如果`i=1`,`num = nums[i]`(3)，而`nums[num] = num`,所以可以判断出`num`即为重复元素，

   - `nums[num]`的元素和`num`不相等，那么久交换当前元素`nums[i]`和`nums[num]`, 将元素放入正确的位置

     ```js
     /**
      * @param {number[]} nums
      * @return {number}
      */
     var findRepeatNumber = function(nums) {
         const len = nums.length;
         for(let i = 0,num = 0; i< len; ++i) {
             while((num = nums[i]) != i) {
                 if(num === nums[num]) {
                     return num;
                 }
                 [nums[i],nums[num]] = [nums[num],nums[i]]
             }
         }
     };
     ```

     

3. `set`去重

   `ES6`提出的`set`是全新的解决方案，通过使用`set`忽略重复元素的特点，只需判断`set`长度即可

   ```js
   /**
    * @param {number[]} nums
    * @return {number}
    */
   var findRepeatNumber = function(nums) {
       let s = new Set()
       for(let num in nums) {
           let len = s.size
           s.add(nums[num])
           if(s.size === len) return nums[num]
       }
   };
   ```

4. 数组排序法（**最容易理解**）

   该方法将数组进行排序并且对排序后的数组进行遍历只要相邻元素相等即可

   ```js
   /**
    * @param {number[]} nums
    * @return {number}
    */
   var findRepeatNumber = function(nums) {
       nums.sort();
       for(var i=0, len = nums.length;i< len -1;i++){
           if(nums[i]==nums[i+1]) return nums[i];
       }
   };
   ```

   