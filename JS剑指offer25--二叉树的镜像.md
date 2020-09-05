# `JS`剑指*offer*25--二叉树的镜像

> 请完成一个函数，输入一个二叉树，该函数输出它的镜像。
>
> 例如输入：
>
>      	4
>       /   \
>       2     7
>      / \   / \
>     1   3 6   9
>
> 镜像输出：
>
>      	 4
>        /   \
>       7     2
>      / \   / \
>     9   6 3   1
>  示例 1：
>
> 输入：`root` = [4,2,7,1,3,6,9]
> 输出：[4,7,2,9,6,3,1]
>
>
> 限制：
>
> 0 <= 节点个数 <= 1000
>
> 来源：力扣（LeetCode）
> 链接：https://leetcode-cn.com/problems/er-cha-shu-de-jing-xiang-lcof
> 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

es6三行请赐教

搞清楚镜像的定义，简单来说就是：从上到下，依次交换每个节点的左右节点。

来自《剑指 Offer》的示意图：
![img](https://pic.leetcode-cn.com/0f4a336f536d7bcb4c6d06c2ca72e0ff7505e269b9121689e2dc10aa4dd3c7cf.jpg)

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
 * @return {TreeNode}
 */
var mirrorTree = function(root) {
    if(!root) {
        return null
    }
    [root.left, root.right] = [mirrorTree(root.right), mirrorTree(root.left)];
    return root
};
```

