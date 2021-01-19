## Two pointers ##
 ### 主要题型 ###
 * array partition - move 比k小的到左边，大的到右边
 * two sum求和， 先sort，然后往中间移动。
 * remove duplicate。同向双指针，慢的存留下的元素最后位置的index， 快的往前找不重复的元素。
 * 求最大面积的问题， 相对往中间移动，不断换值比较大/小的元素。
 * intersection of two arrays. 先sort然后同向移动，找出相同的值。
 * subarray问题，一般都是要先求presum。
 ### 相对双指针
 一般需要sort
    * Two sum 
    * Container With Most Water
 ### 同向双指针 ###
 * sliding window  
 * pointer 1 for string 1 and point 2 for string 2.  
    ```cpp
    int j = 0;
    for (int i = 0; i < n; i++) {
        // 不满⾜则循环到满⾜搭配为⽌
        while (j < n && i 到 j之间不满⾜条件) {
        j += 1;
    }
    
    if (i 到 j之间满⾜条件) {
        /* 处理i，j这次搭配 */
    }
    ```
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
