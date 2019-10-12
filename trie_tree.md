
Trie Tree
===========
### 主要操作 ### 
- 创建
- 查找
- 删除
- 求公共前缀

### 主要问题 ###
- 前缀问题 比hash table快
- 空间优化 hash table的字符串相关问题， 

### 数据结构 ###
```cpp
   class TrieNode {
       bool is_leaf;
       TrieNode* children[26];
       TrieNode () {
           is_leaf = false;
           for (int i = 0; i < 26; ++i) {
               children[i] = nullptr;
           }
       }
   };
   
   void insert(string word) {
       TrieNode* cur = root;
       for (char c : word) {
           if (nullptr == cur->children[c - 'a']) {
               cur->children[c - 'a'] = new TrieNode();
           }
           cur = cur->children[c - 'a'];
       }
       cur->is_left = true;
       return;
   }
   
   bool search(string word) {
       TrieNode* cur = root;
       for (char c : word) {
           if (nullptr == cur->children[c - 'a']) {
               return false;
           }
           cur = cur->children[c - 'a'];
       }
       return cur->is_leaf;
   }
```
```python
  ## hash table - setdefault()
  ## The method setdefault() is similar to get(), but will set dict[key]=default if key is not already in dict.
class Trie(object):

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.root = {}
        self.END = "/"

    def insert(self, word):
        """
        Inserts a word into the trie.
        :type word: str
        :rtype: void
        """
        node = self.root
        for c in word:
            node = node.setdefault(c, {})
        node[self.END] = None
        

    def search(self, word):
        """
        Returns if the word is in the trie.
        :type word: str
        :rtype: bool
        """
        node = self.root
        for c in word:
            if c not in node:
                return False
            node = node[c]
        if self.END in node:
            return True
        else:
            return False

    def startsWith(self, prefix):
        """
        Returns if there is any word in the trie that starts with the given prefix.
        :type prefix: str
        :rtype: bool
        """
        node = self.root
        for c in prefix:
            if c not in node:
                return False
            node = node[c]
        return True
```
