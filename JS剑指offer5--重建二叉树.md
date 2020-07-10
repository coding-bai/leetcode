# `JS`剑指*offer*5--重建二叉树

> 重建二叉树：
>
> 输入某二叉树的前序遍历和中序遍历的结果，请重建该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。
>
> 例如，给出
>
> 前序遍历 preorder = [3,9,20,15,7]
> 中序遍历 inorder = [9,3,15,20,7]
> 返回如下的二叉树：
>
> ```js
> 	3
>    / \
>   9  20
>     /  \
>    15   7
> 
> ```
>   
>
>
> 限制：
>
> 0 <= 节点个数 <= 5000
>
> 来源：力扣（LeetCode）
> 链接：https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof

这里先来了解一下三种遍历方式：

- 前序遍历（VLR）： 
    1.访问根节点 
    2.前序遍历左子树 
    3.前序遍历右子树 

- 中序遍历（LVR）： 
    1.中序遍历左子树 
    2.访问根节点 
    3.中序遍历右子树 

- 后序遍历（LRV）： 
    1.后序遍历左子树 
    2.后序遍历右子树 
    3.访问根节点 

  ---

  1.分治思想

  通过读题可知题中所给二叉树前序遍历可知二叉树根节点为3，便可在中序遍历中得知左子树只有一个节点那就是3,并且20、15、7是右子树，然后根据前序遍历可知右子树的根节点为20，便可通过递归进行解题。

  ```js
  var buildTree = function(preorder, inorder) {
      if(!(preorder.length || inorder.length)) {
          return null
      }
      //确定根节点
      let node = new TreeNode(preorder[0]);
      //获取根节点所在中序遍历的位置
      let index = inorder.indexOf(preorder[0])
      //利用根节点所在位置划分左右子树
      node.left = buildTree(preorder.slice(1, index +1),inorder.slice(0,index))
      node.right = buildTree(preorder.slice(index+1),inorder.slice(index+1))
      return node
  };
  ```

