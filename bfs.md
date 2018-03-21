## Breadth First Search ##

1. 注意判断需不需要使用分层遍历。
2. __能用BFS一定不用DFS__，non-recursion and easy understanding!

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
