
IMU不依托额外设备实现标定

- 参考论文:[A Robust and Easy to Implement Method for IMU Calibration without External Equipments ](http://www.dis.uniroma1.it/~pretto/papers/tpm_icra2014.pdf)
  
- DEMO链接:https://bitbucket.org/alberto_pretto/imu_tk
- 光学陀螺输入输出特性建模及补偿技术研究[D].哈尔滨工程大学,2002.

---
IMU确定性误差校正步骤:

将IMU静止放置,初始化50秒至1分钟;
将IMU旋转一个位置,静止20秒;
重复步骤2的操作,将IMU旋转至与之前不同的位置,重复该动作10次后结束;
将IMU静止放置20秒,结束数据采集.

---
该方案优点:不需要额外的设备辅助标定(三轴转台),对IMU的摆放位置没有特殊的要求(相比于六面法标定);

方案的缺点:加速度计标定时需要预先设定传感器的零偏,若设置实际值有误差,校正结果也会有误差.

---

论文中提到:首先在静态测量样本间隔进行加速度计矫正.然后利用这些结果,通过数值积分的方法实现陀螺仪的参数校正.

---
[MEMS IMU的入门与应用-胡佳兴](https://www.bilibili.com/video/BV1Vs411k7NG?from=search&seid=15197424126110122027)