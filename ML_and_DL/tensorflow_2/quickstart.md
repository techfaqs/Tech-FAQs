# Intro
Tensorflow 2 is a new version of one of the most widely used frameworks for Deep Learning.
It is still fast and efficient, but this incremental change adds a lot in terms of usability. This is something TF has been lacking, compared to it's main competitor - PyTorch.
TensorFlow 1.X requires users to manually stitch together an abstract syntax tree (the graph) by making tf.* API calls. It then requires users to manually compile the abstract syntax tree by passing a set of output tensors and input tensors to a session.run() call. TensorFlow 2.0 executes eagerly (like Python normally does) and in 2.0, graphs and sessions should feels like implementation details.
So writing code using TF2.0 feel more "pythonic" and user-friendly. Combined with Keras library being embedded into TF itself now, this lowers the bar for staring building neural networks.

# Quickstart
Most of the examples for building first ANN (artificial neural network) are focusing on recognizing hand written digits. There is dataset, called [MNIST](https://en.wikipedia.org/wiki/MNIST_database "MNIST"), which consists of annotated images of digits. Let's be a bit more creative and use a dataset of clothing items, provided by Zalando.
Most comfortable way to use various TF apis is tf.keras. Keras in abstraction layer, which serves as high-level API.


Let's start with importing necessary libraries and making sure, there is correct version on TF installed

```
pythonimport tensorflow as tf
from tensorflow import keras

print(tf.__version__) # => should print 2.x.x

# Helper libraries
import numpy as np
import matplotlib.pyplot as plt
```

## Import dataset
Fashion MNIST dataset contains 70,000 grayscale images in 10 categories. The images show individual articles of clothing at low resolution (28 by 28 pixels).
60,000 images will be used to train the network and 10,000 images to evaluate how accurately the network learned to classify images.
This dataset can be imported and used directly from TensorFlow:

```python
fashion_mnist = keras.datasets.fashion_mnist

(train_images, train_labels), (test_images, test_labels) = fashion_mnist.load_data()
```

The images are 28x28 NumPy arrays, with pixel values ranging from 0 to 255. The labels are an array of integers, ranging from 0 to 9. These correspond to the class of clothing the image represents:

| Label | Class       |
|-------|-------------|
| 0     | T-shirt/top |
| 1     | Trouser     |
| 2     | Pullover    |
| 3     | Dress       |
| 4     | Coat        |
| 5     | Sandal      |
| 6     | Shirt       |
| 7     | Sneaker     |
| 8     | Bag         |
| 9     | Ankle boot  |


## Preprocess the data
The data must be preprocessed before training the network. If you inspect the first image in the training set, you will see that the pixel values fall in the range of 0 to 255:
```python
plt.figure()
plt.imshow(train_images[0])
plt.colorbar()
plt.grid(False)
plt.show()
```
![some shoe](https://www.tensorflow.org/tutorials/keras/classification_files/output_m4VEw8Ud9Quh_0.png)

Let's scale these values to a range of 0 to 1 before feeding them to the neural network model. To do so, divide the values by 255. It's important that the training set and the testing set be preprocessed in the same way:
```python
train_images = train_images / 255.0

test_images = test_images / 255.0
```

## Building the model
Building the neural network requires configuring the layers of the model, then compiling the model.

### 1. Set up the layers
The basic building block of a neural network is the layer. Layers extract representations from the data fed into them. Hopefully, these representations are meaningful for the problem at hand.

Most of deep learning consists of chaining together simple layers. Most layers, such as tf.keras.layers.Dense, have parameters that are learned during training.
```python
model = keras.Sequential([
    keras.layers.Flatten(input_shape=(28, 28)),
    keras.layers.Dense(128, activation='relu'),
    keras.layers.Dense(10, activation='softmax')
])
```
The first layer in this network, tf.keras.layers.Flatten, transforms the format of the images from a two-dimensional array (of 28 by 28 pixels) to a one-dimensional array (of 28 * 28 = 784 pixels). Think of this layer as unstacking rows of pixels in the image and lining them up. This layer has no parameters to learn; it only reformats the data.

After the pixels are flattened, the network consists of a sequence of two tf.keras.layers.Dense layers. These are densely connected, or fully connected, neural layers. The first Dense layer has 128 nodes (or neurons). The second (and last) layer is a 10-node softmax layer that returns an array of 10 probability scores that sum to 1. Each node contains a score that indicates the probability that the current image belongs to one of the 10 classes.

### 2. Compile the model
Before the model is ready for training, it needs a few more settings. These are added during the model's compile step:

* Loss function —This measures how accurate the model is during training. You want to minimize this function to "steer" the model in the right direction.
* Optimizer —This is how the model is updated based on the data it sees and its loss function.
* Metrics —Used to monitor the training and testing steps. The following example uses accuracy, the fraction of the images that are correctly classified.

```python
model.compile(optimizer='adam',
              loss='sparse_categorical_crossentropy',
              metrics=['accuracy'])
```

### 3. Training the neural network model

Feed the training data to the model. In this example, the training data is in the train_images and train_labels arrays.
The model learns to associate images and labels.
You ask the model to make predictions about a test set—in this example, the test_images array. Verify that the predictions match the labels from the test_labels array.
To start training, call the model.fit method—so called because it "fits" the model to the training data:

```python
model.fit(train_images, train_labels, epochs=10)
```

### 4. Evaluate accuracy
Next, compare how the model performs on the test dataset:

```python
test_loss, test_acc = model.evaluate(test_images,  test_labels, verbose=2)

print('\nTest accuracy:', test_acc) # => ~0.88
```
It turns out that the accuracy on the test dataset is a little less than the accuracy on the training dataset. This gap between training accuracy and test accuracy represents overfitting. Overfitting is when a machine learning model performs worse on new, previously unseen inputs than on the training data.

## Make predictions
With the model trained, you can use it to make predictions about some images.
```python
predictions = model.predict(test_images)
```
A prediction is an array of 10 numbers. They represent the model's "confidence" that the image corresponds to each of the 10 different articles of clothing. You can see which label has the highest confidence value:
np.argmax(predictions[0]) # => 9
So, the model is most confident that this image is an ankle boot, or class_names[9]. Examining the test label shows that this classification is correct:
```python
test_labels[0] # => 9
```
# Conclusion
TensorFlow 2 and Keras make it really easy to start with Deep Learning. Tasks like these now take less than 50 lines of code to implement.
