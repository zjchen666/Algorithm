## 位操作 ##
1. 异或操作  
* a ^ b ^ a = b  
* a ^ a = 0  
× ^ 1 = ~x
x ^ 0 = x
 - exchange two varable:
    a = a ^ b;
    b = b ^ a;
    a = a ^ b;

2. Remove the last 1 bit
 x = x & (x - 1)
