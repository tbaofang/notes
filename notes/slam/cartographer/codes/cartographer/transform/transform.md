
```
template <typename FloatType>
FloatType GetAngle(const Rigid3<FloatType>& transform)

template <typename T>
T GetYaw(const Eigen::Quaternion<T>& rotation)

template <typename T>
T GetYaw(const Rigid3<T>& transform)


template <typename T>
Eigen::Matrix<T, 3, 1> RotationQuaternionToAngleAxisVector(
    const Eigen::Quaternion<T>& quaternion)

template <typename T>
Eigen::Quaternion<T> AngleAxisVectorToRotationQuaternion(
    const Eigen::Matrix<T, 3, 1>& angle_axis)   

template <typename T>
Rigid2<T> Project2D(const Rigid3<T>& transform)    

template <typename T>
Rigid3<T> Embed3D(const Rigid2<T>& transform)
```