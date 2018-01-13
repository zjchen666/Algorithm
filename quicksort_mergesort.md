## Sorted Array ##
   * Quick Sort
   * Merge Sort
   * Select Sort
   * Insert Sort
   * Bubble Sort
   * Quick Select
   
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
## Quick Select ###
   + 用途： 数组中求第K大，第K小的数。
```python
class Solution:
    """
    @param: k: An integer
    @param: nums: An integer array
    @return: kth smallest element
    """
    def kthSmallest(self, k, nums):
        # write your code here
        start = 0
        end = len(nums) - 1
        self.result = 0
        self.quickSelect(k, nums, start, end)
        return self.result
        
    def quickSelect(self, k, nums, start, end):
        # write your code here
        if start == end:
            self.result = nums[start]
            return
            
        i = start
        j = end
        pivot = nums[i + (j - i)/2]
        
        while i <= j:
            while i <= j and nums[j] > pivot:
                j -= 1
            while i <= j and nums[i] < pivot:
                i += 1
            if i <= j:
                nums[i], nums[j] = nums[j], nums[i]
                i += 1
                j -= 1
        if k - 1 <= j: 
            self.quickSelect(k, nums, start, j)
            
        if k - 1 >= i:
            self.quickSelect(k, nums, i, end)
        # case 1: [j][k][i]
        # case 2: [j][i] 
        if k - 1 < i and k - 1 > j:
            self.result = nums[k-1]
            return
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
