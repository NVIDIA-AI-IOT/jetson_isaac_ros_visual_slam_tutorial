!!! danger "Attention"

    **This tutorial is deprecated.**

    Please reference the official [Isaac ROS Docs Site](https://nvidia-isaac-ros.github.io/) to get the latest information and the [quickstart guide](https://nvidia-isaac-ros.github.io/repositories_and_packages/isaac_ros_visual_slam/isaac_ros_visual_slam/index.html#quickstart) on `isaac_ros_visual_slam`.
    
# SD Card image

We provide a custom SD card image for Jetson Orin Nano Developer Kit that is pre-configured with Isaac ROS software and other tools.

## License

By downloading and using the SD card image, you accept the terms and conditions of this [NVIDIA Isaac ROS Software License Agreement](./NVIDIA-ISAAC-ROS-SOFTWARE-LICENSE.md).

The SD card image is built on top JetPack 5.1.1 SD card image for Jetson Orin Nano Developer Kit, which includes [Jetson Linux 35.3.1 BSP](https://developer.nvidia.com/embedded/jetson-linux-r3531).

## Download

[Download custom SD card image for Jetson Orin Nano (20GB) :fontawesome-solid-download:](https://developer.nvidia.com/downloads/isaac-ros-visual-slam-orin-nano-image){ .md-button .md-button--primary }

## Misc. information about SD card image

### How SD card is configured

1. Flash the official SD card image

    - [JetPack 5.1.1 SD card image for Jetson Orin Nano Developer Kit](https://developer.nvidia.com/downloads/embedded/l4t/r35_release_v3.1/sd_card_b49/jp511-orin-nano-sd-card-image.zip/)

1. RAM disk setup

    See [this](https://gitlab-master.nvidia.com/isaac_ros/isaac_ros_common/-/blob/cyato/docs-ramdisk/docs/dev-env-setup_jetson.md#optinal-ramdisk-setup).

1. Uninstall some of the Debian packages

    ```
    sudo apt purge firefox thunderbird libreoffice-common
    sudo apt purge libcudnn8-dev libcublas-dev-11-4 libcufft-dev-11-4 libcusparse-dev-11-4 libcusolver-dev-11-4 libnpp-dev-11-4 libcurand-dev-11-4
    ```

1. Follow the Isaac ROS Visual SLAM (DP3) set up documents.

    - [Isaac ROS Development Environment Setup](https://github.com/NVIDIA-ISAAC-ROS/isaac_ros_common/blob/main/docs/dev-env-setup.md)
    - [Isaac ROS Development Environment Setup - Jetson](https://github.com/NVIDIA-ISAAC-ROS/isaac_ros_common/blob/main/docs/dev-env-setup_jetson.md)
    - [Isaac ROS RealSense Setup](https://github.com/NVIDIA-ISAAC-ROS/.github/blob/main/profile/realsense-setup.md)
    - [Tutorial for Visual SLAM using a RealSense camera with integrated IMU](https://github.com/NVIDIA-ISAAC-ROS/isaac_ros_visual_slam/blob/main/docs/tutorial-realsense.md#tutorial-for-visual-slam-using-a-realsense-camera)

1. Auto-set ROS_DOMAIN_ID in `run_dev.sh`

1. Register `isaac_ros_container` command alias. 

1. Wipe out all the sensitive history and config information.

    ``` { .bash .copy }
    docker logout
    git config --global --unset user.name
    git config --global --unset user.email
    git config --global --edit
    sudo rm /etc/NetworkManager/system-connections/*
    rm ~/.bash_history
    ```

1. Prepare for the SD card image partition auto resize.

    ``` { .bash .copy }
    sudo touch /etc/nv/nvautoconfig
    ```

1. Power off Jetson Orin Nano Developer Kit, take out the SD card, and pop that into your PC's SD card slot.

1. On the PC, run `GParted` to resize the APP parition.

1. Run [`host_make_expandable_image.sh`](https://github.com/NVIDIA-AI-IOT/jetcard/blob/master/scripts/host_make_expandable_image.sh) from `jetcard` with the "Last sector" number noted from `GParted`.
