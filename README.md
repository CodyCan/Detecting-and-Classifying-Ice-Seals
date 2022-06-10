# Detecting and Classifying Ice Seals

## Problem Statement
Global warming has led to massive ice melt that greatly affects the habitat of many animals. Information on their populations is important. Recent development of aerial imaging by drone together with high resolution satellite images has opened up new avenues for population surveys without disturbing the normal activities of these animals. However, the counting is still largely being done manually. Such a process is laborious, time consuming, error-prone. This has motivated us to develop a machine learning tool that is capable of detecting and counting animals from aerial images. In particular, we build deep learning object detection models to detect ice seals and classify their species from RGB imagery.

The main metric will be the mean Average Precision (mAP) which takes into account both the precision and recall. I will be aiming for an mAP of 0.7 at Intersection over Union (IoU) of 0.5.

## Data Acquisition and Preprocessing
The full dataset stored on Azure contains a large number of RGB and IR images (about 40,000 each). The RGB and IR images are pairs of the same view. In this project, I will be using RGB images only. Each RGB image takes up a volume of about 40 MB and has a dimension of 6,576 pixels by 4,384 pixels. In this dataset, about 4,000 images have been annotated. For the train dataset, I programmatically download 1,000 annotated images to Google Drive. The annotation is provided in a csv file. From the csv file, I extracted 6 features that will be used in training an object detector including the file path, the bounding information (xmin, ymin, xmax, ymax), and the class for each bounding box. There are 6 different classes, with one of them accounting for 80% of the time.

## Data Analysis
For this project, I decided to use the RetinaNet object detection model. In general, deep learning object detectors are either one-stage or two-state. In comparison, one-stage detectors are faster at the cost of lower precision. RetinaNet is a one-stage object detector developed by Facebook AI lab with improved precision due to the implementation of a novel loss function called focal loss, and the feature pyramid network. Thus RetinaNet is fast and has high precision. It has also been shown to work well on images with dense and small objects like in the case of satellite images.

A common challenge associated with the high resolution aerial and satellite images that is the large image dimension and the small objects of interest.  As mentioned above, each image has a dimension of 6,576 pixels by 4,384 pixels. By default, RetinaNet will resize the image to 1,333 pixels by 800 pixels. However, we notice that on average the objects of interest have the dimension of 50 pixels by 50 pixels. Thus the resizing would lead to very small bounding boxes. Thus I decided to bypass the resizing step. Even then, many objects are still too small for the default sizes of the anchor boxes in RetinaNet which has the smallest anchor box of 32 pixels by 32 pixels. So an extra step to optimize the dimension of the anchor boxes was needed using the anchor-optimization repo.

## Conclusions
Object detection is a challenging task especially when dealing with images that have dense and small objects. Nevertheless, using RetinaNet, we were able to achieve a mAP of at IoU of 0.5. 

The model can be used to detect, classify, and count ice seals.

The procedure outlined in this project can be also used in many other applications.

Future work include: further optimize the detector, include more images in the train dataset, combine with IR images.
