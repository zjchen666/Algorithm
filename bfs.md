## Breadth First Search 

### 主要题型  
   **图的遍历 Traversal in Graph**
    • 层级遍历 Level Order Traversal  
    • 由点及面 Connected Component  
    • 拓扑排序 Topological Sorting  
   **最短路径 Shortest Path in Simple Graph**
    • 仅限简单图求最短路径即，图中每条边长度都是1，或者边长都相等  
   **非递归的方式找所有方案 Iteration solution for all possible results**

### 注意事项
   1. **注意判断需不需要使用分层遍历**
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
```cpp
   template <class name T>
   void bfs(T & node):
       queue<T> q = {node};
       int size = 0;
       
       while (!q.empty()) {
           size = q.size();
           while (size > 0)
               head_node = q.pop_front();
               # find next level nodes and push them into queue
               ...
               q.push_back(new_node);
               size -= 1;
       }
       return;
```
