tags:: #ROS

- # 命名空间
	- ROS中的命名空间类似于C++，主要是为了避免命名冲突
	- 添加命名空间
		- 通过 `rosrun rospkg ros_node ns:=/home/user1` 将节点放到命名空间`/home/user`下
		- 通过<group>标签的ns属性添加命名空间
		  ```xml
		  <group ns="A"></group>
		  ```
	- 名称分类
		- 基本名称
			- name
			- 没有命名空间限定符的相对名称
		- 相对名称
		- relative/name
			- 依赖默认命名空间
			  id:: 62722c2d-1ada-4bda-804f-2bc68e6d9ae7
		- 全局名称
			- /global/name
			- 属于全局命名空间
		- 私有名称
			- ~private/name
			- 它的解析不依赖与默认命名空间，而是依赖包名称
		- 示例
		- |*Node*|*Relative (default)*|*Global	Private*|*Private*|
		  |/node1|bar -> /bar|/bar -> /bar|~bar -> /node1/bar|
		  |/wg/node2|bar -> /wg/bar|/bar -> /bar|~bar -> /wg/node2/bar|
		  |/wg/node3	|foo/bar -> /wg/foo/bar|/foo/bar -> /foo/bar|~foo/bar -> /wg/node3/foo/bar|
- # 重映射
	- 给节点或者话题起别名
	- 通过 `rosrun rospkg ros_node __name:=A` 将节点重映射为A
	- 通过<remap>标签进行重映射
	  ```xml
	  <remap from="ns1" to="ns2"/><!-- 更改命名空间 -->
	  <remap from="topic1" to="topic2"/><!-- 更改topic名称 -->
	  ```
	-
- # 句柄
	- 创建节点句柄nh时，指明了它的命名空间
	- Nodeandle nh("node")
	  这个节点里的所有的参数，话题前面都在/node下
- 参考博客
	- [ROS之命名空间](https://blog.csdn.net/u014587147/article/details/75647002)
	- [ROS学习 之 命名空间（NameSpace）、重映射（Remapping）、名称（Names）](https://blog.csdn.net/jrc_january/article/details/76587630)
	- [ROS中的命名空间;句柄;重映射](https://zhuanlan.zhihu.com/p/135310435)
	- [动手学ROS（6）：命名空间之group与remap](https://www.guyuehome.com/34830)