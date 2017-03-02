# **P2: Traffic Sign Recognition**

---

## In my first submission...

I used LeNet Architecture, almost same with model in class:

| Layer			           |Input          |
|:--------------------:|:-------------:|
| 5x5 Conv,  6, stride1| 32x32x3       |
| 2x2 Max Pooling		   | 28x28x6			 |
| 5x5 Conv, 16, stride1| 14x14x6 	 	   |
| 2x2 Max Pooling      | 10x10x16		   |
| FCL, 120        		 | 5x5x16 --> 400|
| FCL, 84         		 | 120           |
| FCL, 43         		 | 84            |

And test accuracy becomes **91.3%**, but not robust for some images as follow:
![alt text][image1]

Here are the results of the prediction:

| Image      |   Prediction	        					|
|:----------:|:------------------------------:|
| 100km/h    | 80km/h (99%) 					        |
| 70km/h     | 80km/h (93%), 30km/h (6%) 			|
| 60km/h	   | Dangerous curve to right	(99%)	|
| 120km/h    | 30km/h (99%)			 		          |
| 100km/h	   | 70km/h (99%)      							|

Here is the starting point, and To Do is:

1. Data Processing (normalization, augmentation)
2. Change Model (filter size, pooling, dropout)


[//]: # (Image References)

[image1]: ./examples/img_5.png "5 Signs"
[image2]: ./examples/num_augmented_data.png "Visualization"

---

## 1. Data Processing

From first results, I assumed that dark image is difficult to predict, so data augmentation may improve the results.

### 1.1. Data augmentation

I used gamma conversion to generate dark image. Simply, size of training data becomes double.
![alt text][image2]

The accuracy becomes **91.7%**, not changed drastically. But results are changed.

| Image      |   Prediction	        					|
|:----------:|:------------------------------:|
| 100km/h    | 100km/h (59%), 50km/h(30%), 120km/h(10%) 					        |
| 70km/h     | 70km/h (100%) 			|
| 60km/h	   | Slippery road (99%)	|
| 120km/h    | Bicycles crossing (99%)			 		          |
| 100km/h	   | 30km/h (99%)      							|

Accuracy for these samples become 40% from 0% !! But others are totally different.
I found that some images are completely black, and it may affect the performance.
(Black image w/ label is not necessary), so it should be rejected as next step.

## 2. Change Model

a
