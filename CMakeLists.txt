cmake_minimum_required(VERSION 2.8.3)
project(wit-imu-driver)

## Compile as C++11, supported in ROS Kinetic and newer
add_compile_options(-std=c++11 -O3)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS
    roscpp
    std_msgs
    serial
    sensor_msgs
)

catkin_package(
#  INCLUDE_DIRS include
#  LIBRARIES serial
 CATKIN_DEPENDS roscpp
 serial
 sensor_msgs
#  DEPENDS system_lib
)

include_directories(
include
${catkin_INCLUDE_DIRS}
)

add_executable(${PROJECT_NAME}_node src/wit_imu_node.cpp src/JY901.cpp)

message(${catkin_LIBRARIES})
target_link_libraries(${PROJECT_NAME}_node
  ${catkin_LIBRARIES}
)

install(TARGETS ${PROJECT_NAME}_node
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(DIRECTORY launch
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)
