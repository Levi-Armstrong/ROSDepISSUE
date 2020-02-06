cmake_minimum_required(VERSION 3.5.0)
project(catkin_pkg)

find_package(catkin REQUIRED COMPONENTS
  roscpp
)

find_package(opw_kinematics REQUIRED)

catkin_package(
#  INCLUDE_DIRS
#    include
#  LIBRARIES
#  CATKIN_DEPENDS
  DEPENDS
    opw_kinematics
)

# Create test executable
add_executable(${PROJECT_NAME}_node src/test.cpp)
set_target_properties(${PROJECT_NAME}_node PROPERTIES OUTPUT_NAME node PREFIX "")
target_link_libraries(${PROJECT_NAME}_node opw_kinematics::opw_kinematics)

install(
  TARGETS ${PROJECT_NAME}_node
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
