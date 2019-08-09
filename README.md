# GStreamer Video Analytics (GVA) Plugin

## Overview
<div align="center"><img src="intro.gif" width=900/></div>

This repository contains GStreamer elements that enable CNN model-based video analytics capabilities in the GStreamer framework. These elements include such things as object detection, classification, and recognition. Example above shows concise GStreamer pipeline that runs detection & emotion classification, using specific models on a video file:
```sh
gst-launch-1.0 filesrc location=cut.mp4 ! decodebin ! videoconvert ! gvadetect model=face-detection-adas-0001.xml ! gvaclassify model=emotions-recognition-retail-0003.xml model-proc=emotions-recognition-retail-0003.json ! gvawatermark ! ximagesink sync=false
```

The solution leverages:
* Open-source GStreamer framework for pipeline management
* GStreamer plugins for input and output, such as media files and real-time streaming from a camera or network
* Video decode and encode plugins, including either CPU-optimized plugins or GPU-accelerated plugins, [based on VAAPI](https://github.com/GStreamer/gstreamer-vaapi)

In addition, the solution installs the following Deep Learning-specific elements, also available in this repository:
* Inference plugins leveraging [Intel OpenVINO](https://software.intel.com/en-us/openvino-toolkit) for high-performance inference using CNN models
* Visualization of computer vision results (such as bounding boxes and labels of detected objects) on top of video stream

The following diagram shows how the GVA plugin fits into the common software stack. 

<div align="center"><img src="https://user-images.githubusercontent.com/26006277/58497636-11285480-8185-11e9-80da-b812877bc898.png" width=900/></div>

Diagram color key:
* GVA plugin components: light blue
* Oher Intel components: dark blue
* Standard GStreamer components: gray
* Linux kernel: green

## License
The GStreamer Video Analytics Plugin is licensed under the [MIT license](LICENSE).

## Prerequisites
### Hardware
* The Intel(R) OpenVINO(TM) toolkit has information about the [hardware requirements for inference elements](https://software.intel.com/en-us/openvino-toolkit/hardware)
* On platforms with Intel Gen graphics, see the gstreamer-vaapi for [hardware accelerated video decode and encode requirements](https://github.com/GStreamer/gstreamer-vaapi)

### Software
* Intel(R) OpenVINO(TM) toolkit 2019 R1 (Inference Engine 1.6.0) or above
* Linux* system with kernel 4.15 or above
* GStreamer framework 1.14 or above

## Getting Started
* Start here: [Getting Started Guide](https://github.com/opencv/gst-video-analytics/wiki/Getting-Started-Guide-%5BR1.2%5D)
* [API reference](https://opencv.github.io/gst-video-analytics/)

## Samples
See the [command-line examples](samples/shell) and [C++ example](samples/cpp/face_attributes)
NOTE: For running samples, the wiki should be modified to use 2018 branch of open_model_zoo as the master version downloads version 6 models which are not supported by this version of OpenVino and the models do not run). Then use the following command to download the models (the 2018 branch version of downloader does not take list file as cmd line parameter):

cd ~/gva/open_model_zoo/model_downloader
python3 downloader.py -c ./list_topologies.yml --name `paste -s -d ',' ~/gva/gstreamer-plugins/samples/model_downloader_configs/intel_models_for_samples.LST` -o ~/gva/data/models/intel/

## Reporting Bugs and Feature Requests
Report bugs and requests [on the issues page](https://github.com/opencv/gst-video-analytics/issues)

## Usage and integration into application
### Pipelining and data flow
[Details](https://github.com/opencv/gst-video-analytics/wiki/Data-flow) about pipeline construction and the data flow between pipeline elements

### Metadata
[Details](https://github.com/opencv/gst-video-analytics/wiki/Metadata) about metadata generated by inference plugins and attached to video frames

### Model preparation
[Details](https://github.com/opencv/gst-video-analytics/wiki/Model-preparation) about how to prepare Tensorflow*, Caffe*, and other models for the inference plugins

### Plugins parameters
[Elements list](https://github.com/opencv/gst-video-analytics/wiki/Elements) and properties list for each element

## How to contribute
Pull requests aren't monitored, so if you have bug fix or an idea to improve this project, post a description on the [issues page](https://github.com/opencv/gst-video-analytics/issues). 

---
\* Other names and brands may be claimed as the property of others.
