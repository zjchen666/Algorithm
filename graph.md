# 目录 #
<<<<<<< HEAD
* [无向图](#无向图)
      * [遍历](#遍历)
      * [单点可达性](#单点可达性)
      * [判断联通](#1.3)
      * [找寻联通分量](#1.4)
      * [检测环](#检测环)
      * [双色问题](#双色问题)
* [有向图](#有向图)
=======
   * [无向图](#无向图)
      * [遍历](#1.1)
      * [单点可达性](#1.2)
      * [判断联通](#1.3)
      * [找寻联通分量](#1.4)
      * [Has Circle](#1.5)
      * [双色问题](#1.6)
   * [有向图](#2)
>>>>>>> 5d678b9a76756bfa24d818211e3ea478c89d72aa
      * [检测环](#2.1)
      * [单点可达性](#2.2)
      * [拓扑排序](#2.3)

## 无向图 ##
### 遍历
### 单点可达性
### 检测环
### DFS search 模版
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

<<<<<<< HEAD


## 有向图
=======
<span id="1"></span>
# 有向图 #
>>>>>>> 5d678b9a76756bfa24d818211e3ea478c89d72aa
## Has Circle ##
  + marked判断 不要漏掉。
  + on_stack判断， 是w而不是v。
  + 输入是边的话如何创建图，数据结构：list + set。

## topological sort ##
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
