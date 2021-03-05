# DLweek3-4

## Mini Assignment Week 3/4

For this assignment I tried to follow the "Age regression and sex classification from T1-weighted brain MR images" tutorial from the blog. I tried to train a model on the IXI_HH Data, evaluate the model with tensorboard, and deploy the model.

## Create virtual environment and download data

`conda create -n dltk tensorflow=1` <br>
`pip install dltk` <br>
All packages used in requirements.txt <br>
I downloaded the data using the DLTK/data/IXI_HH/download_IXI_HH.py file. I had to change `.as_matrix()` to `.to_numpy()` to get it to work. <br>
I ended up with a demographic.csv and demographic.xls files, and 1mm and 2mm folders in the directory.

## Train the model
I ran `python train.py --data_csv ../../../data/IXI_HH/demographic_HH.csv --model_path ./` to train the model. I had to change `.as_matrix()` to `.to_numpy()` to get it to work. And I had to run `conda install nomkl` to get it to work <br>
I couldn't get past the following error: 
```
StopIteration


The above exception was the direct cause of the following exception:


Traceback (most recent call last):

  File "/Users/alechay/opt/anaconda3/envs/dltk/lib/python3.7/site-packages/tensorflow_core/python/ops/script_ops.py", line 235, in __call__
    ret = func(*args)

  File "/Users/alechay/opt/anaconda3/envs/dltk/lib/python3.7/site-packages/tensorflow_core/python/data/ops/dataset_ops.py", line 594, in generator_py_func
    values = next(generator_state.get_iterator(iterator_id))

RuntimeError: generator raised StopIteration


	 [[{{node PyFunc}}]]
	 [[IteratorGetNext]]
```
After consulting with classmates I still was not able to solve this issue. We concluded that this error began when python 3.7 was introduced. In python>=3.7, the StopIteration calls are no longer silenced, and therefore what was previously okay now causes the code to break.

## Evaluate the model with Tensorboard
Even though the model didn't finish training, there were a few files produced. I ran `tensorboard --logdir ./`. Tensorboard launched and was able to show some output. <br> 
### Scalars
![Screen Shot 2021-03-04 at 8 06 03 PM](https://user-images.githubusercontent.com/55260698/110053518-914ef700-7d27-11eb-8733-fda10b003c5d.png)
### Images
![Screen Shot 2021-03-04 at 8 06 13 PM](https://user-images.githubusercontent.com/55260698/110053524-9449e780-7d27-11eb-9084-9697324f8eef.png)
### Graphs
![Screen Shot 2021-03-04 at 8 06 25 PM](https://user-images.githubusercontent.com/55260698/110053525-957b1480-7d27-11eb-9e07-259a07843977.png)
## Deploy model
I was not able to deploy my model because it didn't train fully. But I was able to download a pre-trained model referenced by the tutorial. I ran `python -u deploy.py --model_path IXI_HH_sex_classification/`. As you can see in the output, there are two classes, male and female, corresponding to 1 or 0. For each image there is a prediction, the actual class, and the run time for that prediction. The model was able to classify sex at 96% accuracy. I have pasted the output: 
```
WARNING:tensorflow:From deploy.py:104: The name tf.logging.set_verbosity is deprecated. Please use tf.compat.v1.logging.set_verbosity instead.

WARNING:tensorflow:From deploy.py:104: The name tf.logging.ERROR is deprecated. Please use tf.compat.v1.logging.ERROR instead.

Loading from IXI_HH_sex_classification/1511133313
/Users/alechay/opt/anaconda3/envs/dltk/lib/python3.7/site-packages/dltk/io/augmentation.py:284: FutureWarning: Using a non-tuple sequence for multidimensional indexing is deprecated; use `arr[tuple(seq)]` instead of `arr[seq]`. In the future this will be interpreted as an array index, `arr[np.array(seq)]`, which will result either in an error or a different result.
  ex_image = image_list[j][slicer][np.newaxis]
id=IXI566; pred=1; true=1.0; run time=5.42 s; 
id=IXI567; pred=1; true=1.0; run time=4.94 s; 
id=IXI568; pred=1; true=1.0; run time=4.86 s; 
id=IXI572; pred=1; true=1.0; run time=4.81 s; 
id=IXI575; pred=1; true=1.0; run time=4.87 s; 
id=IXI577; pred=1; true=1.0; run time=4.92 s; 
id=IXI586; pred=0; true=0.0; run time=4.87 s; 
id=IXI598; pred=0; true=0.0; run time=4.90 s; 
id=IXI599; pred=0; true=0.0; run time=4.89 s; 
id=IXI600; pred=0; true=0.0; run time=4.95 s; 
id=IXI601; pred=0; true=0.0; run time=4.92 s; 
id=IXI603; pred=1; true=1.0; run time=4.85 s; 
id=IXI605; pred=0; true=1.0; run time=4.86 s; 
id=IXI606; pred=0; true=0.0; run time=4.88 s; 
id=IXI608; pred=0; true=0.0; run time=4.88 s; 
id=IXI609; pred=0; true=0.0; run time=4.93 s; 
id=IXI610; pred=0; true=0.0; run time=4.84 s; 
id=IXI611; pred=0; true=0.0; run time=4.93 s; 
id=IXI612; pred=0; true=0.0; run time=4.84 s; 
id=IXI613; pred=0; true=0.0; run time=4.86 s; 
id=IXI614; pred=1; true=1.0; run time=4.92 s; 
id=IXI631; pred=0; true=0.0; run time=4.84 s; 
id=IXI632; pred=0; true=0.0; run time=4.93 s; 
id=IXI633; pred=0; true=0.0; run time=4.83 s; 
id=IXI634; pred=0; true=0.0; run time=4.83 s; 
id=IXI635; pred=0; true=0.0; run time=4.88 s; 
id=IXI636; pred=0; true=0.0; run time=4.66 s; 
id=IXI646; pred=1; true=1.0; run time=4.84 s; 
accuracy=0.9642857142857143
```
## Final thoughts
I did a lot of troubleshooting in this assignment. It is difficult looking through someone else's code (especially if it has been created a few years back) and forcing it to work. This was created using outdated versions of python and tensorflow, which have changed substantially in the last few years. However, I did learn the basics of how to load medical image data using tensorflow and DLTK. I will at least know how to use these packages for my final project. In the future, I will search for packages that can load medical image data using Tensorflow 2, as it will make my life much easier.
