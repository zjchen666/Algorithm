## Binary Search ##
* 二分查找
* 二分答案

### 查找 target
```cpp
    int binarySearch(vector<int> nums, target) {
        int lo = 0, hi = num.size() - 1;
        
        while (lo + 1 < hi) {
            int mid = lo + (hi - lo) / 2;
            if (nums[mid] < target) {
                lo = mid;
            } else {
                hi = mid;
            }
        }
        
        if (nums[lo] == target) return lo;
        if (nums[hi] == target) return hi;
        return -1;
    }
```
```python
   def binarySearch(self, array, target):
        n = len(array)
        lo, hi = 0, n-1
        
        while lo + 1 < hi:
            mid = lo + (hi - lo)/2
            if array[mid] > target:
                hi = mid
            elif array[mid] < target:
                lo = mid
            else:
                return mid
        if array[lo] == target:
            return lo
        if array[hi] == target:
            return hi
        return -1
```

### 查找 Position
   - 返回index 其中 a[index] >= target or a[index] > target  
   - 适用于DP的二分优化
```python
    def binarySearch(self, array, target):
        n = len(array)
        lo, hi = 0, n-1
        
        while lo <= hi:
            mid = lo + (hi - lo)/2
            if array[mid] > target:
                hi = mid - 1
            elif array[mid] < target:
                lo = mid + 1
            else:
                return mid
        return lo
```

### 二分答案
1. 定义出 answer的范围 min - max
2. 在范围内二分查找，依据满足条件或不满足条件来缩小范围
```cpp
       int binarySearch(vector<int> nums) {
        int lo = 0, hi = num.size() - 1;
        
        while (lo + 1 < hi) {
            int target = lo + (hi - lo) / 2;
            if (isValid(mid, nums) < target) {
                lo = mid;
            } else {
                hi = mid;
            }
        }
        
        if (nums[lo] == target) return lo;
        if (nums[hi] == target) return hi;
        return -1;
    }
    
    bool/int isValid(target) {
        // verify the target.
    }
```
https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/  
https://leetcode.com/problems/split-array-largest-sum

