给定两个单词（beginWord 和 endWord）和一个字典，找到从 beginWord 到 endWord 的最短转换序列的长度。转换需遵循如下规则：

每次转换只能改变一个字母。
转换过程中的中间单词必须是字典中的单词。
说明:

如果不存在这样的转换序列，返回 0。

所有单词具有相同的长度。

所有单词只由小写字母组成。

字典中不存在重复的单词。

你可以假设 beginWord 和 endWord 是非空的，且二者不相同。

### 示例 1:

输入:
beginWord = "hit",
endWord = "cog",
wordList = ["hot","dot","dog","lot","log","cog"]

输出: 5

解释: 一个最短转换序列是 "hit" -> "hot" -> "dot" -> "dog" -> "cog",
     返回它的长度 5。

### 示例 2:

输入:
beginWord = "hit"
endWord = "cog"
wordList = ["hot","dot","dog","lot","log"]

输出: 0

解释: endWord "cog" 不在字典中，所以无法进行转换。

# BFS算法解决：

## BFS的标准套路：
for head in all_node():

    if head 没有visited过   
    # 以上两步是为了防止有孤立的部分存在而被遗漏，如果没有孤立的部分可以不写，直接放queue里一个就开始循环即可
        queue.append(head)
        mark head
        # 主干部分
        while queue is not empty:
            cur_node = queue.pop() # 我们不需要关心node将会以何种顺序出queue，我们只在乎如何往queue里进就行了。
            # 找邻居
            for 所有 cur_node 的邻居们：
                if cur_neighbour 没有visit过：
                    deal -> cur_neighbour
                    mark -> cur_neighbour
                    inject -> cur_neighbour

## 结构总结
上述过程可以总结为四个模块


for 找head
    while queue：
        for 找邻居
            if 没有重复：处理，标记，入队

## 如何mark
mark的方法有很多，常见的方法是把所有遍历过的node放到set里，每次都去set里查看，是否已经存在于set里了。
也可以写一个dict，key是node，value是bool，表示是否访问过了

## 如何找邻居
在这道题中，找邻居的方法比较复杂：


for 所有可能去掉一个字母的同源
    for 每个同源的都是邻居


```python
from collections import defaultdict
from collections import deque
class Solution(object):
    def ladderLength(self, beginWord, endWord, wordList):
        # 建立通用list
        size, general_dic = len(beginWord), defaultdict(list)
        for w in wordList:
            for _ in range(size):
                general_dic[w[:_]+"*"+w[_+1:]].append(w)
        # BFS
        queue = deque()
        queue.append((beginWord, 1))  # 因为在BFS中，queue中通常会同时混合多层的node，这就无法区分层了，要区分层就要queue中直接加入当前node所属层数。
        mark_dic = defaultdict(bool)  # bool 的默认值是false，因此所有不在list里的是false
        mark_dic[beginWord] = True
        while queue:
            cur_word, level = queue.popleft()   # queue头出来一个
            for i in range(size):               # 找邻居，这里的所有邻居都在level+1层
                for neighbour in general_dic[cur_word[:i]+"*"+cur_word[i+1:]]:
                    if neighbour == endWord: return level + 1
                    if not mark_dic[neighbour]:
                        mark_dic[neighbour] = True
                        queue.append((neighbour, level+1))  #符合条件（neighbour + unmarked)的进去
        return 0

```

# defaultdict 与 dequeue总结

dequeue双向队列 ： https://www.cnblogs.com/zhenwei66/p/6598996.html

defaultdict（带默认值的字典）： https://blog.csdn.net/real_ray/article/details/17919289


```python

```
