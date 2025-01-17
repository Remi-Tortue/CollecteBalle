cmake_minimum_required(VERSION 3.5)
project(bot_control)

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

####################################################################################################
# C++
####################################################################################################
# find dependencies
find_package(ament_cmake REQUIRED)
# find_package(rclcpp REQUIRED)
find_package(std_msgs REQUIRED)
find_package(sensor_msgs REQUIRED)
find_package(geometry_msgs REQUIRED)


####################################################################################################
# Python
####################################################################################################

find_package(ament_cmake_python REQUIRED)
find_package(rclpy REQUIRED)

# Installer les modules python custom comme roblib (dans le dossier $PROJECT_NAME
# ici package_template)
# ament_python_install_package(${PROJECT_NAME})


# Installer les executables pythons (dans le dossier scripts)
install(PROGRAMS
  src/brain.py
  DESTINATION lib/${PROJECT_NAME}
)
install(DIRECTORY
        launch
        DESTINATION share/${PROJECT_NAME})



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

# Install Python modules
# ament_python_install_package(${PROJECT_NAME})
ament_python_install_package(src)

# Install Python executables
install(PROGRAMS
  src/camera.py
  src/control_test.py
  src/arm_control.py
  src/joy_to_gazebo.py
  DESTINATION lib/${PROJECT_NAME}
)

# install(PROGRAMS
#   src/control_test.py
#   DESTINATION lib/${PROJECT_NAME}
# )
# install(PROGRAMS
#   src/arm_control.py
#   DESTINATION lib/${PROJECT_NAME}
# )

ament_package()
