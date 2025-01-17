cmake_minimum_required(VERSION 3.16)
project(my_arac LANGUAGES CXX)

if(CMAKE_CXX_COMPILER_ID MATCHES "(GNU|Clang)")
  add_compile_options(-Wall -Wextra)
endif()

# set the same behavior for windows as it is on linux
set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS ON)

# find dependencies
set(THIS_PACKAGE_INCLUDE_DEPENDS
  pluginlib
  rclcpp
  rclcpp_lifecycle
)

# find dependencies
find_package(backward_ros REQUIRED)
find_package(ament_cmake REQUIRED)
foreach(Dependency IN ITEMS ${THIS_PACKAGE_INCLUDE_DEPENDS})
  find_package(${Dependency} REQUIRED)
endforeach()

# INSTALL
install(
  DIRECTORY description/launch description/ros2_control description/urdf
  DESTINATION share/my_arac
)
install(
  DIRECTORY bringup/launch bringup/config
  DESTINATION share/my_arac
)

if(BUILD_TESTING)
  find_package(ament_cmake_pytest REQUIRED)
endif()

## EXPORTS
ament_export_dependencies(${THIS_PACKAGE_INCLUDE_DEPENDS})
ament_package()
