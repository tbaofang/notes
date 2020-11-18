cartographer/mapping/imu_tracker.h

```
const double imu_gravity_time_constant_;
common::Time time_;
common::Time last_linear_acceleration_time_;

Eigen::Quaterniond orientation_;
Eigen::Vector3d gravity_vector_;
Eigen::Vector3d imu_angular_velocity_;
```

```
ImuTracker(double imu_gravity_time_constant, common::Time time);

void Advance(common::Time time);

void AddImuLinearAccelerationObservation(
    const Eigen::Vector3d& imu_linear_acceleration);
void AddImuAngularVelocityObservation(
    const Eigen::Vector3d& imu_angular_velocity);

common::Time time() const { return time_; }
Eigen::Quaterniond orientation() const { return orientation_; }

```