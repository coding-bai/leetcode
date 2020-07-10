# `JS`剑指*offer*6--用两个栈实现队列

> 用两个栈实现队列：
>
> 用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )
>
> 示例 1：
>
> 输入：
>
> ```js
> ["CQueue","appendTail","deleteHead","deleteHead"]
> [[],[3],[],[]]
> 输出：[null,null,3,-1]
> 示例 2：
> 
> 输入：
> ["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
> [[],[],[5],[2],[],[]]
> 输出：[null,-1,null,null,5,2]
> 
> ```
>
> 提示：
>
> 1 <= values <= 10000
>
> 最多会对 appendTail、deleteHead 进行 10000 次调用
>
> 来源：力扣（LeetCode）
> 链接：https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof

1. 双栈实现

   ```js
   var CQueue = function() {
       this.instack = []
       this.outstack = []
   };
   
   /** 
    * @param {number} value
    * @return {void}
    */
   CQueue.prototype.appendTail = function(value) {
       this.instack[this.instack.length] = value
   };
   
   /**
    * @return {number}
    */
   CQueue.prototype.deleteHead = function() {
       if(!this.outstack.length) {
           let cur  = null
           while(cur = this.instack.pop()) {
               this.outstack.push(cur)
           }
       }
       if(!this.outstack.length) {
           return -1
       } else {
           return this.outstack.pop()
       }
   };
   
   /**
    * Your CQueue object will be instantiated and called as such:
    * var obj = new CQueue()
    * obj.appendTail(value)
    * var param_2 = obj.deleteHead()
    */
   ```

2. 利用对象模拟队列

   ```js
   
   var CQueue = function() {
       this.stackObj = {}
       this.count = 0
       this.bottom = 0
   };
   
   /** 
    * @param {number} value
    * @return {void}
    */
   CQueue.prototype.appendTail = function(value) {
       this.stackObj[this.count] = value
       this.count ++
   };
   
   /**
    * @return {number}
    */
   CQueue.prototype.deleteHead = function() {
       if(this.count - this.bottom === 0) {
           return -1
       }
       let head = this.stackObj[this.bottom]
       delete this.stackObj[this.bottom]
       this.bottom ++
       return head
   };
   
   /**
    * Your CQueue object will be instantiated and called as such:
    * var obj = new CQueue()
    * obj.appendTail(value)
    * var param_2 = obj.deleteHead()
    */
   ```

3. `es6`小技巧瞒天过海

   ```js
   var CQueue = function() {
       this.outStack = []
       this.inStack = []
   };
   
   /** 
    * @param {number} value
    * @return {void}
    */
   CQueue.prototype.appendTail = function(value) {
      this.inStack.push(value)
   };
   
   /**
    * @return {number}
    */
   CQueue.prototype.deleteHead = function() {
       let {outStack, inStack} = this
       if (!outStack.length) {
           while(inStack.length) {
               outStack.push(inStack.pop());
           }
       }
       return outStack.pop() || -1;
   };
   
   /**
    * Your CQueue object will be instantiated and called as such:
    * var obj = new CQueue()
    * obj.appendTail(value)
    * var param_2 = obj.deleteHead()
    */
   
   ```

   