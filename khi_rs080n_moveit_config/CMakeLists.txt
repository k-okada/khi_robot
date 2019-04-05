cmake_minimum_required(VERSION 2.8.3)
project(khi_rs080n_moveit_config)

find_package(catkin REQUIRED)

catkin_package()

install(DIRECTORY launch DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
  PATTERN "setup_assistant.launch" EXCLUDE)
install(DIRECTORY config DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION})

if(CATKIN_ENABLE_TESTING)
  find_package(catkin REQUIRED COMPONENTS rostest roslaunch)
  file(GLOB LAUNCH_FILES RELATIVE ${CMAKE_CURRENT_SOURCE_DIR}/launch/ *.launch)
  message("===> ${LAUNCH_FILES}")
  list(REMOVE_ITEM LAUNCH_FILES setup_assistant.launch joystick_control.launch run_benchmark_ompl.launch default_warehouse_db.launch)
  message("===> ${LAUNCH_FILES}")
  foreach(LAUNCH_FILE ${LAUNCH_FILES})
    message(status "Testing ${LAUNCH_FILE}")
    roslaunch_add_file_check(launch/${LAUNCH_FILE})
  endforeach()
endif()
