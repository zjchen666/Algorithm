## Breadth First Search ##

1. 注意判断需不需要使用分层遍历。
2. __能用BFS一定不用DFS，non-recursion and easy understanding!__
3. clone 类问题要结合hashtable or hashset
4. 对于矩阵型BFS，如果需要，可以使用一个同样大小的矩阵储存状态。
5. 注意queue的初始化，可以加快速度。
   [ocean-water-flow](https://leetcode.com/problems/pacific-atlantic-water-flow/description/)



### 模板 ###
```python
   def bfs( node ):
       q = [node]
       while q:
           size = len(q)
           while size > 0
               # find next level nodes and push them into queue
               q.insert(0, next)
               size -= 1
```
