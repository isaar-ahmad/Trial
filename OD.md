# Setup environment for TensorFlow Objection detection for GPU (on IITD HPC)

### LabelImg
- Used for annotation according to PASCAL VOC standard
https://github.com/tzutalin/labelImg

### Conda 
- Download latest minconda setup script from the site (say, `Miniconda3-latest-Linux-x86_64.sh` and run `bash Miniconda3-latest-Linux-x86_64.sh`
- One Time Create python env for all python 3 libraries `conda create -n py35 python=3.5`
- Activate the env, `source activate py35` and deactivate env by `source deactivate`

### Tensorflow
- Due to some [issue](https://github.com/tensorflow/tensorflow/issues/17629), and modules doesn't have Cuda 9.0, I'm using Cuda 8.0 for TensorFlow 1.4.
- Cython is an optimising static compiler. `conda install cython`
#### CUDA
- CUDA is a parallel computing platform and application programming interface model created by Nvidia
- Use cuda from available modules. Choose the cuda version from `module avail 2> >(grep cuda)`.
- Load cuda as `module load compiler/cuda/8.0/compilervars`.
- Check install location of CUDA tootkit `nvcc --version` and check if it is added in the required environment variables (pretty print) 
```
sed 's/:/\n/g' <<< "$PATH"
sed 's/:/\n/g' <<< "$LD_LIBRARY_PATH"
```
#### cuDNN
- The NVIDIA CUDA Deep Neural Network library (cuDNN) is a GPU-accelerated library of primitives for deep neural networks. 
- Pick the cudnn version from `module avail 2> >(grep cudnn)`. Load it as `module load lib/cudnn/7.0.3/precompiled`

#### Tensorflow
- Activate virtual environment `conda activate py35`
- Install tensorflow gpu. `pip install --ignore-installed --upgrade tensorflow-gpu==1.4`

### Reference: 
- https://conda.io/miniconda.html
- http://tensorflow-object-detection-api-tutorial.readthedocs.io/en/latest/install.html#tensorflow-gpu
- https://www.pyimagesearch.com/2017/09/27/setting-up-ubuntu-16-04-cuda-gpu-for-deep-learning-with-python/