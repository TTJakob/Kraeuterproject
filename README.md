# Kraeuterproject
Deeplearning with herbs and mushrooms

![Ergebnisse VGG16](https://github.com/TTJakob/Kraeuterproject/blob/1.1/3VVG16.PNG)


 
 
xxxxxxxxxxxxxxxxxxxxxxxxxxxx


## Getting Started und Idee


Auf die Idee kam ich eig schon länger als mein Opa der sehr aktiv im Bereich Wald Holz und Natur ist Pilze sammelte und mir danach verschiedene Pilze und Kräuter aus einem Buch und seinem Gedächtniss benannte.

So kam mir die Idee den Lernaufwand dafür zu verringern und Sammlern einen einfachen und effektiven Weg zu geben ihre gesammelten Pilze und Kräuter zu Identifizieren.

Natürlich ist es etwas ambitioniert direkt alle verschiedenen Pilze und Kräuter erkennen zu wollen und Fehler bei der Bestimmung können z.B. beim Knollenblätterpilz sogar tötlich enden.

Deswegen als "Grundprojekt" erstmal die Abgrezung von Pilzen und Kräutern voneinander und von anderen (Other Class).

### Prerequisites

Ive did this project on Anaconda useing Tensorflow and Keras

## Transfer learning

Transfer learning is used to build highly accurate computer vision models for your custom purposes, even when you have relatively little data. Transfer learning uses a pre-trained network and only train a custom classifier that reduces development and training time and provides good results.

![Transfer Learning](https://tensorflow.rstudio.com/blog/images/keras-pretrained-convnet/swapping_fc_classifier.png)

A pre-trained network is simply a saved network previously trained on a large dataset, typically on a large-scale image classification task. If this original dataset is large enough and general enough, then the features learned by the pre-trained network can effectively act as a generic model of our visual world in therms of identifying shapes and objects and extract different features out of a picture. So one pre-trained model/convolutional base can prove useful for many different computer vision problems.


```
Give examples
```

### Installing

The first thing after the Anaconda enviroment was was to accquire the Pictures to execute the transfer learning 

Say what the step will be

```
Give the example
```

And repeat

```
until finished
```

End with an example of getting some data out of the system or using it for a little demo

## Running a first Network

My first step to get in touch with an actuall deeplearning network was to 
use an easy exisiting network that was close to my environment and only needed small changes.

I have used the VGG16 with the "Cats vs Dogs" usecase which is desinged for, as you guessed, distinguish cats and dogs.
https://tensorflow.rstudio.com/blog/keras-image-classification-on-small-datasets.html

If this neural network can predict if the picture displayes a cat or a dog we may can tweek it to identify champignon (mushroom) from cress.

<p align="center">
<img src="https://github.com/TTJakob/Kraeuterproject/blob/pictures/champ019.jpg"  width="250" height="250" /> <img src="https://vignette.wikia.nocookie.net/deathbattle/images/4/47/VS.png/revision/latest?cb=20160727174407" width="200" height="225" /> <img src="https://github.com/TTJakob/Kraeuterproject/blob/pictures/kresse004.jpg" width="250" height="250" />
<p>

So we reuse the VGG 16 pretrained model
```
_________________________________________________________________
Layer (type)                 Output Shape              Param #   
=================================================================
input_1 (InputLayer)         (None, 150, 150, 3)       0         
_________________________________________________________________
block1_conv1 (Conv2D)        (None, 150, 150, 64)      1792      
_________________________________________________________________
block1_conv2 (Conv2D)        (None, 150, 150, 64)      36928     
_________________________________________________________________
block1_pool (MaxPooling2D)   (None, 75, 75, 64)        0         
_________________________________________________________________
block2_conv1 (Conv2D)        (None, 75, 75, 128)       73856     
_________________________________________________________________
block2_conv2 (Conv2D)        (None, 75, 75, 128)       147584    
_________________________________________________________________
block2_pool (MaxPooling2D)   (None, 37, 37, 128)       0         
_________________________________________________________________
block3_conv1 (Conv2D)        (None, 37, 37, 256)       295168    
_________________________________________________________________
block3_conv2 (Conv2D)        (None, 37, 37, 256)       590080    
_________________________________________________________________
block3_conv3 (Conv2D)        (None, 37, 37, 256)       590080    
_________________________________________________________________
block3_pool (MaxPooling2D)   (None, 18, 18, 256)       0         
_________________________________________________________________
block4_conv1 (Conv2D)        (None, 18, 18, 512)       1180160   
_________________________________________________________________
block4_conv2 (Conv2D)        (None, 18, 18, 512)       2359808   
_________________________________________________________________
block4_conv3 (Conv2D)        (None, 18, 18, 512)       2359808   
_________________________________________________________________
block4_pool (MaxPooling2D)   (None, 9, 9, 512)         0         
_________________________________________________________________
block5_conv1 (Conv2D)        (None, 9, 9, 512)         2359808   
_________________________________________________________________
block5_conv2 (Conv2D)        (None, 9, 9, 512)         2359808   
_________________________________________________________________
block5_conv3 (Conv2D)        (None, 9, 9, 512)         2359808   
_________________________________________________________________
block5_pool (MaxPooling2D)   (None, 4, 4, 512)         0         
=================================================================
Total params: 14,714,688
Trainable params: 14,714,688
Non-trainable params: 0
_________________________________________________________________
```
We dont want want to Train all 14 Million parameters (and imagenet provides allready trained parameters for the VGG16 Network)

We only need to add and train our custom classifier

```
conv_base.trainable = False

model = models.Sequential()
model.add(conv_base)
model.add(layers.Flatten())
#model.add(layers.Dropout(0.15))
model.add(layers.Dense(256, activation='relu'))
model.add(layers.Dense(1, activation='sigmoid'))
```
so our model now looks like this
```
_________________________________________________________________
Layer (type)                 Output Shape              Param #   
=================================================================
vgg16 (Model)                (None, 4, 4, 512)         14714688  
_________________________________________________________________
flatten_5 (Flatten)          (None, 8192)              0         
_________________________________________________________________
dense_11 (Dense)             (None, 256)               2097408   
_________________________________________________________________
dense_12 (Dense)             (None, 1)                 257       
=================================================================
Total params: 16,812,353
Trainable params: 2,097,665
Non-trainable params: 14,714,688
_________________________________________________________________

```
### Break down into end to end tests

Explain what these tests test and why

```
Give an example
```

### Sources

François Chollet’s and J.J. Allaire’s book Deep Learning with Python

https://tensorflow.rstudio.com/blog/keras-image-classification-on-small-datasets.html
```
Give an example
```



## Authors

* **Tim Jakob** - *Idear and start up work* - TTJakob
