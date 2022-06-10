FROM nvcr.io/nvidia/deepstream:6.0.1-devel AS Base

ARG DEBIAN_FRONTEND=noninteractive
# Update the repository
RUN apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/3bf863cc.pub && \
    apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64/7fa2af80.pub &&  \
    apt update

# Install the required libraries
# 1. Install the genetic tools
RUN DEBIAN_FRONTEND=noninteractive apt install -y --no-install-recommends \
    build-essential cmake  wget unzip pkg-config yasm checkinstall \
    git g++ make vim curl ssh net-tools

# 2. Image I/O libs
RUN DEBIAN_FRONTEND=noninteractive apt install -y --no-install-recommends \
    libjpeg-dev libpng-dev libtiff-dev

# 2. Video/Audio Libs — FFMPEG, GSTREAMER, x264 and so on
RUN DEBIAN_FRONTEND=noninteractive apt install -y --no-install-recommends \
    libavcodec-dev libavformat-dev libswscale-dev libavresample-dev \
    libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev  \
    libxvidcore-dev x264 libx264-dev libfaac-dev libmp3lame-dev libtheora-dev \
    libfaac-dev libmp3lame-dev libvorbis-dev

# 3. OpenCore — Adaptive Multi Rate Narrow Band (AMRNB) and Wide Band (AMRWB) speech codec
RUN DEBIAN_FRONTEND=noninteractive apt install -y --no-install-recommends \
    libopencore-amrnb-dev libopencore-amrwb-dev

# 4. Cameras programming interface libs
RUN DEBIAN_FRONTEND=noninteractive apt install -y --no-install-recommends \
    libdc1394-22 libdc1394-22-dev libxine2-dev libv4l-dev v4l-utils &&  \
    cd /usr/include/linux && ln -s -f ../libv4l1-videodev.h videodev.h

# 5. GTK lib for the graphical user functionalites coming from OpenCV highghui module
RUN DEBIAN_FRONTEND=noninteractive apt install -y --no-install-recommends \
    libgtk-3-dev

# 6. Python
RUN DEBIAN_FRONTEND=noninteractive apt install -y --no-install-recommends \
    python3 python3-pip python3-numpy python3-dev python3-testresources


# 6. Parallelism library C++ for CPU
RUN DEBIAN_FRONTEND=noninteractive apt install -y --no-install-recommends \
    libtbb-dev


# 7. Optimization libraries for OpenCV
RUN DEBIAN_FRONTEND=noninteractive apt install -y --no-install-recommends \
    libatlas-base-dev gfortran

# 8. Install Gstreamer on ubuntu
RUN DEBIAN_FRONTEND=noninteractive apt install -y --no-install-recommends \
    libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev libgstreamer-plugins-bad1.0-dev  \
    gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly  \
    gstreamer1.0-libav gstreamer1.0-doc gstreamer1.0-tools gstreamer1.0-x gstreamer1.0-alsa gstreamer1.0-gl  \
    gstreamer1.0-gtk3 gstreamer1.0-qt5 gstreamer1.0-pulseaudio


FROM Base AS Runtime
WORKDIR /project
