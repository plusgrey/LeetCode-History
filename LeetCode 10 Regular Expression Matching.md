给你一个字符串 s 和一个字符规律 p，请你来实现一个支持 ' . ' 和 ' * ' 的正则表达式匹配。

'.' 匹配任意单个字符

'*' 匹配零个或多个前面的那一个元素

所谓匹配，是要涵盖整个字符串s的，而不是部分字符串。

 
示例 1：

输入：s = "aa" p = "a"

输出：false

解释："a" 无法匹配 "aa" 整个字符串。

示例 2:

输入：s = "aa" p = "a*"

输出：true

解释：因为 '*' 代表可以匹配零个或多个前面的那一个元素, 在这里前面的元素就是 'a'。因此，字符串 "aa" 可被视为 'a' 重复了一次。

示例 3：

输入：s = "ab" p = ".*"

输出：true

解释：".*" 表示可匹配零个或多个（'*'）任意字符（'.'）。


```python
class Solution:
    @lru_cache(None)
    def isMatch(self, s: str, p: str) -> bool:
        if not p: return not s  # 结束条件

        first_match = (len(s) > 0) and p[0] in {s[0], '.'}
        # 先处理 `*`
        if len(p) >=2 and p[1] == '*':
            # 匹配0个 | 多个
            return self.isMatch(s, p[2:]) or (first_match and self.isMatch(s[1:], p))
        
        # 处理 `.` ，匹配一个
        return first_match and self.isMatch(s[1:], p[1:])
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-1-eaf87da88383> in <module>
    ----> 1 class Solution:
          2     @lru_cache(None)
          3     def isMatch(self, s: str, p: str) -> bool:
          4         if not p: return not s  # 结束条件
          5 
    

    <ipython-input-1-eaf87da88383> in Solution()
          1 class Solution:
    ----> 2     @lru_cache(None)
          3     def isMatch(self, s: str, p: str) -> bool:
          4         if not p: return not s  # 结束条件
          5 
    

    NameError: name 'lru_cache' is not defined

