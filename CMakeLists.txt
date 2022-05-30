cmake_minimum_required(VERSION 3.10)
project(GstreamerStudy)

set(CMAKE_CXX_STANDARD 14)

set(CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/cmake/)

find_package(PkgConfig REQUIRED)

#using pkg-config to getting Gstreamer
pkg_check_modules(GSTREAMER REQUIRED gstreamer-1.0)

#including GStreamer header files directory
include_directories(
        ${GLIB_INCLUDE_DIRS}
        ${GSTREAMER_INCLUDE_DIRS}
)

#linking GStreamer library directory
link_directories(
        ${GLIB_LIBRARY_DIRS}
        ${GSTREAMER_LIBRARY_DIRS}
)
#
#pkg_search_module(GLIB REQUIRED glib-2.0)
#pkg_check_modules(GSTREAMER REQUIRED gstreamer-1.0)
#pkg_check_modules(GST_APP REQUIRED gstreamer-app-1.0)
#pkg_check_modules(GST_VIDEO REQUIRED gstreamer-video-1.0)
#
#target_include_directories(GstreamerStudy PRIVATE ${GST_INCLUDE_DIRS})
#target_link_libraries(GstreamerStudy ${GST_LIBRARIES})

#building target executable
add_executable(${PROJECT_NAME} simplePipeline.cpp)

#linking Gstreamer library with target executable
target_link_libraries(${PROJECT_NAME} ${GSTREAMER_LIBRARIES})