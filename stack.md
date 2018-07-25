### Mono-Stack ###
单调栈这种数据结构，通常应用在一维数组上。
如果遇到的问题，和前后元素之间的大小关系有关系的话，我们可以试图用单调栈来解决。
入栈的元素一般是index,O(n)线性时间的复杂度。


### Flatten 问题
解法，
init时把数据入栈，
has next的时候判断是子集和单个元素，
若是子集则弹出子集并将单个元素入栈。
getnext直接返回栈顶元素。

[Flatten 2D Vector](https://leetcode.com/problems/flatten-2d-vector/description/)   
[Flatten Nested List Iterator](https://leetcode.com/problems/flatten-nested-list-iterator/description/)   
[Flatten Binary Tree to Linked List](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/description/)   

