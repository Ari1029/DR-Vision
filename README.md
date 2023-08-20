# DR-Vision
Diabetic Retinopathy stage classification using transfer learning and ensembling.

This project leverages transfer learning and ensembling techniques in order to classify varying stages of diabetic retinopathy (0 - No DR, 1 - Mild, 2 - Moderate, 3 - Severe, 4 - Proliferative DR). There were 2 datasets used in this project. The first includes approximately 35000 retina images from a 2015 Kaggle competition called 'Diabetic Retinopathy Detection'. These images were used to pretrain a base model. The next dataset includes 4700 retina images from the 'ATPOS 2019 Blindness Detection' challenge.

A variety of techniques were used throughout this project. First, I pre-trained an EfficientNet B3 model using transfer learning on the first dataset due to the abundance of retina images availalbe. Then, I created 4 models with different combinations of image preprocessing and augmentations in order to mimic possible variations of retina images. These 4 models were finetuned on 80% of the 2019 data, using the remaining 20% as the cross validation set.

Here is an example of the auto-cropping results, one of the preprocessing techniques used. Notice how the retina images are focused and unnecessary borders are completely cropped:

<img width="700" height="100" alt="image" src="https://github.com/Ari1029/DR-Vision/assets/45503218/e0466e32-1f5b-4fd3-87b4-cddf7a127e2b">

Finally, test time augmentation (TTA) was used for each image during inference. In particular, 90 degree rotations, vertical and horizontal flips were applied to each image. This results in 4 predictions for each model, which were averaged to obtain one model's final prediction. Then, the final predictions for each sample are averaged to decide on the final class. A test set was created, as the cross validation set was used to optimize for the best-performing threshold.

We observe that the final model achieves an 86% test set accuracy.

Here is the resulting confusion matrix for test set classifications:

<img width="467" alt="image" src="https://github.com/Ari1029/DR-Vision/assets/45503218/03a98814-3efa-40bd-841f-a16831a9157e">
