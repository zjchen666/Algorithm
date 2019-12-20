## Binary Search ##
* 二分查找
    - 一般都要先排序
    - 查找 target
    - 查找position，low bound/high bound
* 二分答案：二分后，判断是否是要的答案
    - 一般不需要排序？
    - 如何找到判断条件？ find peak 比较左右判断上升还是下降。

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
    int binarySearch(vector<int>& nums, int m) {
        long lo = 0, hi = 0;
        
        for (int num : nums) {
            lo = lo > num ? lo : num;
            hi += num;
        }
        
        if (m == 1) return hi;
        
        while (lo + 1 < hi) {
            int mid = lo + (hi - lo) / 2;
            
            if (isValid(mid, m, nums)) {
                hi = mid;
            } else {
                lo = mid;
            }
        }
        
        if (isValid(lo, m , nums)) return lo;
        
        return hi;
    }
    
    bool isValid(int target, int m, vector<int> & nums) {
        int count = 1;
        long sum = 0;
        
        //validate the candidate
                
        return true;
    }
```
https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/  
https://leetcode.com/problems/split-array-largest-sum

