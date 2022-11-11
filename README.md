## Project Description

The goal of this project was to train a [Convolutional Neural Network](https://en.wikipedia.org/wiki/Convolutional_neural_network) (CNN), so that we can scan the image of a patient's eye and find out whether their gender is male or female. The project is my submission for [DPhi's "5 Weeks of Deep Learning Challenge"](https://dphi.tech), November 2022.

## Data

The training dataset contains 9220 eye pictures of males and females. It is sourced from Ruskino RU (PavelBiz). Their labels are stored in a different file.
A test dataset with 2305 more eye pictures was provided that was to be used for prediction.

## Data Preprocessing

Before the data could be fed into a Neural Network, it had to be prepared. The first step was to extract it from the image folder and put it into a pandas DataFrame. For processing the images, I used the [OpenCV](https://docs.opencv.org/4.x/) library. After reading the data from the files, it was in a different order, so I had to match the correct data-target pairs by joining the two DataFrames on data and target on their filename as a common id.

By plotting histograms of the images's dimensions it became clear that the data had different formats. It had to be downscaled to the dimensions of the smallest image, using the cv2.resize() method. Then, I greyscaled and normalised all images, to attain some uniformity. Those two steps might not have been necessary, but as my model was hardly training in the beginning, I figured that this would help it jump over local minima more easily.

## Model

I build a CNN with three convolutional layers (each followed by pooling layers to reduce the size of the output), one flatten layer, three dense layers (each followed by dropout layers to prevent overfitting) and an output layer, that was activated with [sigmoid](https://en.wikipedia.org/wiki/Sigmoid_function).

The model was then trained regarging the loss of the validation data (automatically split off by the model).

The accuary of the predicted values (y_pred) served as a loss for the final evaluation on the test data. On submitting, my model obtained an accuracy score of 89.85 percent on the test data.
