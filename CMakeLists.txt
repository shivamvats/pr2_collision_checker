# Catkin User Guide: http://www.ros.org/doc/groovy/api/catkin/html/user_guide/user_guide.html
# Catkin CMake Standard: http://www.ros.org/doc/groovy/api/catkin/html/user_guide/standards.html
cmake_minimum_required(VERSION 2.8.3)
project(pr2_collision_checker)
# Load catkin and all dependencies required for this package
# TODO: remove all from COMPONENTS that are not catkin packages.
find_package(catkin REQUIRED COMPONENTS roscpp tf tf_conversions kdl arm_navigation_msgs leatherman sbpl_manipulation_components sbpl_geometry_utils pviz trajectory_msgs geometry_msgs message_filters pr2_arm_kinematics)

# catkin_package parameters: http://ros.org/doc/groovy/api/catkin/html/dev_guide/generated_cmake_api.html#catkin-package
# TODO: fill in what other packages will need to use this package
catkin_package(
    DEPENDS roscpp tf tf_conversions kdl     
    CATKIN_DEPENDS arm_navigation_msgs leatherman sbpl_manipulation_components sbpl_geometry_utils pviz trajectory_msgs geometry_msgs message_filters pr2_arm_kinematics
    INCLUDE_DIRS include ${catkin_INCLUDE_DIRS}# TODO include
    LIBRARIES ${catkin_LIBRARIES}# TODO
)
# include_directories(include ${Boost_INCLUDE_DIR} ${catkin_INCLUDE_DIRS})
# CATKIN_MIGRATION: removed during catkin migration
# cmake_minimum_required(VERSION 2.4.6)

# CATKIN_MIGRATION: removed during catkin migration
# include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)

# Set the build type.  Options are:
#  Coverage       : w/ debug symbols, w/o optimization, w/ code-coverage
#  Debug          : w/ debug symbols, w/o optimization
#  Release        : w/o debug symbols, w/ optimization
#  RelWithDebInfo : w/ debug symbols, w/ optimization
#  MinSizeRel     : w/o debug symbols, w/ optimization, stripped binaries
set(ROS_BUILD_TYPE RelWithDebInfo)


# CATKIN_MIGRATION: removed during catkin migration
# rosbuild_init()

#set the default path for built executables to the "bin" directory
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)
include_directories(include ${catkin_INCLUDE_DIRS})

add_library(pr2_collision_checker src/sbpl_arm_model.cpp
                                           src/pr2_collision_space.cpp
                                           src/pr2_collision_space_interface.cpp
                                           src/pr2_collision_space_monitor.cpp)
target_link_libraries(pr2_collision_checker leatherman sbpl_manipulation_components pviz ${catkin_LIBRARIES})

#add_executable(testVoxelizer src/test_voxelizer.cpp)
#target_link_libraries(testVoxelizer pr2_collision_checker leatherman)

