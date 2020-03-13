 ## Segment Tree ##
 建树 O(n）
 查询及单点更新都是 O(log(n))
 ``` cpp
     Clase TreeNode {
         int start;
         int end;
         int max;
         TreeNode * left;
         TreeNode * right;
         TreeNode(int start, int end) {
             this->start = start;
             this->end = end;
             this->left = NULL;
             this->right = NULL:
             this->max = INT_MIN;
         }
     }
 
    TreeNode * build (int left, int right, vector<int> &A) {
        int mid = 0;
        
        TreeNode * node = new SegmentTreeNode(left, right);
        
        if (left == right) {
            node->max = A[left];
            return node;
        }
        
        mid = left + (right - left) / 2;
        node->left = build(left, mid, A);
        node->right = build(mid + 1, right, A);
        
        node->max = max(node->left->max, node->right->max);
        
        return node;
    }
    
    int query(TreeNode * root, int start, int end) {
        // write your code here
        if (root == NULL) return INT_MIN;
        
        if ((root->end < start) || (root->start > end)) return INT_MIN;
        
        if ((root->start >= start) && (root->end <= end)) return root->max;
        
        return max(query(root->left, start, end), query(root->right, start, end));
    }
    
    void modify(SegmentTreeNode * root, int index, int value) {
        // write your code here
        if (root == NULL) return;
        
        if (root->start == root->end) {
            root->max = value;
            return;
        }
            
        if (root->left->end >= index) {
            modify(root->left, index, value);    
        } else {
            modify(root->right, index, value);    
        }
        
        root->max = root->left->max > root->right->max? root->left->max : root->right->max;
             
        return;
    }
 ```  
 ## Binary Index Tree ## 
__用法__ :  O(log(n)) 的时间内求一段区间内的和.

__主要操作__ ：update 某一点(Olog(n))， 区间求和(Olog(n)), 建树 O(n).

__离散化__ ： discretization. 用于降低区间范围 

```cpp
    int lowbit(int x) {
        return x & (~x + 1);
    }
    
    void create(vector<int> & input, vector<int> & arr) {
        int size = arr.size();
        for (int i = 1; i < size; ++i) {
            arr[i] += input[i - 1];
            if (i + lowbit(i) < size)
                arr[i + lowbit(i)] += input[i - 1];
        }
        return;
    }
    
    void update(int a, int pos, vector<int> arr) {
        while (pos < arr.size()) {
            arr[pos] += a;
            pos += lowbit(pos);
        }
        return;
    }
    
    int getSum(int pos, vector<int> arr) {
        int sum = 0;
        while(pos > 0) {
            sum += arr[pos];
            pos -= lowbit(pos);
        }
        return sum;
    }
```

```python
        def descretization(A):
            hash = {}
            A.sorted()
            count = 1
            for num in A:
                if num not in hash:
                    hash[num] = count
                    count += 1
            return
            
        def add(x, tree):
            while x <= len(tree) - 1:
                tree[x] += 1
                x += x & -x
                
            return
        
        def query(x, tree):
            result = 0
            while x > 0:
                result -= tree[x]
                x = x & -x
            return result
```
