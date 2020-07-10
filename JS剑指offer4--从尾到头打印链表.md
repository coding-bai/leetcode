# `JS`剑指*offer*4--从尾到头打印链表

>从尾到头打印链表:
>
>输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。
>
>示例 1：
>
>输入：head = [1,3,2]
>输出：[2,3,1]
>
>
>限制：
>
>0 <= 链表长度 <= 10000
>
>来源：力扣（LeetCode）
>链接：https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof

1. 用栈存储

   - 通过不断从数组首部插入链表元素便可

     ```js
     /**
      * Definition for singly-linked list.
      * function ListNode(val) {
      *     this.val = val;
      *     this.next = null;
      * }
      */
     /**
      * @param {ListNode} head
      * @return {number[]}
      */
     var reversePrint = function(head) {
         const arr = [];
         while(head) {
             arr.unshift(head.val)
             head = head.next
         }
         return arr
     };
     ```

2. 正序存入数组然后通过`reverse`方法逆置数组

3. 暂时还没找到更好的方法