##
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

* ord() inverse of chr().
* int()
* sorted(s) is a LIST!

### 主要解题思路 ###
* 排序
* 子字符串查找
* 模拟算法
* two pointers
* hash table(可以用size 为 128 byte的数组替换)
* DP

## LongestSubstring with k Distinct:
* 解法 sliding window + hash

```python
    def lengthOfLongestSubstringKDistinct(self, s):
        """
        :type s: str
        :rtype: int
        """
        n = len(s)
        result = 0
        hash = {}

        j = 0
        for i in xrange(n):
            while j < n:
                if s[j] in hash or len(hash) <= 1:
                    hash[s[j]] = hash.get(s[j], 0) + 1
                    j += 1
                    result = max(result, j-i)
                    continue
                else:
                    break
            
            hash[s[i]] = hash[s[i]] - 1
            if hash[s[i]] == 0:
                del hash[s[i]]
                
        return result
```
https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/description/
https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/description/
https://leetcode.com/problems/longest-substring-without-repeating-characters/description/

* stack相关问题

### string DP 问题 ###
思路：使用二维矩阵, 填充true/false 还是计算的结果length？数组的size是n 还是n+1？
* Longest palindrome substring
* Edit distance.
* Longest commom sequence.

