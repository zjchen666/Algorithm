## Dynamic Programming ##
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
  - f为二维数组时， 优化空间时可以考虑使用滚动数组。  
   
#### 坐标型动态规划
   一般不需要多分配元素，f 为 m * n 矩阵.
   
#### 双序列型动态规划
 - f 为 (M+1) * (N+1) 矩阵， f[i][j] 为A序列前 1 ～ i 个元素，和B序列前 1 - j 个元素的子问题。
 - 注意 判断时 compare s1[i - 1] and s2[j - 1]
 - 扫描方式为按行扫描。
 
      int minDistance(string word1, string word2) {
       int m = word1.size(), n = word2.size();
       
       vector<vector<int>> f(m + 1, vector<int>(n + 1, 0));
       
       for (int i = 0; i < m + 1; ++i) {
           for (int j = 0; j < n + 1; ++j) {
               if (i == 0) {
                   f[i][j] = j;
               } else if (j == 0) {
                   f[i][j] = i;
               } else {
                   if (word1[i - 1] == word2[j - 1]) {
                       f[i][j] = f[i - 1][j - 1];
                   } else {
                       int val = min(f[i - 1][j], f[i][j - 1]);
                       f[i][j] = min(f[i - 1][j - 1], val) + 1;
                   }
               }
           }
       } 
       return f[m][n];
   }
https://leetcode.com/problems/regular-expression-matching/description/
https://leetcode.com/problems/wildcard-matching/description/
1092. Shortest Common Supersequence
1062. Longest Repeating Substring
516. Longest Palindromic Subsequence

#### 区间型动态规划
   - 一般是一个数组，字串。  
   - F 为 m * n 矩阵， 子问题为 f[i][j]代表区间为 i - j 的子问题。  
   - 按照对角线初始化以及搜索。  
```cpp
      对角线扫描方法
        for (int len = 0; len < n; len++) {
            for (int i = 0; i < n - len; i++) {
                j = i + len;
            }
        }
```
   - O(n^3) burst bullon
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
https://leetcode.com/problems/longest-palindromic-substring/description/  
https://leetcode.com/problems/longest-valid-parentheses/

#### 划分型动态规划
• 给定长度为N的序列或字符串，要求划分成若干段 – 段数不限，或指定K段  
– 每一段满足一定的性质  
• 做法  
– 类似于序列型动态规划，但是通常要加上段数信息  
– 一般用f[i][j]记录前i个元素(元素0~i-1)分成j段的性质，如最小代价  

#### 背包型动态规划
   * 0-1 背包：
   - 选 或 不选 
   - 2D 数组 size为 f[n + 1][v + 1]
   - F[i][j] = max(F[i-1][j], F[i - 1][j - W[i]] + C[i])  
   - 优化为一维滚动数组需要逆序计算， size： f[v + 1] 
```cpp
    vector<vector<int>> f(v + 1, vector<int>(n + 1, 0));
    for (int i = 0; i <= n; ++i) {
        for (int j = 0; j <= v; ++j) {
            if (j > A[i])
                f[i][j] = max(f[i - 1][j], f[i - 1][j - A[i]] + A[i]);
        }
    }
    return f[n][v];
```
```python
      # n - number of items
      # V - volume of backpack
      # W - weights of items
      # C - values of items
      for i in range(n):
          for v in range(V, W[i], -1):
              f[j] = max(f[j], f[j - W[i]] + C[i]]
```
   * 完全背包: 
   - 不选 或 当前 v - Ci 容量 + 当前 重量  
   - 数组size为 v + 1
   - F[i][j] = max(F[i-1][j], F[i][j - W[i]] + C[i]）  
   - 滚动数组正序计算
   
```python
      # n - number of items
      # V - volume of backpack
      # W - weights of items
      # C - values of items
      for i in range(n):
          for v in range(W[i], V):
              f[j] = max(f[j], f[j - W[i]] + C[i]]
```   

   * 多重背包: 
   - 可以认为 0 - 1 背包 多了一些 物品
   - 数组size为 v + 1
   ```python
      # n - number of items
      # V - volume of backpack
      # W - weights of items
      # C - values of items
      # K - quantity of iteams
      for i in range(n):
          for k in range(K[i]):
              for v in range(V, W[i], -1):
                  f[j] = max(f[j], f[j - W[i]] + C[i]]
```  

#### 博弈型动态规划
- 要理解 所有子问题必胜则必拜， 一个子问题必败则必胜。
- 注意minimax如何处理。每一步要按照上一步的min（对手最坏情况）来计算。
    
    1. DFS + memo 解法模板，
```python
    def dfs(nums, memo):
        if (满足条件):
            return True
           
        if memo[nums]:
            return memo

        for i in range(len(nums)):
            if False == dfs(sub_nums, memo):
                memo[nums[i]] = True 
                return True
        memo[nums[i]] = False 
        return False
```
https://leetcode.com/problems/can-i-win/description/   
https://leetcode.com/problems/flip-game-ii/description/   
https://leetcode.com/problems/guess-number-higher-or-lower-ii/description/  
https://leetcode.com/problems/stone-game/description/
