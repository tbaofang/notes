

sensor_msgs::PointCloud2   和  pcl::PointCloud<T>之间的转换使用 pcl::fromROSMsg 和 pcl::toROSMsg 

sensor_msgs::PointCloud   和   sensor_msgs::PointCloud2之间的转换
使用sensor_msgs::convertPointCloud2ToPointCloud 和sensor_msgs::convertPointCloudToPointCloud2


pcl_conversions::toPCL(*input, *cloud);

pcl_conversions::fromPCL(cloud_filtered, output);