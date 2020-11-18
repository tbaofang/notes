
node_main->
->sensor_bridge



```
  struct Subscriber {
    ::ros::Subscriber subscriber;
    std::string topic;
  };      

  struct TrajectorySensorSamplers {
    TrajectorySensorSamplers(const double rangefinder_sampling_ratio,
                             const double odometry_sampling_ratio,
                             const double fixed_frame_pose_sampling_ratio,
                             const double imu_sampling_ratio,
                             const double landmark_sampling_ratio)
        : rangefinder_sampler(rangefinder_sampling_ratio),
          odometry_sampler(odometry_sampling_ratio),
          fixed_frame_pose_sampler(fixed_frame_pose_sampling_ratio),
          imu_sampler(imu_sampling_ratio),
          landmark_sampler(landmark_sampling_ratio) {}

    ::cartographer::common::FixedRatioSampler rangefinder_sampler;
    ::cartographer::common::FixedRatioSampler odometry_sampler;
    ::cartographer::common::FixedRatioSampler fixed_frame_pose_sampler;
    ::cartographer::common::FixedRatioSampler imu_sampler;
    ::cartographer::common::FixedRatioSampler landmark_sampler;
  };


  const NodeOptions node_options_;

  tf2_ros::TransformBroadcaster tf_broadcaster_;

  cartographer::common::Mutex mutex_;
  MapBuilderBridge map_builder_bridge_ GUARDED_BY(mutex_);

  ::ros::NodeHandle node_handle_;

  ::ros::Publisher submap_list_publisher_;
  ::ros::Publisher trajectory_node_list_publisher_;
  ::ros::Publisher landmark_poses_list_publisher_;
  ::ros::Publisher constraint_list_publisher_;
  ::ros::Publisher scan_matched_point_cloud_publisher_;   

  std::vector<::ros::ServiceServer> service_servers_;


  std::map<int, ::cartographer::mapping::PoseExtrapolator> extrapolators_;

  std::unordered_map<int, TrajectorySensorSamplers> sensor_samplers_;
  std::unordered_map<int, std::vector<Subscriber>> subscribers_;
  std::unordered_set<std::string> subscribed_topics_;
  std::unordered_map<int, bool> is_active_trajectory_ GUARDED_BY(mutex_);

  std::vector<::ros::WallTimer> wall_timers_;
```

```
  Node(const NodeOptions& node_options,
       std::unique_ptr<cartographer::mapping::MapBuilderInterface> map_builder,
       tf2_ros::Buffer* tf_buffer);

  void HandleLaserScanMessage(const int trajectory_id,
                                  const std::string& sensor_id,
                                  const sensor_msgs::LaserScan::ConstPtr& msg)


  void HandleOdometryMessage(int trajectory_id, const std::string& sensor_id,
                             const nav_msgs::Odometry::ConstPtr& msg);       

  void HandleImuMessage(int trajectory_id, const std::string& sensor_id,
                        const sensor_msgs::Imu::ConstPtr& msg);     



template<typename MessageType>                                                
::ros::Subscriber SubscribeWithHandler(
  void (Node::*handler)(int, const std::sring&, const typename MessageType::ConstPtr&),
  const int trajectory_id, const std::string& topic,
  ::ros::NodeHandle* const node_handle, Node* const node);
)
```

StartTrajectoryWithDefaultTopics -> **AddTrajectory** -> ComputeExpectedSensorIds 
                                                  -> MapbuilderBridge::AddTrajectory
                                                  -> AddExtrapolator
                                                  -> AddSensorSamplers
                                                  -> LaunchSubscribers


HandleFinishTrajectory ->  FinishTrajectoryUnderLock                                                  
