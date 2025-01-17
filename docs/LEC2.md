# Lecture 2: Image Classification

Image classification is a core computer vision task

## Challenges

- Semantic Gap: the difference between the visual appearance of an object and the semantic meaning of the object, and the computer cannot overcome this by intuition

- Viewpoint Variation: the appearance of an object can change drastically depending on the viewpoint

- Intra-class Variation: mass variation within the same class

- Fine-Grained Categories: the difference between classes is very subtle

- Background Clutter: the background can be very complex and can confuse the model

- Illumination: the appearance of an object can change drastically depending on the lighting

- Deforamation: the appearance of an object can change drastically depending on the deformation

- Occlusion: objects can be partially occluded

## Use Cases

- Medical Imaging
- Galaxy Classification
- ......

Image classification can also be a building block for other computer vision tasks, such as object detection, segmentation, etc.

## Image Classifier

Machine learning is a data-driven approach for building image classifiers. The process is as follows:

1. Collect a dataset of images and labels
2. Use a machine learning algorithm to train a classifier
3. Evaluate the classifier on new images

### Datasets

Some famous datasets for image classification:

- MNIST
- CIFAR-10
- ImageNet
- MIT Places

One direction is to build larger datasets, while another direction is to build more challenging datasets.

- Omniglot: meant to test few-shot learning

### Algorithms

**Nearest Neighbor Classifier**
During training, the classifier memorizes all the training data. During testing, the classifier finds the most similar training image to the testing image and assigns the label of the most similar training image to the testing image.

Distance matrices can be used to find the most similar training image. L1 distance is the sum of the absolute differences between the pixel values of the two images. 

$$
d_1(I_1, I_2) = \sum_p |I_1^p - I_2^p|
$$

The training speed of the nearest neighbor is constant "O(1)". However, the testing speed is slow "O(N)".

Images with low L1 distance can still be very different. Nearest neighbors tend to perform poorly on high-dimensional data. Its decision boundary is very noisy.

**K-Nearest Neighbor Classifier**
Instead of finding the most similar training image, the classifier finds the K most similar training images and assigns the label that appears the most among(majority vote) the K most similar training images.

An increase in K can smooth the decision boundary, but empty space can be misclassified.

Using other distance metrics can also improve the performance of the classifier, such as L2 distance. This is a way human knowledge can be incorporated into the model.

**Hyperparameters**
Hyperparameters are parameters that are not learned during training. They are set before training and are not changed during training. For example, K in the K-Nearest Neighbor Classifier is a hyperparameter.

Hyperparameters are very problem-dependent. Some ideas to set hyperparameters are:

- Choose hyperparameters that work best on the training set: K=1 is a bad example
- Choose hyperparameters that work best on the testing set: No idea how the algorithm will perform on new data, and the testing set should not be used to improve the model
- Choose hyperparameters that work best on the validation set: split the training set into training set, testing set and validation set, and use the validation set to tune the hyperparameters. The testing set is only used to evaluate the model.
- Cross-validation: split the training set into many folds, and use each fold as the validation set and the rest as the training set. The average performance of the model on the validation set is the performance of the model. This is computationally expensive but good for small datasets.

**Curse of Dimensionality**
For uniformly distributed data, the volume of the data increases exponentially with the dimensionality of the data. This means that the data becomes sparse in high-dimensional space. This is a problem for the nearest neighbor classifier and the reason why it is rarely used in practice.