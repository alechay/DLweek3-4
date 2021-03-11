# Week 6 Assignment

## Objective

The goal for this assignment was to tinker with the Neural Network Playground and see how different manipulations affect the output of the model. There were 3 main objectives:

1. Play with the regularization types, adjust the learning rate, activation functions etc and see how it affects the model.
2. Try to understand the different feature types, and how the noise and batch size impact the model as well.
3. Adjust the number of layers / neurons. Did that improve the output or make it worse? Why?

## Base output

Took about 400 epochs to train an accurate classifier, with a test loss of 0.001.
![base](https://user-images.githubusercontent.com/55260698/110721431-8dffb380-81de-11eb-823d-e3ee67b4f0b5.png)

## Regularization types

Used l2 regularization, which was similarly effective as none. It took about 400 epochs to train an accurate classifier, with a test loss of 0.001.
![l2](https://user-images.githubusercontent.com/55260698/110721667-f6e72b80-81de-11eb-82d8-df1fd046efdf.png)

## Learning Rate

Used a learning rate of 1 instead of 0.03. The model trained much faster, but was unable to reach the same accuracy (minimum loss was about 0.075). I also tried a learning rate of 0.00001, which resulted in ridiculously slow training times. I didn't attach a screenshot of that.
![learning rate](https://user-images.githubusercontent.com/55260698/110721838-4a597980-81df-11eb-93e2-3839c8f2e93f.png)

## Activation functions

Used a ReLU activation function instead of tanh. The model trained slightly faster, and reached a test loss of 0.02 after about 300 epochs. However, that seemed to be the max loss. The shape of the classifying region in the visualization was also changed.
![activation function](https://user-images.githubusercontent.com/55260698/110722074-b3d98800-81df-11eb-8344-4ac0633bde5f.png)

## Feature types

Used X1 squared and Y1 squared instead of X1 and Y1. The model trained much, much faster, reaching a test loss of 0.01 after less than 50 epochs. I also tried sin(X1) and sin(X2), which didn't work for this classification task.
![features](https://user-images.githubusercontent.com/55260698/110722372-1f235a00-81e0-11eb-9904-3fb1f4ca9a0d.png)

## Noise

Increased noise to 30 from 0. After about 250 epochs, it became clear that the model wouldn't be as accurate. Because of the mixing of points, the best test loss was capped at about 0.148.
![Noise](https://user-images.githubusercontent.com/55260698/110722574-86d9a500-81e0-11eb-9213-4e86707d5186.png)

## Batch size

Increased batch size to 20 from 10. Training was much slower. It took about 1500 epochs to reach a test loss of 0.07. Decreasing the batch size sped up training.
![batch size](https://user-images.githubusercontent.com/55260698/110722735-d3bd7b80-81e0-11eb-8877-787b1bb3bd8e.png)

## Number of layers

Increasing the number of layers from 2 to 4 did not make much of a difference. It maybe slowed down training slightly, but similar accuaracy was achieved.
![layers](https://user-images.githubusercontent.com/55260698/110723012-58a89500-81e1-11eb-8fe2-0fe978eda9de.png)

## Number of neurons

I increased the number of neurons in the first layer from 4 to 8 and in the second layer from 2 to 4. Increasing the number of neurons also didn't make too much of a difference. Again, maybe a little slower training speed with a little worse accuracy. Decreasing the number of neurons to 2 and 1 prevented the model from achieving respectable accuracy.
![neurons](https://user-images.githubusercontent.com/55260698/110723263-c3f26700-81e1-11eb-9467-51b0dc2f4147.png)

## Conclusion

There are many different things in a deep learning model that can be tweaked to improve training speed and accuracy. In this case, using different feature types (X1 squared and Y1 squared instead of X1 and Y1) and decreasing the batch size significantly decreased the training time to achieve ideal loss (or accuracy). Significantly increasing the learning rate, using sin(X1) and sin(Y1) as features, and severely decreasing the number of neurons prevented the model from achieving respectable accuracy. While these modifications had a specific effect this time, every task is different, and they may improve/decrease performance on a different task. Therefore, it is always good tweak different things to try to boost model performance.
