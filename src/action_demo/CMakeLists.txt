cmake_minimum_required(VERSION 3.0.2)
project(action_demo)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
  geometry_msgs
  message_generation
  actionlib_msgs
  actionlib
)

add_action_files(
  FILES
  PickupPlace.action
)

generate_messages(
  DEPENDENCIES
  geometry_msgs
  std_msgs
  actionlib_msgs
)

catkin_package(
  CATKIN_DEPENDS geometry_msgs roscpp rospy std_msgs message_runtime
)

include_directories(
  # include
  ${catkin_INCLUDE_DIRS}
)

add_executable(action_server src/action_server.cpp)
target_link_libraries(action_server ${catkin_LIBRARIES})
add_dependencies(action_server ${PROJECT_NAME}_generate_messages_cpp ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

add_executable(action_client src/action_client.cpp)
target_link_libraries(action_client ${catkin_LIBRARIES})
add_dependencies(action_client ${PROJECT_NAME}_generate_messages_cpp ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

catkin_install_python(PROGRAMS
  scripts/action_server.py scripts/action_client.py
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
