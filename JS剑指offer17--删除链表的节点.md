# ` JS`剑指*offer*17--删除链表的节点

> 给定单向链表的头指针和一个要删除的节点的值，定义一个函数删除该节点。
>
> 返回删除后的链表的头节点。
>
> 注意：此题对比原题有改动
>
> 示例 1:
>
> 输入: head = [4,5,1,9], val = 5
> 输出: [4,1,9]
> 解释: 给定你链表中值为 5 的第二个节点，那么在调用了你的函数之后，该链表应变为 4 -> 1 -> 9.
> 示例 2:
>
> 输入: head = [4,5,1,9], val = 1
> 输出: [4,5,9]
> 解释: 给定你链表中值为 1 的第三个节点，那么在调用了你的函数之后，该链表应变为 4 -> 5 -> 9.
>
> 来源：力扣（LeetCode）
> 链接：https://leetcode-cn.com/problems/shan-chu-lian-biao-de-jie-dian-lcof
> 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

1. 找到停止法（这是我自己起的名字）

   思路就是找到要删除的值退出循环然后并进行删除操作

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
    * @param {number} val
    * @return {ListNode}
    */
   var deleteNode = function(head, val) {
       if(head.val === val) return head.next
       let node,pre
       for(node = head.next, pre = head; node.val !== val;pre = node, node = node.next);
       pre.next = node.next
       return head
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
    * @param {number} val
    * @return {ListNode}
    */
   var deleteNode = function(head, val) {
       if(head.val == val){
           return head.next
       }
       /**
        * 假设【1，2，3】，目标值是2
        * 当前head是1.
        * 本来head.next是2,但是调用deletenode函数的时候刚刚好2==2,把2（head）的下一个值3的指针返回回去
        * 所以head.next = 3
        * 1->3
        * 
       */
       head.next = deleteNode(head.next,val);
       return head
   };
   
   ```

   

