cmake_minimum_required(VERSION 3.0.2)
project(tf_demo)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
  geometry_msgs
  message_generation
  tf2
  tf2_ros
)

catkin_package(
  CATKIN_DEPENDS geometry_msgs roscpp rospy std_msgs message_runtime
)

include_directories(
  # include
  ${catkin_INCLUDE_DIRS}
)

add_executable(tf_pub src/tf_pub.cpp)
target_link_libraries(tf_pub ${catkin_LIBRARIES})
add_dependencies(tf_pub ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

add_executable(tf_listen src/tf_listen.cpp)
target_link_libraries(tf_listen ${catkin_LIBRARIES})
add_dependencies(tf_listen ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

# Mark executable scripts (Python etc.) for installation
catkin_install_python(PROGRAMS
  scripts/tf_pub.py scripts/tf_listen.py
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)