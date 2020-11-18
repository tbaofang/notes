```
pcl::PointCloud<PointType>::Ptr laserCloudIn;
pcl::PointCloud<PointXYZIR>::Ptr laserCloudInRing;

pcl::PointCloud<PointType>::Ptr fullCloud; 
pcl::PointCloud<PointType>::Ptr fullInfoCloud; 

pcl::PointCloud<PointType>::Ptr groundCloud;
pcl::PointCloud<PointType>::Ptr segmentedCloud;
pcl::PointCloud<PointType>::Ptr segmentedCloudPure;
pcl::PointCloud<PointType>::Ptr outlierCloud;

PointType nanPoint; 

cv::Mat rangeMat; 
cv::Mat labelMat; 
cv::Mat groundMat; 
int labelCount;

float startOrientation;
float endOrientation;

cloud_msgs::cloud_info segMsg; 

std::vector<std::pair<int8_t, int8_t> > neighborIterator; 

uint16_t *allPushedIndX; 
uint16_t *allPushedIndY;

uint16_t *queueIndX; 
uint16_t *queueIndY;
```


```
void cloudHandler(const sensor_msgs::PointCloud2ConstPtr& laserCloudMsg)

void copyPointCloud(laserCloudMsg)
void findStartEndAngle()
void projectPointCloud()
void groundRemoval()
void cloudSegmentation()

void publishCloud()
void resetParameters()
```


ImageProjection()

-> cloudHander()

-> copyPointCloud()

-> findStartEndAngle()
1.以X轴负轴为基准, 最末角度为2π减去计算值 ??

->projectPointCloud()







