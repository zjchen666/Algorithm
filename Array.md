Array
======================
## 数组的时间复杂度 ##
* 一个数组的subarray共有(n+1)*n/2。O(n^2)  1 + 2 + .... + n = (n + 1) * n / 2;
* 一个数组的sequence有2^n。O(2^n)
* 一个数组的permutation有n!个 O(n!)

## 问题分类 ##
* [Array rotation](#array-rotation)
* [Two Pointers 问题](#two-pointers)
* [Subarray 问题](#subarray)
* [Subsequence 问题](#subsequence)
* [Interval 问题](#interval)
* [Select and Sort](/quicksort_mergesort.md)
* [swich sort 问题](#switch-sort)
* [One/Two Pass 问题](#one-two-pass)
* [2D 数组问题](#2d-array)

## switch sort ##
   适用于 0 < nums[i] <= n, n 为array的size一类问题。 solution: switch and re-order  
   https://leetcode.com/problems/find-all-duplicates-in-an-array/description/  
   https://leetcode.com/problems/first-missing-positive/description/
```cpp
     vector<int> findDuplicates(vector<int>& nums) {
        vector<int> res;
        
        for (int i = 0; i < nums.size(); i++)
        {
            while ((nums[i] != i + 1) && (nums[i] != nums[nums[i] - 1]))
            {
                int tmp = nums[i] - 1;
                swap(nums[i], nums[tmp]);
            }
        }
        
        for (int i = 0; i < nums.size(); i++)
        {
            if (nums[i] != i + 1)
            {
                res.push_back(nums[i]);
            }
        }
        return res;
    }
```
## one two pass ##
```cpp
   left -> right calculate status.
   right -> left calculate status.
```  
53 Maximum Subarray  
121 Best Time to Buy and Sell Stock  
152 Maximum Product Subarray  
238 Product of Array Except Self  
739 Daily Temperatures  
769 Max Chunks to Make Sorted  
770 Max Chunks to Make Sorted II  
821 Shortest Distance to a Character  
845 Longest Mountain in Array  
926 Flip String to Monotone Increasing


## Array rotation ##
### 解法 ###
   * 三步反转法
```python
        #left
        lo = 0
        hi = k
        while lo < hi:
            nums[lo], nums[hi] = nums[hi], nums[lo]
            lo += 1
            hi -= 1

        #right
        lo = k + 1
        hi = n - 1
        while lo < hi:
            nums[lo], nums[hi] = nums[hi], nums[lo]
            lo += 1
            hi -= 1

        #the whole array
        lo = 0
        hi = n - 1
        while lo < hi:
            nums[lo], nums[hi] = nums[hi], nums[lo]
            lo += 1
            hi -= 1
```
## Two pointers ##
 ### 模板 ###
 ```python
     # partition
     def two_pointers(self, array, target):         lo = 0
         hi = len(array) - 1
         while lo < hi:
             while lo < hi and array[lo] > target:
                 lo += 1
             while lo < hi and array[hi] <= target:
                 hi -= 1
             if lo < hi:
                 array[lo], array[hi] = array[hi], array[lo]:
         return
 ```       
 ### 主要题型 ###
 * partition array - move 比k小的到左边，大的到右边. pivot 一定要用value 而不是nums[index], 因为 nums[pivot]可能在partition的过程中被修改。
 * two element运算， 求和，差，积，etc。 先sort，然后往中间移动。
 * 求最大面积的问题， 相对往中间移动，不断换值比较大/小的元素。
 * remove duplicate。同向双指针，慢的存留下的元素最后位置的index， 快的往前找不重复的元素。
 * intersection of two arrays. 先sort然后同向移动，找出相同的值。
 * subarray问题，一般都是要先求presum。
 * window 问题， 前向指针。
 
 ### 解法 ###
 * 相向型指针 - Two elements, Container With Most Water, partition array, subarray. 
 * 前向型指针 - remove duplicate, intersection of arrays, presum, window。  
  - __快慢指针__ 
  __remove duplicate__:    
  283. Move Zeroes  
  https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/description/  
  https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/
```cpp
    int removeDuplicates(vector<int>& nums) {
        if (nums.size() <= 1)
            return nums.size();
        
        int i = 0, j = 1;
        int k = 2;
        int count = 1;
        
        while (j < nums.size())
        {
            if (nums[i] != nums[j])
            {
                nums[++i] = nums[j];
                count = 1;
            }
            else
            {
                if (count < k)
                {
                    nums[++i] = nums[j];;
                    count++;
                }
            }
            j++;
        }   
        return i + 1;
    }
```
   - __窗口问题__  __window 从头到尾__ ：
- 主要是用来优化两层for循环。 
- 外层仍然需要从头到尾遍历。  
- 内层不需要回退！
- 题目：
[Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/description/)   
[max-consecutive-ones-ii](https://leetcode.com/problems/max-consecutive-ones-ii/description/)

```python
    # window 类 forward pointers 优化 O(N^2) 到 O(N):
     j = 0
     for i in range(n):
         while j < n:
             if (condition):
                 j += 1
                 udpate j 
             else:
                 break
         update i
```

## Subarray ##
### 主要算法 ###
- **brtual force**
    从第一个元素开始遍历直到结尾，依次缩短array长度寻找结果。时间复杂度O(n*m),不需要额外空间。
- **presum**
    - 令 PrefixSum[i] = nums[0] + nums[1] + ... nums[i], PrefixSum[0] = nums[0] 易知构造 PrefixSum 耗费 O(n) 时间和 O(n) 空间 如需计算子  数组从下标i到下标j之间的所有数之和 则有 Sum(i~j) = PrefixSum[j] - PrefixSum[i-1]。
    - 需要排序的话，使用hashtable作为数据结构存储index和presum的mapping。注意subarray的起始点是hash[sum]+1 而不是hash[sum]
```python
    pre_sum = [0 for i in range(n)]
    pre_sum[0] = nums[0]
    
    for i in xrange(1, n):
        pre_sum[i] = pre_sum[i-1] + nums[i]
   
    #maximum subarray sum
    min_pre = 0
    max_sum = nums[0]
    for i in xrange(1, n):
        min_pre = min(min_pre, pre_sum[i-1])
        max_sum = max(max_sum, pre_sum[i]-min_pre)
        
    #minimum subarray sum
    max_pre = 0
    min_sum = nums[0]
    for i in xrange(1, n):
        max_pre = max(max_pre, pre_sum[i-1])
        min_sum = max(min_sum, pre_sum[i]-max_pre)
```
- **product**
   subarray 乘法技巧， 用两个数组分别记录最大值和最小值。遇到负值就切到最小值数组，再遇到就再切回max数组。遇到零下一个元素重置。
```python
    def maxProduct(self, nums):
        n = len(nums)
        
        max_val = [0 for i in range(n)]
        min_val = [0 for i in range(n)]
        max_val[0] = nums[0]
        min_val[0] = nums[0]
        
        for i in range(1, n):
            max_val[i] = nums[i]
            min_val[i] = nums[i]
            if nums[i] >= 0:
                max_val[i] = max(max_val[i], max_val[i-1]*nums[i])
                min_val[i] = min(min_val[i], min_val[i-1]*nums[i])
            if nums[i] < 0:
                max_val[i] = max(max_val[i], min_val[i-1]*nums[i])
                min_val[i] = min(min_val[i], max_val[i-1]*nums[i])
        return max(max_val)
```
   
- **backward and forward travesal**
    适用于需要依次计算某一数组元素左右两边（和/积）的情况。第一遍计算从1～n-1， 第二遍计算从n-2～0， 之后合并结果。
```python
        array = [0 for i in range(n)]
        # calculation from n-2 ~ 0
        for i in xrange(n-2, -1, -1): 
            array[i] = xxx
            
        # calculation from 1 ~ n-1
        for i in xrange(1, n):
            # combine the calculation results
            array[i] = xxx
```



Given an integer array, find a subarray where the sum of numbers is zero. Your code should return the index of the first number and the index of the last number.
 Notice：
There is at least one subarray that it's sum equals to zero.
Example
Given [-3, 1, 2, -3, 4], return [0, 2] or [1, 3].
 
```python
import copy
class Solution:
    """
    @param: nums: A list of integers
    @return: A list of integers includes the index of the first number and the index of the last number
    """
    def subarraySum(self, nums):
        # write your code here
        if not nums:
            return []
        hash = {}
        sum = 0
        result = []
        for i in range(0, len(nums)):
            sum += nums[i]
            if sum == 0:
                return [0,i]
            if sum in hash:
                hash[sum] = i
            else:
                result = [hash[sum]+1, i]
                break
        return result
```
### Maximum Subarray ###
   + 使用以下模版, 注意min_prefix = 0而不是nums[0]，因为全为正数的话，最大sum是与0之差。
   
```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int min_sum = 0, sum = 0, result = INT_MIN;
        
        for (auto num: nums) {
            sum += num;
            result = max(sum - min_sum, result);
            min_sum = min(sum, min_sum);
        }
        return result;
    }
};
```

### Subarray Sum Closet ###
+ 依然是presum，之后需要排序，找出相邻节点最小差值。
```python
import sys
class Solution:
    """
    @param: nums: A list of integers
    @return: A list of integers includes the index of the first number and the index of the last number
    """
    def subarraySumClosest(self, nums):
        if not nums:
            return []
        if len(nums) == 1:
            return [0,0]
        # write your code here
        minVal = sys.maxsize
        prefixSum = list()
        hash = {}
        resuls = []
        sum = 0
        for i in range(len(nums)):
            sum += nums[i]
            prefixSum.append(sum)
            if sum in hash:

return [hash[sum]+1, i]
            else:
                hash[sum] = i
        prefixSum.sort()
        for i in range(len(nums)-1):
            if abs(prefixSum[i+1] - prefixSum[i]) < minVal:
                minVal = abs(prefixSum[i+1] - prefixSum[i])
                if hash[prefixSum[i+1]] > hash[prefixSum[i]]:
                    result = [hash[prefixSum[i]]+1, hash[prefixSum[i+1]]]
                else:
                    result = [hash[prefixSum[i+1]]+1, hash[prefixSum[i]]]
        return result
```
## Maximun Subarray IV ##
### 解法 ###
   1. presum 之后 brutal force 循环会超时。
   2. presum 之后 one pass，只需要记住i - k之前的最小sum即可。

Given an integer arrays, find a contiguous subarray which has the largest sum and length should be greater or equal to given length k.
Return the largest sum, return 0 if there are fewer than k elements in the array.
Notice
Ensure that the result is an integer type.
Example
Given the array [-2,2,-3,4,-1,2,1,-5,3] and k = 5, the contiguous subarray [2,-3,4,-1,2,1] has the largest sum = 5.

```python
class Solution:
    """
    @param: nums: an array of integer
    @param: k: an integer
    @return: the largest sum
    """
    def maxSubarray3(self, nums, k):
        # write your code here
        if not nums or k > len(nums):
            return 0
        
        for i in range(1,len(nums)):
            nums[i] = nums[i] + nums[i-1]
            
        largest_sum = nums[k-1]
        # O(N*N) TLE
        for j in range(k, len(nums)+1):
            if nums[j-1] > largest_sum:
                largest_sum = nums[j-1]
            for i in range(j, len(nums)):
                if nums[i] - nums[i-j] > largest_sum:
                    largest_sum = nums[i] - nums[i-j]
        return largest_sum
    
    def maxSubarray4(self, nums, k):
        # write your code here
        if not nums or k > len(nums):
            return 0
            
        result = 0
        for i in range(0, k):
            result += nums[i]
            
        min_prefix = 0
        sum = [0 for i in range(len(nums))]
        sum[0] = nums[0]

        for i in range(1, len(nums)):
            sum[i] = sum[i-1] + nums[i]
            if i >= k:
                min_prefix = min(min_prefix, sum[i-k])
                result = max(sum[i] - min_prefix, result)

        return result
```
   
## Interval ##
   解题方法
   1. 把所有线段排序。
   2. 扫描所有线段输出结果。
```cpp
模板
    bool compare(vector<int> &a, vector<int> &b) {
        /* 依据需要实现 end节点 */
        if (a[0] == b[0]) {
            return a[1] > b[1];
        } else {
            return a[0] < b[0];
        }
    }

    int intervals(vector<vector<int>>& intervals) {
        int res = intervals.size();
        if (res == 0)
            return 0;
            
        /* 排序 */
        sort(intervals.begin(), intervals.end(), compare/*function*/);
            
        int end = intervals[0][1];
        
        for (int i = 1; i < intervals.size(); ++i) {
            /* 扫描节点 并做对应处理 */
        }
        
 这是一个通用的算法，就是遇到任何interval，将interval的start当成key存入，value+1，遇到end，存入。但是要-1； 用一个TreeMap存储，保证key的值是sort的。 时间复杂度是O(N) 该方法可以用于如何calendar以及meeting room的题解。

public int minMeetingRooms(List<Interval> intervals) {
        TreeMap<Integer, Integer> tmap = new TreeMap<>();
        int ans = 0, cnt = 0;
        for (Interval i : intervals) {
            int start = i.start, end = i.end;
            tmap.put(start, tmap.getOrDefault(start, 0) + 1);
            tmap.put(end, tmap.getOrDefault(end, 0) - 1);
        }
        for (int k : tmap.keySet()) {
            cnt += tmap.get(k);
            ans = Math.max(ans, cnt);
        }
        return ans;
}
```
## 2d array ##
   1. roate 问题
    一般做对角线，行列的reverse。
    注意reverse的时候只需要处理一半
```
        int m = matrix.size();
        int n = matrix[0].size();
        
        for (int i = 0; i < m; ++i) {
            for (int j = i; j < n; ++j) {
                swap(matrix[i][j], matrix[j][i]);
            }
        }

        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n / 2; ++j) {
                swap(matrix[i][j], matrix[i][n - j - 1]);
            }
        }
```
