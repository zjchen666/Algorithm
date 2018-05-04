### 主要考点 ###

## 模运算 ##
运算规则
模运算与基本四则运算有些相似，但是除法例外。其规则如下：
(a + b) % p = (a % p + b % p) % p    
(a - b) % p = (a % p - b % p + p) % p    
(a * b) % p = (a % p * b % p) % p    
(a^b) % p = ((a % p)^b) % p  

* 求质数
* 分解质因数

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
