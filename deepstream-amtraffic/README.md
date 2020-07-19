# Deepstream AM-Traffic samples

[Python SDK Reference](https://docs.nvidia.com/metropolis/deepstream/python-api/index.html)

## deepstream-test5-helloworld1

This is a test2 app with rtsp/mp4 input

### Pipeline
- One input source (rtsp/file[mp4])
- resnet10.caffemodel 4-classes detector
- Default tracker
- Three networks (car class, type, ...)
- Output in the window

### How to run

```sh
cd /opt/nvidia/deepstream/deepstream-5.0/sources/python/apps/deepstream-test5-helloworld1
python3 deepstream_test_5.py file:///opt/nvidia/deepstream/deepstream-5.0/samples/streams/sample_720p.mp4
```

## deepstream-test6-helloworld2

This is test5 with a TrafficCamNet as a primary network

### Pipeline
- One input source (rtsp/file[mp4])
- TrafficCamNet (!)
- Default tracker
- Three networks (car class, type, ...)
- Output in the window

### How to run

```sh
cd /opt/nvidia/deepstream/deepstream-5.0/sources/python/apps/deepstream-test6-helloworld2
python3 deepstream_test_6.py file:///opt/nvidia/deepstream/deepstream-5.0/samples/streams/sample_720p.mp4
```

## deepstream-test7-helloworld3

This is test6 with a TrafficCamNet -> Tracker -> Car type classifier -> License plate detector

### Pipeline
- One input source (rtsp/file[mp4])
- TrafficCamNet 
- Default tracker
- Secondary network - car type
- Primary network - license plate
- Output in the window

### How to run

```sh
cd /opt/nvidia/deepstream/deepstream-5.0/sources/python/apps/deepstream-test7-helloworld3
python3 deepstream_test_7.py file:///opt/nvidia/deepstream/deepstream-5.0/samples/streams/StreamRecord_cam2_test.mp4
```

## deepstream-test8-helloworld4

This is test7 with rtsp output

### Pipeline
- One input source (rtsp/file[mp4])
- TrafficCamNet 
- Default tracker
- Secondary network - car type
- Primary network - license plate
- rtsp output 

### How to run

```sh
cd /opt/nvidia/deepstream/deepstream-5.0/sources/python/apps/deepstream-test8-helloworld4
python3 deepstream_test_8.py file:///opt/nvidia/deepstream/deepstream-5.0/samples/streams/StreamRecord_cam2_test.mp4

rtsp://192.168.1.132:8554/ds-test
```

## deepstream-test9-helloworld5

This is a merge between test8 and deepstream-imagedata_multistream

### Pipeline
- One input source (rtsp/file[mp4])
- TrafficCamNet 
- Default tracker
- Secondary network - car type
- Primary network - license plate
- rtsp output + save frames with bounding boxes to a folder


### How to run

```sh
cd /opt/nvidia/deepstream/deepstream-5.0/sources/python/apps/deepstream-test9-helloworld5
python3 deepstream_test_9.py file:///opt/nvidia/deepstream/deepstream-5.0/samples/streams/StreamRecord_cam2_test.mp4

rtsp://192.168.1.132:8554/ds-test
```


## deepstream-test10-helloworld6

Improvement of test9 with on-screen license plate recognition

### Pipeline
- One input source (rtsp/file[mp4])
- TrafficCamNet 
- Default tracker
- Secondary network - car type
- Primary network - license plate
- Python OpenALPR integration
- rtsp output


### How to run

```sh
cd /opt/nvidia/deepstream/deepstream-5.0/sources/python/apps/deepstream-test10-helloworld6
python3 deepstream_test_10.py file:///opt/nvidia/deepstream/deepstream-5.0/samples/streams/StreamRecord_cam2_test.mp4

rtsp://192.168.1.132:8554/ds-test
```

## deepstream-test11-helloworld7

Improvement of test10 with FPS, license plate results output

### Pipeline
- One input source (rtsp/file[mp4])
- TrafficCamNet 
- Default tracker
- Secondary network - car type
- Primary network - license plate
- Python OpenALPR integration
- rtsp output

### Statistics
Application is running at 7.6 FPS on Jetson Nano (720p video). License plates text is not detected.

### How to run

```sh
cd /opt/nvidia/deepstream/deepstream-5.0/sources/python/apps/deepstream-test11-helloworld7
python3 deepstream_test_11.py file:///opt/nvidia/deepstream/deepstream-5.0/samples/streams/StreamRecord_cam2_test.mp4

rtsp://192.168.1.132:8554/ds-test
```

## deepstream-test12-helloworld8

Improvement of test10 with FPS, license plate results output
+
Print of Frame number, pgie, sgie ids

### Pipeline
- One input source (rtsp/file[mp4])
- TrafficCamNet 
- Default tracker
- Secondary network - car type
- Python OpenALPR integration
- rtsp output

### Statistics
Application is running at 2.8 FPS on Jetson Nano (720p video). License plates text can be recognized

### How to run

```sh
cd /opt/nvidia/deepstream/deepstream-5.0/sources/python/apps/deepstream-test12-helloworld8
python3 deepstream_test_12.py file:///opt/nvidia/deepstream/deepstream-5.0/samples/streams/StreamRecord_cam2_test.mp4

python3 deepstream_test_12_global.py file:///opt/nvidia/deepstream/deepstream-5.0/samples/streams/StreamRecord_cam2_test.mp4

python3 deepstream_test_12_saving.py file:///opt/nvidia/deepstream/deepstream-5.0/samples/streams/StreamRecord_cam2_test2.mp4

python3 deepstream_test_12_saving.py file:///opt/nvidia/deepstream/deepstream-5.0/samples/streams/StreamRecord_cam2_test3.mp4

rtsp://192.168.1.132:8554/ds-test
```
