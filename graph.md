# 目录
   * [无向图](#无向图)
      * [遍历](#遍历)
      * [单点可达性](#单点可达性)
      * [判断联通](#判断联通)
      * [找寻联通分量](#找寻联通分量)
      * [检测环](#检测环)
      * [双色问题](#双色问题)
   * [有向图](#有向图)
      * [检测环](#检测环)
      * [单点可达性](#单点可达性)
      * [拓扑排序](#拓扑排序)

## 无向图
### 遍历
* DFS search 模版
```python
   def graph_search(self, node):
       marked = set()
       dfs(node, marked)

   def dfs(self, node, marked):
       marked.add(root)
       for w in node.neighbors:
           if w not in marked:
               dfs(w, marked)
```
### 单点可达性
 * DFS
 * BFS
### 检测环
 * DFS
### 判断联通
 * Union Find
 * DFS
### 找寻联通分量
 * Union Find 
     - 适合只提供边的情况。和定点的值在范围 0 ～ N的情况。
     - 节点的顺序没有要求。
```python
        def find(p, id):
            while id[p] != p:
                p = id[p]
            return p
            
        def union(p, q, id):
            pRoot = find(p)
            qRoot = find(q)
            if pRoot != qRoot:
                id[pRoot] = qRoot
                count -= 1
            return
```
 * DFS 
    - 需要对图进行预处理， 适合提供完整图的情况。
    - 不适合二维矩阵的情况
```python
        for w in nodes:
            if marked[w] != True:
                dfs(w, marked, id)
                count += 1
              
        def dfs(w, marked, stack):
            marked[w] = True
            id[w] = count
            for v in w.neighbors:
                if marked[v] != True:
                    dfs(v, marked, stack)
```
### 双色问题
   * DFS
    
## 有向图
### 单点可达性
### 检测环
  + marked判断 不要漏掉。
  + on_stack判断， 是w而不是v。
  + 输入是边的话如何创建图，数据结构：list + set。

### 拓扑排序
  + BFS. 从indegree 为0的vertex开始。
  + DFS 逆后序输出结果即可。

```python
class Solution(object):
    def canFinish(self, numCourses, prerequisites):
        """
        :type numCourses: int
        :type prerequisites: List[List[int]]
        :rtype: bool
        """
        on_stack = [False for i in range(numCourses)]
        marked = [False for i in range(numCourses)]
        graph = [set() for i in range(numCourses)]
        self.has_circle = False
        for v, w in prerequisites:
            graph[v].add(w)    
        
        for v in range(numCourses):
            if not marked[v]:
                self.dfs(v, graph, on_stack, marked)
        return not self.has_circle
    
    def dfs(self, v, graph, on_stack, marked):        
        if self.has_circle == True:
            return
        
        marked[v] = True
        on_stack[v] = True
        for w in graph[v]:
            if marked[w] != True:
                self.dfs(w, graph, on_stack, marked)
            elif on_stack[w] == True:
                self.has_circle = True
        on_stack[v] = False
```