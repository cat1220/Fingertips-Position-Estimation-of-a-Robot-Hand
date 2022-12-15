# Fingertips-Position-Estimation-of-a-Robot-Hand

There are 6 google colab files in the code part. Each is named after model and input type. For model, I choose between cnn and ResNet50.

For input data, I create 4 combinations.

------1 channel of RGB image from a single perspective, which I denote as 1img0 in filename.

------3 channels of RGB images from a single perspective, which I denote as 3img0 in filename.

------2 channels of RGB images from a single perspective + 1 channel of depth image from one perspective, which I denote as 2img0+1depth in filename.

------3 channels of depth image from 3 perspective, which I denote as 3depth in filename.

In each file, I basically go through preparing input data, loading train dataset and test dataset, constructing model, cross-validatation, doing grid search. 

In some files, I also tried varing number of epoches, applying learning rate decay and applying data augmentation.

Findings------------------(Not a surprise)
1. ResNet are generally much better than classic CNN models. According to Kaggle results, CNN models have twice the loss of Res models, (0.0004 compared to 0.0002).
2. It's not necessary that the top1 hyperparametes on validation set outperform top2 or 3 hyperparameters on 20 run of whole training set. For example, in res_3depth, after grid search on validation set, the hyperparameters combination lr = 1e-3, momentum = 0.91 is better than the combination lr = 9e-4, momentum = 0.91. But after trying both combinations on 20 run of whole training set, the latter one gives better results.  Just like someone who leads in the first might not keep the leading position in the last.
3. Also, it's not necessary that the top1 optimizer on 20 run of whole training set outperforms the second coming one on Kaggle results. This might because Kaggle only uses part of testing data. Or because there exists over-fitting in our training. For example, in res_3img0, although ADAM with best parameters perform better than SGD, on Kaggle, SGD still wins over ADAM. 
4. Not all augmentation improve the prediction accuracy, even if it seems to improve the quality of picture according to human eyes. For example, in res_3depth with augmentation, although I carefully picked a augmentation among all possible augmentations,  which is to invert the depth image to make it brighter and more colorful, in the first round of grid search, the loss is much larger than previously without augmentation. This suggests that whether an augmentation is good or not shall be verified after training rather than just looking.
5. Within a model, increasing number of training epoches (like to 50 run) might not increase performance because of over-fitting problem on the training set.

Findings--------------------(A surprise)
1. Although CNN loses and Res wins, their score gap isn't very large, which is surprising. If you further take into account the length of training, CNN is actually not a bad choice.
2. Mixing both RGB image and depth image gives the worst performance. This suggests that too much redundant information might hurt performance. Maybe that's why no researchers publish results using them. 
3. All the best learning rate are close to 1e-3. Rather than the lucky learning rate 2e-5.
4. Applying learning rate decay within 20 training epoches doesn't increase performance. Although package torch.optim.lr\_scheduler sounds fancy, it doesn't help us improve performance in this goal.
5. 3 channels of RGB data performs better than 1 channel of RGB data, although they contain same information for human eyes.
