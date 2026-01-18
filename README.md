# UNeXt: Paper Implementation for EN3160 - Image Processing and Machine Vision

## Table of Contents
- [Introduction](#introduction)
- [Architecture](#architecture)
- [Installation](#installation)
- [Dataset](#dataset)
- [Results](#results)
- [Video Segmentation](#video-segmentation)
- [References](#references)

## Introduction

The **UNeXt** is lightweight, more efficient segmentation architecture that maintains state of the art accuracy. The UNeXt paper proposes a hybrid model that combines the strengths of convolutional layers with MLP layers to enhance feature extraction, all while reducing computational costs. This project aims to implement and replicate  the results of the the UNeXt model as a part of EN3160 Image Processing and Machine Vision module.

## Citation & Acknowledgment

This is a restructured re-implementation of the work from the following paper:

```bibtex
@article{valanarasu2022unext,
  title={UNeXt: MLP-based Rapid Medical Image Segmentation Network},
  author={Valanarasu, Jeya Maria Jose and Patel, Vishal M},
  journal={arXiv preprint arXiv:2203.04967},
  year={2022}
}
```

The codebase is based on the original author's repository: [https://github.com/jeya-maria-jose/UNeXt-pytorch](https://github.com/jeya-maria-jose/UNeXt-pytorch)

**All credit goes to the original authors.**

## Architecture
The following diagram shows the architecture of the UNeXt model.

![model_image](https://jeya-maria-jose.github.io/UNext-web/resources/fastunet-arch.png)

## Installation

To set up the environment, follow these steps:

1. Clone this repository:
   ```bash
   git clone https://github.com/nadunnr/UNeXt.git
   cd UNeXt
   ```

2. Set up the dataset as specified in [Dataset](#dataset):

3. Run the `train.py` file for model training by giving a model name:
   ```bash
   python3 train.py --name model_1
   ```
4. Run the `val.py` file for model inferencing by specifying the model name:
   ```bash
   python3 val.py --name experiment1 --load_model model_1
   ```
5. Run the `export.py` file to export an optimized model as ONNX format:
   ```bash
   python3 export.py --input model_1.pth --output model_1
   ```


## Dataset

For this project, we have used the BUSI dataset, which provides annotated ultrasound images. The dataset should be organized in the following structure. Note that multiple annotation masks can be provided under nested folders inside `masks` folder. Rename them with class indeces.:

```plaintext
data/
├── images/
│   ├── 001.png
│   ├── 002.png
├── masks/
│   ├── 0/
│   |   ├── 001.png
|   |   ├── 002.png
```

Refer to the dataset provider’s terms and conditions for use.

## Results

These results were obtained from the best model we trained in our reimplementation of the UNeXt paper.

| Metric                            | Authors' Results (BUSI)  | Our Results               |
|-----------------------------------|--------------------------|---------------------------|
| **Dice Coefficient (F1 Score)**   | 79.37 ± 0.57             | 85.89                     |
| **IoU (Intersection over Union)** | 66.95 ± 1.22             | 75.48                     |
| **Parameter Count**               | 1.47 M                   | 1.4719 M                  |
| **Inference Speed (per image)**   | 25 ms                    | 21.45 ms                  |
| **GFLOPs**                        | 0.57                     | 0.573                     |
| **Dataset**                       | BUSI                     | BUSI                      |


## Video-Segmentation
Using the UNeXt's lightweight structure we inferenced on  Breast Ultrasound video footage to achieve real time segmentation at 40 fps. We also tested this on a Raspberry Pi 4 model B with 2 GB RAM, which resulted in a segmentation at 5 fps. We used the [Breast Ultrasound Video Dataset](https://paperswithcode.com/dataset/breast-lesion-detection-in-ultrasound-video) for video data. The result is as follows.




## References

- [UNeXt: MLP-based Rapid Medical Image Segmentation Network](https://arxiv.org/abs/2203.04967)
- Official UNeXt Implementation: [GitHub Repository](https://github.com/jeya-maria-jose/UNeXt-pytorch)
