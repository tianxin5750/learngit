1. Topic 异步通讯   [多对多]  [publish/subscribe]   [talker/listener]
   Service 同步通讯   [server/client]   [一对多]
   参数通讯(动态param更新)

2. 文件系统 ---- 元功能包 ---- 功能包 ---- 功能包清单  消息类型  服务类型  代码  other
bin 可执行程序    include 代码头文件    lib 可执行文件/程序/节点
share 功能包/cmake配置文件/msg接口文件/service接口定义/接口具体信息/action

3. CMakeList.txt
   find_package(catkin REQUIRED COMPONENTS roscpp rospy std_msgs message_generation actionlib actionlib_msgs)    [声明编译本包所需的其他ROS包]
   add_message_files(FILES ...)
   add_service_files(FILES ...)
   add_action_files(DIRECTORY ... FILES ...)
   generate_message(DEPENDENCIES std_msgs actionlib_msgs)
   catkin_package(CATKIN_DEPENDS roscpp rospy std_msgs message_runtime)  [声明依赖本包同时需要的其他ros包]
   add_executable(talker src/talker.cpp)    [声明编译本包生成的可执行文件]
   target_link_libraries(talker ${catkin_LIBRARIES})   [链接可执行文件和依赖库]
   add_dependencies(${PROJECT_NAME}_node ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

4.package.xml    每个包的描述文件，都需要放置在包的根目录下，对包的名字/版本/作者/维护者/依赖关系进行说明
  <build_depend>message_generation</build_depend>
  <exec_depend>message_runtime</exec_depend>
  <build_depend>actionlib</build_depend>
  <build_depend>actionlib_msgs</build_depend>
  <exec_depend>actionlib</exec_depend>
  <exec_depend>actionlib_msgs</exec_depend>

5. ros的C++程序编译
   安装ros 
   创建程序空间 mkdir -p ~/catkin_ws/src       cd ~/catkin_ws/src      catkin_init_workspace
   将ros用户自己的工程目录配置到bash/zsh中 gedit ~./zshrc   最后一行加入export ROS_PACKAGE_PATH=~/catkin_ws:$ROS_PACKAGE_PATH       source /home/ann/catkin_ws/devel/setup.zsh
   基于catkin创建自己的ros包  cd ~/catkin_ws/src     catkin_create_pkg beginner_tutorials std_msgs rospy roscpp
   创建源代码 -> 编写.cpp文件 -> 修改编译CMakeLists.txt package.xml -> catkin_make 
 
6. action
   一种问答通信机制；带有连续反馈；可以在任务过程中止运行；基于ROS的消息机制实现  
   action接口  goal发布任务目标   cancel请求取消任务   ##客户端 -> 服务器
   status通知客户端当前的状态   feedback周期反馈任务运行的监控数据   result向客户端发送任务的执行结果，只发布一次   ##服务器 -> 客户端
   
   #define the goal
   uint32 dishwasher_id
   ---
   #define the result
   uint32 total_dishes_cleaned
   ---
   #define a feedback message
   float32 percent_complete

   动作服务器实现：
       初始化ROS节点 -> 创建动作服务器实例 -> 启动服务器，等待动作请求 -> 在回调函数中完成动作服务功能的处理，
            并反馈进度信息 -> 动作完成，发送结束信息

   动作客户端实现：
       初始化ROS节点 -> 创建动作客户端实例 -> 连接动作服务器 -> 发送动作目标 -> 根据不同的服务器端反馈处理回调函数

7. 分布式通信
   ROS是一种**分布式**软件框架，节点之间通过**松耦合**的方式进行组合
      设置IP地址，确保底层链路的联通（通过hosts）    ping命令测试网络是否联通
      在从机端设置ROS_MASTER_URI，让从机找到ROS_Master       export ROS_MASTER_URI=http://hcx-pc:11311(当前终端有效)
          echo "export ROS_MASTER_URI=http://hcx-pc:11311" >> ~/.bzshrc  (所有终端有效)

8. launch文件
   Launch文件：通过XML文件实现多节点的配置启动（可以自动启动ROS Master)
   
   启动节点   <node pkg="package-name" type="executable-name" name="node-name" />    
      pkg:节点所在的功能包名称   type:节点的可执行文件名称  name:节点运行时的名称   output  respawn required ns args
   
   参数设置   <param name="output_frame" value="odom" />   设置ROS系统运行中的参数，存储在参数服务器中
      name:参数名   value:参数值
      加载参数文件中的多个参数   <rosparam file="params.yaml" command="load" ns="params" />
   
   <arg> launch文件内部的局部变量，仅限于launch文件使用
      <arg name="arg-name" default="arg-value" />      name:参数名   value:参数值

   重映射ROS计算图资源的命名
      <remap from="/turtlebot/cmd_vel" to="/cmd_vel" />    from:原命名  to:映射之后的命名

   <include>包含其他launch文件，类似C语言中的头文件包含
       <include file="$(dirname)/other.launch" />       file:包含的其他launch文件路径
 
9. TF坐标变换
   定义TF广播器
   创建坐标变换值
   发布坐标变换

10. 实现TF监听器
    定义TF监听器
    查找坐标变换

11. Qt工具箱
    rqt_console    日志输出工具
    rqt_graph      计算图可视化工具
    rqt_plot       数据绘图工具
    rqt_reconfigure参数动态配置工具

12. Rviz可视化平台

13. Gazebo物理仿真环境

