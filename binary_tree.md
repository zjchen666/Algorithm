
## 主要知识点 ##
1. 二叉树的概念:
      * 二叉搜素树 binary search tree: 所有left node都小于root，与heap区别？
      * 完全二叉树 complete binary tree：heap的数据结构
      * 满二叉树 full binary tree：
      * 平衡二叉树 balanced binary tree：
2. 解题思路:
      * Traverse，自顶向下。
      * Divid Conquer. 自下而上。90%的二叉树问题都可以用 Divide Conquer。
3. 理解 DFS, traverse and divide-conquer。 traverse and divide-conquer 都属于 DFS。
      traverse 传参数， divide-conquer 返回值。
      
## 主要考点：
* [二叉树的递归与非递归遍历](#遍历)
```cpp
    TreeNode& traverse(TreeNode &root) {
        if (root == NULL)
            return NULL;
      
        /* pre-order do something */
        traverse(root->left);
        /* in-order do something */
        traverse(root->right);
        /* postorder do something */
        
        return result;
    } 
```
* Convert preorder/inorder/postorder into binary tree. -> Traverse. 注意如何找root，如何slice左右子树。
* 两个Tree 比较问题 - 考虑每个树的subtree该如何比较， divide conquer
* Sub Tree 问题
* Path 问题
  Solution: DFS left and right, 根据返回值计算结果。
  典型题目：  
  https://leetcode.com/problems/binary-tree-longest-consecutive-sequence/description/   
  https://leetcode.com/problems/binary-tree-longest-consecutive-sequence-ii/
* 动态规划相关
* 数据结构
* [Tree 的 serialize 和 deserialize](#serialize/deserialize)
  要注意负值 “-1” size是2，每个节点要使用 “，”隔开， deserialize的时候先转换成数组。
  
## serialize/deserialize ##
```python
       def serialize(self, root):
        """Encodes a tree to a single string.
        
        :type root: TreeNode
        :rtype: str
        """
        if not root:
            return None
        
        queue = [root]
        result = []
        
        while queue:
            node = queue.pop()
            if node:
                result.append(str(node.val))
                queue.insert(0, node.left)
                queue.insert(0, node.right)
            else:
                result.append("#")
        while result[-1] == "#":
            result.pop()
        
        return ",".join(result)
        

    def deserialize(self, data):
        """Decodes your encoded data to tree.
        :type data: str
        :rtype: TreeNode
        """
        if not data:
            return None
        
        array = data.split(",")
        root = TreeNode(array[0])
        queue = [root]
        index = 0
        left = True
        
        for val in array[1:]:
            if val != "#":
                if left:
                    #print val
                    queue[index].left = TreeNode(int(val))
                    queue.append(queue[index].left)
                else:
                    queue[index].right = TreeNode(int(val))
                    queue.append(queue[index].right)
                    
            if not left:
                index += 1
            left = not left

        return root
```
## 遍历 ##
## non-recursion templete ##
```python
    def traverse(root):
        stack = []
        result = []
        node = root
        while node:
            stack.append(node)
            # result.append() preorder
            node = node.left
            
        while stack:
            node = stack.pop()
            # result.append() inorder
            if node.right:
                node = node.right
                while node:
                    stack.append(node)
                    # result.append preorder
                    node = node.left
                    
        return result
```

## Pre-order Recursion and Non-recursion
```python
    def preorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        stack = []
        node = root
        result = []
        
        while stack or node:
            if node:
                result.append(node.val) -- output
                stack.append(node)
                node = node.left
            else:
                node = stack.pop()
                node = node.right
        return result
```

```python 
    def preorderRecur(self, root):
        if not root:
            return []
        self.preorder = []
        self.traverse(root)
        return self.preorder

    def traverse(self, root):
        if root == None:
            return
        self.preorder.append(root.val)
        self.traverse(root.left)
        self.traverse(root.right)
```

## In-order Recursion and Non-Recursion ##
```python
    def inorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        if not root:
            return []
        
        stack = []
        result = []
        node = root
        
        while stack or node:
            if node:
                stack.append(node)
                node = node.left
            else:
                node = stack.pop()     
                result.append(node.val) -- output
                node = node.right
        return result
```
```python
    def inorderRecur(self, root):
        if not root:
            return []
        self.inorder = []
        self.traverse(root)
        return self.inorder

    def traverse(self, root):
        if root == None:
            return
        self.traverse(root.left)
        self.inorder.append(root.val)
        self.traverse(root.right)
```

## Post-Order Recursion and non-recursion ##
```python
    def postorderRecur(self, root):
        # write your code here
        self.postorder = []
        if not root:
            return []
        self.traverse(root)
        return self.postorder
    
    def traverse(self, root):
        if root == None:
            return
        self.traverse(root.left)
        self.traverse(root.right)
        self.postorder.append(root.val)
        
    def post_order(root):
        stack = []
        result = []
        node = root
        while node:
            stack.append(node)
            node = node.left
            
        while stack:
            if stack[-1].right and node != stack[-1].right:
                node = stack[-1].right
                while node:
                    stack.append(node)
                    node = node.left
            else:
                node = stack.pop()
                results.append(node.val)
                    
        return result
            
```
