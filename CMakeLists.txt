cmake_minimum_required(VERSION 3.5)

project(px4_msgs)

list(INSERT CMAKE_MODULE_PATH 0 "${CMAKE_CURRENT_SOURCE_DIR}/cmake")

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
	add_compile_options(-Wall -Wextra)
endif()

find_package(ament_cmake REQUIRED)
find_package(builtin_interfaces REQUIRED)
find_package(rosidl_default_generators REQUIRED)

# ##############################################################################
# Generate ROS messages, ROS2 interfaces and IDL files
# ##############################################################################

# Define the limited set of messages you need
set(PX4_MSGS
  "ActuatorArmed.msg"
  # "ActuatorInhibit.msg"
  "ActuatorControlsStatus.msg"
  "ActuatorMotors.msg"
  "ActuatorOutputs.msg"
  "BatteryStatus.msg"
  # "FullState.msg"
  "OffboardControlMode.msg"
  "RcChannels.msg"
  "TrajectorySetpoint.msg"
  "VehicleCommand.msg"
  "VehicleCommandAck.msg"
  "VehicleControlMode.msg"
  "VehicleGlobalPosition.msg"
  "VehicleLocalPosition.msg"
  "VehicleRatesSetpoint.msg"
  "VehicleStatus.msg"
  "VehicleThrustSetpoint.msg"
  "VehicleTorqueSetpoint.msg"
  "VehicleOdometry.msg"
)

# Make paths relative to msg/ directory
list(TRANSFORM PX4_MSGS PREPEND "msg/")

# Get all srv files (auto-discover from srv directory)
set(SRVS_DIR "${CMAKE_CURRENT_SOURCE_DIR}/srv")
file(GLOB PX4_SRVS RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}" "${SRVS_DIR}/*.srv")

# Generate introspection typesupport for C and C++ and IDL files
rosidl_generate_interfaces(${PROJECT_NAME}
	${PX4_MSGS}
	${PX4_SRVS}
	DEPENDENCIES builtin_interfaces
	ADD_LINTER_TESTS
)

ament_export_dependencies(rosidl_default_runtime)

ament_package()
