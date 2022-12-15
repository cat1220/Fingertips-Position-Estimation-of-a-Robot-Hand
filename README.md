# Fingertips-Position-Estimation-of-a-Robot-Hand
ML final project

There are 6 google colab files in the code part.

Each is named after model and input type.

For model, I choose between cnn and ResNet50.

For input data, I create 4 combinations.

1 channel of RGB image from a single perspective, which I denote as 1img0 in filename.
3 channels of RGB images from a single perspective, which I denote as 3img0 in filename.
2 channels of RGB images from a single perspective + 1 channel of depth image from one perspective, which I denote as 2img0+1depth in filename.
3 channels of depth image from 3 perspective, which I denote as 3depth in filename.

In each file, I basically go through preparing input data, loading train dataset and test dataset, constructing model, cross-validatation, doing grid search. 

In some files, I also tried varing number of epoches, applying learning rate decay and applying data augmentation.

Findings(Not a surprise)
1. ResNet are generally much better than classic CNN models.
2. Within a model, increasing number of training epoch (like to 50) might not increase performance because of over-fitting problem on the training set.


Findings(A surprise)
1. Although CNN loses and Res wins, their score gap isn't very large, which is surprising.
2. All the best learning rate are close to 1e-4 and 1e-3. Rather than the lucky learning rate 2e-5.
3. Not all augmentation improve the prediction accuracy, although I tried multiple augmentations, which seems to improve the quality of picture according to my eyes. This suggests that for clear original input like the RGB and depth data given, augmentation may not be necessary.
4. Mixing both RGB image and depth image gives the worst performance. This suggests that too much redundant information might hurt performance. Maybe that's why no researchers publish results using them. 
