# AnomalyDetectionCVPR2018-Pytorch
Pytorch version of - https://github.com/WaqasSultani/AnomalyDetectionCVPR2018

## Future Improvements
In this section, I list the future improvements I intend to add to this repository. Please feel free to recommend new features. I also happily accept PR's! :smirk:

* I3D feature extraction
* MFNET feature extraction

## Known Issues:

* AUC is not exactly as reported in the paper (0.70 vs 0.75) - might be affected by the weights of C3D

## Install Anaconda Environment
```conda env create -f environment.yml```


```conda activate adCVPR18```

## 
C3D Weights
I couldn't upload here the weights for the C3D model because the file is too big, but it can be found here:
https://github.com/DavideA/c3d-pytorch

## Precomputed Features
Can be downloaded from:

### C3D features
https://drive.google.com/drive/folders/1rhOuAdUqyJU4hXIhToUnh5XVvYjQiN50?usp=sharing

### ResNet-101 features (by @Daniele Mascali)
https://drive.google.com/file/d/1kQAvOhtL-sGadblfd3NmDirXq8vYQPvf/view?usp=sharing

### ResNet-152 features (by @Henryy-rs)
https://drive.google.com/file/d/17wdy_DS9UY37J9XTV5XCLqxOFgXiv3ZK/view

## Pre-Trained Anomaly Detector
Check out <a href="exps/">exps/</a> for for trained models on the pre-computed features

## Features Extraction
Download the dataset from: https://github.com/WaqasSultani/AnomalyDetectionCVPR2018
Arguments:
* dataset_path - path to the directory containing videos to extract features for (the dataset is available for download above)
* model_type - which type of model to use for feature extraction (necessary in order to choose the correct pre-processing)
* pretrained_3d - path to the 3D model to use for feature extraction
```python feature_extractor.py --dataset_path "path-to-dataset" --model_type "fe-model-eg-c3d" --pretrained_3d "path-to-pretrained-fe"```

## Training
Arguments:
* features_path - path to the directory containing the extracted features (pre-computed features are available for download above, or supply your own features extracted from the previous stage)
* annotation_path - path to the annotations file (Available in this repository as `Train_annotations.txt`
```python TrainingAnomalyDetector_public.py --features_path "path-to-dataset" --annotation_path "path-to-train-annos"```

## Generate ROC Curve
Arguments:
* features_path - path to the directory containing the extracted features (pre-computed features are available for download above, or supply your own features extracted from the previous stage)
* annotation_path - path to the annotations file (Available in this repository as `Test_annotations.txt`
* model_path - path to the trained anomaly detection model
```python generate_ROC.py --features_path "path-to-dataset" --annotation_path "path-to-annos" --model_path "path-to-model"```

Using my pre-trained model after 40K iterations, I achieve this following performance on the test-set. I'm aware that the current model doesn't achieve AUC of 0.75 as reported in the original paper. This can be caused by different weights of the C3D model.

<img src=graphs/roc_auc.png width="600"/>

## Demo *

### Off-line (with video loader)
Arguments:
* feature_extractor - path to the 3D model to use for feature extraction
* feature_method - which type of model to use for feature extraction (necessary in order to choose the correct pre-processing)
* ad_model - path to the trained anomaly detection model
* n_segments - the number of segments to chunk the video to (the original paper uses 32 segments)
```python video_demo.py --feature_extractor "path-to-pretrained-fe" --feature_method "fe-method" --ad_model "path-to-pretrained-ad-model" --n_segments "number-of-segments"```

The GUI lets you load a video and run the Anomaly Detection code (including feature extraction) and output a video with a graph of the Anomaly Detection prediction below.

### On-line (via webcam)
Arguments:
* feature_extractor - path to the 3D model to use for feature extraction
* feature_method - which type of model to use for feature extraction (necessary in order to choose the correct pre-processing)
* ad_model - path to the trained anomaly detection model
* clip_length - the length of each video clip (in frames)
```python AD_live_prediction.py --feature_extractor "path-to-pretrained-fe" --feature_method "fe-method" --ad_model "path-to-pretrained-ad-model" --clip_length "number-of-frames"```

The GUI lets you load a video and run the Anomaly Detection code (including feature extraction) and output a video with a graph of the Anomaly Detection prediction below.


*Contrbuted by Peter Overbury of Sussex Universty IISP Group

## Cite
```
@misc{anomaly18cvpr-pytorch,
  author       = "Eitan Kosman",
  title        = "Pytorch implementation of Real-World Anomaly Detection in Surveillance Videos",
  howpublished = "\url{https://github.com/ekosman/AnomalyDetectionCVPR2018-Pytorch}",
  note         = "Accessed: 20xx-xx-xx"
}
```

## FAQ
1. 
```
Q: video_demo doesn't show videos
A: Downlaod and install LAVFilters: http://forum.doom9.org/showthread.php?t=156191
```
