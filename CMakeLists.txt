cmake_minimum_required(VERSION 2.8.3)
project(nav_pcontroller)


find_package(catkin REQUIRED COMPONENTS visualization_msgs roscpp roslib tf)


catkin_package(
  INCLUDE_DIRS
  LIBRARIES
  CATKIN_DEPENDS roscpp visualization_msgs
)

include_directories(include ${catkin_INCLUDE_DIRS})

add_executable(${PROJECT_NAME} src/nav_pcontroller.cc src/BaseDistance.cc)
target_link_libraries(${PROJECT_NAME} ${catkin_LIBRARIES})

add_executable(speed_filter src/speed_filter.cc src/BaseDistance.cc)
target_link_libraries(speed_filter ${catkin_LIBRARIES})


install(TARGETS ${PROJECT_NAME} speed_filter
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)


install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.h"
  PATTERN ".svn" EXCLUDE
)
