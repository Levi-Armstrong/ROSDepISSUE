cmake_minimum_required(VERSION 3.5.0)
project(cmake_pkg)

find_package(opw_kinematics REQUIRED)

# Create test executable
add_executable(${PROJECT_NAME}_node src/test.cpp)
set_target_properties(${PROJECT_NAME}_node PROPERTIES OUTPUT_NAME node PREFIX "")
target_link_libraries(${PROJECT_NAME}_node opw_kinematics::opw_kinematics)

install(
  TARGETS ${PROJECT_NAME}_node
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION bin
)

# Create an ament_index resource file to allow ROS2 ament_index_cpp to locate the installed path to this package.
# This is a workaround to let the ROS2 version of pluginlib find tesseract_collision's plugins, since tesseract_collision is a non-ROS CMake package.
# ADDITIONAL REQUIREMENT: The installed path must be added to the AMENT_PREFIX_PATH environment variable at runtime, which is outside the scope of CMakeLists.txt.
file(WRITE ${CMAKE_INSTALL_PREFIX}/share/ament_index/resource_index/packages/${PROJECT_NAME} "")
file(WRITE ${CMAKE_INSTALL_PREFIX}/share/${PROJECT_NAME}/hook/ament_prefix_path.dsv "prepend-non-duplicate;AMENT_PREFIX_PATH;")
file(APPEND ${CMAKE_INSTALL_PREFIX}/share/${PROJECT_NAME}/package.dsv "source;share/${PROJECT_NAME}/hook/ament_prefix_path.dsv")
