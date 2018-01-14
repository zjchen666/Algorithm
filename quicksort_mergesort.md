## Sort Algrithom ##
   * Quick Sort
   * Merge Sort
   * Select Sort
   * Heap Sort
   * Bucket Sort
   * Insert Sort
   * Bubble Sort
   * [Quick Select](#quick-select)

### 各种排序性能及稳定性比较 ###

### 主要问题 ###
   * find peak


=================

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
            while left <= right and A[left] < pivot:
                left += 1
            
            while left <= right and A[right] > pivot:
                right -= 1
            
            if left <= right:
                A[left], A[right] = A[right], A[left]
                
                left += 1
                right -= 1
        
        self.quickSort(A, start, right)
        self.quickSort(A, left, end)
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
## MergeSort ##
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
