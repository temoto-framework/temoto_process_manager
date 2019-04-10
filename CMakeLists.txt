cmake_minimum_required(VERSION 2.8.3)
project(temoto_er_manager)
add_compile_options(-std=c++11)

find_package(catkin REQUIRED
  roscpp
  roslib
  genmsg
  std_msgs
  temoto_core
)

add_service_files(
  FILES
  LoadExtResource.srv
)

generate_messages(
  DEPENDENCIES
  std_msgs
  temoto_core
)

catkin_package(
  INCLUDE_DIRS include
  CATKIN_DEPENDS temoto_core std_msgs roscpp roslib
)


include_directories(
  include
  ${catkin_INCLUDE_DIRS}
)

add_executable(temoto_er_manager src/temoto_er_manager.cpp
	                               src/temoto_er_manager_node.cpp
)
add_dependencies(temoto_er_manager ${catkin_EXPORTED_TARGETS} ${${PROJECT_NAME}_EXPORTED_TARGETS})
target_link_libraries( temoto_er_manager 
  ${catkin_LIBRARIES}
  temoto_core_components
)