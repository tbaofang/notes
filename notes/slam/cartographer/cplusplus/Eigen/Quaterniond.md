Eigen::Quaterniond

```
Identity()

inverse()

conjugate() //表示旋转轴不变,旋转角相反 

FromTwoVectors() 返回v1到v2的旋转四元素
```


```
  const Eigen::Quaterniond rotation = Eigen::Quaterniond::FromTwoVectors(
      gravity_vector_, orientation_.conjugate() * Eigen::Vector3d::UnitZ());  
```

求共轭

q*=(-x, -y, -z, w)

求逆

对于向量逆的定义, q-1 =q*/|q|2

对于单位四元素，分母为1，q-1 = q* =(-x, -y, -z, w)


对于单位四元素 共轭 = 逆