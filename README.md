The objective of this project is to identify whether a person is COVID + given his
X-ray image (posteroanterior view) available and ready to be feeded to the
model.
D A T A C O L L E C T I O N
For Covid positive x-ray images, I used a standard open dataset from IEEE
hosted on github (Link) and for the normal x-ray images I used a Kaggle Dataset
(Link).
S T E P S T A K E N :
• A metadata file is available in the covid positive dataset which gives us a lot
of data about the patient, in that dataset I cross-referenced the image
using a function and filtered out only the images where RT-PCR test came
out as positive after testing and only the posteroanterior view of the
images as in Normal X-ray dataset we have only posteroanterior images.
• Total number of images Came out to be 220.
• Since the count was less, 70:30 ration for train and validation purposes
were followed.
• Model Building:
a. Model was a traditional CNN with 3 ConV layers, all having pooling
layers and ReLU as activation function. A dropout of 0.25 has been
added to all the three dense layers in order to remove overfitting.
The output layer has a single neuron unit with sigmoid function.
b. The model has been compiled using binary crossentropy with
optimization algo as ADAM.
c. The summary of model can be seen below:
Layer (type) Output Shape Param #
=================================================================
conv2d_8 (Conv2D) (None, 222, 222, 32) 896
_________________________________________________________________
conv2d_9 (Conv2D) (None, 220, 220, 64) 18496
_________________________________________________________________
max_pooling2d_6 (MaxPooling2 (None, 110, 110, 64) 0
_________________________________________________________________
dropout_8 (Dropout) (None, 110, 110, 64) 0
_________________________________________________________________
conv2d_10 (Conv2D) (None, 108, 108, 64) 36928
_________________________________________________________________
max_pooling2d_7 (MaxPooling2 (None, 54, 54, 64) 0
_________________________________________________________________
dropout_9 (Dropout) (None, 54, 54, 64) 0
_________________________________________________________________
conv2d_11 (Conv2D) (None, 52, 52, 128) 73856
_________________________________________________________________
max_pooling2d_8 (MaxPooling2 (None, 26, 26, 128) 0
_________________________________________________________________
dropout_10 (Dropout) (None, 26, 26, 128) 0
_________________________________________________________________
flatten_2 (Flatten) (None, 86528) 0
_________________________________________________________________
dense_4 (Dense) (None, 64) 5537856
_________________________________________________________________
dropout_11 (Dropout) (None, 64) 0
_________________________________________________________________
dense_5 (Dense) (None, 1) 65
=================================================================
Total params: 5,668,097
Trainable params: 5,668,097
Non-trainable params: 0
• Image augmentation: Since we have very less count of images in the train
and test dataset, we need to do the image augmentation. Horizontal flip
and zoom range of 0.2 was used to generate variety and give a model a
chance to learn better.
• Results:
a. First trial was with 15 epochs where we received the following
results:
Epoch 15/15 4/4 [==============================] -
23s 6s/step - loss: 0.1493 - accuracy: 0.9417 -
val_loss: 0.1470 - val_accuracy: 0.9667
Which is quite good.
b. Next the model was tested against images with pneumonic
symptoms and normal X-ray images where we got result as below:
Training Loss & Accuracy: [0.03196219727396965,
0.9937499761581421]
Validation Loss & Accuracy: [0.07270810753107071,
0.9833333492279053]
• Next the model was saved with h5 format.
• A heat-map of confusion matrix was built to visualize the results better:
Recall 1.0
Precision 0.96
