## Dynamic programming ##
### 动态规划分类 ###
+ [序列型动态规划](#序列型动态规划)
+ [坐标型动态规划](#坐标型动态规划)
+ [划分型动态规划](#划分型动态规划)
+ [区间型动态规划](#区间型动态规划)
+ [博弈型动态规划](#博弈型动态规划)
+ [背包型动态规划](#背包型动态规划)
+ [双序列型动态规划](#双序列型动态规划)
+ 混合型动态规划 - hash table， tree

#### 序列型动态规划
  - 不带状态： 一般是 f[i] = max(f[i] + k, f[i-j] ) |  i > j >= 0  
  - 带状态：二维数组，k种状态： f[i][k] = max(f[i-1][k], f[i][k-1])  
  - 处理边界条件时， 可能需要多分配一个元素。  
  - f为二维数组时， 优化空间时可以使用滚动数组。  
   
#### 坐标型动态规划
   一般不需要多分配元素，f 为 m * n 矩阵.
  

#### 区间型动态规划
   - f 为 m * n 矩阵， 子问题为 f[i][j]代表区间为 i - j 的子问题。  
   - 按照对角线初始化以及搜索。  
   
```python
        n = len(s)
        f = [[False for i in range(n)] for j in range(n)]
        
        # length == 1
        for i in xrange(n):
            f[i][i] = 1
        
        # length == 2
        for i in xrange(n-1):
            f[i][i+1] = 2 if s[i] == s[i+1] else 1
            
        # len 3 -> n
        for length in xrange(3, n + 1):
            for i in xrange(n + 1 - length):
                j = i + length - 1
                if s[i] == s[j] and f[i+1][j-1]:
                    f[i][j] = f[i+1][j-1] + 2
                else:
                    f[i][j] = max(f[i+1][j], f[i][j+1])

        return f[0][-1]
```
#### 双序列型动态规划
   - f 为 (M+1) * (N+1) 矩阵， f[i][j] 为A序列前 1 ～ i 个元素，和B序列前 1 - j 个元素的子问题。
   
