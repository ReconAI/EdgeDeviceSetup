# Deepstream 4.0 
Installation, articles, tutorials

## Installation

1. Donwnload latests Deepstream 4.X version from [here](https://developer.nvidia.com/embedded/deepstream-on-jetson-downloads-archived) (make sure that Jetpack version is correct //Use **jtop**)
2. Unzip archive on device
3. Follow the [guide](https://docs.nvidia.com/metropolis/deepstream/4.0/dev-guide/index.html)

## Sample applications

Samples description can be found [here](https://docs.nvidia.com/metropolis/deepstream/4.0/dev-guide/index.html#page/DeepStream_Development_Guide%2Fdeepstream_quick_start.html%23wwpID0E0GB0HA)

Samples are run from console like:

```sh
./deepstream-test1-app ../../../samples/streams/sample_720p.h264
```

Basically each sample among 'test-' apps is built one upon another:<br>
1. deepstream-test1 is a an app with single network - Object Detector, it's taking video file as input and returns video with annotation
2. deepstream-test2 has two Networks and a Tracker - Object Detector (from test1), Tracker and Object Classifier, input and ouptut are the same as test1
3. deepstream-test3 - takes RTSP stream as input
4. deepstream-app - is a universal reference application, which takes config file as an input and can recieve any type of input/output with any network running as primary/secondary detector
5. objectDetector_Yolo - Deepstream implementation of Yolo detector. Can take pretrained yolo weights, configs and labels as input

## Videos

| Project        | Description           | Link  |
| ------------- |:-------------:| -----:|
| Streamline Deep Learning for Video Analytics with DeepStream SDK 2 0      | Introduction into Deepstream and GStreamer  | [Link](https://www.youtube.com/watch?v=H2blB7MGnx4) |
| DeepStream SDK — Accelerating Real Time AI Based Video and Image Analytics      | Introduction into Deepstream and GStreamer v2 | [Link](https://www.youtube.com/watch?v=ANAljY680mE) |

## Courses

| Name        | Description | Price          | Link  |
| ------------- |:-------------:| -----:| -----:|
| Getting Started with DeepStream for Video Analytics on Jetson Nano      | Set of hands-on tutorials: How to setup Jetson Nano (headless mode), How to run Deepstream 4.0 samples, how to edit samples to get different results | Free | [Link](https://courses.nvidia.com/courses/course-v1:DLI+C-IV-02+V1/about) |

[Other courses](https://www.nvidia.com/en-us/deep-learning-ai/education/)

## Examples

| Project        | Description           | Link  |
| ------------- |:-------------:| -----:|
| Redaction app      | Hide License Plates and Faces using Nvidias' pretrained network  | [Link](https://github.com/NVIDIA-AI-IOT/redaction_with_deepstream) |
| Back-to-Back detector      | Application with step detector: 1. Find cars; 2. Hide License plates      |   [Link](https://github.com/NVIDIA-AI-IOT/deepstream_reference_apps/tree/master/back-to-back-detectors) |
| TLT and deepstream usage      | How to deploy TLT-trained networks in Deepstream applications      |   [Link](https://github.com/NVIDIA-AI-IOT/deepstream_4.x_apps) |


