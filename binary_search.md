## Binary Search ##
* single array
* multi array


### 查找 target
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

### 切分数组
Divide some goods into groups and put them into different bags.
find the minimum size of bag
https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/
