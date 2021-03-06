
## 考点
  1. add string  
  2. sliding window  
  3. one pass scan to proccessing substr
  4. rearrang string  

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
* 两个字符串比较
* 子字符串查找
* 模拟算法
* two pointers
* hash table(可以用size 为 128 byte的数组替换)
* DP
* 子串处理
* 字符串替换： 
   - 从后向前替换
   https://leetcode.com/problems/find-and-replace-in-string/description/
  
  
## 判断一个字符串是否由子串构成
1：串中有重复字串的串的特点：按位旋转，转动一定位数，会和原来的串一个顺序 2：我们的目标就是找到按位旋转的所有情况。 3：两个串相加就包含所有情况 4：若两串相加且去头去尾，还包含目标串，则说明旋转一定位数后，能够回到原来的串，也就说明该串是重复字符串。

## 两个字符串比较
   solutions:   
     1. 填充短的。  https://leetcode.com/problems/compare-version-numbers/description/  
     2. 按min(len1, len2)先处理。  verify alien dictionary  
     3. 按max(len1, len2)先处理。  add numbers  
     4. 同向 two pointer。 https://leetcode.com/problems/long-pressed-name/  
     5. 字符串长度相同， 不同？模版
## 一层循环的子串处理问题
```cpp
        i = 0;
        for (int j = 0; j <= s.size(); ++j){
            # end or condition
            if (condition meet or j == s.size()) {
                # update
                # i = j;
            }
        }
```
https://leetcode.com/problems/reverse-words-in-a-string-ii/  
https://leetcode.com/problems/count-binary-substrings/  
https://leetcode.com/problems/string-compression/description/  
https://leetcode.com/problems/number-of-segments-in-a-string/description/  
https://leetcode.com/problems/count-and-say/description/  
https://leetcode.com/problems/long-pressed-name/  
https://leetcode.com/problems/brace-expansion/  //TODO optimize  
https://leetcode.com/problems/expressive-words/

## Sliding window 的问题
  模板
```cpp
    int lengthOfLongestSubstringKDistinct(string s, int k) {
        int n = s.size();
        unordered_map<int, int> map;
        int left = 0, res = 0;
        
        // scan from begin to end
        for (int right = 0; right < n; right++) {
            // do something
            map[s[right]]++;
            
            // condition is broken, fix it
            while (map.size() > k) {
                // update result here if for a minimum result. for instance, minimum slideing window
                map[s[left]]--;
                if (map[s[left]] == 0) map.erase(s[left]);
                left++;
            }
            
            // update result here for maxinum result
            res = max(res, right - left + 1);
        }
        
        return res;
    }
```
https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/description/  
https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/description/  
https://leetcode.com/problems/longest-substring-without-repeating-characters/description/   
https://leetcode.com/problems/minimum-window-substring/description/      
https://leetcode.com/problems/longest-repeating-character-replacement/  
https://leetcode.com/problems/max-consecutive-ones-ii/description/  
https://leetcode.com/problems/get-equal-substrings-within-budget/
https://leetcode.com/problems/longest-substring-with-at-least-k-repeating-characters/

### Rearrange String
   Solution:
      1. find the char with maximum repeat count.
      2. use PQ to simulate the rearrange, return failure if can not finish.

```cpp
    string rearrangeString(string s, int k) {
        vector<int> counts(26, 0);
        priority_queue<pair<int, char>> pq;
        string result;
        
        # find char with maximum count
        if (k <= 1)
            return s;
        
        for (int i = 0; i < s.size(); i++){
            counts[s[i] - 'a']++;
        }

        // init the PQ
        for (int i = 0; i < 26; i++){
            if (counts[i] > 0){
                pq.push({counts[i], 'a' + i});
            }
        }
        
        // rearrange the string with cache
        int pos = 0;
        int length = s.size();
        while (!pq.empty())
        {
            vector<pair<int, char>> cache;
            // insert k char or remain chars for each round
            int n = min(k, length);
            for (int i = 0; i < n; i++)
            {
                if (pq.empty())
                {
                    return "";
                }
                pair<int, int> c = pq.top();
                pq.pop();
                c.first--;
                result.push_back(c.second);
                if (c.first > 0)
                    cache.push_back({c.first, c.second});
                length--;
            }

            for (auto it: cache)
            {
                pq.push(it);
            }
        }
        return result;
    }
```
https://leetcode.com/problems/rearrange-string-k-distance-apart/description/  
https://leetcode.com/problems/reorganize-string/description/  
https://leetcode.com/problems/task-scheduler/description/  

### string DP 问题 ###
思路：使用二维矩阵, 填充true/false 还是计算的结果length？数组的size是n 还是n+1？
* Longest palindrome substring
* Edit distance.
* Longest commom sequence.

