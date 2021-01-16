### 单调栈 Stack ###
单调栈这种数据结构，通常应用在一维数组上。
如果遇到的问题，和前后元素之间的大小关系有关系的话，我们可以试图用单调栈来解决。
入栈的元素一般是index,O(n)线性时间的复杂度。

模板
```python
    def monostoneStack(self, arr)
        stack = []
        ans = 定义一个长度和 arr 一样长的数组，并初始化为 -1
        循环 i in  arr:
            while stack and arr[i] > arr[栈顶元素]:
                peek = 弹出栈顶元素
                ans[peek] = i - peek
            stack.append(i) （注意压栈的是index）
        return ans
```

[Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/description/)  
[Maximal Rectangle](https://leetcode.com/problems/maximal-rectangle/description/)  
[sum-of-subarray-minimums](https://leetcode.com/problems/sum-of-subarray-minimums/description/)  
https://leetcode.com/problems/online-stock-span/description/

### 单调队列 ###

### Flatten 问题
解法，
init时把数据入栈，
has next的时候判断是子集和单个元素，
若是子集则弹出子集并将单个元素入栈。
getnext直接返回栈顶元素。

[Flatten 2D Vector](https://leetcode.com/problems/flatten-2d-vector/description/)   
[Flatten Nested List Iterator](https://leetcode.com/problems/flatten-nested-list-iterator/description/)   
[Flatten Binary Tree to Linked List](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/description/)   

