tags:: #毕业设计

- # 安装
  ```shell
  cd ~/catkin_ws/src/
  git clone https://github.com/ethz-asl/voxblox.git
  wstool init . ./voxblox/voxblox_https.rosinstall
  wstool update
  cd ~/catkin_ws/src/
  catkin build voxblox_ros
  ```
	- **编译失败的原因**
		- 没有用c++14编译，修改cmake
# 显示
```shell
source voxblox_ws/devel/setup.bash
rosmake voxblox_rviz_plugin
```