# Week 5 Assignment

## Objective

The goal for this assignment was to work through the NVIDIA Radiomics Deep Learning exercise. I followed along with the Jupyter Notebook as it showed me how to build and test a model. Then, I went back and explored how I could change and possibly improve the model. I tried the following things:
1. Adding additional layers to the network
2. Changing the number of neurons in those layers
3. Changing some of the hyper-parameters in the network configuration like dropout or learning rate, etc.

## Baseline model performance

I ran the default model that they provided and these are the results I got.
```
_________________________________________________________________
Layer (type)                 Output Shape              Param #   
=================================================================
conv2d_189 (Conv2D)          (None, 238, 238, 16)      160       
_________________________________________________________________
batch_normalization_189 (Bat (None, 238, 238, 16)      64        
_________________________________________________________________
re_lu_1 (ReLU)               (None, 238, 238, 16)      0         
_________________________________________________________________
max_pooling2d_9 (MaxPooling2 (None, 119, 119, 16)      0         
_________________________________________________________________
conv2d_190 (Conv2D)          (None, 117, 117, 32)      4640      
_________________________________________________________________
batch_normalization_190 (Bat (None, 117, 117, 32)      128       
_________________________________________________________________
re_lu_2 (ReLU)               (None, 117, 117, 32)      0         
_________________________________________________________________
max_pooling2d_10 (MaxPooling (None, 58, 58, 32)        0         
_________________________________________________________________
conv2d_191 (Conv2D)          (None, 56, 56, 64)        18496     
_________________________________________________________________
batch_normalization_191 (Bat (None, 56, 56, 64)        256       
_________________________________________________________________
re_lu_3 (ReLU)               (None, 56, 56, 64)        0         
_________________________________________________________________
max_pooling2d_11 (MaxPooling (None, 28, 28, 64)        0         
_________________________________________________________________
conv2d_192 (Conv2D)          (None, 26, 26, 128)       73856     
_________________________________________________________________
batch_normalization_192 (Bat (None, 26, 26, 128)       512       
_________________________________________________________________
re_lu_4 (ReLU)               (None, 26, 26, 128)       0         
_________________________________________________________________
max_pooling2d_12 (MaxPooling (None, 5, 5, 128)         0         
_________________________________________________________________
gaussian_noise_1 (GaussianNo (None, 5, 5, 128)         0         
_________________________________________________________________
flatten_1 (Flatten)          (None, 3200)              0         
_________________________________________________________________
dense_1 (Dense)              (None, 128)               409728    
_________________________________________________________________
re_lu_5 (ReLU)               (None, 128)               0         
_________________________________________________________________
dropout_1 (Dropout)          (None, 128)               0         
_________________________________________________________________
dense_2 (Dense)              (None, 3)                 387       
_________________________________________________________________
activation_189 (Activation)  (None, 3)                 0         
=================================================================
Total params: 508,227
Trainable params: 507,747
Non-trainable params: 480
_________________________________________________________________
None
```

Insert picture of performance

## Add layers

I added the following layers at the beginning of the model
```
    model.add(Conv2D(8, (3, 3), activation='tanh',kernel_initializer='he_uniform', 
                     input_shape=(240, 240, 1)))
    model.add(BatchNormalization())
    model.add(ReLU())   # add an advanced activation
    model.add(MaxPooling2D(pool_size=(2, 2)))
```

Insert picture of performance

## Change number of neurons

I changed the number of neurons in the dense layer from 128 to 64.

```
model.add(Dense(64))
```

Insert picture of performance

## Try different optimizer

I used the SGD optimizer instead of Adam, as was used in the base model.
```
altoptimizer=keras.optimizers.SGD(lr=0.0001)

model.compile(optimizer=altoptimizer, loss='categorical_crossentropy', metrics=['accuracy'])
```

Insert picture of performance

## Change convolution size

I changed the convolution size in each layer to (5, 5)
```
    model.add(Conv2D(16, (5, 5),activation='linear',kernel_initializer='he_uniform', 
                     input_shape=(240, 240, 1)))
```

Insert picture of performance

## Change dropout rate

I changed the dropout rate from 0.25 to 0.33
```
model.add(Dropout(0.33))
```

Insert picture of performance

## Conclusion

Performance of the models was measured by the f1-score (a harmonic mean of precision and recall) on the test set. Adding layers, decreasing neurons in the dense layer, and using the SGD optimizer instead of the Adam optimizer significantly decreased performance. Increasing dropout slightly decreased performance. Increasing the convolution size from (3, 3) to (5, 5) actually slightly increased performance. Making these changes all resulted in noticeable differences, and different models are best suited for different tasks. Therefore, any of these changes can result in better performance, given the right task.

