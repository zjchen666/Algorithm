## heap ##
### python PQ 库函数
```python
import heapq

# 把 list heap 化
heapq.heapify(list)

heapq.heappush(heap, item)

item = heapq.heappop(heap)

list = heapq.nsmallest(heap)

list = heapq.nlargest(heap)

```
### 时间复杂度：
   create heap - O(N)
   insert - O(logN)
   delete - O(logN)
