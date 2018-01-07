### Two point ###
 ## 相对 move ##
    * Two sum
    * Container With Most Water
 ## 同向move ##
    Minimum Size Subarray Sum
    
Given an array of integers, find how many pairs in the array such that their sum is less than or equal to a specific target number. Please return the number of pairs.
Given nums = [2, 7, 11, 15], target = 24. 
Return 5. 
2 + 7 < 24
2 + 11 < 24
2 + 15 < 24
7 + 11 < 24
7 + 15 < 25

### 关键点 ###
  + 解法一， hash table O(n)
  + 解法二，双指针 数组必须先排序。O(nlogn)
 
```python
class Solution:
    """
    @param: nums: an array of integer
    @param: target: an integer
    @return: an integer
    """
    def twoSum5(self, nums, target):
        # write your code here
        if not nums or len(nums) < 2:
            return 0
        nums.sort()
        start = 0
        end = len(nums) - 1
        count = 0
        while start < end:
            if nums[start] + nums[end] > target:
                end -= 1
            else:
                count += end - start
                start += 1
                end -= 1
        return count
```
