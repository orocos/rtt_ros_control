cmake_minimum_required(VERSION 2.8.6)

project(rtt_ros_control)

find_package(catkin REQUIRED
  COMPONENTS 
  rtt_ros 
  rtt_rosparam
  rtt_ros_tools
  rtt_sensor_msgs
  kdl_urdf_tools
  control_toolbox)

find_package(OROCOS-RTT REQUIRED)
find_package(orocos_kdl REQUIRED)
find_package(Eigen REQUIRED)

include(${OROCOS-RTT_USE_FILE_PATH}/UseOROCOS-RTT.cmake )

include_directories(
  ${catkin_INCLUDE_DIRS}
  ${USE_OROCOS_INCLUDE_DIRS}
  ${Eigen_INCLUDE_DIRS}
  ${orocos_kdl_INCLUDE_DIRS})
link_directories(
  ${catkin_LIBRARY_DIRS}
  ${orocos_kdl_LIBRARY_DIRS}
  ${USE_OROCOS_LIBRARY_DIRS})

orocos_component(${PROJECT_NAME}
  src/effort_controller_wrapper.cpp
  )

target_link_libraries(
  ${PROJECT_NAME}
  ${USE_OROCOS_LIBRARIES} 
  ${catkin_LIBRARIES})

orocos_generate_package()
