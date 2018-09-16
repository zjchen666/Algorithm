### 单调栈 Stack ###
单调栈这种数据结构，通常应用在一维数组上。
如果遇到的问题，和前后元素之间的大小关系有关系的话，我们可以试图用单调栈来解决。
入栈的元素一般是index,O(n)线性时间的复杂度。
```templete
    def mono_stack(nums):        
        result = 0
        stack = []
        
        for i, num in enumerate(nums):
            while stack and num < nums[stack[-1]]:
                index = stack.pop()
                distance = i if not stack else i - stack[-1] - 1
                ## Do something and output ##
            stack.append(i)
            
        return result 
```
[Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/description/)  
[Maximal Rectangle](https://leetcode.com/problems/maximal-rectangle/description/)  
[sum-of-subarray-minimums](https://leetcode.com/problems/sum-of-subarray-minimums/description/)  
https://leetcode.com/problems/online-stock-span/description/

### Flatten 问题
解法，
init时把数据入栈，
has next的时候判断是子集和单个元素，
若是子集则弹出子集并将单个元素入栈。
getnext直接返回栈顶元素。

[Flatten 2D Vector](https://leetcode.com/problems/flatten-2d-vector/description/)   
[Flatten Nested List Iterator](https://leetcode.com/problems/flatten-nested-list-iterator/description/)   
[Flatten Binary Tree to Linked List](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/description/)   

