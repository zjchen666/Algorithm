## Sort Algrithom ##
   * Quick Sort
      * [QuickSelect](#quick-select)
      * [3 Way QuickSort](#3-way-quickSort)
   * [Merge Sort](#merge-sort)
   * [Counting Sort](#counting-sort)
   * Select Sort
   * [Heap Sort](#heap-sort)
   * Bucket Sort
   * Insert Sort
   * Bubble Sort
   * [Quick Select](#quick-select)

### 各种排序性能及稳定性比较 ###
| Algrithm    | Stability  |   Time Complexity   | Extra Space |
| ------------- | ---------- | -----------------   | ------------|
| Counting Sort | Yes | O(n) | K + N |
| Quick Sort    | No | O(nlogn) | 0 |
| Merge Sort    | Yes | O(nlogn) | N |
| Insertion Sort    | Yes | O(n^2) | 0 |
| heap Sort    | No | O(nlogn) | N | 

### 主要问题 ###
   * find peak


=================
### Counting Sort ###
```python
    def counting_sort(self, nums, k):
        
        count = [0 for i in range(k+1)]
        results = [0 for i in range(len(nums))]
        
        for num in nums:
            count[num] += 1

        for i in range(1, k+1):
            count[i] += count[i-1]

        for i in range(len(nums)-1, -1, -1):
            results[count[nums[i]]-1] = nums[i]
            count[nums[i]] -= 1

        return results
```
### QuickSort ###

```python
class Solution:
    # @param {int[]} A an integer array
    # @return nothing
    def sortIntegers2(self, A):
        # Write your code here
        self.quickSort(A, 0, len(A) - 1)
    
    def quickSort(self, A, start, end):
        if start >= end:
            return
        
        left, right = start, end
        # key point 1: pivot is the value, not the index, as A[pivot] value will be CHANGED!!!
        pivot = A[(start + end) / 2]

        # key point 2: every time you compare left & right, it should be 
        # left <= right not left < right
        while left <= right:
            while A[left] < pivot:
                left += 1
            
            while A[right] > pivot:
                right -= 1
            
            if left <= right:
                A[left], A[right] = A[right], A[left]
                
                left += 1
                right -= 1
        
        self.quickSort(A, start, right)
        self.quickSort(A, left, end)
```
### 3 Way QuickSort ###
   * 3 way partition
```pythion
    def partition(self, lo, hi, nums):
	i = lo
	pivot = lo + (hi - lo)/2
	
	while i < hi:
	    if nums[i] < pivot:
	    	nums[i], nums[lo] = nums[lo], nums[i]
		i += 1
		lo += 1
	    elif nums[i] > pivot:
	        nums[i], nums[hi] = nums[hi], nums[lo]
		hi -= 1
	    else:
	        i += 1
```

### Quick Select ###
   + 用途： 数组中求第K大从后向前数，第K小的数（从前向后）。
   
```python
class Solution:
    """
    @param: k: An integer
    @param: nums: An integer array
    @return: kth smallest element
    """
    def quickSelect(self, start, end, k, nums):
        if start == end:
            print nums
            return nums[start]

        lo = start
        hi = end
        pivot = nums[lo + (hi-lo)/2]
        
        while lo <= hi:
            while lo <= hi and nums[hi] > pivot:
                hi -= 1
            while lo <= hi and nums[lo] < pivot:
                lo += 1
            if lo <= hi:
            	nums[lo], nums[hi] = nums[hi], nums[lo]
            	lo += 1
            	hi -= 1
        
        if k <= hi:
            return self.quickSelect(start, hi, k, nums)
        elif k >= lo:
            return self.quickSelect(lo, end, k, nums)
        else:
            return nums[k]
```

### MergeSort ###
- 可用于解决，数组的一类需要排序后 O(N)的recurence问题：  
   https://leetcode.com/problems/reverse-pairs/description/  
   https://leetcode.com/problems/count-of-smaller-numbers-after-self/description/  
   https://leetcode.com/problems/count-of-range-sum/description/
   
```python
            def mergeSort(self, A, start, end, aux):
		if start == end:
			return
		mid = start + (end - start)/2
		self.mergeSort(A, start, mid, aux)
		self.mergeSort(A, mid+1, end, aux)
		i = start
		j = mid + 1
		k = start
		while i <= mid and j <= end:
			if A[i] <= A[j]:
				aux[k] = A[i]
				i += 1
			else:
				aux[k] = A[j]
				j += 1
			k += 1
		while i <= mid:
			aux[k] = A[i]
			k += 1
			i += 1
		while j <= end:
			aux[k] = A[j]
			k += 1
			j += 1
		k = start
		while k <= end:
			A[k] = aux[k]
			k += 1
		return
```
### Heap Sort ###
```cpp
    void heapify(vector<int>& A, int i, int heap_size) {
        int l = i * 2;
        int r = i * 2 + 1;
        int largest = i;
        
        if (l <= heap_size && A[l - 1] > A[i - 1]) {
            largest = l;
        }
        
        if (r <= heap_size && A[r - 1] > A[largest - 1]) {
            largest = r;
        }
        
        if (i != largest) {
            swap(A[i - 1], A[largest - 1]);
            heapify(A, largest, heap_size);
        }
        
        return;
    }
    
    void buildHeap(vector<int>& A) {
        int size = A.size();
        
        for (int i = size / 2; i >= 1; --i) {
            heapify(A, i, size);
        }
        
        return;
    }
    
    void heapSort(vector<int>& A) {
        // 1. build heap
        buildHeap(A);
        
        // 2. exchange max val with last element in array
        for (int i = A.size() - 1; i > 0; --i) {
            swap(A[0], A[i]);
            heapify(A, 1, i);
        }
        
        return;
    }
```
