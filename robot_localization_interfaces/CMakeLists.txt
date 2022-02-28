cmake_minimum_required(VERSION 3.5)

project(robot_localization_interfaces)

find_package(builtin_interfaces REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(geographic_msgs REQUIRED)
find_package(diagnostic_msgs REQUIRED)

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()
if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

find_package(ament_cmake REQUIRED)
find_package(rosidl_default_generators REQUIRED)

set(srv_files
  "srv/FromLL.srv"
  "srv/GetState.srv"
  "srv/SetDatum.srv"
  "srv/SetPose.srv"
  "srv/ToggleFilterProcessing.srv"
  "srv/ToLL.srv"
)

rosidl_generate_interfaces(${PROJECT_NAME}
  ${srv_files}
  DEPENDENCIES
    builtin_interfaces
    geometry_msgs
    geographic_msgs
    diagnostic_msgs
  ADD_LINTER_TESTS
)

ament_export_dependencies(rosidl_default_runtime)

ament_package()