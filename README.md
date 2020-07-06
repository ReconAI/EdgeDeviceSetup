# EdgeDeviceSetup
Instructions and Manuals on how to set up Nvidia edge device<br>

Instructions below can be applied mainly to Jetson Nano device for Development and Testing<br>

## 0. Pre-installation tips

1. Install 32Gb (or bigger) SD card if possbile

## 1. OS installation
Current version is r32.4.2 (5/16/2020)

1. Follow [this](https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit#write) instruction to download and flash sd card.

## 2. First boot

1. On the first boot when you'd be asked to set up 'APP folder' size select maximum available value

## 3. System tuning

1. By default system has factory settings (low ram and buffer) which might result in hanging and crashes of resource-greedy programs (like Neural network inference). To fix this issue extend system swap file. Current swap file size can be checked here:
<p align="center">
  <img src="images/01_swapSize.png" height="672" width="947" title="swap size"/>
</p>
* To extend swap file download and unpack this [repo](https://github.com/JetsonHacksNano/resizeSwapMemory) <br>
* Execute:

```sh
./setSwapMemorySize -g 4
```

* (Optional) Size of zram can be modified, see links in resizeSwapMemory repo<br>

2. For additional clock speed increase run following commands:

```sh
sudo nvpmodel -m 0
sudo jetson_clocks
```

## 4. Remote access

1. To access Edge device in Remote Desktop mode install 'NoMachne for arm' ([link](https://www.nomachine.com/download/linux&id=30&s=ARM)) on Edge device and 'NoMachine Desktop' on your computer. Software works only in local network, in order to access device in other network VPN has to be setup.
2. (Optional) OpenVPN installation.<br>
Go to OpenVPN website to check the latest versions of commands. But basically you would need OpenVPN server with public IP, from this server you have to create a new connection (.ovpn file) with certificaties and keys. Move .ovpn on the Edge device and execute command below:

```sh
sudo apt-get install openvpn //To install openvpn on edge device
sudo openvpn --config jetsonHome.ovpn //To run open vpn on edge device
```

if OpenVPN was installed, NoMachine connection can be established via IP-address assigned by OpenVPN network.
3. (Optional) AutoSSH conection can be established. Approach is similar to OpenVPN.

## 5. Software installation

1. **jtop** - tool similar to System Monitor, **jetson_release** - tool to display all installed libraries and their versions (helpful when you need to know Jetpack, cuDNN and CUDA versions). Both tools can be donwloaded from [here](https://github.com/rbonghi/jetson_stats). Installation:

```sh
sudo -H pip install -U jetson-stats
*Reboot device*
```

Usage:

```sh
jtop
jetson_release
```

2. **VSCode** - IDE for developement. Follow this [tutorial](https://www.jetsonhacks.com/2019/10/01/jetson-nano-visual-studio-code-python/). Use following commands to isntall:

```sh
git clone https://github.com/JetsonHacksNano/installVSCode.git
cd installVSCode
./installVSCode.sh
```

To run:

```sh
code-oss
```

3. (Optional) **Tensorflow**. Check the [instruction](https://docs.nvidia.com/deeplearning/frameworks/install-tf-jetson-platform/index.html). For Jetpack 4.4 Tensorflow v1.X.X installation command looks like:

```sh
sudo pip3 install --pre --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v44 ‘tensorflow<2’
```

Tensorflow (1.X) installation:

```sh
sudo pip3 install --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v44 tensorflow-gpu==1.15.2+nv20.4
```

4. (Optional) **Scikitlearn**. Install via pip, if you'd face issues, please refer [this thread](https://stackoverflow.com/questions/60448903/cannot-install-scikit-learn-on-jetson-nano)

5. (Optional) **OpenCV with CUDA**

Install required dependencies:

```sh
sudo apt-get install build-essential cmake unzip pkg-config libjpeg-dev libpng-dev libtiff-dev libdc1394-22-dev libavcodec-dev libavformat-dev libswscale-dev libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev libv4l-dev v4l-utils qv4l2 v4l2ucp libxvidcore-dev libx264-dev libgtk-3-dev libatlas-base-dev gfortran python-dev python3-dev python-numpy python3-numpy libtbb2 libtbb-dev

sudo jetson_swap -s 4 # for Nano only, we need to have bigger swap to prevent build failure
```

Set parameter depending on machine. See [reference](https://developer.nvidia.com/cuda-gpus).

```sh
export CUDA_ARCH_BIN=5.3 # Nano
export CUDA_ARCH_BIN=7.2 # Xavier
```

Execute below to see OpenCV version and CUDA compilation status
```sh
jetson_release
```

Set parameter depending on OpenCV version:

```sh
export OPENCV_VER=4.1.1
```

Download and compile OpenCV:

```sh
cd ~
wget -O opencv.${OPENCV_VER}.zip https://github.com/opencv/opencv/archive/${OPENCV_VER}.zip
wget -O opencv_contrib.${OPENCV_VER}.zip https://github.com/opencv/opencv_contrib/archive/${OPENCV_VER}.zip
unzip opencv.${OPENCV_VER}.zip
unzip opencv_contrib.${OPENCV_VER}.zip

cd ~/opencv-${OPENCV_VER}

sed -i 's/include <Eigen\/Core>/include <eigen3\/Eigen\/Core>/g' modules/core/include/opencv2/core/private.hpp

mkdir -p build
cd build

cmake -D CMAKE_BUILD_TYPE=RELEASE \
-D CMAKE_INSTALL_PREFIX=/usr/local \
-D INSTALL_PYTHON_EXAMPLES=ON \
-D OPENCV_ENABLE_NONFREE=ON \
-D WITH_CUDA=ON \
-D WITH_CUDNN=ON \
-D OPENCV_DNN_CUDA=ON \
-D ENABLE_FAST_MATH=1 \
-D CUDA_FAST_MATH=1 \
-D CUDA_ARCH_BIN="${CUDA_ARCH_BIN}" \
-D CUDA_ARCH_PTX="" \
-D WITH_CUBLAS=1 \
-D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib-${OPENCV_VER}/modules \
-D WITH_GSTREAMER=ON \
-D WITH_LIBV4L=ON \
-D BUILD_opencv_python2=ON \
-D BUILD_opencv_python3=ON \
-D INSTALL_C_EXAMPLES=OFF \
-D BUILD_TESTS=OFF \
-D BUILD_EXAMPLES=OFF ..

make -j3 #resource hungry operation - requires ~10Gb free memory

sudo make install
```

Verify OpenCV installation (CUDA has to be enabled):
```sh
opencv_version -v
```
Alternative verification:
```sh
jetson_release
```


6. (Optional) **OpenVPN**

```sh
sudo apt-get install openvpn
```

Run:

```sh
sudo openvpn --config jetsonHome.ovpn
```


## 6. Deepstream 4.0

[Link](https://github.com/ReconAI/EdgeDeviceSetup/tree/master/deepstream40)

## 7. Deepstream 5.0

[Link](https://github.com/ReconAI/EdgeDeviceSetup/tree/master/deepstream50)