# Convolutional Neural Network

## Dataset 1: Fashion MNIST

#### About the Dataset:

- We'll need TensorFlow Datasets, an API that simplifies downloading and accessing datasets, and provides several sample datasets to work with.
- The Fashion MNIST dataset, which contains 70,000 grayscale images in 10 categories. The images show individual articles of clothing at low resolution (28  ×  28 pixels), as seen here

<img width="500" alt="Screenshot 2020-10-20 at 7 30 17 PM" src="https://user-images.githubusercontent.com/31176045/96596906-da6b5500-130a-11eb-8506-6d7197f45639.png">


- The labels are an array of integers, in the range [0, 9]. These correspond to the class of clothing the image represents:

<img width="500" alt="Screenshot 2020-10-20 at 7 38 04 PM" src="https://user-images.githubusercontent.com/31176045/96597783-da1f8980-130b-11eb-840d-821fec7adb39.png">

#### Applying Convolutional NN Model

- The details of the model is shown below:
  <img width="1000" alt="Screenshot 2020-10-20 at 7 40 43 PM" src="https://user-images.githubusercontent.com/31176045/96598268-53b77780-130c-11eb-9547-109ba56067cc.png">
  
  
#### Experiments Performed and their outcome:

- **Consider single hidden layer**

| Dense Layers  | Train Accuracy | Test Accuracy |
| ------------- | -------------- | ------------- |
|    512        |    86.75       |     86.18     |
|    10         |    79.99       |     85.02     |

- **Consider single hidden layer and without normalising images**

| Dense Layers  | Train Accuracy | Test Accuracy |
| ------------- | -------------- | ------------- |
|    128        |    85.98       |     87.51     |

- **Consider two hidden layer**

| Dense Layers  | Train Accuracy | Test Accuracy |
| ------------- | -------------- | ------------- |
|    128        |    93.30       |     89.74     |

- The above case with two hidden layers is an example of **overfitting**.


## Dataset 2: Dogs and Cats

#### Goal : Classify whether image is of cat(label 1) or dog(label 0)

#### About the dataset:

- The dataset used is a filtered version of Dogs vs. Cats dataset from Kaggle (ultimately, this dataset is provided by Microsoft Research).
- In this project, we use the class **tf.keras.preprocessing.image.ImageDataGenerator** which will read data from disk. We therefore need to directly download Dogs vs. Cats from a URL and unzip it to the runtime environment.

#### Challenges and Solutions

- This dataset consists of images of different size but our model requires fixed size input, thus we resize our image to 150x150 pixel resolution.
- This dataset consists of colored images thus in our model we provide input_shape=(150,150,**3**) where the 3 refers to **RGB** channel of the color image.

#### Model Evalution

- The summary of our model is shown below:

<img width="1000" alt="Screenshot 2020-10-20 at 11 02 05 PM" src="https://user-images.githubusercontent.com/31176045/96623124-83747880-1328-11eb-9768-eed8cada260c.png">

- Upon processing our data using the above mentioned model we get the following output after 20 epochs:

<img width="500" alt="Screenshot 2020-10-20 at 10 59 35 PM" src="https://user-images.githubusercontent.com/31176045/96623293-c6cee700-1328-11eb-81d7-bc83b772ea62.png">

- Thus it is clearly visible that our training accuracy reached approx. 100% accuracy after 17 epochs whereas the validation accuracy started to pan out after 20 epochs. This means the model has memorized the training input and thus it performs poorly on validation set(newly seen data). This is a simple case of **overfitting**.

#### To mitigate overfitting we take following steps on the DogsvsCats dataset

- Generate validation set from training images
- **Image Augmentation:** To perform image transformation on training images such that our CNN model does not memorise the training images since our training set deosn't have sufficient training examples.
- Perform **dropout** on the neurons of the hidden layers with certain probability.
- The resulting output is shown on modifying the model as mentioned above:

<img width="550" alt="Screenshot 2020-10-21 at 7 24 42 AM" src="https://user-images.githubusercontent.com/31176045/96663618-a32e8f80-136e-11eb-9ad8-508d1765d041.png">

- Thus we can see our model perform much better than our previous model on performing the above transformations.

## Dataset 3: Flower Classification

#### Goal : To classify images of flowers

- The dataset contains images of 5 types of flowers: Rose, Daisy, Dandelion, Sunflowers, Tulips.

- Upon performing the experiment on 10 epochs we saw that after 7 epochs the validation accuracy decreases in comparison to training accuracy. Thus we can stop our model at 8 epochs(**Early Stopping**).

<img width="500" alt="Screenshot 2020-10-21 at 8 27 12 AM" src="https://user-images.githubusercontent.com/31176045/96667749-484d6600-1377-11eb-86ff-6425dc24a2c8.png">

### Transfer Learning

- Transfer learning is a process where you take an existing trained model, and extend it to do additional work. This involves leaving the bulk of the model unchanged, while adding and retraining the final layers, in order to get a different set of possible outputs.

- We use the feature vector that corresponds to the [Inception v3 model](https://tfhub.dev/s?module-type=image-feature-vector&q=tf2).

- There's a huge boost in performance compared to previous models. The training and validation accuracy and loss plot are shown below:

<img width="500" alt="Screenshot 2020-10-21 at 11 59 52 AM" src="https://user-images.githubusercontent.com/31176045/96681591-2662dc00-1395-11eb-8457-3429e56fb40e.png">

- The validation performance is better than training performance right from the begining of execution because validation performance is measured at the end of the epoch, but training performance is the average values across the epoch.
