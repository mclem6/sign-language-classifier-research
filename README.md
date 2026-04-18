Sign Language Classifier

A sign language classification system built using transfer learning with convolutional neural networks.

This project compares two pretrained CNN architectures, ResNet50 and MobileNetV2, to evaluate their performance on a domain-shifted dataset consisting of low-resolution grayscale images, in contrast to their original training on the ImageNet dataset.

Dataset

The model was trained on the Sign Language MNIST dataset, which contains approximately 35,000 grayscale images (28×28) of hand gestures representing alphabet letters (excluding J and Z due to motion)

Approach

To adapt the dataset for pretrained models, a custom preprocessing and training pipeline was built using TensorFlow. To choose hyperparameters, random search was performed across 8 models per architecture, then the configuration with the highest accuracy was chosen for the evaluation. 

Key steps included:

Splitting data into training, validation, and test sets
Resizing images from 28×28 → 128×128 to balance computational efficiency with feature preservation. 
Converting grayscale images to RGB (3 channels) to match pretrained model input formats
Applying model-specific preprocessing functions (normalization and scaling) to ensure compatibility with pretrained weights


Results
waititng for results.......

Results


Key Insights


How to Run

