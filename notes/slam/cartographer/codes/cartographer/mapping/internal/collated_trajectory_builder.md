cartographer_ros/senaor_bridge ->

```
  sensor::CollatorInterface* const sensor_collator_;
  const int trajectory_id_;
  std::unique_ptr<TrajectoryBuilderInterface> wrapped_trajectory_builder_;

  std::chrono::steady_clock::time_point last_logging_time_;
  std::map<std::string, common::RateTimer<>> rate_timers_;
```