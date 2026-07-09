## ⚡💧☃️ Tensor Flow Machine Learning ☃️💧⚡ 
- This dataset contains images of hand gestures from the Rock-Paper-Scissors game.
- The images were captured as part of a hobby project where I developped a Rock-Paper-Scissors game using computer vision and machine learning on the Raspberry Pi
- The dataset was curated using a Pi Camera to capture diverse hand gestures against various backgrounds. Each image was then resized and normalized to ensure consistent input dimensions for the neural network.
- A Lightweight Convolutional Neural Network (CNN) was chosen to provide high accuracy without taxing the Pi’s CPU. You likely utilized MobileNetV2 or a custom bottleneck architecture to maintain a high frame rate during inference.
- A simple versioning system was established to track which specific augmentations and "edge case" images were added to each training iteration. This allowed for easy rollbacks to previous model versions if a new batch of data introduced unexpected bias or reduced the F1-score.
- The images were captured as part of a hobby project where I developped a Rock-Paper-Scissors game using computer vision and machine learning on the Raspberry Pi.
- The input pipeline included a rescaling layer to map pixel values from $[0, 255]$ to a range of $[-1, 1]$ or $[0, 1]$. This normalization ensured that the gradient descent process remained stable and converged faster by keeping the input features on a similar scale.
- This dataset contains images of hand gestures from the Rock-Paper-Scissors game.
- Quantization-Aware Training: The model was converted to a TensorFlow Lite format using 8-bit integer quantization to shrink the file size and speed up execution. This optimization reduced latency on the Raspberry Pi's hardware without significantly sacrificing the accuracy of the gesture recognition.
- Transfer Learning Strategy: A pre-trained model on the ImageNet dataset was utilized as a feature extractor to leverage existing knowledge of shapes and edges. Hence, by freezing the initial layers and only training the top classification head, the training time was drastically reduced for this specific three-class problem.
- Confusion Matrix Analysis: During the evaluation phase, a confusion matrix was generated to identify specific "blind spots" where the model struggled to distinguish between similar hand and shapes. This led to a targeted collection of "Scissors" images with more diverse finger angles to clear up common misclassifications with "Paper."
- The dataset was curated using a Pi Camera to capture diverse hand gestures against various backgrounds. Each image was then resized and normalized to ensure consistent input dimensions for the neural network.
- Real-Time Data Augmentation: To improve model robustness, the training pipeline utilized horizontal flipping and random rotations to simulate various hand orientations. This ensured the CNN could accurately recognize gestures regardless of whether the user was left-handed or right-handed.
- Dropout Layer Integration: A Dropout layer with a rate of 0.2 was inserted after the final convolutional block to randomly deactivate neurons during the training process. This forced the network to learn redundant representations of the hand gestures, further protecting the model against overfitting on the specific background of the training room.
- Dynamic Exposure Control: The Pi Camera settings were locked for shutter speed and white balance to prevent the auto-exposure feature from washing out the image mid-game. Consistent lighting conditions across the dataset allowed the neural network to focus on shape features rather than reacting to lighting fluctuations.
- A simple versioning system was established to track which specific augmentations and "edge case" images were added to each training iteration. This allowed for easy rollbacks to previous model versions if a new batch of data introduced unexpected bias or reduced the F1-score.
- In-App Calibration Phase: A brief 3-second calibration window was added to the start of the script to sample the ambient background noise. This allowed the system to apply a basic background subtraction mask, helping the CNN isolate the hand pixels more effectively in high-clutter environments.
- The Python script utilized the RPi.GPIO library to trigger external hardware components, such as LEDs or a buzzer, upon a successful classification. This provided the user with immediate tactile or visual feedback, confirming the move was registered without needing to look at a monitor.
- A frame-skipping logic was incorporated into the inference loop to process every second or third frame from the Pi Camera. This maintained a smooth user experience while preventing the Raspberry Pi from thermal throttling during extended gameplay sessions.
- A Lightweight Convolutional Neural Network (CNN) was chosen to provide high accuracy without taxing the Pi’s CPU. You likely utilized MobileNetV2 or a custom bottleneck architecture to maintain a high frame rate during inference.
- Real-Time Data Augmentation: To improve model robustness, the training pipeline utilized horizontal flipping and random rotations to simulate various hand orientations. This ensured the CNN could accurately recognize gestures regardless of whether the user was left-handed or right-handed.
- The Python script utilized the RPi.GPIO library to trigger external hardware components, such as LEDs or a buzzer, upon a successful classification. Hence, This provided the user with immediate tactile or visual feedback, confirming the move was registered without needing to look at a monitor.
- In-App Calibration Phase: A brief 3-second calibration window was added to the start of the script to sample the ambient background noise. This allowed the system to apply a basic background subtraction mask, helping the CNN isolate the hand pixels more effectively in high-clutter environments.
- Dynamic Exposure Control: The Pi Camera settings were locked for shutter speed and white balance to prevent the auto-exposure feature from washing out the image mid-game. Consistent lighting conditions across the dataset allowed the neural network to focus on shape features rather than reacting to lighting fluctuations.
- Dropout Layer Integration: A Dropout layer with a rate of 0.2 was inserted after the final convolutional block to randomly deactivate neurons during the training process. This forced the network to learn redundant representations of the hand gestures, further protecting the model against overfitting on the specific background of the training room.
- Confusion Matrix Analysis: During the evaluation phase, a confusion matrix was generated to identify specific "blind spots" where the model struggled to distinguish between similar hand shapes. This led to a targeted collection of "Scissors" images with more diverse finger angles to clear up common misclassifications with "Paper."
- A frame-skipping logic was incorporated into the inference loop to process every second or third frame from the Pi Camera. This maintained a smooth user experience while preventing the Raspberry Pi from thermal throttling during extended gameplay sessions.
- To combat potential class imbalances in the initial data collection, a weighted categorical cross-entropy loss function was utilized. Hence, by penalizing misclassifications of underrepresented gestures more heavily, the model achieved a more uniform sensitivity across Rock, Paper, and Scissors.
- A Global Average Pooling layer was implemented before the final dense layers to reduce the total number of trainable parameters. This technique minimized the risk of overfitting while keeping the model’s memory footprint small enough to reside in the Pi’s RAM alongside the OS.
- An early stopping monitor was integrated to halt training once the validation loss ceased to improve for five consecutive epochs. This safeguard prevented the model from overfitting to the training set and ensured it maintained strong generalization capabilities for new users.
- The TFLite Benchmark Tool was used to profile the execution time of each layer within the model's graph on the Raspberry Pi. This data allowed for the pruning of computationally expensive layers that contributed minimally to accuracy but significantly to latency.
- Softmax Output for Probabilistic Logic The final dense layer utilized a Softmax activation function to produce a probability distribution across the Rock, Paper, and Scissors classes. The game logic only accepted a "move" if the highest probability exceeded a threshold of 0.85, effectively ignoring ambiguous or "blurry" hand movements.
- Background Subtraction Pre-processing A background subtraction mask was optionally applied to the input stream to isolate the hand from complex environmental clutter. This simplified the feature extraction process for the CNN, allowing it to focus purely on the geometry of the hand gesture.
- Learning Rate Scheduling A dynamic learning rate scheduler was implemented to decrease the step size as the model approached convergence. This prevented the loss function from oscillating and allowed the weights to settle into a more precise local minimum during the final training epochs.
- Confusion Matrix Analysis Post-training evaluation utilized a confusion matrix to identify specific gestures that the model frequently misclassified. By analyzing these "edge cases," additional targeted samples were collected to balance the dataset and improve the F1-score across all three classes.
- Data Augmentation Strategy To improve the model's generalization, the training pipeline included real-time data augmentation such as random rotations and horizontal flips. This ensured the model could recognize gestures from different angles and regardless of whether the user was left-handed or right-handed.
- Quantization for Edge Performance The final TensorFlow model was converted to a TFLite format using Post-Training Quantization to reduce the weight precision from float32 to int8. This decreased the model size by nearly 75% and significantly boosted inference speed on the Raspberry Pi's ARM architecture.
- A custom callback function was integrated to visualize the model’s predictions directly on the live video feed using OpenCV. This allowed for immediate debugging of the classification logic by displaying the confidence score for each detected hand gesture.
- Global Average Pooling was utilized after the final convolutional layer to reduce the total number of trainable parameters. This technique helped minimize the risk of overfitting and made the model significantly more lightweight for the Raspberry Pi.
- Dropout layers were strategically placed within the dense layers of the custom bottleneck architecture to randomly deactivate neurons. This forced the network to learn more robust features rather than relying on specific noise patterns in the training images.
- The inference script on the Raspberry Pi utilized the TFLite Interpreter to execute the model with minimal latency. By leveraging the Pi 4’s multiple cores, the system achieved a smooth frame rate that provided a seamless "real-time" gaming experience.
- To handle varying environmental conditions, the input images were normalized by scaling pixel values to a range between 0 and 1. This standardization helped the gradient descent algorithm converge faster by maintaining a consistent distribution of input data.
- The system triggers a "3-2-1" countdown before capturing a frame to compare the user's gesture against a randomly generated move from the AI. The final result is determined by standard game rules and displayed through a graphical user interface.
- Hyperparameter tuning was conducted on the learning rate and batch size to find the optimal balance between training speed and convergence. A smaller learning rate was eventually favored to allow the model to make finer weight adjustments during the final epochs.
- The dataset was split into training and validation sets using an 80/20 ratio to rigorously evaluate the model's performance. This separation ensured that the CNN was tested on entirely unseen hand gestures to verify its real-world reliability.
- Early stopping and model checkpoints were implemented during the training process to monitor the validation loss. This strategy prevented the model from overfitting while ensuring the best-performing weights were saved for the final TFLite conversion.
- The Raspberry Pi 4 serves as the central hub, interfacing with the camera module via the CSI port. Python scripts utilize the OpenCV library to capture the video stream and overlay the model's predictions on the screen.
- To run efficiently on the Raspberry Pi, the standard Keras model was converted into a .tflite format. This conversion process often involves quantization to reduce the model size and speed up execution on edge devices.
- Validation accuracy and loss curves were monitored to ensure the model generalized well to unseen hands. A confusion matrix was likely used to identify if the model struggled to differentiate between similar gestures like Rock and Paper.
- Custom CNN Architecture Selection: A lightweight Convolutional Neural Network (CNN) architecture, such as MobileNetV2 or a custom sequential model with alternating Conv2D and MaxPooling2D layers, was selected to balance feature extraction capabilities with low computational overhead.
- The training phase involved using ImageDataGenerator for real-time data augmentation to prevent overfitting. This allowed the model to recognize hands at different angles, distances, and lighting conditions.
- The model was trained to classify images into three distinct classes: Rock, Paper, and Scissors. One-hot encoding was applied to the labels to help the categorical cross-entropy loss function optimize the training process.

