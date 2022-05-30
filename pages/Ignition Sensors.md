tags:: #ROS

- # 介绍
	- > Ignition Senors is an open source library that provides a set of sensor and noise models accessible through a C++ interface. The goal of Ignition Sensors is to generate realistic sensor data suitable for use in robotic applications and simulation. The code behind Ignition Sensors was originally developed as a suite of sensor models internal to Gazebo. With the addition of some refactoring, the high-quality sensor models previously contained within Gazebo are now available for use in your next project without encumbering you with a complete simulation system.
	- Ignition Sensors是一个开源库，提供了一组可通过C++接口访问的传感器和噪声模型。点火传感器的目标是生成适合机器人应用和仿真的真实传感器数据。点火传感器背后的代码最初是作为Gazebo内部的一套传感器模型开发的。通过添加一些重构，Gazebo中先前包含的高质量传感器模型现在可以在您的下一个项目中使用，而无需使用完整的仿真系统。
- # 安装
	- ## Ubuntu
		- ### 二进制安装
			- 1. Setup your computer to accept software from packages.osrfoundation.org:
			  ```bash
			  sudo sh -c 'echo "deb http://packages.osrfoundation.org/gazebo/ubuntu-stable `lsb_release -cs` main" > /etc/apt/sources.list.d/gazebo-stable.list'
			  wget http://packages.osrfoundation.org/gazebo.key -O - | sudo apt-key add -
			  sudo apt-get update
			  ```
			- Install Ignition Sensors
			  ```bash
			  # Change <#> to a version number, like 3 or 4 lastest is 6
			  sudo apt install libignition-sensors<#>-dev
			  sudo apt install libignition-common<#>-dev
			  ```
- # 自定义传感器
-
- 参考文章
	- [Tutorials](https://gazebosim.org/api/sensors/6.0/tutorials.html)
	-