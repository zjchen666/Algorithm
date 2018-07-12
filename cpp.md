
## C++ STL
### auto:
### vector:
```cpp
   vector<int> nums
   iterator nums.begin(), nums.end()
   
   vector<string>

   vector<double>

   size()

   push_back()

   pop()
```
### list:
### stack:
### deque:
### priority_queue:
### unordered_map:
```cpp
   unordered_map<char, int> map;
   if (map.find(key) != map.end())
```
### unordered_set:
```cpp
   unordered_set<char> set;
   if (set.find(key) != set.end())
   set.insert(val)
   set.delete(val)
```
### queue:
### string:
```cpp
   string s, s.push_back(), s.size(), s.pop()
```
   
定义queue对象的示例代码如下：

queue<int> q1;

queue<double> q2;

queue的基本操作有：

入队，如例：q.push(x); 将x接到队列的末端。

出队，如例：q.pop(); 弹出队列的第一个元素，注意，并不会返回被弹出元素的值。

访问队首元素，如例：q.front()，即最早被压入队列的元素。

访问队尾元素，如例：q.back()，即最后被压入队列的元素。

判断队列空，如例：q.empty()，当队列空时，返回true。

访问队列中的元素个数，如例：q.size()
