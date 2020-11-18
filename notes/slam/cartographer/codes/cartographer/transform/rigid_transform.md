transform/rigid_transform.h

#### class Rigid2

```
using Vector = Eigen::Matrix<FloatType, 2, 1>;
using Rotation2D = Eigen::Rotation2D<FloatType>;

Vector translation_;
Rotation2D rotation_;
```


#### class Rigid3

```
using Vector = Eigen::Matrix<FloatType, 3, 1>;
using Quaternion = Eigen::Quaternion<FloatType>;
using AngleAxis = Eigen::AngleAxis<FloatType>;

Vector translation_;
Quaternion rotation_;
```

```
Rigid3() : translation_(Vector::Zero()), rotation_(Quaternion::Identity()) {}
Rigid3(const Vector& translation, const Quaternion& rotation)
    : translation_(translation), rotation_(rotation) {}
Rigid3(const Vector& translation, const AngleAxis& rotation)
    : translation_(translation), rotation_(rotation) {}
```