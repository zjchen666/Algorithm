 ## Binary Index Tree ## 
__用法__ :  O(log(n)) 的时间内求一段区间内的和.

__主要操作__ ：update 某一点， 区间求和 .

__离散化__ ： discretization. 用于降低区间范围 


```python
        def descretization(A):
            hash = {}
            A.sorted()
            count = 1
            for num in A:
                if num not in hash:
                    hash[num] = count
                    count += 1
            return
            
        def add(x, tree):
            while x <= len(tree) - 1:
                tree[x] += 1
                x += x & -x
                
            return
        
        def query(x, tree):
            result = 0
            while x > 0:
                result -= tree[x]
                x = x & -x
            return result
```
