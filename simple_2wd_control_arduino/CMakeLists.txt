cmake_minimum_required(VERSION 2.8.3)
project(simple_2wd_control_arduino)

find_package(catkin REQUIRED COMPONENTS
  rosserial_arduino
  rosserial_client
  simple_arduino_control_msgs
)

catkin_package()

rosserial_generate_ros_lib(
  PACKAGE rosserial_arduino
  SCRIPT make_libraries.py
)

rosserial_configure_client(
  DIRECTORY firmware
  TOOLCHAIN_FILE ${ROSSERIAL_ARDUINO_TOOLCHAIN}
)

rosserial_add_client_target(firmware controller ALL)
rosserial_add_client_target(firmware controller-upload)
