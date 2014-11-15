# Dockerfile for ros-indigo base

FROM local/base-1404

# setup source-list and keys
RUN sh -c 'echo "deb http://packages.ros.org/ros/ubuntu trusty main" > /etc/apt/sources.list.d/ros-latest.list'
RUN apt-get install -y wget
RUN wget https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -O - | sudo apt-key add -
RUN apt-get update

# install ros-indigo base and initialize rosdep
RUN apt-get install -y ros-indigo-ros-base
RUN rosdep init

# add ros user and login to it
RUN adduser --gecos "a ROS user" --disabled-password ros
USER ros

# set home to new ros user and update rosdep
ENV HOME /home/ros
RUN rosdep update

# copy bashrc
ADD conf/bashrc /home/ros/ros.bash
RUN echo "source /home/ros/ros.bash" >> ~/.bashrc
