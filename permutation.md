## 全排列算法 ##
* 交换法
* 字典序法
* 全排列去重

### 交换法 ###
   * 使用DFS 递归交换元素。输出结果。
    
### 字典序法 ###
1. 字典序（lexicographical order）可以排列数字或字符串， 字符使用ASCII码比较。boat < boot < cap < card < cat < to < too < two < up 
2. 求下一个字典序，3步:
   * 找最后一个正序。 最后一个 nums[i] < nums[i+1]
   * 找最后一个比nums[i]大的num。
   * 将nums[i+1:] reverse. -> 注意不需要排序， 为什么？（第一步可以保证）
3. 求上一个字典序， 3步：
   * 找最后一个降序。 最后一个 nums[i] > nums[i+1]
   * 找最后一个比nums[i]小的num。
   * 将nums[i+1:] reverse. -> 注意不需要排序， 为什么？（第一步可以保证）

### 全排列去重 ###
1. 交换法， 遇重不交换。