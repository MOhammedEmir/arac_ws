cmake_minimum_required(VERSION 3.5)
project(arac_urdf)

find_package(ament_cmake REQUIRED)


install(
  DIRECTORY arac/urdf arac/rviz
  DESTINATION share/${PROJECT_NAME}/carlikebot
)



ament_package()
