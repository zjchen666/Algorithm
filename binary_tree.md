
## 主要知识点 ##
   + Traverse，自顶向下。
   + Divid Conquer. 自下而上。90%的二叉树问题都可以用 Divide Conquer。
   + 理解 DFS, traverse and divide-conquer。 traverse and divide-conquer 都属于 DFS。
     traverse 传参数， divide-conquer 返回值。
   + 二叉树的递归与非递归遍历。
   + 平衡二叉树
    
## 遍历 ##
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

## Post-Order Recursion ##
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
```

