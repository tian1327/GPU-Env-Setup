# GPU-Env-Setup
Set up Nvidia GPU in conda env with CUDA

### Problem
Tensorflow pauses for noticeable time after giving message `Successfully opened dynamic library libcublas.so.10`. Then it worked. See examples given [here](https://stackoverflow.com/questions/67847219/using-tensorflow-with-gpu-taking-a-long-time-for-loading-library-related-to-cuda).

### Cause
Using conda command `conda create -n tf tensorflow-gpu` will install bundled packages as listed below, which are incompatible with each other and may cause the above behaviours/errors. See answers [here](https://stackoverflow.com/questions/67175987/why-does-tensorflow-pause-for-3-minutes-after-successfully-opened-the-dynamic-l).   
`tensorflow=2.4.1`   
`cudatoolkit=10.1`  
`cudnn=7.6`  

See [conda package versions](https://anaconda.org/anaconda/cudnn/files).

### Solution
Check for compatible versions between `tensorflow`, `python`, `GCC compiler`, `CUDA`, `cudnn` specified by [Tensorflow](https://www.tensorflow.org/install/source#gpu).

Install selected versions while creating a new conda env:
```console
conda create -n cuda10.1 tensorflow=2.3 python=3.7 cudatoolkit=10.1 cudnn=7.6  
```
Or
```console
conda create -n cuda11.0 tensorflow=2.4 python=3.7 cudatoolkit=11.0  
```

Activate conda env with:
```console
conda activate cuda10.1
```

### Other
To address message `Not creating XLA devices, tf_xla_enable_xla_devices not set` (see more [here](https://github.com/tensorflow/tensorflow/issues/44683#:~:text=The%20Not%20creating%20XLA%20devices%2C%20tf_xla_enable_xla_devices%20not%20set%20message%20is%20an%20information%20log%20which%20you%20can%20safely%20ignore.)):
```console
export TF_XLA_FLAGS=--tf_xla_enable_xla_devices
```

