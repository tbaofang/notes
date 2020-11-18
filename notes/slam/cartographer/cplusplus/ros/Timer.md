
```
ros::Timer ros::NodeHandle::createTimer(ros::Duration period, <callback>, bool oneshot = false);

```

ros::TimerEvent结构体

ros::TimerEvent结构体说明：
- ros::Time last_expected 上次回调期望发生的时间
- ros::Time last_real 上次回调实际发生的时间
- ros::Time current_expected 本次回调期待发生的时间
- ros::Time current_real 本次回调实际发生的时间
- ros::WallTime profile.last_duration 上次回调的时间间隔（结束时间-开始时间），是wall-clock时间。