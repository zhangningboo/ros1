cmake_minimum_required(VERSION 3.0.2)
project(marker_demo)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
  geometry_msgs
  message_generation
  dynamic_reconfigure
)

generate_dynamic_reconfigure_options(
    cfg/PubMarker.cfg
)

catkin_package(
  CATKIN_DEPENDS geometry_msgs roscpp rospy std_msgs message_runtime
)

include_directories(
  # include
  ${catkin_INCLUDE_DIRS}
)

add_executable(pub_marker src/pub_marker.cpp)
target_link_libraries(pub_marker ${catkin_LIBRARIES})
add_dependencies(pub_marker ${PROJECT_NAME}_gencfg ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

catkin_install_python(PROGRAMS
  scripts/pub_marker.py
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
