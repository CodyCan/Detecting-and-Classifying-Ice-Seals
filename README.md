# Detecting and Classifying Ice Seals

## Problem Statement
Global warming has led to massive ice melt that greatly affects the habitat of many animals. Information on their populations is important. Recent development of aerial imaging by drone together with high resolution satellite images has opened up new avenues for population surveys without disturbing the normal activities of these animals. However, the counting is still largely being done manually. Such a process is laborious, time consuming, error-prone. This has motivated me to develop a machine learning tool that is capable of detecting and counting animals from aerial images. In particular, I build deep learning object detection models to detect ice seals and classify their species from RGB and IR imagery.

The main metric will be the mean Average Precision (mAP) which takes into account both the precision and recall. I will be aiming for an mAP of 0.8 and above.


## Data Acquisition and Preprocessing
I wrote a Python function to automatiacally download and save images to local machine. The RGB images seems to be much bigger than the IR counterparts (tens of MB vs. hundreds of kB).

## Data Analysis
I plan to start with small scale modelings with about 100 images to make sure that the workflow works properly without worrying about the performance. Once everything works, I will scale it up to the whole training dataset that contains ~4,000 RGB and ~4,000 IR images. There are many pre-trained models for object detection. This project does not aim at real time detection, so I will prioritize performance over speed. These pre-trained models are well developed, but they are essentially black boxes. Therefore, in order to gain a more concrete understanding of deep learning object detection, I would also like to explore the process of building and training models from scratch.

## Conclusions