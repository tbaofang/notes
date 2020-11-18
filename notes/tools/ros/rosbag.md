```
rosbag recode -a
rosbag recode /scan /odom /imu

rosbag play --clock -r 2 **.bag

<node pkg="rosbag" / >

```