# Rotated Word Vector Representations and their Interpretability


## Overview
We open a Python (PyTorch) source code for our paper, Rotated Word Vector Representations and their Interpretability (EMNLP 2017) [<a href="http://aclweb.org/anthology/D17-1041">paper</a>, <a href="https://sungjoonpark.github.io./assets/emnlp2017_poster.pdf">poster</a>] These files are originated from Python (Numpy) implementation of rotation algorithms, to accelerate computation speed by using GPU. https://github.com/mvds314/factor_rotation


## Requirements
- Python 3.6.3
- PyTorch 1.0
- NumPy 1.13.3
- gensim 3.1.0


## How to Run
First, you should prepare input word vectors representation. Basically, the input vectors is regarded as unrotated matrix, so the source code computes rotation matrix T, in order to represent vectors based on the rotated axis.

Here we upload example input file: 'text8_word2vec_50_5_100.csv'. The example vectors are generated by using <a href="https://radimrehurek.com/gensim/">gensim</a> library, trained over <a href="http://mattmahoney.net/dc/textdata.html">text8</a> corpus. The program produces rotated word vector representation saved as numpy array, .npy format.


### Run the program
To run the program, you can just run the test python file.
```
python example.py
```

Or you can simply do:
```
import factor_rotation as fr
import numpy as np
import torch

A = np.random.randn(8,2)
L, T = fr.rotate_factors(A, 'varimax', dtype=torch.float64, device=torch.device("cuda"))
print(L)
print(T)
```
by importing the library. A is input word vector matrix, and the output T is rotation matrix. As a result, the matrix L is rotated word vectors, L = AT.


### Small Tips
1. Normalizing the input matrix (word vectors) before computing a rotation matrix T improves performance. In the example, all of the elements in the unrorated word vector matrix are divided by the maximum value of that matrix, to ensure that all values are between from -1 to 1.

2. The size of the input word vector matrix matters. If the size rather small, like (10000, 300), the algorithm will easily converge within a few hours with GPU support. However, if the matrix gets larger (N of word vectors > 100000, Number of dimensions > 500), it might take 1~2 day of training time to obtain resonable results.

3. You can adjust parameters of the function `GPA`, such as `tol` or `max_tries` to find better solution of T.

## Update log
12.23.18: To address some code maintenance issues, we change our implementation from Tensorflow to PyTorch.

## Reference

Robert I Jennrich. 2001. A simple general procedurefor orthogonal rotation. Psychometrika66(2):289–306
