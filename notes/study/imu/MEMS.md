

随机游走 -- 白噪声积分结果

噪声密度 -- 

### 陀螺误差模型

主要由两部分构成:随机 漂移和刻度系数误差
随机漂移误差主要分为三种分量: 逐次启动漂移/慢变漂移/快变漂移

### 加速度计误差模型
随机常值误差

## 标定

加速度计六面法标定


---

姿态解算是将陀螺仪的角速度数据,加速度计的加速度数据,磁力计的磁场数据进行融合,解算出当前载体的姿态角.

姿态是反应物体相对于参考坐标系的指向,常使用欧拉角代表物体的姿态,描述物体姿态需要三个角度,分别是yaw(偏航角, 绕z轴的角度),pitch(俯仰角),roll(横滚角).

陀螺仪是测量角度的传感器,测量三个正交方向上旋转的角速度,通过积分可以估算三个方向上的旋转角度.

最常用的陀螺仪是微机电(MEMS)陀螺仪,其基本原理是利用旋转时产生的科里奥利力引发电容的变化,从而将旋转的角速度转化为电信号.

加速度计能够测量三个正交方向的加速度,MEMS加速度计原理是利用加速度变化使内部质量块产生力的变化,从而改变电容大小,转化为电信号.

零漂现象是指当物理量输入为零,传感器测量的输出不为零的现象.
零漂受温度影响
测量出零漂的大小,将IMU测量到的值与零漂值相减.