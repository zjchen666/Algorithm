 ## Binary Index Tree ## 
__用法__ :  O(log(n)) 的时间内求一段区间内的和.

__主要操作__ ：update 某一点(Olog(n))， 区间求和(Olog(n)), 建树 O(n).

__离散化__ ： discretization. 用于降低区间范围 

```cpp
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
