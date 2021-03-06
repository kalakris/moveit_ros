cmake_minimum_required(VERSION 2.8.3)
project(moveit_ros_perception)

if(NOT CMAKE_CONFIGURATION_TYPES AND NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release)
endif()

find_package(Eigen REQUIRED)
find_package(Boost REQUIRED thread signals)
find_package(catkin REQUIRED COMPONENTS
  moveit_core
  roscpp
  rosconsole
  urdf
  message_filters
  tf
  tf_conversions
  pcl_ros
)

find_package(octomap REQUIRED)

catkin_package(
  INCLUDE_DIRS
    robot_self_filter/include
    occupancy_map_monitor/include
    ${OCTOMAP_INCLUDE_DIRS}
  LIBRARIES  
    moveit_robot_self_filter
    moveit_occupancy_map_monitor
    ${OCTOMAP_LIBRARIES}
  CATKIN_DEPENDS
    moveit_core)

include_directories(robot_self_filter/include
                    occupancy_map_monitor/include
                    ${catkin_INCLUDE_DIRS} 
                    )
include_directories(SYSTEM
                    ${EIGEN_INCLUDE_DIRS}
                    ${Boost_INCLUDE_DIRS}
                    )

link_directories(${Boost_LIBRARY_DIRS})
link_directories(${catkin_LIBRARY_DIRS})

add_subdirectory(robot_self_filter)
add_subdirectory(occupancy_map_monitor)
