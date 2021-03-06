# ros_openpose

ROS wrapper for OpenPose | It supports *(currently but others are planned)*-

- [x] Intel RealSense Camera :heavy_check_mark:
- [x] Microsoft Kinect v2 Camera :heavy_check_mark:
- [x] Any color camera such as webcam etc :heavy_check_mark:

</br>

<p align="center">
    <img src="files/ros_openpose.gif", width="800">
    </br>
    <sup>Sample video showing visualization on RViz</sup>
</p>


## Dependencies
[OpenPose](https://github.com/CMU-Perceptual-Computing-Lab/openpose)

_Note: Additionally camera specific ROS drivers such as [realsense-ros](https://github.com/IntelRealSense/realsense-ros), [iai_kinect2](https://github.com/code-iai/iai_kinect2) etc are required as per your camera model._


## Installation
1. Make sure to download the complete repository. Use `git clone https://github.com/ravijo/ros_openpose.git` or download zip as per your convenience.
1. Invoke catkin tool inside ros workspace i.e., `catkin_make`
1. Make python scripts executable by using command below-
```
roscd ros_openpose/scripts
chmod +x *.py
```


## Troubleshooting
1. While compiling the package, if the following error is reported at the terminal-
    ```
    error: no match for ‘operator=’ (operand types are ‘op::Matrix’ and ‘const cv::Mat’)
    ```
    In this case, please update the OpenPose. Most likely, an old version of OpenPose is installed. So please checkout Openpose from the master branch as [described here](https://github.com/CMU-Perceptual-Computing-Lab/openpose/blob/master/doc/installation.md#update-openpose). Alternatively, you can checkout OpenPose version 1.5.1 by running the following command at the root directory of OpenPose installation-


       git checkout tags/v1.5.1


    Do not forget to run `sudo make install` to install the OpenPose system-wide.


## Configuration
The main launch file is `run.launch`. It has the following important arguments-
1. `model_folder`: It represents the full path to the model directory of OpenPose. Kindly modify it as per OpenPose installation in your machine. Please edit `run.launch` file as shown below-
    ```
    <arg name="openpose_args" --model_folder /home/ravi/openpose/models/"/>
    ```
1. `openpose_args`: It is provided to support the standard OpenPose command-line arguments. Please edit `run.launch` file as shown below-
    ```
    <arg name="openpose_args" value="--face --hand"/>
    ```
1. `camera`: It can only be one of the following: `realsense`, `kinect`, `nodepth`. Default value of this argument is `realsense`. See below for more information.


## Steps to Run with Intel RealSense Camera
1. Make sure that ROS env is sourced properly by executing the following command-
    ```
    source devel/setup.bash
    ```
1. Invoke the main launch file by executing the following command-
    ```
    roslaunch ros_openpose run.launch
    ```


## Steps to Run with Microsoft Kinect v2 Camera
1. Make sure that ROS env is sourced properly by executing the following command-
    ```
    source devel/setup.bash
    ```
1. Invoke the main launch file by executing the following command-
    ```
    roslaunch ros_openpose run.launch camera:=kinect
    ```


## Steps to Run with any Color Camera such as Webcam etc.
1. Make sure that ROS env is sourced properly by executing the following command-
    ```
    source devel/setup.bash
    ```
1. Start the ROS package of your camera. Basically, this package is going to capture images from your camera, and then it is going to publish those images on a ROS topic. Make sure to set the correct ROS topic to `color_topic` inside [config_nodepth.launch](https://github.com/ravijo/ros_openpose/blob/d5d8e05978a1b085d8d6ffdc7604dc99a664d8d8/launch/config_nodepth.launch#L10) file.
1. Invoke the main launch file by executing the following command-
    ```
    roslaunch ros_openpose run.launch camera:=nodepth
    ```

Note: To confirm that ROS package of your camera is working properly, please check if the ROS package is publishing images by executing the following command-
```
rosrun image_view image_view image:=YOUR_ROSTOPIC
```
Here `YOUR_ROSTOPIC` must have the same value as `color_topic`.



## Note
This package has been tested on the following environment configuration-

| Name      | Value                                  |
| ----------| -------------------------------------- |
| OS        | Ubuntu 14.04.6 LTS (64-bit)            |
| RAM       | 16 GB                                  |
| Processor | Intel® Core™ i7-7700 CPU @ 3.60GHz × 8 |
| Kernel    | Version 4.4.0-148-generic              |
| ROS       | Indigo                                 |
| GCC       | Version 5.5.0                          |
| OpenCV    | Version 2.4.8                          |
| OpenPose  | Version 1.5.1                          |
| GPU       | GeForce GTX 1080                       |
| CUDA      | Version 8.0.61                         |
| cuDNN     | Version 5.1.10                         |


## Issues (or Error Reporting)
Please check [here](https://github.com/ravijo/ros_openpose/issues) and create issues accordingly.
