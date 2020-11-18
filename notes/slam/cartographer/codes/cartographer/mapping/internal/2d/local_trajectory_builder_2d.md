class LocalTrajectoryBuilder2D

```
  struct InsertionResult {
    std::shared_ptr<const TrajectoryNode::Data> constant_data;
    std::vector<std::shared_ptr<const Submap2D>> insertion_submaps;
  };

  struct MatchingResult {
    common::Time time;
    transform::Rigid3d local_pose;
    sensor::RangeData range_data_in_local;
    std::unique_ptr<const InsertionResult> insertion_result;
  };
```

```
  explicit LocalTrajectoryBuilder2D(
      const proto::LocalTrajectoryBuilderOptions2D& options,
      const std::vector<std::string>& expected_range_sensor_ids);

  std::unique_ptr<MatchingResult> AddRangeData(
      const std::string& sensor_id,
      const sensor::TimedPointCloudData& range_data);

  void AddImuData(const sensor::ImuData& imu_data);

  void AddOdometryData(const sensor::OdometryData& odometry_data);

  static void RegisterMetrics(metrics::FamilyFactory* family_factory);      
```


-->extrapolator