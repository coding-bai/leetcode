# `JS`剑指*offer*22--反转链表

> 定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。
>
> 示例:
>
> 输入: 1->2->3->4->5->NULL
> 输出: 5->4->3->2->1->NULL
>
>
> 限制：
>
> 0 <= 节点个数 <= 5000
>
> 来源：力扣（LeetCode）
> 链接：https://leetcode-cn.com/problems/fan-zhuan-lian-biao-lcof
> 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

1. 双指针

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
    * @return {ListNode}
    */
   var reverseList = function(head) {
       let prev = null, cur = head;
       while(cur){ 
           [cur.next, prev, cur] = [prev, cur, cur.next];
       }
       return prev;
   };
   ```

2. 递归

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
    * @return {ListNode}
    */
   var reverseList = function(head) {
       if(head == null || head.next == null) return head;
       let newReverseList = reverseList(head.next), newReverseListTail = head.next
       newReverseListTail.next = head
       head.next = null
       return newReverseList
   };
   ```

