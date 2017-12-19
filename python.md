- if i not in dict() 要比 if i in dict() 耗时。前者O（n）后者O（1）。
   用 if None == dict.get() 最快
- hash table 取value的操作：hash.get(key)
- 二维数组预定义：
```python
matrix = [[0 for i in range(3)] for i in range(3)]
```
以下是错误的因为这个二维数组的每一个obj都是一样的
```python
>>> a = [[1]] * 5
>>> a
[[1], [1], [1], [1], [1]]
>>> a = [1] * 5
>>> a
[1, 1, 1, 1, 1]
```
- 二维list数组扩大 
```python
   array = []
   array.append([])
   array[0].append(x)
```
- 所有括号外的运算符都要空格
```python
   list[i] % list[j]
```
- 赋值， shallow copy 和 deep copy。
```python
  a = [1,2,3]
  b = a #改变a， b的值会跟着变，因为它们指向同一个对象
  b = copy.copy(a)  #改变a， b不变， copy会生成一个新的对象
  b = deepcopy.copy(a) #改变a， b不变， copy会生成一个新的对象
  
  The difference between shallow and deep copying is only relevant for compound objects
  a = [[1,2,3], [1,2,3]]
  b = copy.copy(a) #改变a[i]， b跟着变， copy会生成一个新的对象，inner object和a是一样的
  b = copy.deepcopy(a) #改变a[i]， b不变， deepcopy 会复制所有的的对象
```
- Set
```python
  set(str) 是取string 不重复的字符。
  set([str]) 是将一个字符串加到set里
  set(a)
  set(['a', 'c', 'b'])
```
