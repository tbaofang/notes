
微机电系统（MEMS, Micro-Electro-Mechanical System）,微机电系统其内部结构一般在微米甚至纳米量级，是一个独立的智能系统。

加速度计工作原理:
- 其测量原理可以用一个质量块+弹簧+指示计来表示.
- 加速度计测量值$a_m$为弹簧拉力对应的加速度,
  $$a_m = \frac{f}{m} = a - g$$

其中,f为弹簧拉力, a为物体在惯性系下的加速度,g为重力加速度.

- 通过受力影响位移,位移影响电容大小,通过测量电流的方式获得$a_m$

---

陀螺工作原理:

陀螺仪主要用来测量物体的旋转角速度,按测量原理分有震动陀螺/光纤陀螺等.

一般采用震动陀螺原理,通过测量Coriolis force 来间接得到角速度.

一个主动运动轴 + 一个敏感轴

---

音叉振动陀螺

- 音叉中间为旋转轴,音叉左右两个质量块,做方向相反的正弦运动,质量块受到的科氏力方向相反.
- 为什么要这么做?一个质量块行不行?

---  



陀螺仪的G-sensitivity

实际上,两个质量块不可能完全一致,也就是说陀螺仪的测量会受到外部加速度的影响,即常称的G-sensitivity.

加速度计不需要考虑科氏力的影响吗?