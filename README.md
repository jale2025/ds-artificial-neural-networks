# Artificial Neural Networks

In this repo we will have a look at artificial neural networks.

## Task

Please work in pairs through all the notebooks in this particular order:

### Day 1

Typical libraries are pytorch, TensorFlow & Keras. We will use TensorFlow & Keras in this course. The following notebooks will show you how to implement DNN for regression and classification problems. Additionally, you can find the notebooks for dealing with over- and underfitting. And you will find a notebook on how to save and load models.

1. [Regression with TensorFlow & Keras](day_1/02_Regression_TensorFlow_Keras.ipynb)
2. [Classification with TensorFlow & Keras](day_1/03_Classification_TensorFlow_Keras.ipynb)
3. [Over- and Underfitting](day_1/04_Overfit_Underfit.ipynb)
4. [Load Models](day_1/05_Load_saved_Models.ipynb) (optional)

### Day 2

On day 3 you have the possibility to implement a Neural Network for your second project.

5. [DNN Assignment](day_2/06_DNN_Assignment.ipynb)

### Bonus

No one is normally creating their own DNN from scratch in python. But it could be a useful exercise for some. In this exercise you will build your own deep neural network with some assistance. This should help you to get a better understanding what is going on when "training" a NN.
Therefore, you will even compute your own back-propagation algorithm. You start this if you finish early on one of the other days, else save it for later review if you are interested.

6. [DNN from scratch](bonus/01_DNN_from_scratch.ipynb) 

## Environment

We have to install hdf5:

```BASH
 brew install hdf5
 brew install graphviz
```
With the system setup like that, we can go and create our environment and install tensorflow

```BASH
pyenv local 3.11.3
python -m venv .venv
source .venv/bin/activate
```

If you have just installed hdf5 with brew, then
```BASH
export HDF5_DIR=/opt/homebrew/Cellar/hdf5/1.14.1
```
If it was already installed, check your version number by navigating to that directory, and if needed, amend it to match the version you already had installed.


```BASH
pip install -U pip
pip install --no-binary=h5py h5py
pip install -r requirements.txt
```

