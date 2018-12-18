# ANN-ActionRecognitionInVideo
Hand gesture or action recognition in videos

For this project, the data flow or overview of the implementation steps are: 
1. Data segregation in to test and train. This split is provided by the dataset. Our job was to move the files into separate folders which we did using python.
2. CNN model requires images as input where as LSTM requires features extracted from these images. The next step was to extract images from videos and features from these images. Image extraction was done using ffmpeg, an open source multimedia tool. Its default frame rate is 40 fps. We then used Google’s Inceptionv3 model pre trained with set weights on Imagenet dataset to get features for images from its final layer. This feature numpy output was then stored to be later passed as input to our LSTM model.
3. Data cleaning done was simple resizing all images to the same size along with rescaling. Here rescaling is nothing but having equal length of sequences of images from input videos. When we give videos of different length as input for image extraction, different counts of images are extracted for different videos. For training the model, each input videos will have equal length of sequence images. We have also performed one hot encoding for all labels.
4. Summarize the data in a csv file to be fed as input to the preprocessing steps. Video name, if it is test or train, label and frame count is the data in the csv. The implementation uses this data to fetch the images for each video, its label and data type.
5. Training the model with the data was done using three models 3D-CNN, LSTM, CNN-LSTM.
6. Predict using the three models to compare performance of the networks.

We have implemented neural network for hand gesture recognition using data from UCF data set. The dataset contains videos like writing, typing. There are 13,320 videos from 101 action categories. They are diverse in terms of actions, variations in camera motion, object appearance and pose. They are taken with cluttered background. The link for the dataset is given below. Since the data set contains 101 classes and requires huge computational power (one epoch took 8 hours), we have trained with only 1/10th of the data set.
[dataset.rar](http://crcv.ucf.edu/data/UCF101/UCF101.rar)

The results of running the training on all three models for 20 epochs is given below. 
```
TABLE I. 	Training Result comparison
Performance
Parameters    3D-CNN	    LSTM	    CNN-LSTM
Time taken
(per step)    4 seconds	      145 ms	    459 ms
Accuracy      0.31	      0.655	    0.414
Loss	      1.52	      1.12	    1.6
```

The prediction results are given in the below table for the above training performance parameters.
```
TABLE II.  Prediction Result Comparison
Performance
Parameters    3D-CNN    LSTM    CNN-LSTM
Baby
Crawling	0.26	0.46	0.22
BalanceBeam	0.23	0.29	0.22
Apply
Makeup	        0.22	0.16	0.20
Apply
Lipstick	0.21	0.06	0.19
Archery	        0.09	0.03	0.17
```

[Video classification methods implemented in Keras](https://blog.coast.ai/five-video-classification-methods-implemented-in-keras-and-tensorflow-99cad29cc0b)
