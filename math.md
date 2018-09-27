
### 主要考点 ###
## reverse a number ##
```cpp
    int n = 0;
    while (x)
    {
        n = n * 10;
        n += x % 10;
        x = x / 10;
    }
    
    //overflow
    tmp = res * 10 + x % 10;
    if (tmp / 10 != res)
      //overflow
    else
        res = tmp;
```
https://leetcode.com/problems/palindrome-number/description/  
https://leetcode.com/problems/reverse-integer/description/

## 模运算 ##
运算规则
模运算与基本四则运算有些相似，但是除法例外。其规则如下：
(a + b) % p = (a % p + b % p) % p    
(a - b) % p = (a % p - b % p + p) % p    
(a * b) % p = (a % p * b % p) % p    
(a^b) % p = ((a % p)^b) % p  

## 欧几里得 GCD 算法 ##

```python
def gcd(x, y):
   a, b = x, y if x > y else y, x
   a = a % b
   if a == 0:
       return b
   else:
       return gcd(b, a)
```

## 求质数 ##
