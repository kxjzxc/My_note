- # 类
	- ## VoxelGrid
		- 通过输入的点云数据创建一个三维体素栅格，在每个体素(三维立方体)里面，求取该立方体内的所有点云重心点来代表这个立方体的表示，以此达到下采样的目的
		- |*函数接口*|*接口功能*|
		  |setLeafSize |设置每个体素的大小|
		  |getLeafSize |获取每个体素的大小|
		  |setDownsampleAllData |设置下采样的维度|
		  |getDownsampleAllDatas |获取每个体素的大小|
		  |setInputCloud |设置输入点云|
		  |filter|执行过滤|
	- ## KdTreeFLANN
		- 一种使用kD树结构的通用3D空间定位器
		- |*函数接口*|*接口功能*|
		  |nearestKSearch | 搜索给定查询点的k近邻 |
- # 常用函数
	- |*函数名*|*函数功能*|
	  |removeNaNFromPointCloud|去除无效点|
	-