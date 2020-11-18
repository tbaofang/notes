
### imu_tracker
imu_tracker更新imu_angular_velocity_/重力向量gravity_vector_/姿态orientation_;

通过获得的角速度(AddImuAngularVelocityObservation)更新imu_angular_velocity_,进一步更新(Advanc)gravity_vector和orientation_;
通过获得的线加速度(AddImuLinearAccelerationObservation)更新gravity_vector和orientation_;

可以认为当前时刻的gravity_vector_的更新依赖于上一时刻gravity_vector_/当前的姿态orientation_;
当前时刻的姿态orientation_的更新依赖于上一时刻的orientation_和当前时刻的gravity_vector_

### pose_extrapolator

通过(ExtrapolatePose())进行平移和旋转插值,


1. 共轭 = 逆
2. 求共轭 = 对应三个轴角度取反
3. 两个四元素乘积 = 对应三个轴角度做加法
4. 四元素乘向量 = 对向量做旋转