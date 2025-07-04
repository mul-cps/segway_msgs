cmake_minimum_required(VERSION 3.5)
project(segway_msgs)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fpic")
set(CMAKE_C_FLAGS   "${CMAKE_C_FLAGS}   -fpic")
# Default to C99
if(NOT CMAKE_C_STANDARD)
  set(CMAKE_C_STANDARD 99)
endif()

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(std_msgs REQUIRED)
####find_package(builtin_interface REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(rosidl_default_generators REQUIRED)
find_package(action_msgs REQUIRED)

set(msg_files
  "msg/BmsFb.msg"
  "msg/ChassisCtrlSrcFb.msg"
  "msg/ChassisMileageMeterFb.msg"
  "msg/ChassisModeFb.msg"
  "msg/ErrorCodeFb.msg"
  "msg/MotorWorkModeFb.msg"
  "msg/SpeedFb.msg"
  "msg/TicksFb.msg"
)

set(srv_files
  "srv/ChassisSendEvent.srv"
  "srv/RosGetChargeMosCtrlStatusCmd.srv"
  "srv/RosGetLoadParamCmd.srv"
  "srv/RosGetSwVersionCmd.srv"
  "srv/RosGetVelMaxFeedbackCmd.srv"
  "srv/RosSetChargeMosCtrlCmd.srv"
  "srv/RosSetChassisEnableCmd.srv"
  "srv/RosSetChassisPoweroffCmd.srv"
  "srv/RosSetLoadParamCmd.srv"
  "srv/RosSetRemovePushCmd.srv"
  "srv/RosSetVelMaxCmd.srv")

set(action_files
  "action/RosSetIapCmd.action"
)
rosidl_generate_interfaces(${PROJECT_NAME}
  ${msg_files}
  ${srv_files}
  ${action_files}
  DEPENDENCIES  geometry_msgs std_msgs ADD_LINTER_TESTS)

# ament_export_dependencies(rosidl_default_generators)
ament_export_dependencies(rosidl_default_runtime)
# ament_export_include_directories(include)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # the following line skips the linter which checks for copyrights
  # uncomment the line when a copyright and license is not present in all source files
  #set(ament_cmake_copyright_FOUND TRUE)
  # the following line skips cpplint (only works in a git repo)
  # uncomment the line when this package is not in a git repo
  #set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
