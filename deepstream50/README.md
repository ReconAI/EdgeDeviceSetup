# Deepstream 5.0 

Deepstream is an Nvidia gramework to develop and run deep learning applications on Nvidia hardware (especially Edge devices)

## Installation

1. Download latests Deepstream 5.X version from [here](https://developer.nvidia.com/deepstream-getting-started) (make sure that Jetpack version is correct //Use **jtop**)
2. Unzip archive on device
3. Follow the [guide](https://docs.nvidia.com/metropolis/deepstream/dev-guide/index.html)

## Samples

Deepstream contains multiple samples listed in [guide](https://docs.nvidia.com/metropolis/deepstream/dev-guide/index.html) see 'Sample Application Source Details' <br>
Sample can be tested by running command below:<br>

```sh
deepstream-app -c <path_to_config_file>
```

For example:<br>

```sh
cd /opt/nvidia/deepstream/deepstream-5.0
deepstream-app -c samples/configs/deepstream-app/source8_1080p_dec_infer-resnet_tracker_tiled_display_fp16_nano.txt
```
Sample above demonstrates 8 Decode + Infer + Tracker; for Jetson Nano only.
Check config files txt for information on input/ouput format (rtsp or file) and internal modules (neural nets and trackers)

## Python API

For reference see [guide](https://docs.nvidia.com/metropolis/deepstream/dev-guide/index.html) -> 'Python Sample Application Source Details' and [Deepstream Python Apps](https://github.com/NVIDIA-AI-IOT/deepstream_python_apps)

Github project contains following samples: <br>

| Sample        | Description           |
| ------------- |-------------:|
| deepstream-test1 | 4-class object detection pipeline (Vehicle , RoadSign, Bicycle, Person)  |
| deepstream-test2 | 4-class object detection (Vehicle , RoadSign, Bicycle, Person), tracking and attribute classification (vehicle color, maker and type) pipeline |
| deepstream-test3 | Multi-stream pipeline performing 4-class object detection (Vehicle , RoadSign, Bicycle, Person) |
| deepstream-test4 | msgbroker for sending analytics results to the cloud |
| deepstream-imagedata-multistream | Multi-stream pipeline with access to image buffers |
| deepstream-ssd-parser | SSD model inference via Triton server with output parsing in Python |
| deepstream-test1-usbcam | deepstream-test1 pipelien with USB camera input |
| deepstream-test1-rtsp-out | deepstream-test1 pipeline with RTSP output |

# Transfer Learning Toolkit 2.0

Transfer Learning Toolkit is a software for easy neural netowk training using Nvidia hardware

## Installation instruction

Provided instruction is based on this [article](https://medium.com/@Smartcow_ai/nvidia-transfer-learning-toolkit-a-comprehensive-guide-75148d1ac1b) describing Transfer Leraning Toolkit v.1 installation.<br>

<b>Prerequisites</b><br><br>

To successfully utilize TLTv2 you would need a machine with Nvidia graphics card with preinstalled Linux operating system.
To follow along the instruction following software has to be installed:M<br>
1. curl<br>
```sh
sudo apt install curl
```
2. pip3
```sh
sudo apt install python3-pip
```
3. Jupyter Notebook
```sh
pip3 install jupyter
```
Create '/workspace' folder and run jupyter notebook in it via:<br>
```sh
cd /workspace
jupyter notebook --ip 0.0.0.0 --allow-root
```
4. Docker
```sh
sudo apt install docker.io
```
To run docker service run
```sh
sudo systemctl start docker
```
5. [Nvidia Container Runtime](https://github.com/NVIDIA/nvidia-container-runtime) <b>Make sure that CUDA 10.2 was installed</b>

6. In addition please create [NGC](https://ngc.nvidia.com) account<br>

<b>Installation process</b><br><br>

Valid instruction is located [here](https://ngc.nvidia.com/catalog/containers/nvidia:tlt-streamanalytics)
1. Pull docker image

```sh
docker pull nvcr.io/nvidia/tlt-streamanalytics:v2.0_dp_py2
```

2. Run docker image

```sh
docker run --runtime=nvidia -it \
 -v "/workspace":"/workspace" \
 -p 8888:8888 nvcr.io/nvidia/tlt-streamanalytics:v2.0_dp_py2 /bin/bash
```

3. Create NGC API key

4. Run notebook (if it wasn't started before)
```sh
jupyter notebook --ip 0.0.0.0 --port 8888 --allow-root
```

5. Open http://0.0.0.0:8888 in browser

6. From here you can follow instructions on training of different models:
- [Object Detection](https://ngc.nvidia.com/catalog/models/nvidia:tlt_pretrained_object_detection)
- [DetectNet_v2](https://ngc.nvidia.com/catalog/models/nvidia:tlt_pretrained_detectnet_v2)
- [Image Classification](https://ngc.nvidia.com/catalog/models/nvidia:tlt_pretrained_classification)

## Examples/Pretrained networks

NGC repository contains few pretrained models which can be used in commercial product:

1. [PeopleNet](https://ngc.nvidia.com/catalog/models/nvidia:tlt_peoplenet)
Nework is based on NVIDIA DetectNet_v2 detector with ResNet34 as a feature extractor.<br>
Input resolution - Color Images of resolution 960 X 544 X 3<br>
Detected classes - persons, bags and faces<br>
Output - Category labels (people) and bounding-box coordinates for each detected people in the input image<br>
Training data - ground level images<br>
Real-time inference:<br>
Jetson Nano - 10.6 FPS<br>
Jetson Xavier NX - 119.6 FPS<br>

2. [TrafficCamNet](https://ngc.nvidia.com/catalog/models/nvidia:tlt_trafficcamnet)
Nework is based on NVIDIA DetectNet_v2 detector with ResNet18 as a feature extractor.<br>
Input resolution - Color Images of resolution 960 X 544 X 3<br>
Detected classes - car, person, road sign, two-wheeler<br>
Output - Category labels and bounding-box coordinates for each detected object in the input image<br>
Training data - ground level images<br>
Real-time inference:<br>
Jetson Nano - 17.7 FPS<br>
Jetson Xavier NX - 340 FPS<br>

3. [DashCamNet](https://ngc.nvidia.com/catalog/models/nvidia:tlt_dashcamnet)
Nework is based on NVIDIA DetectNet_v2 detector with ResNet18 as a feature extractor.<br>
Input resolution - Color Images of resolution 960 X 544 X 3<br>
Detected classes - car, person, road sign, bicycle<br>
Output - Category labels and bounding-box coordinates for each detected object in the input image<br>
Training data - ground level images<br>
Real-time inference:<br>
Jetson Nano - 17 FPS<br>

4. [FaceDetect-IR](https://ngc.nvidia.com/catalog/models/nvidia:tlt_facedetectir)
Nework is based on NVIDIA DetectNet_v2 detector with ResNet18 as a feature extractor.<br>
Input resolution - Color Images of resolution 384 X 240 X 3<br>
Detected classes - face<br>
Output - Category labels and bounding-box coordinates for each detected object in the input image<br>
Real-time inference:<br>
Jetson Nano - 103.9 FPS<br>
Jetson Xavier NX - 2000 FPS<br>

5. [VehicleMakeNet](https://ngc.nvidia.com/catalog/models/nvidia:tlt_vehiclemakenet)
Input resolution - Color Images of resolution 224 X 224 X 3<br>
Detected classes - Acura, Audi, BMW, Chevrolet, Chrysler, Dodge, Ford, GMC, Honda, Hyundai, Infiniti, Jeep, Kia, Lexus, Mazda, Mercedes, Nissan, Subaru, Toyota, and Volkswagen<br>
Output - Category label<br>
Real-time inference:<br>
Jetson Nano - 120 FPS<br>
Jetson Xavier NX - 2689 FPS<br>

6. [VehicleTypeNet](https://ngc.nvidia.com/catalog/models/nvidia:tlt_vehicletypenet)
Input resolution - Color Images of resolution 224 X 224 X 3<br>
Detected classes - coupe, sedan, SUV, van, large vehicle, truck
Output - Category label<br>
Real-time inference:<br>
Jetson Nano - 172.8 FPS<br>
Jetson Xavier NX - 3275 FPS<br>

7. [Google Open Image Model](https://ngc.nvidia.com/catalog/models/nvidia:iva:tlt_iva_classification_resnet18)
Nework is a ResNet18 trained on Google Open Image Dataset<br>

## Transfer Learning Toolkit usage with AWS

TLTv2 can be used in continuous training process. It requires a dedicated Linux machine with Nvidia GPU and CUDA.
