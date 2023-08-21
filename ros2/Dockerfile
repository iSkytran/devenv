FROM devenv:base

RUN echo "Etc/UTC" | sudo tee -a /etc/timezone && \
    sudo ln -s /usr/share/zoneinfo/Etc/UTC /etc/localtime && \
    sudo apt-get update && \
    sudo apt-get install -q -y --no-install-recommends tzdata

# Repository configuration.
RUN sudo apt-get install software-properties-common -y \
    && sudo add-apt-repository universe -y \
    && sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg \
    && echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null

# Install development tools.
RUN sudo apt-get update \
    && sudo apt-get install ros-dev-tools -y

# Install ROS 2.
RUN sudo apt-get update \
    && sudo apt-get upgrade -y \
    && sudo apt install ros-iron-desktop -y

# Source ROS workspace.
COPY ./ros_entrypoint.sh /
RUN sudo chmod +x /ros_entrypoint.sh
ENTRYPOINT ["/ros_entrypoint.sh"]
CMD ["/bin/zsh"]
