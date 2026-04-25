# Sign Language Classifier

A sign language classification system built using transfer learning with convolutional neural networks.

This project compares two pretrained CNN architectures, ResNet50 and MobileNetV2, to evaluate their performance on a domain-shifted dataset of low-resolution grayscale images, despite their original training on the ImageNet dataset.

Live demo! https://sign-language-classifier-app.vercel.app/  

> [!NOTE]
> Best results with a plain background, good lighting, and centered hand. Model was trained on controlled studio images — real-world performance may vary.

## Dataset

The model was trained on the Sign Language MNIST dataset, which contains approximately 35,000 grayscale images (28×28) of hand gestures representing alphabet letters (excluding J and Z due to motion)

## Approach

To adapt the dataset for pretrained models, a custom preprocessing and training pipeline was built using TensorFlow. To choose hyperparameters, random search was performed across 8 models per architecture, then the configuration with the highest accuracy was chosen for the evaluation. 

Key steps included:

Splitting data into training, validation, and test sets
Resizing images from 28×28 → 128×128 to balance computational efficiency with feature preservation. 
Converting grayscale images to RGB (3 channels) to match pretrained model input formats
Applying model-specific preprocessing functions (normalization and scaling) to ensure compatibility with pretrained weights


## Results

### MobileNetV2 best model results
<img width="633" height="318" alt="image" src="https://github.com/user-attachments/assets/3bf5a1b7-7d64-4ef4-aec4-b875fc136bd4" />  

### ResNet50 best model results
<img width="633" height="297" alt="image" src="https://github.com/user-attachments/assets/484f8a84-fce1-4db3-9b42-4faf9f206941" />  

## Test results 
<img width="1034" height="115" alt="image" src="https://github.com/user-attachments/assets/07b7c4a0-2b0d-4531-accd-6f1cbc911968" />

### Inference Test results
<img width="622" height="462" alt="image" src="https://github.com/user-attachments/assets/88eebf1a-2fdc-45e7-8b22-28f0b44d195a" />  
<br>

MobileNetV2 achieved 99.1% test accuracy vs ResNet50 at 98.9%, with average inference time of 0.0893 seconds vs 0.1187 seconds, respectively.


## Key Insight
Transfer learning is powerful even on small, domain-shifted datasets. Both ResNet50 and MobileNetV2 were pretrained on ImageNet yet both achieved >98% accuracy on a dataset of low-resolution grayscale hand gestures. This suggests that the low-level features these models learned (edges, textures, shapes) are general enough to transfer across very different visual domains with minimal fine-tuning.

One important detail for transfer learning is that you must both preprocess your data appropriately for each pretrained model and apply the per-model preprocessor function to transform the image into a structure more similar to the one the model was trained on. Take note of what the model's preprocessing function already does, and do not do these steps in your custom preprocessing.  For custom preprocessing, the most important steps were resizing and converting black-and-white images to RGB. I was only achieving ~.4 accuracy, however, until I applied the per-model preprocessor function, which increased accuracy to >.70 within the first epoch!

One concern I had when creating this experiment was determining which hyperparameter values yielded the best-performing model for the specific architecture. I first decided to do a brute-force search, which I quickly learned is a long, computationally intensive method for discovering these hyperparameter values. I switched to randomness because it provides a good approximation of optimal solutions without the cost of searching for one.  Once I started training my models and saw the accuracy they reached fairly quickly, I realized that for tasks that are not too challenging for the model, hyperparameter choices have little effect on the model's performance (meaning that no special combination was needed and that following conventions for learning rate, dense layers, and dropout rate is good enough).  Both models consistently achieved accuracy>.95 within only 5 epochs. 


## How to Run

1. Clone the repo
   
```bash
   git clone https://github.com/yourusername/sign-language-research.git
```

2. Open in Google Colab (recommended) — all dependencies are installed in the first cell

3. Or run locally with Jupyter — run the first cell to install dependencies

