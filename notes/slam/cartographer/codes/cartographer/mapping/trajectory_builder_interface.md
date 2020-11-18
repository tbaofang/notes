class TrajectoryBuilderInterface

```
  struct InsertionResult {
    NodeId node_id; 
    std::shared_ptr<const TrajectoryNode::Data> constant_data; 
    std::vector<std::shared_ptr<const Submap>> insertion_submaps;
  };

  using LocalSlamResultCallback =
      std::function<void(int , common::Time,
                         transform::Rigid3d ,
                         sensor::RangeData ,
                         std::unique_ptr<const InsertionResult>)>;  

  struct SensorId {
    enum class SensorType {
      RANGE = 0,
      IMU,
      ODOMETRY,
      FIXED_FRAME_POSE,
      LANDMARK,
      LOCAL_SLAM_RESULT
    };
                             
```

```

```