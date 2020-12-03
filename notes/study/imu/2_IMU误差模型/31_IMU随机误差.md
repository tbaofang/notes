IMU随机误差

高斯白噪声
IMU数据连续时间上受到一个均值为0,方差为$\sigma$,各时刻之间相互独立的高斯过程$n(t)$:

$$
\begin{aligned}
  & E[n(t)] = 0 \\
  & E[n(t_1)n(t_2)] = \sigma^2 \delta(t1-t2)
\end{aligned}
$$
其中,$\delta()$表示狄拉克函数.

Bias随机游走
通常用维纳过程(wiener process)来建模bias随时间连续变化的过程,离散时间下称之为随机游走.

$$
\dot{b}(t) = n_b(t) = \sigma_b w(t)
$$

其中,$ w$是方差为1的白噪声.

---

问题:
实际上,IMU传感器获取的数据为离散采样,离散和连续高斯白噪声存在何种关系?

假设有一个单轴角速度信号收到高斯白噪声和bias随机游走的影响,建模如下:
$$
\begin{aligned}
  &\widetilde{w}(t) = w(t) + b(t) + n(t) \\
  & \dot{b}(t) = n_b(t)
\end{aligned}
$$

当传感器采集信号时,假设采样时间段内信息为常数:
$$
\frac{1}{\Delta t} \int^{t_0+\Delta t}_{t_0} \widetilde{w}(t) dt = \frac{1}{\Delta t} \int^{t_0+\Delta t}_{t_0}[w(t)+b(t)+n(t)]dt
$$
即
$$
\widetilde{w}(t_0+\Delta t) = w(t_0+\Delta t)+\frac{1}{\Delta t} \int^{t_0+\Delta t}_{t_0}[b(t)+n(t)]dt
$$

---

高斯白噪声的离散化

只考虑高斯白噪声的积分
$$
n_d[k] \triangleq n(t_0 + \Delta t) \simeq \frac{1}{\Delta t} \int ^{t_0+\Delta t}_{t_0} n(t) dt
$$

协方差为:
$$
\begin{aligned}
  E(n^2_d[k]) &= E(\frac{1}{\Delta t^2} \int ^{t_0+\Delta t}_{t_0} \int ^{t_0+\Delta t}_{t_0} n(\tau) n(t))d\tau dt \\
  &= \frac{1}{\Delta t^2} \int ^{t_0+\Delta t}_{t_0} \int ^{t_0+\Delta t}_{t_0} E(n(\tau) n(t))d\tau dt \\
  &= \frac{\sigma^2}{\Delta t^2} \int ^{t_0+\Delta t}_{t_0} \int ^{t_0+\Delta t}_{t_0} \delta(t-\tau)d\tau dt \\
  &= \frac{\sigma^2}{\Delta t}
\end{aligned}
$$

---
bias随机游走的离散化

提取bias积分部分

$$
b(t_0+\Delta t) = b(t_0) + \int ^{t_0+\Delta t}_{t_0} n_b(t) dt
$$

由此可得离散化下的bias协方差:
$$
E\{b^2(t_0+\Delta t)\} = E\{[b(t_0)+\int ^{t_0+\Delta t}_{t_0}n_b(t)dt][b(t_0)+\int ^{t_0+\Delta t}_{t_0}n_b(\tau)d\tau]\}
$$

由于$E\{n_b(t)n_b(\tau)\} = \sigma^2_b \delta(t-\tau)$有:
$$
E\{b^2(t_0+\Delta t)\} = E\{b^2(t_0)\} + \sigma^2_b \Delta t
$$

---
即:
$$
b_d[k] = b_d[k-1] + \sigma_{bd}w[k]
$$

其中,
$$
\begin{aligned}
  & w[k] \sim N(0, 1)\\
  & \sigma_{bd} = \sigma_b \sqrt{\Delta t}
\end{aligned}
$$

  bias随机游走的噪声方差从连续时间到离散之间需要乘以$\sqrt{\Delta t}$










