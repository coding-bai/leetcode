# `JS`剑指*offer*21--链表中倒数第k个节点

> 输入一个链表，输出该链表中倒数第k个节点。为了符合大多数人的习惯，本题从1开始计数，即链表的尾节点是倒数第1个节点。例如，一个链表有6个节点，从头节点开始，它们的值依次是1、2、3、4、5、6。这个链表的倒数第3个节点是值为4的节点。
>
>  
>
> 示例：
>
> ```js
> 给定一个链表: 1->2->3->4->5, 和 k = 2.
> 
> 返回链表 4->5.
> ```
>
> 来源：力扣（LeetCode）
> 链接：https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof
> 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

1. 栈方法

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
    * @param {number} k
    * @return {ListNode}
    */
   var getKthFromEnd = function(head, k) {
       const stack = []
       let ans = null
       while(head) {
           stack.push(head)
           head = head.next
       }
       while( k > 0) {
           ans = stack.pop()
           k--
       }
       return ans
   };
   ```

2. 双指针

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
    * @param {number} k
    * @return {ListNode}
    */
   var getKthFromEnd = function(head, k) {
       //双指针
       let p = head, q = head
       while(p){
           if(k > 0){
               p = p.next//p先走k步，保证p、q之间相差k步
               k--
           }else{
               p = p.next;//当p走到结尾时，此时的q就是倒数的第k个
               q = q.next
           }
       }
       return q
   };
   ```

   