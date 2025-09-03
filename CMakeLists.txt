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
# Generate ROS messages, ROS2 interfaces and IDL files #
# ##############################################################################

# # get all msg files
# set(MSGS_DIR "${CMAKE_CURRENT_SOURCE_DIR}/msg")
# file(GLOB PX4_MSGS RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}" "${MSGS_DIR}/*.msg")

# # get all srv files
# set(SRVS_DIR "${CMAKE_CURRENT_SOURCE_DIR}/srv")
# file(GLOB PX4_SRVS RELATIVE "${CMAKE_CURRENT_SOURCE_DIR}" "${SRVS_DIR}/*.srv")

# set(PX4_MSGS
#   msg/VehicleOdometry.msg

#   # add only what you need…
# )

set(PX4_MSGS
  "ActuatorArmed.msg"
  "ActuatorInhibit.msg"
  "ActuatorControlsStatus.msg"
  "ActuatorMotors.msg"
  "ActuatorOutputs.msg"
  "BatteryStatus.msg"
  "FullState.msg"
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

# make them relative paths (NOT absolute)
list(TRANSFORM PX4_MSGS PREPEND "msg/") #transform px4_msgs variable by prepending the msg directory to all the msg files to avoid repeating msg/ before every .msg name above



# get only the srv files you want (or leave empty)
set(PX4_SRVS
  "srv/VehicleCommand.srv"
)

# Generate introspection typesupport for C and C++ and IDL files
rosidl_generate_interfaces(${PROJECT_NAME}
	${PX4_MSGS}
	${PX4_SRVS}
	DEPENDENCIES builtin_interfaces
	ADD_LINTER_TESTS
)

ament_export_dependencies(rosidl_default_runtime)

ament_package()
