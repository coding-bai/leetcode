# `JS`剑指*offer*26--对称的二叉树

> 请实现一个函数，用来判断一棵二叉树是不是对称的。如果一棵二叉树和它的镜像一样，那么它是对称的。
>
> 例如，二叉树 [1,2,2,3,4,4,3] 是对称的。
>
>     	1
>        / \
>       2   2
>      / \ / \
>     3  4 4  3
>
> 但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:
>
>     	1
>        / \
>       2   2
>        \   \
>        3    3
> 示例 1：
>
> 输入：root = [1,2,2,3,4,4,3]
> 输出：true
> 示例 2：
>
> 输入：root = [1,2,2,null,3,null,3]
> 输出：false
>
>
> 限制：
>
> 0 <= 节点个数 <= 1000
>
> 来源：力扣（LeetCode）
> 链接：https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof
> 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

1. 递归（优化）

   ```js
   /**
    * Definition for a binary tree node.
    * function TreeNode(val) {
    *     this.val = val;
    *     this.left = this.right = null;
    * }
    */
   /**
    * @param {TreeNode} root
    * @return {boolean}
    */
   const isSymmetric = (root) => {
     // 1. 递归树
     const recursion = (root1, root2) => {
       // 2. 如果两个节点同时为空，则为 true
       if (!root1 && !root2) {
         return true;
       }
   
       // 3. 如果只有一个节点为空，则为 false
       if (!root1 || !root2) {
         return false;
       }
   
       // 4. 判断左边和右边是否相等，并且交互判断
       return root1.val === root2.val && recursion(root1.left, root2.right) && recursion(root1.right, root2.left);
     };
   
     // 5. 返回结果
     return recursion(root, root);
   };
   ```

2. 迭代

   ```js
   /**
    * Definition for a binary tree node.
    * function TreeNode(val) {
    *     this.val = val;
    *     this.root1 = this.root2 = null;
    * }
    */
   /**
    * @param {TreeNode} root
    * @return {boolean}
    */
   const isSymmetric = (root) => {
     // 1. 设置当前层
     const nowRoot = [root, root];
     
     // 2. 判断当前层是否可以延续
     while (nowRoot.length) {
   
       // 3. 获取左右部分
       const root1 = nowRoot.pop();
       const root2 = nowRoot.pop();
   
       // 4. 如果两者是空节点，继续
       if (!root1 && !root2) {
         continue;
       }
   
       // 5. 如果左边右边只有一个空，或者左边的值不等于右边
       if (!root1 || !root2 || root1.val !== root2.val) {
         return false;
       }
   
       // 6. 重点：添加值
       nowRoot.push(root1.left);
       nowRoot.push(root2.right);
   
       nowRoot.push(root1.right);
       nowRoot.push(root2.left);
     }
   
     // 7. 如果上面没情况发生
     return true;
   };
   ```

   

   