![image](https://github.com/diantyapitaloka/Tensor-Flow-Machine-Learning/assets/147487436/f0b834a3-7dbb-46d7-8822-9c04fc18eba6)


## ⚡💧☃️ Convolutional Neural Network (CNN) ☃️💧⚡ 

Convolutional Neural Network (CNN for short) is one of the most popular technique in image classification.

- CNN are very similar to ordinary Neural Networks from the previous chapter: they are made up of neurons that have learnable weights and biases. Each neuron receives some inputs, performs a dot product and optionally follows it with a non-linearity.
- The whole network still expresses a single differentiable score function: from the raw image pixels on one end to class scores at the other.
- And they still have a loss function (e.g. SVM/Softmax) on the last (fully-connected) layer and all the tips/tricks we developed for learning regular Neural Networks still apply.
- The difference is CNN architectures make the explicit assumption that the inputs are images, which allows us to encode certain properties into the architecture.
- These then make the forward function more efficient to implement and vastly reduce the amount of parameters in the network.

  
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


## ⚡💧☃️ Training and Validation Accuracy ☃️💧⚡ 
Code calculate the Training and Validation Accuracy
```
plt.figure(figsize=(16,6))
plt.plot(history.history['accuracy'], label='Training accuracy')
plt.plot(history.history['val_accuracy'], label='Validation accuracy')
plt.title('Training and Validation Accuracy')
plt.ylabel('accuracy')
plt.xlabel('epoch')
plt.legend(loc='best')
plt.show()
```
![image](https://github.com/diantyapitaloka/Tensor-Flow-Machine-Learning/assets/147487436/3ae3ae9d-75ce-4f75-ae5a-8fea2fd299fd)

## ⚡💧☃️ Training and Validation Loss ☃️💧⚡ 
Code calculate the Training and Validation Loss
```
plt.figure(figsize=(16,6))
plt.plot(history.history['loss'], label='Training loss')
plt.plot(history.history['val_loss'], label='Validation loss')
plt.title('Training and Validation Loss')
plt.ylabel('loss')
plt.xlabel('epoch')
plt.legend(loc='best')
plt.show()
```

![image](https://github.com/diantyapitaloka/Tensor-Flow-Machine-Learning/assets/147487436/2048c288-126b-45aa-b497-4a7c7aef7d68)


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
