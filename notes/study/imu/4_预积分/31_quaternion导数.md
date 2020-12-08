
IMU旋转状态推导:
$$
q_{k+1} = q_k \otimes \int_{t \in [k, k+1]} \dot{q}_t dt \qquad 
$$

推导:  $\dot{q} = \frac{1}{2} q_t \otimes \begin{bmatrix}
  0 \\ w
\end{bmatrix}$

引入左乘和右乘符号:

<!-- $$
\begin{aligned}
q_a \otimes q_b &=  \mathfrak{R}(q_b) q_a = 
\begin{bmatrix}
  s_b & z_b & -y_b & x_b \\
  -z_b & s_b & x_b & y_b  \\
  y_b & -x_b & s_b & z_b \\
  -x_b & -y_b & -z_b & s_b \\
\end{bmatrix}
\begin{bmatrix}
  x_a \\ y_a \\ z_a \\ s_a 
\end{bmatrix} \\
&=  \mathfrak{L}(q_a) q_b = 
\begin{bmatrix}
  s_a & -z_a & y_a & x_a \\
  z_a & s_a & -x_a & y_a  \\
  -y_a & x_a & s_a & z_a \\
  -x_a & -y_a & -z_a & s_a \\
\end{bmatrix}
\begin{bmatrix}
  x_b \\ y_b \\ z_b \\ s_b 
\end{bmatrix}
\end{aligned}
$$ -->

$$
\begin{aligned}
q_a \otimes q_b &=  \mathfrak{R}(q_b) q_a = 
\begin{bmatrix}
  s_b & -x_b & -y_b & -z_b \\
  x_b & s_b & z_b & -y_b  \\
  y_b & -z_b & s_b & x_b \\
  z_b & y_b & -x_b & s_b \\
\end{bmatrix}
\begin{bmatrix}
  s_a \\x_a \\ y_a \\ z_a 
\end{bmatrix} \\
&=  \mathfrak{L}(q_a) q_b = 
\begin{bmatrix}
  s_a & -x_a & -y_a & -z_a \\
  x_a & s_a & -z_a & y_a  \\
  y_a & z_a & s_a & -x_a \\
  z_a & -y_a & x_a & s_a \\
\end{bmatrix}
\begin{bmatrix}
  s_b  \\ x_b \\ y_b \\ z_b 
\end{bmatrix}
\end{aligned}
$$

为了简化,令$q = [s \ x \ y \ z ] = [s \ w] $, 则:
$$
\begin{aligned}
  & \mathfrak{R}(q) = \Omega(w) + s I_{4 \times 4} = 
  \begin{bmatrix}
    0 & -w^T \\ w & -w^\land 
  \end{bmatrix} + sI_{4 \times 4} \\
    & \mathfrak{L}(q) = \Psi(w) + s I_{4 \times 4} = 
  \begin{bmatrix}
    0 & -w^T \\ w & w^\land 
  \end{bmatrix} + sI_{4 \times 4}
\end{aligned}
$$

---

$$
\begin{aligned}
  \dot{q}_t  &= \lim_{\delta t \rightarrow 0} \frac{1}{\delta t} (q_{t + \delta t} - q_t) = \lim_{\delta t \rightarrow 0} \frac{1}{\delta t} (q_t \otimes q_{t + \delta t}^t - q_t \otimes \begin{bmatrix} 1 \\ 0   
  \end{bmatrix}) \\
  &= \lim_{\delta t \rightarrow 0} \frac{1}{\delta t}(q_t \otimes \begin{bmatrix}
    \cos \frac{\theta}{2} \\ \sin \frac{\theta}{2} \hat{k}  
  \end{bmatrix}) - q_t \otimes \begin{bmatrix}
    1 \\ 0
  \end{bmatrix}) 
  \approx  \lim_{\delta t \rightarrow 0} \frac{1}{\delta t} (q_t \otimes \begin{bmatrix}
    1 \\ \frac{\theta}{2}  \hat{k} 
  \end{bmatrix}) - q_t \otimes \begin{bmatrix}
    1 \\ 0
  \end{bmatrix}) \\
  &= \lim_{\delta t \rightarrow 0} \frac{1}{\delta t} [\mathfrak{R}(\begin{bmatrix}
    1 \\ \frac{\theta}{2} \hat{k} 
  \end{bmatrix})] - \mathfrak{R}(\begin{bmatrix}
    1 \\ 0
  \end{bmatrix}) q_t = \lim_{\delta t \rightarrow 0} \frac{1}{\delta t} \begin{bmatrix}
    0 & \ - \frac{\theta ^ T}{2}  \\
    \frac{\theta}{2} & - \frac{\theta ^\land}{2} 
  \end{bmatrix} q_t
\end{aligned}
$$

因为角速度为:$$w =  \lim_{\delta t \rightarrow 0} \frac{\delta}{\delta t}$$
则上式可以化简为:

$$
\dot{q}_t = \frac{1}{2} \begin{bmatrix}
  0 & -w^T \\ w & - w^\land
\end{bmatrix} q_t = \frac{1}{2} \Omega(w) q_t = \frac{1}{2} \mathfrak{R}(\begin{bmatrix}
  0 \\ w
\end{bmatrix}) q_t = \frac{1}{2} q_t \otimes \begin{bmatrix}
  0 \\ w
\end{bmatrix}
$$

supplence:

$$
q_{t + \delta t}^t = \begin{bmatrix}
  s \\ \lambda \hat{k}
\end{bmatrix}
$$

