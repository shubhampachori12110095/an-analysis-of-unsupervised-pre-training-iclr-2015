# An Analysis of Unsupervised Pre-training in Light of Recent Advances
This repo contains the experiment files for the paper "An Analysis of Unsupervised Pre-training in Light of Recent Advances", available here: http://arxiv.org/abs/1412.6597

## Abstract
Convolutional neural networks perform well on object recognition because of a number of recent advances: rectified linear units (ReLUs), data augmentation, dropout, and large labelled datasets. Unsupervised data has been proposed as another way to improve performance. Unfortunately, unsupervised pre-training is not used by state-of-the-art methods leading to the following question:  
**Is unsupervised pre-training still useful given recent advances? If so, when?**  
We answer this in three parts: we  
1. develop a unsupervised method that incorporates ReLUs and recent unsupervised regularization techniques  
2. analyze the benefits of unsupervised pre-training compared to data augmentation and dropout on CIFAR-10 while varying the ratio of unsupervised to supervised samples  
3. verify our findings on STL-10.  

We discover unsupervised pre-training, as expected, helps when the ratio of unsupervised to supervised samples is high, and surprisingly, hurts when the ratio is low.  

We also use unsupervised pre-training with additional color augmentation to achieve near state-of-the-art performance on STL-10.

### Bibtex
```
@article{paine2014analysis,
  title={An Analysis of Unsupervised Pre-training in Light of Recent Advances},
  author={Paine, Tom Le and Khorrami, Pooya and Han, Wei and Huang, Thomas S},
  journal={arXiv preprint arXiv:1412.6597},
  year={2014}
}
```

## About the repo

The experiments are split into two sections:
+ cifar10
+ stl10

The `README.md` file in each folder will give you more information about running experiments.

The experiments are written in python 2.7, and require open source software to run, including:
+ [numpy][numpy], a standard numerical computing library for python.
+ [anna][anna], our neural network library, which itself depends on [theano][theano] and [pylearn2][pylearn2]. The pylearn dependencies are relatively small, and we may remove them to limit the number of dependencies.

### Installation Note

After successfully installing [pylearn2][pylearn2] and [anna][anna], the user needs to follow the three steps below before training the convolutional autoencoders:

1. Go to the pylearn2 root directory.
2. Open the ./pylearn2/sandbox/cuda_convnet/pool.py file.
3. Add the following function to the MaxPoolGrad class.

``` python
def grad(self, inp, grads):
        """
        .. todo::

            WRITEME
        """
        a, b, c = inp
        ga = gpu_contiguous(a*0)
        gb = gpu_contiguous(b*0)
        gc = gpu_contiguous(c)
        gz, = grads
        gz = gpu_contiguous(gz)
        return [ga, gb, MaxPoolRop(self.ds, self.stride)(a, gz)]
```

[numpy]:http://www.numpy.org/
[theano]:http://deeplearning.net/software/theano/
[pylearn2]:http://deeplearning.net/software/pylearn2/
[anna]:https://github.com/ifp-uiuc/anna

### Status
All experiments are added. Just need to finalize documentation.
