tags:: #CARLA

- # SemanticLidar 属性
	- |*蓝图属性*|*类型 *|*默认*|*描述*|
	  |channels|int|32|激光扫描线数|
	  |range|float|10.0|以米为单位测量/射线投射的最大距离|
	  |points_per_second|int|	56000|每秒所有激光产生的点数|
	  |rotation_frequency|float|10.0|激光雷达旋转频率|
	  |upper_fov|float|10.0|最高激光的角度|
	  |lower_fov|float|	-30.0|最低激光的角度（度数）|
	  |horizontal_fov |float|360.0|以度为单位的水平视野，0 - 360|
	  |sensor_tick|float|0.0|传感器捕获（滴答声）之间的模拟秒数|
- # 输出属性
	- |*传感器数据属性*|*类型*|*描述*|
	  |frame|int|进行测量时的帧数|
	  |timestamp |double|自剧集开始以来的测量模拟时间（以秒为单位）|
	  |transform |carla.Transform|测量时传感器在世界坐标中的位置和旋转|
	  |horizontal_angle|float|当前帧中激光雷达的 XY 平面中的角度（弧度）|
	  |channels|int|激光雷达的通道数（激光器）|
	  |get_point_count(channel) |int|当前帧中捕获的每个通道的点数|
	  |raw_data|bytes|包含具有实例和语义信息的点云的数组|
		- raw_data包含以下内容
			- |*参数*|*类型*|*描述*|
			  |(x,y,z)|float|XYZ 坐标|
			  |CosAngle|float|入射角的余弦|
			  |ObjIdx|包含该点的对象命中的索引|uint32_t|
			  |ObjIdx|包含个该点的对象的语义标签|uint32_t|