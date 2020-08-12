
<p align="center">
<img src="https://github.com/piyalong/volan-yolo/blob/master/Examples/ezgif-3-75d32102d9c6.gif">
</p>

# Volan v.2018: object detection in aerial imagery for disaster response and recovery



## **Table of Contents**
1. [Introduction](#introduction)
2. [Article](#article)
3. [Dataset](#dataset)
4. [BR calculation and data balancing](#br-calculation-and-data-balancing)
4. [Pre-trained models](#pre-trained-models)
5. [Tutorials](#tutorials)

## **Introduction**


Project Volan v.2018 aims at extracting accurate and prompt information on the disaster-affected objects from aerial visual data during disasters. Particularly, a CNN model, YOLO, is used to detect classes including car, undamaged roof, damaged roof, vegetation, debris, and flooded area. A detailed description of the methodology and dataset are described in the following article.

## Article

[Convolutional neural networks for object detection in aerial imagery for disaster response and recovery](https://www.sciencedirect.com/science/article/pii/S1474034619305828)
\
Advanced Engineering Informatics, 43, pp101009\
Yalong Pi, Nipun D. Nath, Amir H. Behzadan


Please cite the article if you use the dataset, model or method(s), or find the article useful in your research. Thank you!

### LaTeX citation:

@article{Pi2020,
    author  = {Yalong Pi and Nipun D. Nath and Amir H. Behzadan},
    title   = {Convolutional neural networks for object detection in aerial imagery for disaster response and recovery},
    journal = {Advanced Engineering Informatics},
    volume  = {43},
    year    = {2020},
    pages   = {101009}


### **Implementation**

### Dependencies
- `Keras 2.0`
- `numpy`
- `opencv`
- `matplotlib`
- `pandas`

**@TODO:** Please stay tuned! The detailed description of the implementation (training + testing) is coming soon.

## **Dataset**

### Dataset statisctics


Volan v.2018 dataset contains 65,580 images extracted from web-mined videos. All the videos, with the same name as appeared in the paper, can be found in the following links. The video annotation files are named as "VOLAN_XXX_gt.txt" with each line corresponding to every consecutive frame in the video named VOLAN_XXX.

[Volan001](https://www.youtube.com/watch?v=vkUlJ8jlbx8)
[Volan002](https://www.youtube.com/watch?v=XRdUV4WqnDE&t=2s)
[Volan003](https://www.youtube.com/watch?v=EsKY6tRsoE4&t=4s)
[Volan004](https://www.youtube.com/watch?v=vkUlJ8jlbx8)
[Volan005](https://www.youtube.com/watch?v=Hl-9BdPkp-0&t=2s)
[Volan006](https://www.youtube.com/watch?v=SybD-lXqYR8&t=133s)
[Volan007](https://www.youtube.com/watch?v=9nLpGrpCP3o)
[Volan008](https://www.youtube.com/watch?v=d5FHtBO6vmw)

### Annotation example

 For each frame, the annotation line looks like below: 
*0,15,104,350,472,552,Undamaged_Roof0,610,316,906,536,Undamaged_Roof1,201,127,265,201,Car0,3,225,158,293,Car1,405,182,539,248,Debris0,348,272,422,317,Car2,447,292,665,398,Damaged_Roof0,762,167,892,244,Damaged_Roof1,560,24,661,54,Undamaged_Roof2,253,50,311,93,Car3,722,88,789,136,Car4,1010,66,1046,93,Car5,998,577,1067,691,Car6,881,434,1001,561,Vegetation0,471,422,557,519,Vegetation1*

Here, the first number (e.g., “0”) indicates the frame number and the second number (e.g., “15”) represents the total number of instances in the frame. Before each label, e.g., “Undamaged_Roof0”, there are four numbers indicating the x1 (top-left x), y1 (top-left y), x2 (bottom-right x), and y2 (bottom-right y) coordinates of the bounding box on the image. Loading one frame with its annotation will display the example as below. 

<img src="https://github.com/piyalong/volan-yolo/blob/master/Examples/annotation.png"   align="middle"/>



## **BR calculation and data balancing**

### Balance Ratio (BR)

As mentioned in the paper, balance ratio (BR) is used to balance the Volan v.2018 dataset that results in better performance on the unseen data (Volan007 and 008). The calculation of BR is expressed in the Equation below and BR.py computes the BR value of any given annotation file. In this Equation, i<sub>nk</sub> indicates the number of instances of class *𝑛* in the frame *𝑘*. The total number of classes is *𝑐*, and the total amount of frames is *𝑓*. Moreover,  ![alt text](https://github.com/piyalong/volan-yolo/blob/master/Examples/nhat.PNG) denotes the average number of instances for class *c* in *f* frames. By definition, the higher BR implies a less-balanced dataset. The most balanced dataset should have a BR value of 0.
<p align="center">
<img width=400 src="https://github.com/piyalong/volan-yolo/blob/master/Examples/BR.png"  >
</p>

### Model training and testing

Particularly in Volan v.2018, the minimum BR is obtained by looping through all the possible cutting thresholds using balance.py, followed by training YOLO model on selected (i.e., balanced) data. In total, 8 models are trained based on different combination and the results are in the following table. The figure below shows the detail performance of Model2 (best on unseen data) on test data from balanced and unbalanced drone, balanced and unbalanced helicopter, Volan007, and 008. 

<img src="https://github.com/piyalong/volan-yolo/blob/master/Examples/Capture.PNG"   align="middle"/>

<p align="center">
<img src="https://github.com/piyalong/volan-yolo/blob/master/Examples/results.jpg" width=800  >
</p>

## **Pre-trained Models**

Models trained on Volan v.2018 dataset are available on the following links: [8 mdoels] (https://drive.google.com/drive/folders/1x__pJZLJomjzeGFjlaz_Ga1XqnzZU5l5)

## **Tutorials**


The model can be trained using train.py with corresponding names of the images and annotations. The trained models will be saved in “tmp/” folder. The evaluation.py takes testing images and annotations to measure the precision, recall and mAP. To apply the trained model, use detection.py to load your images or videos to output the detections.<br/>
**@TODO:** Please stay tuned! The detailed step-by-step tutorials are coming soon.
