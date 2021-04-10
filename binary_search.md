## Binary Search ##
* 二分查找
    - 一般都要先排序
    - 查找 target. 结果 找到，lo 或 hi， 没找到在 lo hi 之间。
    - 查找position，low bound - 结果在hi, high bound: 结果在lo。
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
### Left Bound and Right Bound 查找
   - Left bound - 查找到target的话 right == mid
   - Right bound - 查找到target left = mid
   
```cpp
    int upper_bound(const vector<int> &a, int target)
    {
        int left = 0, mid = 0;
        int right = a.size() - 1;

        while (left + 1 < right) {
            mid = left + (right - left) / 2;
            if (a[mid] <= target) {
                left = mid;
            } else if (a[mid] > target) {
                right = mid;
            }
        }

        if (a[right] == target)
            return right;
        else if (a[left] == target)
            return left;
        else
            return -1;
    }

    int lower_bound(const vector<int> &a, int target)
    {
        int left = 0, mid = 0;
        int right = a.size() - 1;

        while (left + 1 < right) {
            mid = left + (right - left) / 2;
            if (a[mid] < target) {
                left = mid;
            } else if (a[mid] >= target) {
                right = mid;
            }
        }

        if (a[left] == target)
            return left;
        else if (a[right] == target)
            return right;
        else
            return -1;
    }
```


### 二分答案
特点：  
*这道题让我们「查找一个有范围的整数」，以后遇到类似问题，要想到可以尝试使用「二分」；  
*题目描述类似使「最大值」最小化 或者【最小值】最大化；  
*题目中出现的关键字「非负整数」、分割【连续] 成几天，或几段的最小值.  
*在代码层面上，这些问题的特点都是：在二分查找的判别函数里，需要遍历数组一次。    

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
https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/  - 分为几艘船最小capacity 
https://leetcode.com/problems/split-array-largest-sum        
「力扣」第 1482 题：制作 m 束花所需的最少天数（中等）. 分为m段最小天数    
https://leetcode.com/problems/magnetic-force-between-two-balls/。  
https://leetcode.com/problems/koko-eating-bananas/  

 
