cmake_minimum_required(VERSION 3.5.0)
project(ament_pkg)

find_package(ament_cmake REQUIRED)
find_package(opw_kinematics REQUIRED)

# Create test executable
add_executable(${PROJECT_NAME}_node src/test.cpp)
set_target_properties(${PROJECT_NAME}_node PROPERTIES OUTPUT_NAME node PREFIX "")
target_link_libraries(${PROJECT_NAME}_node opw_kinematics::opw_kinematics)

ament_package()

install(
  TARGETS ${PROJECT_NAME}_node
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION bin
)
