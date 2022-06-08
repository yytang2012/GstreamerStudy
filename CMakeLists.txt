cmake_minimum_required(VERSION 3.10)
project(GstreamerStudy)

set(CMAKE_CXX_STANDARD 14)

set(CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/cmake/)

find_package(PkgConfig REQUIRED)
# GTK
find_package(GTK REQUIRED)

#using pkg-config to getting Gstreamer
#pkg_check_modules(GSTREAMER REQUIRED gstreamer-1.0)
pkg_check_modules(GSTREAMER REQUIRED gstreamer-video-1.0)
pkg_check_modules(GTK REQUIRED gtk+-3.0)

#including GStreamer header files directory
include_directories(
        ${GLIB_INCLUDE_DIRS}
        ${GSTREAMER_INCLUDE_DIRS}
        ${GTK_INCLUDE_DIRS}
)

#linking GStreamer library directory
link_directories(
        ${GLIB_LIBRARY_DIRS}
        ${GSTREAMER_LIBRARY_DIRS}
        ${GTK_LIBRARY_DIRS}
)


#building target executable
add_executable(${PROJECT_NAME} tutorials/basic-tutorial-4.cpp)

#linking Gstreamer library with target executable
target_link_libraries(${PROJECT_NAME} ${GSTREAMER_LIBRARIES})
target_link_libraries(${PROJECT_NAME} ${GTK_LIBRARIES})

