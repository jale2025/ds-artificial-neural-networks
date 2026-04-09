[![Shipping files](https://github.com/neuefische/ds-artificial-neural-networks/actions/workflows/workflow-04.yml/badge.svg?branch=main&event=workflow_dispatch)](https://github.com/neuefische/ds-artificial-neural-networks/actions/workflows/workflow-04.yml)

# Artificial Neural Networks

In this repo we will have a look at artificial neural networks.

## Task

Please work in pairs through all the notebooks in this particular order:

### Day 1

Typical libraries are pytorch, TensorFlow & Keras. We will use TensorFlow & Keras in this course. The following notebooks will show you how to implement DNN for regression and classification problems. Additionally, you can find the notebooks for dealing with over- and underfitting. And you will find a notebook on how to save and load models.

1. [Regression with TensorFlow & Keras](day_1/01_Regression_TensorFlow_Keras.ipynb)
2. [Classification with TensorFlow & Keras](day_1/02_Classification_TensorFlow_Keras.ipynb)
3. [Over- and Underfitting](day_1/03_Overfit_Underfit.ipynb)
4. [Load Models](day_1/04_Load_saved_Models.ipynb) (optional)

### Day 2

On day 2 you have the possibility to implement a Neural Network for your second project.

5. [DNN Assignment](day_2/05_DNN_Assignment.ipynb)

### Bonus

No one is normally creating their own DNN from scratch in python. But it could be a useful exercise for some. In this exercise you will build your own deep neural network with some assistance. This should help you to get a better understanding what is going on when "training" a NN.
Therefore, you will even compute your own back-propagation algorithm. You start this if you finish early on one of the other days, else save it for later review if you are interested.

6. [DNN from scratch](bonus/00_DNN_from_scratch.ipynb) 


## Set up your Environment

Please make sure you have forked the repo and set up a new virtual environment.

The added **requirements file** contains all libraries and dependencies we need to execute the NLP notebooks.

**`Note:`**

- If there are errors during environment setup, try removing the versions from the failing packages in the requirements file. silicon shizzle.
- In some cases it is necessary to install the **graphviz** compiler for the transformers library.
- make sure to install **hdf5** if you haven't done it before.

 - Check the **graphviz version**  by run the following commands:
    ```sh
    dot -V
    ```
    If you haven't installed it yet, begin at `step_1`. Otherwise, proceed to `step_2`.


### **`macOS` or  `Linux`** type the following commands : 

- `Step_1:` Update Homebrew and install **hdf5** and **graphviz** by following commands:

    ```BASH
     brew update
     brew install graphviz
    ```
    Then press ```Y``` for the standard installation.
    
    Then we can go on to install hdf5:
    
    ```BASH
     brew install hdf5
    ```

  Restart Your Terminal and then check the **graphviz version**  by running the following commands:
     ```sh
    dot -V
    ```
 
- `Step_2:` Install the virtual environment and the required packages by following commands:

  > NOTE: for macOS with **silicon** chips (other than intel)
    ```BASH
    pyenv local 3.11.3
    python -m venv .venv
    source .venv/bin/activate
    pip install --upgrade pip
    pip install -r requirements_silicon.txt
    ```
  > NOTE: for macOS with **intel** chips
  ```BASH
    pyenv local 3.11.3
    python -m venv .venv
    source .venv/bin/activate
    pip install --upgrade pip
    pip install -r requirements.txt
    ```

    
### **`WindowsOS`** type the following commands :

- `Step_1:` Update chocolatey and install **hdf5** and **graphviz** by following commands:

    ```BASH
     choco upgrade chocolatey
     choco install graphviz
    ```
    Then press ```Y``` for the standard installation.
    
    Then we can go on to install hdf5:
    
  Visit this website [install hdf5](https://www.hdfgroup.org/download-hdf5/)

  Restart Your Terminal and then check the **graphviz version**  by running the following commands:
     ```sh
    dot -V
    ```
     

- `Step_2:` Install the virtual environment and the required packages by following commands.

   For `PowerShell` CLI :

    ```PowerShell
    pyenv local 3.11.3
    python -m venv .venv
    .venv\Scripts\Activate.ps1
    python -m pip install --upgrade pip
    pip install -r requirements.txt
    ```

    For `Git-bash` CLI :
  
    ```BASH
    pyenv local 3.11.3
    python -m venv .venv
    source .venv/Scripts/activate
    python -m pip install --upgrade pip
    pip install -r requirements.txt
    ```

## Data

The dataset for the notebook is stored in the `data.zip` folder. To unzip the data folder directly in the terminal run.

```sh
unzip data.zip
```
