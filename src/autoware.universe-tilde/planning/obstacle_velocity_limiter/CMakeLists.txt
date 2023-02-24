cmake_minimum_required(VERSION 3.5)
project(obstacle_velocity_limiter)

find_package(autoware_cmake REQUIRED)
autoware_package()

find_package(PCL REQUIRED COMPONENTS common)
find_package(pcl_conversions REQUIRED)

ament_auto_add_library(obstacle_velocity_limiter_node SHARED
  DIRECTORY src
)

ament_target_dependencies(obstacle_velocity_limiter_node PCL tilde)
target_include_directories(obstacle_velocity_limiter_node
  SYSTEM PUBLIC
    "${PCL_INCLUDE_DIRS}"
)

# Disable warnings due to external dependencies
get_target_property(lanelet2_core_INCLUDE_DIR
  lanelet2_core::lanelet2_core INTERFACE_INCLUDE_DIRECTORIES
)

rclcpp_components_register_node(obstacle_velocity_limiter_node
  PLUGIN "obstacle_velocity_limiter::ObstacleVelocityLimiterNode"
  EXECUTABLE obstacle_velocity_limiter
)



ament_auto_package(
  INSTALL_TO_SHARE
    launch
    config
    script
)
