# This is a Dockerfile for ros:ros-tutorials
FROM ros:kinetic-ros-base

ENV ROS_DISTRO kinetic

# install ros tutorials packages
RUN apt-get update && apt-get install -y \
    ros-kinetic-ros-tutorials \
    ros-kinetic-common-tutorials \
    && rm -rf /var/lib/apt/lists/*
