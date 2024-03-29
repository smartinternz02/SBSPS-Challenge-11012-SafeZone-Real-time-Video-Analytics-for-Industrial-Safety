# EVA:  fast Edge Video Analytics

## Demo Videos

- <img src="https://render.githubusercontent.com/render/math?math=\sigma">: actual frame processing rate on NCS2
- <img src="https://render.githubusercontent.com/render/math?math=\lambda">: the incoming video stream rate 
- <img src="https://render.githubusercontent.com/render/math?math=\mu">: frame processing rate at no frame dropping
- test video name: [ETH-Sunnyday](https://motchallenge.net/vis/ETH-Sunnyday)

| Original Video (<img src="https://render.githubusercontent.com/render/math?math=\lambda"> = 14 FPS) | Online Detection on one NCS2 <br/> (YOLOv3, <img src="https://render.githubusercontent.com/render/math?math=\sigma"> is set to <img src="https://render.githubusercontent.com/render/math?math=\mu">) <br/> slow detection processing rate <br/> <img src="https://render.githubusercontent.com/render/math?math=\sigma"> = 2.5, <img src="https://render.githubusercontent.com/render/math?math=\lambda"> = 14, <img src="https://render.githubusercontent.com/render/math?math=\mu"> = 2.5 |
|:---:|:---:|
| [![ETH-Sunnyday Original Video](https://j.gifs.com/MwM00O.gif)](https://youtu.be/BZZCMvbAKv0) | [![ETH-Sunnyday Slow Online Detection (YOLOv3, 1 NCS2, <img src="https://render.githubusercontent.com/render/math?math=\sigma"> is set to <img src="https://render.githubusercontent.com/render/math?math=\mu">)](https://j.gifs.com/p8EGGp.gif)](https://youtu.be/jFWfrZqeCUw) |

| Online Detection on one NCS2 <br/> (YOLOv3, <img src="https://render.githubusercontent.com/render/math?math=\sigma"> is set to <img src="https://render.githubusercontent.com/render/math?math=\lambda">) <br/> cause large random frame dropping <br/> <img src="https://render.githubusercontent.com/render/math?math=\sigma"> = 14, <img src="https://render.githubusercontent.com/render/math?math=\lambda"> = 14, <img src="https://render.githubusercontent.com/render/math?math=\mu"> = 2.5 | Online Detection on six NCS2s <br/> (YOLOv3, <img src="https://render.githubusercontent.com/render/math?math=\sigma"> is set to <img src="https://render.githubusercontent.com/render/math?math=\lambda">) <br/> significantly reduce random frame dropping <br/> <img src="https://render.githubusercontent.com/render/math?math=\sigma"> = 14, <img src="https://render.githubusercontent.com/render/math?math=\lambda"> = 14, <img src="https://render.githubusercontent.com/render/math?math=\mu"> = 14.8  |
|:---:|:---:|
| [![ETH-Sunnyday Online Detection (YOLOv3, 1 NCS2, <img src="https://render.githubusercontent.com/render/math?math=\sigma"> is set to <img src="https://render.githubusercontent.com/render/math?math=\lambda">)](https://j.gifs.com/oVDN2j.gif)](https://youtu.be/ZIks3oOGx8M) | [![ETH-Sunnyday Online Detection (YOLOv3, 6 NCS2, <img src="https://render.githubusercontent.com/render/math?math=\sigma"> is set to <img src="https://render.githubusercontent.com/render/math?math=\lambda">)](https://j.gifs.com/k8yJR5.gif)](https://youtu.be/0xu_d2RJ6YA) |

## Introduction

Deep Neural Network (DNN) trained object detectors are widely deployed in many mission-critical systems for real time video analytics at the edge, such as autonomous driving, video surveillance, Internet of smart cameras. A common performance requirement in these mission-critical edge services is the near real-time latency of online object detection on edge devices. However, even with well-trained DNN object detectors, the online detection quality at edge may deteriorate for a number of reasons, such as limited capacity to run DNN object detection models on heterogeneous edge devices, and detection quality degradation due to random frame dropping when the detection processing rate is significantly slower than the incoming video frame rate.

The first result from our project EVA is to address the above problems by exploiting multi-model multi-device detection parallelism for fast object detection in edge systems with heterogeneous edge devices. First, we analyze the performance bottleneck of running a well-trained DNN model at edge for real time online object detection. We use the offline detection as a reference model, and examine the root cause by analyzing the mismatch among incoming video streaming rate, the video processing rate for object detection, and the output rate for real time detection visualization of video streaming. Second, we study performance optimizations by exploiting multimodel detection parallelism. We show that the model-parallel detection approach can effectively speed up the FPS detection processing rate, minimizing the FPS disparity with the incoming video frame rate on heterogeneous edge devices. We evaluate the proposed approach using SSD300 and YOLOv3 (pre-trained DNN models) on benchmark videos of different video stream rates. The results show that exploiting multi-model detection parallelism can speed up the online object detection processing rate and deliver near real-time object detection performance for efficient video analytics at edge.

This research is partially sponsored by Cisco and our first joint paper below documented the results produced by June 2021:

* Yanzhao Wu, Ling Liu, Ramana Kompella."Parallel Detection for Efficient Video Analytics at the Edge." to appear in IEEE 2021 CogMI Special Session on Edge Analytics, Dec. 2021. Also available on arXiv at [https://arxiv.org/abs/2107.12563](https://arxiv.org/abs/2107.12563).


This project is developed based on the following resources:

* [OpenVINO Toolkit](https://github.com/openvinotoolkit/openvino)
* [OpenVINO Toolkit - Open Model Zoo](https://github.com/openvinotoolkit/open_model_zoo)
* [OpenVINO-YoloV3](https://github.com/PINTO0309/OpenVINO-YoloV3)
* [Intel Tutorial on Multiple NCSs](https://www.intel.com/content/www/us/en/developer/articles/technical/leverage-multiple-intel-neural-compute-sticks-with-intel-distribution-of-openvino-toolkit.html)
