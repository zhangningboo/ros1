cmake_minimum_required(VERSION 3.0.2)
project(joint_state_demo)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  sensor_msgs
  std_msgs
  tf
)


catkin_package(
  # CATKIN_DEPENDS roscpp rospy std_msgs message_runtime
)

include_directories(
  # include
  ${catkin_INCLUDE_DIRS}
)

add_executable(joint_states_pub src/joint_states_pub.cpp)
target_link_libraries(joint_states_pub ${catkin_LIBRARIES})
add_dependencies(joint_states_pub ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

catkin_install_python(PROGRAMS
  scripts/joint_states_pub.py
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
