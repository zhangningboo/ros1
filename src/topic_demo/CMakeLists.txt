cmake_minimum_required(VERSION 3.0.2)
project(topic_demo)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
  geometry_msgs
  message_generation
)

add_message_files(
  FILES
  RobotInfo.msg
)

add_service_files(
  FILES
  SetTargetDetec.srv
)

generate_messages(
  DEPENDENCIES
  geometry_msgs 
  std_msgs
)

catkin_package(
  CATKIN_DEPENDS geometry_msgs roscpp rospy std_msgs message_runtime
)

include_directories(
  # include
  ${catkin_INCLUDE_DIRS}
)


add_executable(topic_pub src/topic_pub.cpp)
target_link_libraries(topic_pub ${catkin_LIBRARIES})
add_dependencies(topic_pub ${PROJECT_NAME}_generate_messages_cpp ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

add_executable(topic_sub src/topic_sub.cpp)
target_link_libraries(topic_sub ${catkin_LIBRARIES})
add_dependencies(topic_sub ${PROJECT_NAME}_generate_messages_cpp ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})


add_executable(service_server src/service_server.cpp)
target_link_libraries(service_server ${catkin_LIBRARIES})
add_dependencies(service_server ${PROJECT_NAME}_generate_messages_cpp ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

add_executable(service_client src/service_client.cpp)
target_link_libraries(service_client ${catkin_LIBRARIES})
add_dependencies(service_client ${PROJECT_NAME}_generate_messages_cpp ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

catkin_install_python(PROGRAMS
  scripts/topic_pub.py scripts/topic_sub.py scripts/service_server.py scripts/service_client.py
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
