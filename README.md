# Fingertips-Position-Estimation-of-a-Robot-Hand
ML final project

There are 6 google colab files in the code part.
Each is named after model and input type.

For model, I choose between cnn and ResNet50.
For input data, I create 4 combinations.

1) 1 channel of RGB image from a single perspective, which I denote as 1img0 in filename.
2) 3 channels of RGB images from a single perspective, which I denote as 3img0 in filename.
3) 2 channels of RGB images from a single perspective + 1 channel of depth image from one perspective, which I denote as 2img0+1depth in filename.
4) 3 channels of depth image from 3 perspective, which I denote as 3depth in filename.

In each file, I basically go through preparing input data, loading train dataset and test dataset, constructing model, cross-validatation, doing grid search. 

In some files, I also tried varing number of epoches, applying learning rate decay and applying data augmentation.

