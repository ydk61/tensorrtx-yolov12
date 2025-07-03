## Introduction

Yolov12 model supports TensorRT-8.

Detection training code [link](https://github.com/sunsmarterjie/yolov12/releases/tag/turbo)
Segment training code[link](https://github.com/sunsmarterjie/yolov12/releases/tag/seg)
Classify training code[link](https://github.com/sunsmarterjie/yolov12/releases/tag/cls)

## Environment

* cuda 11.6
* cudnn 8.9.1.23
* tensorrt 8.6.1.6
* opencv 4.8.0
* ultralytics 8.3.63

## Support

* [x] YOLOv12-det support FP32/FP16 and C++ API
* [x] YOLOv12-seg support FP32/FP16 and C++ API
* [x] YOLOv12-cls support FP32/FP16 and C++ API


## Config

* Choose the YOLOv12 sub-model n/s/m/l/x from command line arguments.
* Other configs please check [src/config.h](src/config.h)

## Build and Run (Detection)

1. generate .wts from pytorch with .pt, or download .wts from model zoo

```shell
# Download ultralytics
wget https://github.com/sunsmarterjie/yolov12/releases/tag/turbo -O ultralytics-8.3.63.zip
# Unzip ultralytics
unzip ultralytics-8.3.63.zip
cd ultralytics-8.3.63
# Training your ownself models
to download other models, replace 'yolov12n.pt' with 'yolov12s.pt', 'yolov12m.pt', 'yolov12l.pt' or 'yolov12x.pt'
# Generate .wts
cp [PATH-TO-TENSORRTX]/yolov12/gen_wts.py .
python gen_wts.py -w yolov12n.pt -o yolov12n.wts -t detect
# A file 'yolov12n.wts' will be generated.
```

2. build tensorrtx/yolov12 and run
```shell
cd [PATH-TO-TENSORRTX]/yolov12
mkdir build
cd build
cmake ..
make
```



## Build and Run (Segment)

1. generate .wts from pytorch with .pt, or download .wts from model zoo

```shell
# Download ultralytics
wget https://github.com/sunsmarterjie/yolov12/releases/tag/seg -O ultralytics-8.3.63.zip
# Unzip ultralytics
unzip ultralytics-8.3.63.zip
cd ultralytics-8.3.63
# Training your ownself models
to download other models, replace 'yolov12n-seg.pt' with 'yolov12s-seg.pt', 'yolov12m-seg.pt', 'yolov12l-seg.pt' or 'yolov12x-seg.pt'
# Generate .wts
cp [PATH-TO-TENSORRTX]/yolov12/gen_wts.py .
python gen_wts.py -w yolov12n-seg.pt -o yolov12n-seg.wts -t detect
# A file 'yolov12n-seg.wts' will be generated.
```

2. build tensorrtx/yolov12 and run
```shell
cd [PATH-TO-TENSORRTX]/yolov12
mkdir build
cd build
cmake ..
make
```

## Build and Run (Classify)

1. generate .wts from pytorch with .pt, or download .wts from model zoo

```shell
# Download ultralytics
wget https://github.com/sunsmarterjie/yolov12/releases/tag/cls -O ultralytics-8.3.63.zip
# Unzip ultralytics
unzip ultralytics-8.3.63.zip
cd ultralytics-8.3.63
# Training your ownself models
to download other models, replace 'yolo12n-cls.pt' with 'yolo12s-cls.pt', 'yolo12m-cls.pt', 'yolo12l-cls.pt' or 'yolo12x-cls.pt'
# Generate .wts
cp [PATH-TO-TENSORRTX]/yolov12/gen_wts.py .
python gen_wts.py -w yolo12n-cls.pt -t cls -o yolo12n-cls.wts 
# A file 'yolo12n-cls.wts' will be generated.
```

2. build tensorrtx/yolov12 and run
```shell
cd [PATH-TO-TENSORRTX]/yolov12
mkdir build
cd build
cmake ..
make
```

### Detection
```shell
cp [PATH-TO-ultralytics]/yolov2n.wts .
# Build and serialize TensorRT engine
./yolov12-det -s yolov12n.wts yolov12n.engine [n/s/m/l/x]
# Run inference
./yolov12-det -d yolov12n.engine ../images [c/g]
# results saved in build directory
```

### Segment
```shell
cp [PATH-TO-ultralytics]/yolov2n-seg.wts .
# Build and serialize TensorRT engine
./yolov12-seg -s yolov12n-seg.wts yolov12n-seg.engine [n/s/m/l/x]
# Run inference
./yolov12-seg -d yolov12n-seg.engine ../images [c/g]
# results saved in build directory
```

### Classify
```shell
cp [PATH-TO-ultralytics]/yolov2n-cls.wts .
# Build and serialize TensorRT engine
./yolov12-cls -s yolov12n-cls.wts yolov12n-cls.engine [n/s/m/l/x]
# Run inference
./yolov12-cls -d yolov12n-cls.engine ../images [c/g]
# results saved in build directory
```
