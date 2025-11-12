FROM ros:noetic-ros-base-focal
# https://hub.docker.com/_/ros

# install packages
RUN apt-get update && apt-get install -q -y --no-install-recommends \
    ros-noetic-desktop-full \
    && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install -q -y --no-install-recommends \
    bash-completion \
    dirmngr \
    gnupg2 \
    lsb-release \
    python3-pip \
    vim \
    curl \
    wget \
    && rm -rf /var/lib/apt/lists/*

# some more packages
RUN apt-get update && apt-get install -q -y build-essential git libpoco-dev libeigen3-dev rapidjson-dev

# install newer version of cmake
RUN wget https://github.com/Kitware/CMake/releases/download/v3.26.3/cmake-3.26.3-linux-x86_64.sh &&\
    yes | sh cmake-3.26.3-linux-x86_64.sh --prefix=/opt

# xauth for remote controll
RUN apt-get update -y && apt-get install -y \
    x11-apps \
    xauth

# dependencies
RUN apt-get update -y && apt-get install -y \
    git \
    clang-7 \
    clang-format-7 \
    clang-tidy-7 \
    pycodestyle \
    liborocos-kdl-dev \
    python3-pip \
    python3-catkin-tools \
    ros-noetic-boost-sml \
    ros-noetic-ros-control \
    ros-noetic-eigen-conversions \
    ros-noetic-urdfdom-py \
    && rm -rf /var/lib/apt/lists/*

RUN pip install parameterized

# other dependencies
RUN apt-get update && apt-get install -q -y \
    ros-noetic-ros-controllers

# flir dependencies
RUN apt-get update && apt-get install -q -y \
    ros-noetic-wfov-camera-msgs \
    ros-noetic-sensor-msgs \
    ros-noetic-image-exposure-msgs \
    ros-noetic-vision-msgs \
    ros-noetic-object-recognition-msgs

# qb dependencies
RUN apt-get update && apt-get install -q -y \
    ros-noetic-qb-move-description \
    ros-noetic-rqt-joint-trajectory-controller

# other dependencies
RUN apt-get update && apt-get install -q -y \
    x11-xkb-utils

RUN apt-get update && apt-get install -q -y \
    ros-noetic-ecl-geometry \
    ros-noetic-rviz-visual-tools
   
RUN pip3 install numpy-stl geomdl

RUN sudo apt install -y nlohmann-json3-dev python3-tk liburdfdom-tools nano

# apt autocomplete fix
RUN rm /etc/apt/apt.conf.d/docker-clean &&\
    apt-get update

# user setup
ARG UID=1000
ARG GID=1000

# adding user and group (docker)
RUN groupadd -g $GID docker
RUN useradd -rm -d /home/docker -s /bin/bash -g docker -G sudo -u $UID docker -p "$(openssl passwd -1 docker)"
COPY .bashrc /home/docker/.bashrc

# entrypoint stuff
COPY ./entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

# USER docker
WORKDIR /home/docker/catkin_ws

USER docker

