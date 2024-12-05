# Autoencoder Reconstruction of MNIST Images
## Overview
Using autoencoder architecture to perform re-reconstruction of clothing categories in MNIST fashion dataset. Multiple layers for CNN such as upscaling, downscaling, average pooling and batch normalization are used in the architecture. The similarity of reconstructed images is compared with the original images using SSIM metric. Hyperparameter tuning is done using KerasTuner.

## Data
The data used for training and testing came from a github repository by zalandoresearch (https://github.com/zalandoresearch/fashion-mnist) containing 60.000 images of fashion items with its associated labels. The images are 28x28 in size and the dataset contains 10 labels for 10 types of clothing.

![image](https://github.com/user-attachments/assets/edc5b68f-ba9c-4911-91d6-5b2cf7788ae4)

## Approaches and Techniques
### Architecture
Two model architectures are used, one is the base model and the modified model which is meant to be a comparison after adding several modifications to the base models.

#### Base Model
![image](https://github.com/user-attachments/assets/c0f0c499-233b-412e-a05f-72573c1e9b70)

#### Modifications
* The modified model enlargened version of the base model with an additional upscaling and downscaling layer (from 28 x 28 -> 14 x 14 -> 7 x 7 ) with three upscaling and downscaling steps instead of the two in the base model.
* Batch Normalization
* Changing the UpSampling2D layer into a ConvTranspose2D, which is more complex and uses weights that are updated in model training resulting in a generally better model.
adding batch normalization layers and additionally 

#### Hyper parameter tuning
The modified model is tuned using the Keras Tuner library. A random search algorithm is used to find the best reasonable values for certain parameters.
* activation: ["relu", 'leakyrelu', 'tanh']
* units: [32, 64, 128, 256]
* optimizer: ['adam', 'sgd', 'rmsprop']

The tuner found that LeakyRelu, 32 units, with the rmsprop optimizer performed the best

### Result
These images are the result of the tuned modified autoencoder model.

![image](https://github.com/user-attachments/assets/82b140d9-83da-4818-9a6d-587e729f13a0)

#### SSIM scores
The structural similarity index measure (SSIM) is a method for predicting the quality of an image but it is also used for measuring the similarity between two images. It is the metric that I used to evaluate the performance of the autoencoder.

<table >
  <thead>
    <th>Model</th>
    <th>SSIM</th>

  </thead>
  <tr></tr>
  <tr></tr>
 
  <tr>
    <td>Base Model</td>
    <td>0.925</td>
   
  </tr>
  <tr></tr>


  <tr>
    <td>Modified Model</td>
    <td>0.9421</td>
   
  </tr>
  <tr></tr>

  <tr>
    <td>Tuned Modified Model</td>
    <td>0.9436</td>
   
  </tr>

<table >
  
### Conclusion
  
The modified architecture performed better than the base model by a reasonable margin and is further improved after tuning although the improvement is very marginal
    

