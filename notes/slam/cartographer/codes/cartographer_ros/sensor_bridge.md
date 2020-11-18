
node->



```
  const int num_subdivisions_per_laser_scan_; 

  std::map<std::string, cartographer::common::Time>
      sensor_to_previous_subdivision_time_; 

  const TfBridge tf_bridge_;

  ::cartographer::mapping::TrajectoryBuilderInterface* const
      trajectory_builder_; 

  ::cartographer::common::optional<::cartographer::transform::Rigid3d>
      ecef_to_local_frame_;

```

```
  void HandleLaserScanMessage(const std::string& sensor_id,
                              const sensor_msgs::LaserScan::ConstPtr& msg);

  void HandleOdometryMessage(const std::string& sensor_id,
                             const nav_msgs::Odometry::ConstPtr& msg);

  void HandleImuMessage(const std::string& sensor_id,
                        const sensor_msgs::Imu::ConstPtr& msg);                                                           
```



-> HandleLaserScanMessage()
-> HandleLaserScan() 
-> HandleRangefinder()  

-> CollatedTrajectoryBuilder::AddSensorData()

-> Collator::AddSensorData()


----

Node::AddTrajectory()

-> MapBuilderBridge::AddTrajectory()
-> MapBuilder::AddTrajectoryBuilder()

-> CollatedTrajectoryBuilder::CollatedTrajectoryBuilder()

-> Collator::AddTrajectory()  
-> CollatedTrajectoryBuilder::HandleCollatedSensorData()

-> Dispatchable::AddToTrajectoryBuilder()

-> GlobalTrajectoryBuilder::AddSensorData()