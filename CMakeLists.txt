cmake_minimum_required(VERSION 3.0.2)
project(relative_positional_controller)

find_package(catkin REQUIRED actionlib_msgs message_generation)

add_action_files(FILES
  RelativeMove.action
)

generate_messages(DEPENDENCIES actionlib_msgs)

catkin_package(CATKIN_DEPENDS actionlib_msgs message_runtime)

catkin_install_python(PROGRAMS
  nodes/relative_positional_controller
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)