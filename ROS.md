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
   
