# ImageNet-Extension

The idea behind this assignment was to use three groups of pictures (one each of cats, dogs, and elephants) to train an extension of the InceptionV3 image classification model.

I tried a lot of different combinations of hyperparameters and network architectures in order to arrive at one that generated good loss and accuracy numbers.

The first major change that I made was to switch from a binary classifier to a categorical one. That was important.
Over the course of my experimentation I found that certain things worked and certain ones didn't.
Namely
  1) RMSProp optimizer is not the best one for this exercise
  2) After the Inception Network I had to run either Flatten() or GlobalAveragePooling2D(). In this case the first one worked better.
  3) Using two dense (fully connected) layers after the Flatten() layer didn't improve anything beyond using only one dense layer.
  4) Making the dense layer any larger than 512 neurons didn't help
  5) Dropout actually worsened my output.
  6) In this exercise it was the case that learning rate decay didn't help anything.
  7) Switching to Adamax optimizer was a good step.
  8) Implementing a BatchNormalization() layer after the Dense layer helped.

Ultimately the best architecture and hyperparameters came out to be the following
  1) Structure
    a) Inceptionv3
    b) Flatten
    c) Dense (512 neurons, Relu activation)
    d) BatchNormalization
    e) Dense (3 neurons, Softmax activation)
  2) Hyperparameters
    a) optimizer = Adamax
    b) Learning Rate = .0001 = 10^-4
    c) batch size = 10, steps = 9, epochs = 20

And my final outcome values for training and validation sets were -
  1) loss: 0.0748
  2) accuracy: 0.9889
  3) val_loss: 0.1036
  4) val_accuracy: 0.9617
And the model trained and validated on my computer in 292.70778489112854 seconds.
Back to 1 dense layer of 512. BatchNormalization only after.
