

```
Quaternion<Type>
```

Quaternion<Type>

```
conjugate() //表示旋转轴不变,旋转角相反 

normalized()

w()
x()
y()
z()

vec().norm()

```

 叉乘（q1 * q2）:物理含义是先绕q2做旋转变换,再绕q1做旋转变换.

 向量v绕四元素旋转: q * v * conjugate(q) // ??