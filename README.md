# DLweek3-4
 
All methods require Tensorflow 1
```
{
    # dltk compatible with tensorflow 1
    import tensorflow.compat.v1 as tf
    tf.disable_v2_behavior()
}
```
For all methods, need to change `.as_matrix()` to `.to_numpy()` <br>
<br>
Still get warning message: <br>
FutureWarning: Using a non-tuple sequence for multidimensional indexing is deprecated; use `arr[tuple(seq)]` instead of `arr[seq]`. In the future this will be interpreted as an array index, `arr[np.array(seq)]`, which will result either in an error or a different result. <br>
<br>
The best method to load data is tf_load1, and dltk_load simply doesn't work at the moment.
