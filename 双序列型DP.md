
例题；Edit Distance https://leetcode.com/problems/edit-distance/

思路：
递归： 代码框架
```cpp
    int helper(int i, int j, string word1, string word2) {
        // base case
        if (i == word1.size()) return word2.size() - j;
        if (j == word2.size()) return word1.size() - i;
      
        // recursion      
        if (word1[i] == word2[j]) {
            return = helper(i + 1, j + 1, word1, word2);
        } else {
            return = 1 + min(helper(i + 1, j, word1, word2),
                             helper(i, j + 1, word1, word2));
                             helper(i + 1, j + 1, word1, word2));
        }
    }
```
1. 正向 bottom up
```cpp
    int helper(int i, int j, 
               string word1, 
               string word2, 
               vector<vector<int>>& dp) {
        // base case
        if (i == word1.size()) return word2.size() - j;
        if (j == word2.size()) return word1.size() - i;
        
        int res = 0;
        
        if (dp[i][j] != 0) return dp[i][j];
            
        if (word1[i] == word2[j]) {
            res = helper(i + 1, j + 1, word1, word2, dp);
        } else {
            res = min(helper(i + 1, j, word1, word2, dp),
                      helper(i, j + 1, word1, word2, dp));
            res = min(res, helper(i + 1, j + 1, word1, word2, dp));
            res += 1;
        }
        dp[i][j] = res;
        return dp[i][j];
    }
    int minDistance(string word1, string word2) {
        vector<vector<int>> dp(word1.size(), vector<int>(word2.size(), 0));
        
        return helper(0, 0, word1, word2, dp);
    }
 ```
3. 反向 top bottom
```cpp
    int helper(int i, int j, 
               string word1, 
               string word2, 
               vector<vector<int>>& dp) {
        // base case
        if (i == -1) return j + 1;
        if (j == -1) return i + 1;
        
        int res = 0;
        
        if (dp[i][j] != 0) return dp[i][j];
            
        if (word1[i] == word2[j]) {
            res = helper(i + 1, j + 1, word1, word2, dp);
        } else {
            res = min(helper(i - 1, j, word1, word2, dp),
                      helper(i, j - 1, word1, word2, dp));
            res = min(res, helper(i - 1, j - 1, word1, word2, dp));
            res += 1;
        }
        dp[i][j] = res;
        return dp[i][j];
    }
    int minDistance(string word1, string word2) {
        vector<vector<int>> dp(word1.size(), vector<int>(word2.size(), 0));
        
        return helper(0, 0, word1, word2, dp);
    }
```

DP table


f 为 (M+1) * (N+1) 矩阵， f[i][j] 为A序列前 1 ～ i 个元素，和B序列前 1 - j 个元素的子问题。
注意 判断时 compare s1[i - 1] and s2[j - 1]
扫描方式为按行扫描。
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
