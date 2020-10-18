cmake_minimum_required(VERSION 2.6 FATAL_ERROR)
project(activity_detection)
set( CMAKE_CXX_FLAGS "-std=c++11" )
set( BOOST_ROOT "/home/romero/libs/boost-1.50.0" CACHE PATH "Boost library path" )
set( Boost_INCLUDE_DIR "/home/romero/libs/boost-1.50.0/include" )
include_directories(${Boost_INCLUDE_DIR})
find_package(PCL 1.7.2 REQUIRED COMPONENTS common io search kdtree features surface PATHS /home/romero/libs/pcl-1.7.2 NO_DEFAULT_PATH)
include_directories(${PCL_INCLUDE_DIRS})
link_directories(${PCL_LIBRARY_DIRS})
add_definitions(${PCL_DEFINITIONS})

set(CMAKE_BUILD_TYPE Debug)



FIND_PACKAGE( OpenCV REQUIRED PATHS /home/romero/libs/opencv-2.4.13.6/share/OpenCV NO_DEFAULT_PATH )


add_executable (segment src/get_skel_segments.cpp)
add_executable (extractOPC src/extractObjectPointclouds.cpp)
add_executable (featgenSeg src/featureGenerationForSegments.cpp)
add_executable (frameFeatgen src/featureGenerationForFrames.cpp)
#add_executable (skelViewer src/skeletonViewer.cpp)
add_executable (getTraj src/getObjHandTrajectories.cpp)


TARGET_LINK_LIBRARIES(segment ${PCL_LIBRARIES})
TARGET_LINK_LIBRARIES(extractOPC ${PCL_LIBRARIES} ${OpenCV_LIBS})
TARGET_LINK_LIBRARIES(featgenSeg ${PCL_LIBRARIES} ${OpenCV_LIBS})
TARGET_LINK_LIBRARIES(frameFeatgen ${PCL_LIBRARIES} ${OpenCV_LIBS})
#TARGET_LINK_LIBRARIES(skelViewer ${PCL_LIBRARIES})
TARGET_LINK_LIBRARIES(getTraj ${PCL_LIBRARIES} ${OpenCV_LIBS})
#TARGET_LINK_LIBRARIES(segment ${PCL_LIBRARIES}  ${OpenCV_LIBS})
