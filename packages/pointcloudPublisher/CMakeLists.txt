##############################################################################
# Rosbuild2
##############################################################################

if(ROSBUILD)
  include(rosbuild.cmake OPTIONAL)
  return()
endif()

##############################################################################
# CMake
##############################################################################

cmake_minimum_required(VERSION 2.4.6)

ADD_DEFINITIONS(-DQT_NO_KEYWORDS)

##############################################################################
# Ros Initialisation
##############################################################################

include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)

# EIGEN
find_package(Eigen REQUIRED)
include_directories(${Eigen_INCLUDE_DIRS})

rosbuild_init()
#NOTE: Added to build messages
#rosbuild_genmsg()

#set the default path for built executables to the "bin" directory
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

# Set the build type.  Options are:
#  Coverage       : w/ debug symbols, w/o optimization, w/ code-coverage
#  Debug          : w/ debug symbols, w/o optimization
#  Release        : w/o debug symbols, w/ optimization
#  RelWithDebInfo : w/ debug symbols, w/ optimization
#  MinSizeRel     : w/o debug symbols, w/ optimization, stripped binaries
#set(ROS_BUILD_TYPE Debug)

##############################################################################
# Binaries
##############################################################################
include_directories(include/pointcloudPublisher/)

rosbuild_add_executable(pointcloudPublisher src/pointcloudPublisher.cpp
                                            src/pointcloud_utils.cpp)
rosbuild_add_boost_directories()
target_link_libraries(pointcloudPublisher boost_system boost_filesystem boost_signals)

rosbuild_link_boost(pointcloudPublisher thread signals system)

