cmake_minimum_required(VERSION 3.10)
project(GstreamerStudy)

set(CMAKE_CXX_STANDARD 14)
set(CUDA_VER 11.4)
set(NVDS_VERSION 6.0)

set(CMAKE_CXX_FLAGS “-Wall -g”)

set(CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/cmake/)

find_package(PkgConfig REQUIRED)
# GTK
find_package(GTK REQUIRED)

find_package(CUDA REQUIRED)

#using pkg-config to getting Gstreamer
pkg_check_modules(GSTREAMER REQUIRED gstreamer-1.0)
#
#pkg_check_modules(GSTREAMER-APP REQUIRED gstreamer-app-1.0)
#pkg_check_modules(GSTREAMER-AUDIO REQUIRED gstreamer-audio-1.0)
#pkg_check_modules(GSTREAMER-PBUTILS REQUIRED gstreamer-pbutils-1.0)
#pkg_check_modules(GSTREAMER-FFT REQUIRED gstreamer-fft-1.0)
pkg_check_modules(GSTREAMER-VIDEO REQUIRED gstreamer-video-1.0)
pkg_check_modules(GTK REQUIRED gtk+-3.0)

#including GStreamer header files directory
include_directories(
        ${GLIB_INCLUDE_DIRS}
        ${GSTREAMER_INCLUDE_DIRS}
        ${GTK_INCLUDE_DIRS}
        /usr/local/cuda-${CUDA_VER}/include
        /usr/local/cuda-${CUDA_VER}/targets/x86_64-linux/include
        /opt/nvidia/deepstream/deepstream-6.0/sources/includes

)

#linking GStreamer library directory
link_directories(
        ${GLIB_LIBRARY_DIRS}
        ${GSTREAMER_LIBRARY_DIRS}
        ${GTK_LIBRARY_DIRS}
#        ${GSTREAMER-APP_LIBRARY_DIRS}
#        ${GSTREAMER-AUDIO_LIBRARY_DIRS}
#        ${GSTREAMER-PBUTILS_LIBRARY_DIRS}
#        ${GSTREAMER-FFT_LIBRARY_DIRS}
#        ${GSTREAMER-VIDEO_LIBRARY_DIRS}
#        ${GSTREAMER-BASE_LIBRARY_DIRS}
        /opt/nvidia/deepstream/deepstream-${NVDS_VERSION}/lib/
        /usr/local/cuda-${CUDA_VER}/lib64/
)


#building target executable
add_executable(${PROJECT_NAME} deepstream/deepstream-yolov3-test1/deepstream_yolov3_test1_app.c)

#linking Gstreamer library with target executable
target_link_libraries(
        ${PROJECT_NAME}
        ${GSTREAMER_LIBRARIES}
        ${GTK_LIBRARIES}
#        ${GSTREAMER-APP_LIBRARIES}
#        ${GSTREAMER-AUDIO_LIBRARIES}
#        ${GSTREAMER-PBUTILS_LIBRARIES}
#        ${GSTREAMER-FFT_LIBRARIES}
#        ${GSTREAMER-VIDEO_LIBRARIES}
#        ${GSTREAMER-BASE_LIBRARIES}
#        ${OpenCV_LIBS}
        /opt/nvidia/deepstream/deepstream-${NVDS_VERSION}/lib/
        /usr/local/cuda-${CUDA_VER}/lib64/
        cuda
        cudart
        nvdsgst_meta
        nvds_meta
)


