# EX 3 Convolutional Deep Neural Network for Digit Classification

## AIM
To Develop a convolutional deep neural network for digit classification and to verify the response for scanned handwritten images.

## Problem Statement and Dataset
Digit classification and to verify the response for scanned handwritten images.

The MNIST dataset is a collection of handwritten digits. The task is to classify a given image of a handwritten digit into one of 10 classes representing integer values from 0 to 9, inclusively. The dataset has a collection of 60,000 handwrittend digits of size 28 X 28. Here we build a convolutional neural network model that is able to classify to it's appropriate numerical value.

![data](https://github.com/Dhanudhanaraj/mnist-classification/assets/119218812/0c1b6a12-b388-4409-b2dc-846a0d4e7473)

## Neural Network Model
![Screenshot 2024-03-20 143629](https://github.com/AbishekAnand15/mnist-classification/assets/118706942/c6b0a8cb-8680-4d97-b744-35611e09ad1c)

## DESIGN STEPS

### STEP 1:
Import tensorflow and preprocessing libraries.
### STEP 2:
Download and load the dataset
### STEP 3:
Scale the dataset between it's min and max values
### STEP 4:
Using one hot encode, encode the categorical values
### STEP 5:
Split the data into train and test
### STEP 6:
Build the convolutional neural network model
### STEP 7:
Train the model with the training data
### STEP 8:
Plot the performance plot
### STEP 9:
Evaluate the model with the testing data
### STEP 10:
Fit the model and predict the single input

## PROGRAM

### Name:Abishek Xavier A
### Register Number:212222230004
```
## Load the dataset from the tensorflow library.
import numpy as np
from tensorflow import keras
from tensorflow.keras import layers
from tensorflow.keras.datasets import mnist
import tensorflow as tf
import matplotlib.pyplot as plt
from tensorflow.keras import utils
import pandas as pd
from sklearn.metrics import classification_report,confusion_matrix
from tensorflow.keras.preprocessing import image

## Preprocess the dataset.
(X_train, y_train), (X_test, y_test) = mnist.load_data()
     
X_train.shape

X_test.shape

single_image= X_train[0]
     
single_image.shape

plt.imshow(single_image,cmap='gray')

y_train.shape

X_train.min()

X_train.max()

X_train_scaled = X_train/255.0
X_test_scaled = X_test/255.0

X_train_scaled.min()

X_train_scaled.max()

y_train[0]

y_train_onehot = utils.to_categorical(y_train,10)
y_test_onehot = utils.to_categorical(y_test,10)

type(y_train_onehot)

y_train_onehot.shape

single_image = X_train[500]
plt.imshow(single_image,cmap='gray')

y_train_onehot[500]

X_train_scaled = X_train_scaled.reshape(-1,28,28,1)
X_test_scaled = X_test_scaled.reshape(-1,28,28,1)

## Create and train your model.
model = keras.Sequential()
model.add(layers.Input(shape=(28,28,1)))
model.add(layers.Conv2D(filters=32,kernel_size=(3,3),activation='relu'))
model.add(layers.MaxPool2D(pool_size=(2,2)))
model.add(layers.Flatten())
model.add(layers.Dense(64,activation='relu'))
model.add(layers.Dense(10,activation='softmax'))

model.summary()

## Compile the model
model.compile(loss='categorical_crossentropy',optimizer='adam',metrics='accuracy')

## Fit the model    
model.fit(X_train_scaled ,y_train_onehot, epochs=8,batch_size=128, validation_data=(X_test_scaled,y_test_onehot))

## Include the training loss, validation loss vs iteration plot.
metrics = pd.DataFrame(model.history.history)
metrics.head()

print("Abishek Xavier A 212222230004")
metrics[['accuracy','val_accuracy']].plot()

print("Abishek Xavier A 212222230004")
metrics[['loss','val_loss']].plot()

## Test the model for your handwritten scanned images.
x_test_predictions = np.argmax(model.predict(X_test_scaled), axis=1)

print("Abishek Xavier A 212222230004")
print(confusion_matrix(y_test,x_test_predictions))

print("Abishek Xavier A 212222230004")
print(classification_report(y_test,x_test_predictions))

# Prediction for a single input
img = image.load_img('imagefive.jpg')
type(img)

img = image.load_img('imagefive.jpg')
img_tensor = tf.convert_to_tensor(np.asarray(img))
img_28 = tf.image.resize(img_tensor,(28,28))
img_28_gray = tf.image.rgb_to_grayscale(img_28)
img_28_gray_scaled = img_28_gray.numpy()/255.0
     
x_single_prediction = np.argmax(
    model.predict(img_28_gray_scaled.reshape(1,28,28,1)),
     axis=1)

print(x_single_prediction)

print("Abishek Xavier A 212222230004")
plt.imshow(img_28_gray_scaled.reshape(28,28),cmap='gray')

img_28_gray_inverted = 255.0-img_28_gray
img_28_gray_inverted_scaled = img_28_gray_inverted.numpy()/255.0
     
x_single_prediction = np.argmax(
    model.predict(img_28_gray_inverted_scaled.reshape(1,28,28,1)),
     axis=1)

print("Abishek Xavier A 212222230004")
print(x_single_prediction)
```

## OUTPUT

### Training Loss, Validation Loss Vs Iteration Plot
![Screenshot 2024-03-20 144042](https://github.com/AbishekAnand15/mnist-classification/assets/118706942/47aa09db-93a6-4b07-a07e-b8b081fe0020)

![Screenshot 2024-03-20 144050](https://github.com/AbishekAnand15/mnist-classification/assets/118706942/0fe0b127-0fba-4126-98ea-e3acc405c1e9)


### Classification Report
![Screenshot 2024-03-20 144113](https://github.com/AbishekAnand15/mnist-classification/assets/118706942/5f9894f8-937a-4e0c-898a-8ee372b8a5e7)


### Confusion Matrix
![Screenshot 2024-03-20 144056](https://github.com/AbishekAnand15/mnist-classification/assets/118706942/627246ee-c1b9-4f61-983c-fb7abeca0e88)


### New Sample Data Prediction
![Screenshot 2024-03-20 144131](https://github.com/AbishekAnand15/mnist-classification/assets/118706942/0205ba22-7cdf-49b3-a9fa-fa13ee8e761a)

![Screenshot 2024-03-20 144136](https://github.com/AbishekAnand15/mnist-classification/assets/118706942/a138a74b-0923-40b0-91ed-c7dbfea5139f)


## RESULT
A convolutional deep neural network for digit classification and to verify the response for scanned handwritten images is developed sucessfully.
