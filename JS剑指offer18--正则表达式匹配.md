# `JS`剑指*offer*18--正则表达式匹配

> 请实现一个函数用来匹配包含'. '和'*'的正则表达式。模式中的字符'.'表示任意一个字符，而'*'表示它前面的字符可以出现任意次（含0次）。在本题中，匹配是指字符串的所有字符匹配整个模式。例如，字符串"aaa"与模式"a.a"和"ab*ac*a"匹配，但与"aa.a"和"ab*a"均不匹配。
>
> 示例 1:
>
> 输入:
> s = "aa"
> p = "a"
> 输出: false
> 解释: "a" 无法匹配 "aa" 整个字符串。
> 示例 2:
>
> 输入:
> s = "aa"
> p = "a*"
> 输出: true
> 解释: 因为 '*' 代表可以匹配零个或多个前面的那一个元素, 在这里前面的元素就是 'a'。因此，字符串 "aa" 可被视为 'a' 重复了一次。
> 示例 3:
>
> 输入:
> s = "ab"
> p = ".*"
> 输出: true
> 解释: ".*" 表示可匹配零个或多个（'*'）任意字符（'.'）。
> 示例 4:
>
> 输入:
> s = "aab"
> p = "c*a*b"
> 输出: true
> 解释: 因为 '*' 表示零个或多个，这里 'c' 为 0 个, 'a' 被重复一次。因此可以匹配字符串 "aab"。
> 示例 5:
>
> 输入:
> s = "mississippi"
> p = "mis*is*p*."
> 输出: false
> s 可能为空，且只包含从 a-z 的小写字母。
> p 可能为空，且只包含从 a-z 的小写字母以及字符 . 和 *，无连续的 '*'。
>
> 来源：力扣（LeetCode）
> 链接：https://leetcode-cn.com/problems/zheng-ze-biao-da-shi-pi-pei-lcof
> 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

1. 暴力递归

```js
/**
 * @param {string} s
 * @param {string} p
 * @return {boolean}
 */
var isMatch = function(s, p) {
    if(!p) return !s;
    //console.log('s:' + s + '\n'+ 'p:' +p + '\n-------')
    let fst = false
    if(s && (p[0] === s[0] || p[0] === '.')) {
        fst = true
    }
    if(p.length >= 2 && p[1] === '*') {
        return isMatch(s, p.substr(2)) || (fst && isMatch(s.substr(1), p))
    } else {
        return fst && isMatch(s.substr(1), p.substr(1))
    }
};
```

2. 动态规划

   字母 + 星号的组合在匹配的过程中，本质上只会有两种情况：

   - 匹配 `ss` 末尾的一个字符，将该字符扔掉，而该组合还可以继续进行匹配；
   - 不匹配字符，将该组合扔掉，不再进行匹配。
     对应的状态转移方程为：`match`->`true`

   ```js
   dp[i][j] = dp[i][j] || dp[i-1][j];
   dp[i][j] = dp[i-1][j-1];
   ```

```js
/**
 * @param {string} s
 * @param {string} p
 * @return {boolean}
 */
var isMatch = function(s, p) {
    let m = s.length;
    let n = p.length;
    let dp = Array.from({length: m+1},x=>new Array(n+1).fill(false));
    dp[0][0] = true;
    for(let i = 0; i <= m;i++) {
        for(let j = 1; j <= n; j++) {
            if(p[j-1] === "*") {
                dp[i][j] = dp[i][j-2];
                if(match(s,p,i,j-1)) {
                    dp[i][j] = dp[i][j] || dp[i-1][j];
                }
            } else {
                if(match(s,p,i,j)) {
                    dp[i][j] = dp[i-1][j-1];
                }
            }
        }
    }
    return dp[m][n];
};
const match = (s,p,i,j)=> {
    if(i === 0) return false;
    if(p[j-1] === '.') return true;
    return s[i-1] === p[j-1];
}
```

​	