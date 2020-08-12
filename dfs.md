
## 搜索的问题基本为排列或组合的问题

__递归三要素__:  
__递归的定义__：接受什么参数，返回什么值. 一般包括: 结果, 中间状态, 返回的判断条件,其他参数.  
__递归的拆解__：每次递归都是为了让问题规模变⼩.如何进入子问题.  
__递归的出⼝__：什么时候返回, 判断条件。  

==============
## Subset ##
   1. 选或不选的,选A或选B的 DFS方法 (只用于组合类搜索)
   ```cpp
       void helper(vector<vector<int>> &result, vector<int> &stack, int index, vector<int>& nums) {
        if (index == nums.size()) {
            result.push_back(stack);
            return;
        }
        
        helper(result, stack, index + 1, nums);
        
        stack.push_back(nums[index]);
        helper(result, stack, index + 1, nums);
        stack.pop_back();

        return;
    }
   ```
   2. 标准DFS的方法。
   ```cpp
       void helper(vector<vector<int>> &result, vector<int> &stack, int index, vector<int>& nums) {
        result.push_back(stack);
        
        // 递归出口 for loop判断结束条件
        for (int i = index; i < nums.size(); ++i) {
            stack.push_back(nums[i]);
            helper(result, stack, i + 1, nums);
            stack.pop_back();
        }
        
        return;
    }
   ```
   3. bit mask的方法：
   ```cpp
       for (int i; i < 1 << n; ++i) {
           vector<int> stack;
           for(int j; j < n; ++j) {
               if (i & 1 << j)
                  // add | 标记
                  stack.push_back(nums[j]);
           }
           result.push_back(stack);
           // get one result
       }
   ```
   4. 如何去重：
       a. 先排序。
       b. 如果当前值和前一个相同， 跳过去。
       
```python
   def dfs(nums, index, subset, result):
       result.append(subset)
       
       for i in range(index, n):
           subset.append(nums[i])
           dfs(nums, i + 1, subset, result)
           subset.pop()
       return
``` 
## Combination ##
1. 和subset 类似的通用解法。 区别 不加 一。
2. DP 解法。
3. 如何去重， 同subset
   
## Permutation ##
* 交换法 - 适用于无重复的全排列， 去重比较麻烦
* 字典序法 - 用于求next permutation。
* 类似于subset的通用解法，需要做visited 标记。
* 全排列去重， 如果前一个相同的数未做标记，就跳过。
* 求第K个排列

### 交换法 ###
   * 使用DFS 递归交换元素。输出结果。
    
### 字典序法 ###
1. 字典序（lexicographical order）可以排列数字或字符串， 字符使用ASCII码比较。boat < boot < cap < card < cat < to < too < two < up 
2. 求下一个字典序，3步:
   * 找最后一个正序。 最后一个 nums[i] < nums[i+1]
   * 找最后一个比nums[i]大的num。
   * 将nums[i+1:] reverse. -> 注意不需要排序， 为什么？（第一步可以保证）
3. 求上一个字典序， 3步：
   * 找最后一个降序。 最后一个 nums[i] > nums[i+1]
   * 找最后一个比nums[i]小的num。
   * 将nums[i+1:] reverse. -> 注意不需要排序， 为什么？（第一步可以保证）
```python
   def nextPermutation(self, nums):
       n = len(nums)
       lo = -1
       for i in range(n-2, -1, -1):
           if nums[i] < nums[i+1]:
               lo = i
               break
       
       if lo == -1:
           nums.reverse()
           return nums
           
       hi = lo + 1 
       for i in range(n-1, lo, -1):
           if nums[i] > nums[lo]:
               hi = i
               break
       nums[lo], nums[hi] = nums[hi], nums[lo]
       nums[lo+1:] = nums[n-1:lo:-1]
       return nums
```
### 全排列去重 ###
1. 交换法， 遇重不交换 abb -> bab -> bba。 bab -> bba. 会产生重复，这样不行。
2. 需要另外一个条件，两个交换的元素之间没有和 第二个被交换的元素重复的元素。 

Backtracking
==============

### 模版 ###
```python
void dfs()//参数用来表示状态
{
    if(到达终点状态)
    {
        ...//根据题意来添加, 略如，输出结果
        return;
    }
    if(越界或者是不符合法状态)
    {
        return;
    }
    
    // case 1 ：一般情况
    for(扩展出子状态)
    {
        if(扩展子状态合法)
        {
            ....//根据题意来添加
            标记；
            if (符合条件) //剪枝
                dfs（）；
            还原标记； 
        }
    }
    
    // case 2: 矩阵搜索
       标记；
         for(扩展子状态)
             dfs（）；
       还原标记； 

}
```
