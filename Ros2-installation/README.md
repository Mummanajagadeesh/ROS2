
# Ubuntu (Debian packages)

## Table of Contents

- [Resources](#resources)
- [System setup](#system-setup)
  - [Set locale](#set-locale)
  - [Enable required repositories](#enable-required-repositories)
  - [Install development tools (optional)](#install-development-tools-optional)
- [Install ROS 2](#install-ros-2)
- [Install additional RMW implementations (optional)](#install-additional-rmw-implementations-optional)
- [Setup environment](#setup-environment)
- [Try some examples](#try-some-examples)
- [Next steps](#next-steps)
- [Troubleshoot](#troubleshoot)
- [Uninstall](#uninstall)

## Resources

- **Status Page:**
  - ROS 2 Jazzy (Ubuntu Noble 24.04): amd64, arm64
- **[Jenkins Instance](#)**
- **[Repositories](#)**

## System setup

### Set locale

Ensure UTF-8 locale support:

```bash
locale  # Check current locale
sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8
locale  # Verify settings
```

### Enable required repositories

Enable Ubuntu Universe repository and add ROS 2 repository:

```bash
sudo apt install software-properties-common
sudo add-apt-repository universe
sudo apt update && sudo apt install curl -y
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```

### Install development tools (optional)

Install ROS development tools:

```bash
sudo apt update && sudo apt install ros-dev-tools
```

## Install ROS 2

Update and upgrade apt repositories, then install ROS 2:

```bash
sudo apt update
sudo apt upgrade
sudo apt install ros-jazzy-desktop  # Desktop Install (Recommended)
sudo apt install ros-jazzy-ros-base  # ROS-Base Install (Bare Bones)
```

## Install additional RMW implementations (optional)

Replace or add RMW implementations at runtime:

## Setup environment

Source ROS setup file (replace `.bash` with your shell):

```bash
source /opt/ros/jazzy/setup.bash
```

## Try some examples

Run example nodes:

### C++ talker

```bash
source /opt/ros/jazzy/setup.bash
ros2 run demo_nodes_cpp talker
```

### Python listener

```bash
source /opt/ros/jazzy/setup.bash
ros2 run demo_nodes_py listener
```

## Next steps

Continue with [tutorials and demos](https://docs.ros.org/en/jazzy/Tutorials.html) to configure your environment, create workspaces, and learn ROS 2 core concepts.

## Troubleshoot

Explore [troubleshooting techniques](https://docs.ros.org/en/jazzy/How-To-Guides/Installation-Troubleshooting.html).

## Uninstall

Remove ROS 2 and associated binaries:

```bash
sudo apt remove ~nros-jazzy-* && sudo apt autoremove
sudo rm /etc/apt/sources.list.d/ros2.list
sudo apt update && sudo apt autoremove && sudo apt upgrade
```
