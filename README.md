## ⚡💧☃️ Tensor Flow Machine Learning ☃️💧⚡ 
This dataset contains images of hand gestures from the Rock-Paper-Scissors game. The images were captured as part of a hobby project where I developped a Rock-Paper-Scissors game using computer vision and machine learning on the Raspberry Pi

![image](https://github.com/diantyapitaloka/Tensor-Flow-Machine-Learning/assets/147487436/f0b834a3-7dbb-46d7-8822-9c04fc18eba6)


## ⚡💧☃️ Convolutional Neural Network (CNN) ☃️💧⚡ 

Convolutional Neural Network (CNN for short) is one of the most popular technique in image classification.

CNN are very similar to ordinary Neural Networks from the previous chapter: they are made up of neurons that have learnable weights and biases. Each neuron receives some inputs, performs a dot product and optionally follows it with a non-linearity. The whole network still expresses a single differentiable score function: from the raw image pixels on one end to class scores at the other. And they still have a loss function (e.g. SVM/Softmax) on the last (fully-connected) layer and all the tips/tricks we developed for learning regular Neural Networks still apply.

The difference is CNN architectures make the explicit assumption that the inputs are images, which allows us to encode certain properties into the architecture. These then make the forward function more efficient to implement and vastly reduce the amount of parameters in the network.

  
![image](https://github.com/diantyapitaloka/Tensor-Flow-Machine-Learning/assets/147487436/1cd62f84-ea6e-4bf2-9cc7-bd1945361d08)

## ⚡💧☃️ Contents ☃️💧⚡ 
The dataset contains a total of 2188 images corresponding to the 'Rock' (726 images), 'Paper' (710 images) and 'Scissors' (752 images) hand gestures of the Rock-Paper-Scissors game. All image are taken on a green background with relatively consistent ligithing and white balance.

## ⚡💧☃️ Format ☃️💧⚡ 
All images are RGB images of 300 pixels wide by 200 pixels high in .png format. The images are separated in three sub-folders named 'rock', 'paper' and 'scissors' according to their respective class.

## ⚡💧☃️ Import Library and Download the Dataset ☃️💧⚡ 
This project is created using TensorFlow, Numpy and Matplotlib among others. 

Here are few images taken from the dataset:

![image](https://github.com/diantyapitaloka/Tensor-Flow-Machine-Learning/assets/147487436/1b92d61c-d940-49ac-aabb-5d6aa94afec5)

## ⚡💧☃️ Image Augmentation using ImageDataGenerator ☃️💧⚡ 
ImageDataGenerator is used for data train and data validation. We can use ImageDataGenerator for data preprocessing, separating train and validation data, and image Augmentation. **Image Augmentation** is a technique to increase the volume of data train by duplicating the data with various parameter.

## ⚡💧☃️ Create CNN Model and Model Training ☃️💧⚡ 
For CNN model, we will define the convolutional layer and Pooling layer. We also create callbacks to stop training process when desired model accuracy is achieved.

## ⚡💧☃️ Making Prediction Rock ☃️💧⚡ 
After creating the model, we will predict the class of a new image

```
print(train_generator.class_indices)
```

predict new image based on created model

```
uploaded = files.upload()

for fn in uploaded.keys():

  predicting images
  path = fn
  img = image.load_img(path, target_size=(150,150))

  imgplot = plt.imshow(img)
  x = image.img_to_array(img)
  x = np.expand_dims(x, axis=0)
  images = np.vstack([x])

  classes = model.predict(images, batch_size=10)
  outclass = np.argmax(classes)

  print(fn)
  if outclass==0:
    print('This is a paper hand gesture')
  elif outclass==1:
    print('This is a rock hand gesture')
  else:
    print('This is a scissors hand gesture')
```

![image](https://github.com/diantyapitaloka/Tensor-Flow-Machine-Learning/assets/147487436/5efc07c9-8c09-4840-b12b-810b320cc165)

## ⚡💧☃️ Making Prediction Scissors ☃️💧⚡ 
After creating the model, we will predict the class of a new image

predict new image based on created model

```
uploaded = files.upload()

for fn in uploaded.keys():

  predicting images
  path = fn
  img = image.load_img(path, target_size=(150,150))

  imgplot = plt.imshow(img)
  x = image.img_to_array(img)
  x = np.expand_dims(x, axis=0)
  images = np.vstack([x])

  classes = model.predict(images, batch_size=10)
  outclass = np.argmax(classes)

  print(fn)
  if outclass==0:
    print('This is a paper hand gesture')
  elif outclass==1:
    print('This is a rock hand gesture')
  else:
    print('This is a scissors hand gesture')
```

![image](https://github.com/diantyapitaloka/Tensor-Flow-Machine-Learning/assets/147487436/9e190453-ab6f-4c1c-9b9d-0352d331794c)


## ⚡💧☃️ Model Evaluation ☃️💧⚡ 
We use accuracy for our metrics. 
| Metrics | Training Score | Validation Score |
| --- | --- | --- |
| Accuracy | 0,9700 | 1,000 |
| Loss | 0,0950 | 0,0376 |

## ⚡💧☃️ Recommendation ☃️💧⚡ 
Various technique could be used to increase the accuracy and decrease the loss of the model. Some suggestion are:
- Transfer Learning using VGG16, ResNet and AlexNet.
- Add padding and stride in convolutional layer.
- Understanding Impact Learning Rate in Neural Network.
- Dropout Regularization in Deep Learning.

## ⚡💧☃️ References ☃️💧⚡ 

[1] https://blog.keras.io/building-powerful-image-classification-models-using-very-little-data.html

[2] https://cs231n.github.io/convolutional-networks/

[3] https://deepai.org/machine-learning-glossary-and-terms/max-pooling

[4] https://towardsdatascience.com/understanding-and-implementing-dropout-in-tensorflow-and-keras-a8a3a02c1bfa

[5] https://keras.io/api/callbacks/reduce_lr_on_plateau/

[6] https://keras.io/api/optimizers/adam/
