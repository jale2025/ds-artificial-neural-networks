[![Shipping files](https://github.com/neuefische/ds-artificial-neural-networks/actions/workflows/workflow-04.yml/badge.svg?branch=main&event=workflow_dispatch)](https://github.com/neuefische/ds-artificial-neural-networks/actions/workflows/workflow-04.yml)

# Artificial Neural Networks

In this repo we will have a look at artificial neural networks.

## Task

Please work in pairs through all the notebooks in this particular order:

### Day 1 – Dense Neural Networks (DNN)

Typical libraries are pytorch, TensorFlow & Keras. We will use TensorFlow & Keras in this course. The following notebooks will show you how to implement DNN for regression and classification problems. Additionally, you can find the notebooks for dealing with over- and underfitting. And you will find a notebook on how to save and load models.

1. [Regression with TensorFlow & Keras](day_1/01_Regression_TensorFlow_Keras.ipynb)
2. [Classification with TensorFlow & Keras](day_1/02_Classification_TensorFlow_Keras.ipynb)

### Day 2 – Regularisation & Model Persistence

3. [Over- and Underfitting](day_2/03_Overfit_Underfit.ipynb)
4. [Save & Load Models](day_2/04_Load_saved_Models.ipynb) (optional)

### Day 3 – Convolutions & Transfer Learning

5. [CNN with Keras](day_3/cnn/cnn_keras.ipynb)
6. [Pretrained Networks & Transfer Learning](day_3/pretrained_transfer_learning/Pretrained_networks+transfer_learning.ipynb)

### Bonus

No one is normally creating their own DNN from scratch in python. But it could be a useful exercise for some. In this exercise you will build your own deep neural network with some assistance. This should help you to get a better understanding what is going on when "training" a NN.
Therefore, you will even compute your own back-propagation algorithm. You start this if you finish early on one of the other days, else save it for later review if you are interested.

7. [DNN from scratch](bonus/00_DNN_from_scratch.ipynb)


## Set up your Environment

Please make sure you have forked the repo and set up a new virtual environment.

The added **requirements file** contains all libraries and dependencies we need to execute these neural-network notebooks.

**`Note:`**

- Use the requirements file that matches your platform.
- `graphviz` is only needed for model plots created via `keras.utils.plot_model(...)`.
- A separate system-level HDF5 install is not a general prerequisite for every platform.

 - Check the **graphviz version** by running the following command:
    ```sh
    dot -V
    ```
    If you haven't installed it yet, begin at `step_1`. Otherwise, proceed to `step_2`.


### **`macOS` or `Linux`** type the following commands:

- `Step_1:` Install **graphviz** if you want to render model plots:

    ```BASH
     brew update
     brew install graphviz
    ```
    Then press ```Y``` for the standard installation.

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
    python -m pip install --upgrade pip
    python -m pip install -r requirements_silicon.txt
    ```
  > NOTE: for macOS with **intel** chips
  ```BASH
    pyenv local 3.11.3
    python -m venv .venv
    source .venv/bin/activate
    python -m pip install --upgrade pip
    python -m pip install -r requirements.txt
    ```

    
### Windows 11 (recommended, CPU-only)

For this course, we support under Windows **only Python 3.11.3**.
For the full Windows guide, see [INSTALL_WIN11.md](INSTALL_WIN11.md).
Use a fresh `.venv` for this repo only. Do not merge multiple course repos into one shared environment, and do not mix `requirements_win11.txt` with lines copied from `requirements.txt` or `requirements_silicon.txt`.

1. Check your Python version

   ```powershell
   python --version
   ```

   Expected: `Python 3.11.3`.
   If a different version appears, for example `3.10` or `3.12`, install Python 3.11.3 from `https://www.python.org/downloads/release/python-3113/`.
   Enable the option `Add Python to PATH` during installation.

2. Create and activate the virtual environment

   ```powershell
   cd ds-artificial-neural-networks
   python -m venv .venv
   .\.venv\Scripts\Activate.ps1
   python --version
   ```

3. Install the Windows 11 requirements

   ```powershell
   python -m pip install --upgrade pip
   python -m pip install -r requirements_win11.txt
   python -m pip check
   ```

   Optional sanity check:

   ```powershell
   python -c "import tensorflow as tf, keras, numpy as np; print(tf.__version__); print(keras.__version__); print(np.__version__)"
   ```

   Expected:
   `2.15.0`, `2.15.0`, `1.23.5`

   If `pip check` reports errors, first verify inside the active venv:

   ```powershell
   python --version
   ```

   It must be `Python 3.11.3`.

4. Graphviz (only for model plots)

   `keras.utils.plot_model` requires Graphviz.

   Install Graphviz via the official Windows installer:
   `https://graphviz.org/download/`

   Restart the terminal and verify:

   ```powershell
   dot -V
   ```

   `pydot` is already installed via `requirements_win11.txt` and does not need to be installed separately.

### Troubleshooting (Windows 11)

Common reasons for installation failures:

- Python is not `3.11.3`
- the virtual environment was created with a different interpreter than expected
- the environment is shared with other course repos
- `keras` was upgraded to `3.x` in a reused environment
- `h5py` or `tables` fail because the setup is outside the supported Python version

Checklist:

1. In the course folder, verify:

   ```powershell
   python --version
   ```

   It must show `Python 3.11.3`.

2. In the activated venv, verify again:

   ```powershell
   .\.venv\Scripts\Activate.ps1
   python --version
   ```

   It must also show `Python 3.11.3`.

3. If `h5py` or `tables` fail:

   - delete `.venv`
   - create it again
   - do not reuse an older shared environment
   - rerun exactly:

   ```powershell
   python -m venv .venv
   .\.venv\Scripts\Activate.ps1
   python -m pip install --upgrade pip
   python -m pip install -r requirements_win11.txt
   python -m pip check
   ```

If this still fails, share the full error message, especially the line mentioning `h5py` or `tables`.
In most cases, the root cause is a Python version outside the supported stack.
If you see `Keras 3` / `Keras 2` mismatch messages, the root cause is usually a reused environment and not the notebook itself.

## Data

The dataset for the notebook is stored in the `data.zip` folder. To unzip the data folder directly in the terminal run:
- Tabular datasets used in the dense-network notebooks live in `data/` and include:
  - `boston.csv`
  - `titanic.csv`
  - `vehicle_emissions.csv`

  ```sh
  unzip data.zip
  ```
- The transfer-learning notebook has its own archive at `day_3/pretrained_transfer_learning/data.zip`; unzip it in that folder before running the notebook.
