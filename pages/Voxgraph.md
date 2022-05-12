tags:: #毕业设计

- 基于[[Voxblox]]
- # 算法流程
	- ## VoxgraphMapper
		- 构造函数
			- getParametersFromRos：从ROS参数服务器中获取参数 [[ROS之参数服务]]
				- 子图创建的间隔
				- 网格可视化的间隔
				- ……
			- subscribeToTopics
			- advertiseTopics
			- advertiseServices
		- 回调函数
			- **pointcloudCallback**
				- 查找这个点云的时刻中机器人的姿势
				- 等待上一次位姿图优化完成
				- 将子图融入到地图中
				- 在单独的线程中优化位姿图