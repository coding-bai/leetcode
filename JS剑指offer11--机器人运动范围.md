# `JS`剑指*offer*11--机器人运动范围

> 地上有一个m行n列的方格，从坐标 [0,0] 到坐标 [m-1,n-1] 。一个机器人从坐标 [0, 0] 的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于k的格子。例如，当k为18时，机器人能够进入方格 [35, 37] ，因为3+5+3+7=18。但它不能进入方格 [35, 38]，因为3+5+3+8=19。请问该机器人能够到达多少个格子？
>
> 示例 1：
>
> 输入：m = 2, n = 3, k = 1
> 输出：3
> 示例 2：
>
> 输入：m = 3, n = 1, k = 0
> 输出：1
> 提示：
>
> 1 <= n,m <= 100
> 0 <= k <= 20
>
> 来源：力扣（LeetCode）
> 链接：https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof
> 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

题意关键点：

> - 位数和的计算
> - 四周方向的遍历
> - 限制条件
> - 格子数的统计

- 位数计算

  - 字符串

    ```js
    function getSum(num) {
        let stringAry = num.toString().split('');
    
        return stringAry.reduce((a, b) => Number(a) + Number(b), 0);
    }
    ```

  - 数学公式

    ```js
    function getSum(num) {
        let answer = 0;
    
        while(num) {
            answer += num % 10;
            // 向下取整，因为可能出现小数
            num = Math.floor(num / 10);
        }
    
        return answer;
    } 
    ```

- 代码实现

  - BFS - 1

    ```js
    /**
     * @param {number} m
     * @param {number} n
     * @param {number} k
     * @return {number}
     */
    var movingCount = function(m, n, k) {
        // 位数和
        function getSum(num) {
            let answer = 0;
    
            while(num) {
                answer += num % 10;
                num = Math.floor(num / 10);
            }
    
            return answer;
        } 
        // 方向数组
        const directionAry = [
            [-1, 0], // 上
            [0, 1], // 右
            [1, 0], // 下
            [0, -1] // 左
        ];
    
        // 已经走过的坐标
        let set = new Set(['0,0']);
    
        // 将遍历的坐标队列，题意要求从[0,0]开始走
        let queue = [[0, 0]];
    
        // 遍历队列中的坐标
        while(queue.length) {
            // 移除队首坐标
            let [x, y] = queue.shift();
    
            // 遍历方向
            for(let i = 0; i < 4; i++) {
                let offsetX = x + directionAry[i][0];
                let offsetY = y + directionAry[i][1];
    
    
                // 临界值判断
                if(offsetX < 0 || offsetX >= m || offsetY < 0 || offsetY >= n || getSum(offsetX) + getSum(offsetY) > k || set.has(`${offsetX},${offsetY}`)) {
                    continue;
                }
    
                // 走过的格子就不再纳入统计
                set.add(`${offsetX},${offsetY}`);
    
                // 将该坐标加入队列（因为这个坐标的四周没有走过，需要纳入下次的遍历）
                queue.push([offsetX, offsetY]);
            }
        }
    
        // 走过坐标的个数就是可以到达的格子数
        return set.size;
    };
    ```

  - BFS - 2

    ```JS
    /**
     * @param {number} m
     * @param {number} n
     * @param {number} k
     * @return {number}
     */
    var movingCount = function(m, n, k) {
        let res = 0;
        const directions = [
            [1, 0],
            [0, 1]
        ];
        const queue = [[0, 0]];
        const visited = {
            "0-0": true
        }; // 标记 (x,y) 是否被访问过
    
        while (queue.length) {
            const [x, y] = queue.shift();
            //  (x, y) 的数位之和不符合要求
            // 题目要求节点每次只能走1格，所以无法从当前坐标继续出发
            if (bitSum(x) + bitSum(y) > k) {
                continue;
            }
            ++res;
    
            for (const direction of directions) {
                const newx = direction[0] + x;
                const newy = direction[1] + y;
                if (
                    !visited[`${newx}-${newy}`] &&
                    newx >= 0 &&
                    newy >= 0 &&
                    newx < m &&
                    newy < n
                ) {
                    queue.push([newx, newy]);
                    visited[`${newx}-${newy}`] = true;
                }
            }
        }
    
        return res;
    };
    ```

  - DFS

    ```js
    /**
     * @param {number} m
     * @param {number} n
     * @param {number} k
     * @return {number}
     */
    var movingCount = function(m, n, k) {
        let res = 0;
        const directions = [
            [-1, 0],
            [1, 0],
            [0, -1],
            [0, 1]
        ];
        const visited = {};
        dfs(0, 0);
        return res;
    
        function dfs(x, y) {
            visited[`${x}-${y}`] = true;
            if (bitSum(x) + bitSum(y) > k) {
                return;
            }
            ++res;
    
            for (const direction of directions) {
                const newx = direction[0] + x;
                const newy = direction[1] + y;
                if (
                    !visited[`${newx}-${newy}`] &&
                    newx >= 0 &&
                    newy >= 0 &&
                    newx < m &&
                    newy < n
                ) {
                    dfs(newx, newy);
                }
            }
        }
    };
    ```

    