# Scratch_NeuralNet

In this project our goal was  to implement and train a multi-layer perceptron (MLP) on the CIFAR-10 dataset with data augmentation (Single hidden layer with 64 neurons MLP model).Steps followed are as follows :
1. Download the CIFAR-10 dataset (https://www.cs.toronto.edu/~kriz/cifar.html).Used pickle library to load the dataset.
2. Implemented the image transformation methods mentioned below:
(a) Random Rotation in the range [−180◦, 180◦]
(b) Random cutout (randomly erase a block of pixels from the image with the width and height of the block in the range 0 to 16 pixels. The erased part (cutout) should be filled with a single value)
(c) Random Crop (Add a padding of 2 pixels on all sides and randomly select a block of 32x32 pixels from the padded image)
(d) Contrast & Horizontal flipping. (First, changed the contrast of the image with a factor of α randomly selected from the range (0.5, 2.0) and then fliped the image horizontally with a probability of 0.5)

Insights for changing contrast of an image:
Given an image x with pixel values in range [0, 255], we can change its contrast by a factor of α using the following steps:
i. Change all the pixel values with formula x′(i, j, c) = α·(x(i, j, c)−128)+128. Here,x(i, j, c) refers to the c-th channel value of the (i, j)-th pixel.
ii. Clip the pixel values in x′ so that the final values are in the range [0, 255] Note that α < 1 will decrease the contrast of the image while α > 1 will increase the contrast. For each transformation, define a python function that takes an input image and returns the transformed image. Use of any built-in functions (such as pillow, sklearn, PIL, CV2, etc.) is prohibited for this part. For all the padding operations as well as the gaps created due to the image transformation operations, fill with zero values.
We Demonstrated each transformation method by applying the transform functions on at least one example image.

3. Created the augmented training set using the transformation functions implemented in the previous part. Randomly selected one of the four transformations for each image in the training set and applied it to that image. Combined the transformed images with original training set to get the augmented training set. Note that the number of examples for the augmented training set will be twice that of the unaugmented training set.

4. Use the feature extractor.py file on the original (unaugmented) CIFAR-10 dataset and on the augmented dataset to get 1-dimensional input vectors. You can
ignore the implementation of feature extractor.py and use it directly.

• The feature extractor.py accepts images of size (3×224×224) [Channel×Height×Width].
Use image processing libraries like PIL, CV2 to resize the CIFAR images from (3×32×32)
to (3 × 224 × 224).
• Pass the resized images to feature extraction function of BBResNet18 class to generate
feature vectors
• feature extraction: function expects each image is a numpy.ndarray of dtype: numpy.float32
and shape: [None, 3, 224, 224], where: None represents a variable size. It returns a
numpy.ndarray of dtype: numpy.float32 and shape: [None, 512].

5. Implemented a multi-layer perceptron (MLP) for classification of CIFAR-10 images. Used only a single hidden layer with 64 neurons and ReLu activation function. The input to this MLP will be the 1-dimensional vectors generated in the previous step. 

6. Implemented the back-propagation algorithm from scratch without using any ML library and used it to train the MLP model on:
(a) original training set
(b) augmented training set

7. Evaluated the performance of the following trained MLP models on the original (unaugmented)
test set:
(a) MLP model, trained on original training set
(b) MLP model, trained on augmented training set

