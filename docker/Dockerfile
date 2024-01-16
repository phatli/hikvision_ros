# Start from the ROS Melodic base image
FROM ros:melodic-ros-base

# Install system dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    cmake \
    git \
    libgtk2.0-dev \
    pkg-config \
    libavcodec-dev \
    libavformat-dev \
    libswscale-dev \
    python-dev \
    python-numpy \
    libtbb2 \
    libtbb-dev \
    libjpeg-dev \
    libpng-dev \
    libtiff-dev \
    libdc1394-22-dev \
    libboost-all-dev \
    && rm -rf /var/lib/apt/lists/*

# Install OpenCV 3
RUN apt-get update && apt-get install -y \
    libopencv-dev \
    python-opencv \
    && rm -rf /var/lib/apt/lists/*

# Install ROS packages
RUN apt-get update && apt-get install -y \
    ros-melodic-cv-bridge \
    ros-melodic-image-transport \
    ros-melodic-camera-info-manager \
    && rm -rf /var/lib/apt/lists/*

# Install hikvision driver
RUN . /opt/ros/$ROS_DISTRO/setup.sh && \
    mkdir -p /root/catkin_ws/src && \
    cd /root/catkin_ws/src && git clone https://github.com/phatli/hikvision_ros.git && \
    cd /root/catkin_ws && catkin_make

# Cleanup
COPY ./entrypoint.sh /
RUN chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
CMD ["/bin/bash"]