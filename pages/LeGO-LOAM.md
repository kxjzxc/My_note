tags:: #毕业设计 #SLAM

- # 算法流程
	- ## 启动
		- **启动文件**`run.launch`
		- **启动指令**:`roslaunch run.launch`
		- **启动节点**:
			- rviz
			- camera_init_to_map
			- base_link_to_camera
			- ((27d7dda7-2b9f-4b34-b073-b6b3176b340b))
			- ((5dbdbde0-6910-4460-9bd2-b2482f029ec6))
			- mapOptmization
			- transformFusion
	- ## 头文件
		- **utility.h**
		- **定义参数**
			- 激光雷达参数
			- 图像分割参数
			- 特征提取参数
			- 优化参数
			- 建图参数
		- **定义结构体**
			- 点云
			- 话题
	- ## 核心程序
		- ### imageProjection
		  id:: 27d7dda7-2b9f-4b34-b073-b6b3176b340b
		  ```flow
		  st=>start: 开始
		  op1=>operation: 订阅点云数据回调处理
		  op2=>operation: 点云转换到pcl预处理
		  op3=>operation: 截取一帧激光数据
		  op4=>operation: 投影映射到图像
		  op5=>operation: 地面移除
		  op6=>operation: 点云分割
		  op7=>operation: 发布点云数据
		  op8=>operation: 重置参数
		  end=>end: 结束
		  st->op1->op2->op3->op4->op5->op6->op7->op8->end
		  ```
		  **回调函数**:cloudHandler()
		- ### featureAssociation
		  id:: 5dbdbde0-6910-4460-9bd2-b2482f029ec6
			- **构造函数**
				- 1. 订阅imageProjection处理过后的点云数据
				  
				        "/segmented_cloud"(sensor_msgs::PointCloud2)，数据处理函数laserCloudHandler
				        "/segmented_cloud_info"(cloud_msgs::cloud_info)，数据处理函数laserCloudInfoHandler
				        "/outlier_cloud"(sensor_msgs::PointCloud2)，数据处理函数outlierCloudHandler
				        imuTopic = "/imu/data"(sensor_msgs::Imu)，数据处理函数imuHandler
				- 2. 发布话题，这些topic有：
				  
				        "/laser_cloud_sharp"(sensor_msgs::PointCloud2)
				        "/laser_cloud_less_sharp"(sensor_msgs::PointCloud2)
				        "/laser_cloud_flat"(sensor_msgs::PointCloud2)
				        "/laser_cloud_less_flat"(sensor_msgs::PointCloud2)
				        "/laser_cloud_corner_last"(sensor_msgs::PointCloud2)
				        "/laser_cloud_surf_last"(cloud_msgs::cloud_info)
				        "/outlier_cloud_last"(sensor_msgs::PointCloud2)
				        "/laser_odom_to_init"(nav_msgs::Odometry)
				- 3. 初始化参数
			- **回调函数**
				- **laserCloudHandler**:主要是被分割点和经过降采样的地面点,其 intensity 记录了该点在深度图上的索引位置
				- **laserCloudInfoHandler**
				- **outlierCloudHandler**
				- **imuHandler**:
				    1. 通过接收到的imuIn里面的四元数得到roll,pitch,yaw三个角；
				    2. 对加速度进行坐标变换，进行加速度坐标交换时将重力加速度去除，然后再进行 $x$到 $z$, $y$到$x$,$z$到$y$的变换。
				    3. 将欧拉角，加速度，速度保存到循环队列中；
				    4. 对速度，角速度，加速度进行积分，得到位移，角度和速度(AccumulateIMUShiftAndRotation())；
			- **运行函数**
				- **特征提取**
					- 1. **去除运动畸变**：将点云数据进行坐标变换，进行插补等工作
					  2. **曲率计算**：计算曲率，以相邻左右5个点计算，并保存结果
					  3. **标记瑕点**：相邻但距离较远的点（平行点被误判为平面点的情况），以及邻域距离变化较大的点（遮挡点被误判为边点的情况）
					  4. **特征提取**
					  5. **发布特征点云**
				- **特征关联**
					- 1. **更新先验位姿**：将当前时刻保存的IMU数据作为先验数据
					  2. **更新位姿**：找特征平面，通过面之间的对应关系，以及通过角、边特征的匹配，计算变换矩阵
					  3. **整合信息**：将IMU信息融入到位姿更新当中
					  4. **发布里程计信息**
					  5. **发布点云**
				- **运动物体消除**
					- **函数**：
						- popMovingCornerFeatures()
						- popMovingPlanarFeatures()
			- 参考文章
				- [LEGO-LOAM源码解析 --- FeatureAssociation节点(1)](https://zhuanlan.zhihu.com/p/242559124)
- ## mapOptmization
  **主要内容**：地图优化，拥有三个线程，回环检测、可视化点云
	- ### 构造函数
	  订阅话题:
	  
	    "/laser_cloud_corner_last"(sensor_msgs::PointCloud2)，数据处理函数laserCloudCornerLastHandler
	    "/laser_cloud_surf_last"(sensor_msgs::PointCloud2)，数据处理函数laserCloudSurfLastHandler
	    "/outlier_cloud_last"(sensor_msgs::PointCloud2)，数据处理函数laserCloudOutlierLastHandler
	     "/laser_odom_to_init"(nav_msgs::Odometry)，数据处理函数laserOdometryHandler
	    imuTopic = "/imu/data"(sensor_msgs::Imu)，数据处理函数imuHandler
	  
	  发布话题，这些topic有：
	  
	    "/key_pose_origin"(sensor_msgs::PointCloud2)
	    "/laser_cloud_surround"(sensor_msgs::PointCloud2)
	    "/aft_mapped_to_init"(nav_msgs::Odometry)
	    "/history_cloud"(sensor_msgs::PointCloud2)
	    "/corrected_cloud"(sensor_msgs::PointCloud2)
	    "/recent_cloud"(sensor_msgs::PointCloud2)
	    "/registered_cloud"(sensor_msgs::PointCloud2)
	- ### 主线程
	  
	  1. **坐标变换**：将坐标转移到世界坐标系下，得到可用于建图的Lidar坐标，即修改transformTobeMapped的值；
	  2. **提取周围的关键帧**；
	  3. **下采样当前scan**：将当前各类点云降采样
	  4. **当前scan进行图优化过程**:根据现有地图与最新点云数据进行配准从而更新机器人精确位姿与融合建图，它分为角点优化、平面点优化、配准与更新等部分；
	  5. 保存关键帧和因子；
	  6. 校正位姿；
	  7. 发布Tf；
	  8. 发布关键位姿和帧数据；
	- ### 闭环检测
	  进行闭环检测和闭环修正
	  1. 进行闭环检测detectLoopClosure()
	  2. 使用icp迭代进行对齐。
	  3. 对齐之后判断迭代是否收敛以及噪声是否太大，是则返回并直接结束函数。否则进行迭代后的数据发布处理
	  4. 接得到latestSurfKeyFrameCloud和nearHistorySurfKeyFrameCloudDS之间的位置平移和旋转
	  5. 进行图优化过程
	- ### 可视化地图
	  1. 通过KDTree进行最近邻搜索;
	  2. 通过搜索得到的索引放进队列;
	  3. 通过两次下采样，减小数据量;
- ## transformFusion
  融合粗、精配准的里程计信息
- 参考文章
	- [LOAM(Lidar Odometry and Mapping)](https://leijiezhang001.github.io/LOAM/)