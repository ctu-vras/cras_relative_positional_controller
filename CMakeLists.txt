cmake_minimum_required(VERSION 3.10.2)
project(cras_relative_positional_controller)

find_package(catkin REQUIRED COMPONENTS actionlib_msgs message_generation std_msgs)

add_action_files(FILES
  RelativeMove.action
)

generate_messages(DEPENDENCIES actionlib_msgs std_msgs)

catkin_package(CATKIN_DEPENDS actionlib_msgs message_runtime std_msgs)

catkin_install_python(PROGRAMS
  nodes/relative_positional_controller
  DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

if (CATKIN_ENABLE_TESTING)
  find_package(roslint REQUIRED)

  # catkin_lint - checks validity of package.xml and CMakeLists.txt
  # ROS buildfarm calls this without any environment and with empty rosdep cache,
  # so we have problems reading the list of packages from env
  # see https://github.com/ros-infrastructure/ros_buildfarm/issues/923
  if(DEFINED ENV{ROS_HOME})
      #catkin_lint: ignore_once env_var
      set(ROS_HOME "$ENV{ROS_HOME}")
  else()
      #catkin_lint: ignore_once env_var
      set(ROS_HOME "$ENV{HOME}/.ros")
  endif()

  #catkin_lint: ignore_once env_var
  if(DEFINED ENV{ROS_ROOT} AND EXISTS "${ROS_HOME}/rosdep/sources.cache")
      roslint_custom(catkin_lint -W2 .)
  endif()

  set(ROSLINT_PYTHON_OPTS "--max-line-length=120")
  roslint_python(
    nodes/relative_positional_controller
  )

  roslint_add_test()
endif()
