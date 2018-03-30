
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
* Convert preorder/inorder/postorder into binary tree. -> Traverse. 注意如何找root，如何slice左右子树。
* 两个Tree 比较问题 - divide conquer
* Sub Tree 问题
* Path Sum 问题
* 动态规划相关
* 数据结构
    
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
    def preorderNonRecur(self, root):
        # write your code here
        stack = [root]
        preorder = []

        if root is None:
            return preorder

        while stack:
            node = stack.pop()
            preorder.append(node.val)
            if node.right is not None:
                stack.append(node.right)
            if node.left is not None:
                stack.append(node.left)

        return preorder
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
            while node:
                stack.append(node)
                node = node.left
            node = stack.pop()     
            result.append(node.val)
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
