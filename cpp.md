
## C++ STL
[String](#string) 

[Stack](#stack)

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
```cpp
   stack int s;
   s.push(1)
   s.pop() - Doesn't return any value. top first then pop.
   s.top()
```
### deque:
### sort:
```cpp
// sort algorithm example
#include <iostream>     // std::cout
#include <algorithm>    // std::sort
#include <vector>       // std::vector

bool myfunction (int i,int j) { return (i<j); }

struct myclass {
  bool operator() (int i,int j) { return (i<j);}
} myobject;

int main () {
  int myints[] = {32,71,12,45,26,80,53,33};
  std::vector<int> myvector (myints, myints+8);               // 32 71 12 45 26 80 53 33

  // using default comparison (operator <):
  std::sort (myvector.begin(), myvector.begin()+4);           //(12 32 45 71)26 80 53 33

  // using function as comp
  std::sort (myvector.begin()+4, myvector.end(), myfunction); // 12 32 45 71(26 33 53 80)

  // using object as comp
  std::sort (myvector.begin(), myvector.end(), myobject);     //(12 26 32 33 45 53 71 80)

  // print out content:
  std::cout << "myvector contains:";
  for (std::vector<int>::iterator it=myvector.begin(); it!=myvector.end(); ++it)
    std::cout << ' ' << *it;
  std::cout << '\n';

  return 0;
}
```
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
   isalnum(c), tolower(c)
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
