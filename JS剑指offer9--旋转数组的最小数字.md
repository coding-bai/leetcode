# `JS`剑指*offer*9--旋转数组的最小数字

> 把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个递增排序的数组的一个旋转，输出旋转数组的最小元素。例如，数组 [3,4,5,1,2] 为 [1,2,3,4,5] 的一个旋转，该数组的最小值为1。  
>
> 示例 1：
>
> 输入：[3,4,5,1,2]
> 输出：1
> 示例 2：
>
> 输入：[2,2,2,0,1]
> 输出：0
>
> 来源：力扣（LeetCode）
> 链接：https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof
> 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

1. 双指针

   ```js
   /**
    * @param {number[]} numbers
    * @return {number}
    */
   var minArray = function(numbers) {
       let res = numbers[0]
       for(let i = 0; i< numbers.length/2; i ++) {
           res = Math.min(res,numbers[i],numbers[numbers.length -1 -i])
       }
       return res
   };
   ```

2. 二分法

   >  `(right+left)/2` == `left+(right-left)/2` 

   - 旋转后的数组可以划分为两个有序的子区间，前面区间的元素都大于等于后面的元素，我们要找的是两个子区间的分界，很自然想到二分查找
     - `nums[mid]` > `nums[right]`

   - 最小元素肯定在mid的右边，所以 `left = mid + 1`
     - `nums[mid]` == `nums[right]`

   - 此时 mid 可能处于左边区间，也可能处于右边区间，即最小元素不确定在它的左边还是右边
     所以 right-- ，换一个 `nums[right]` 再试
     - `nums[mid]` < `nums[right]`

   - 此时 mid 肯定处在右边的增区间，所以 `right = mid`

   ```js
   /**
    * @param {number[]} numbers
    * @return {number}
    */
   var minArray = function(numbers) {
       let left = 0, right = numbers.length -1
       while(left < right) {
           const mid = left + right >>> 1
           if (numbers[mid] > numbers[right]) {
               left = mid + 1
           } else if (numbers[mid] === numbers[right]) {
               right --
           } else {
               right = mid
           }
       }
       return numbers[left]
   };
   ```

3. `Array.sort()`方法

   ```js
   /**
    * @param {number[]} numbers
    * @return {number}
    */
   var minArray = function(numbers) {
       return numbers.sort((a,b) => a-b)[0]
   };
   ```

4. `es6`扩展运算符

   ```js
   /**
    * @param {number[]} numbers
    * @return {number}
    */
   var minArray = function(numbers) {
       return Math.min(...numbers)
   };
   ```

   

