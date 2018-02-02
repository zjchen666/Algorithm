
## 字符串
### 基础 知识点 ###
 * ASCII 码
ASCII 码一共规定了128个字符的编码， 前32个不能打印出来，只占用了一个字节的后面7位，最前面的一位统一规定为0。
0 - 48
A - 65
a - 97
 * 转换函数
chr(i)
Return a string of one character whose ASCII code is the integer i. For example, chr(97) returns the string 'a'. This is the inverse of ord(). The argument must be in the range [0..255], inclusive; ValueError will be raised if i is outside that range. See also unichr().

ord() inverse of chr().
int()

### 主要解题思路 ###
* 排序
* 子字符串查找
* 模拟算法
* two pointers
* hash table(可以用size 为 128 byte的数组替换)
