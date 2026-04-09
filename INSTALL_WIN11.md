# Windows 11 Setup

**Important: on Windows 11, this course is supported only with Python 3.11.3.**

This document defines the single tested Windows support path for this repo. Any setup that differs from this stack is outside the support scope and may fail, especially around `tensorflow-intel==2.15.0`, `h5py`, and `tables`.

## Supported Stack

The supported Windows stack for this repo is:

- Windows 11
- Python 3.11.3
- a fresh repo-local virtual environment created with `python -m venv .venv`
- installation only via `python -m pip install -r requirements_win11.txt`

Not supported:

- Python 3.10
- Python 3.12
- Conda Python
- a shared environment reused across multiple course repos

Do not install this repo into a shared course environment. The transcript feedback showed that mixed environments and merged repos are the fastest way to create `tensorflow` / `keras` / `numpy` mismatches that are hard to debug.

## Python Version and Compatibility

`requirements_win11.txt` is tested only on Windows 11 with Python 3.11.3.

Before installing anything, run:

```powershell
python --version
```

Expected output:

```text
Python 3.11.3
```

If you see a different version, for example `3.10.x`, `3.12.x`, or a Conda interpreter:

1. Download the official Python 3.11.3 installer:
   `https://www.python.org/downloads/release/python-3113/`
2. Choose the `Windows installer (64-bit)`.
3. Install Python 3.11.3 alongside other Python versions if needed.
4. Enable `Add Python to PATH` during installation.
5. Open a new terminal in the course folder.
6. Run `python --version` again.

Do not continue until `python --version` shows `Python 3.11.3`.

If multiple Python versions are installed and `python` still points to the wrong one, you can also verify the launcher:

```powershell
py -3.11 --version
```

Then return to the course folder and check `python --version` again. The support path starts only once `python --version` clearly reports `Python 3.11.3`.

## Installation Steps

### 1. Create and activate the virtual environment

In the project folder:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python --version
```

Inside the active venv, the output must still be `Python 3.11.3`.
This `.venv` should be used only for this repo.

### 2. Install the Windows requirements

```powershell
python -m pip install --upgrade pip
python -m pip install -r requirements_win11.txt
python -m pip check
```

If `pip check` reports errors, first verify the active interpreter again:

```powershell
python --version
```

If it is not `Python 3.11.3`, you are outside the supported stack.

Then run a quick version sanity check:

```powershell
python -c "import tensorflow as tf, keras, numpy as np; print(tf.__version__); print(keras.__version__); print(np.__version__)"
```

Expected output:

```text
2.15.0
2.15.0
1.23.5
```

If `keras.__version__` starts with `3`, the environment is wrong for this repo. Delete `.venv` and reinstall into a fresh repo-local environment.

### 3. Install Graphviz

`pydot` is already included in `requirements_win11.txt`, but `keras.utils.plot_model(...)` also needs the Graphviz system executable `dot.exe`.

Install Graphviz via the official Windows installer:

- Download: `https://graphviz.org/download/`

Then open a new terminal and verify:

```powershell
dot -V
```

If `dot` is not found, the Python environment is not the issue. The Graphviz system installation is missing or not on `PATH`.

## Course Rules

- In this repo, always use `python -m pip ...`.
- Use one fresh `.venv` per repo.
- Do not reuse a shared environment across multiple course repos.
- Do not mix lines from `requirements.txt`, `requirements_silicon.txt`, and `requirements_win11.txt`.
- Do not mix `conda`, `pip install hdf5`, Chocolatey HDF5 packages, or other package managers into the same Python environment.
- HDF5 support for this repo comes from the Python wheels for `h5py` and `tables`.
- If `python --version` does not show `3.11.3`, stop and fix the interpreter before trying anything else.

## Expected Green State

Example:

```text
> python --version
Python 3.11.3

> python -m pip check
No broken requirements found.
```

## Troubleshooting

The most common installation failures come from:

- Python not being `3.11.3`
- the virtual environment being created with a different interpreter than expected
- the environment being reused across multiple repos
- `keras` being upgraded or mixed to `3.x` in a shared environment
- Graphviz not being installed or `dot.exe` not being on `PATH`

### Checklist

1. In the course folder, run:

```powershell
python --version
```

It must show `Python 3.11.3`.

2. In the activated venv, run:

```powershell
.\.venv\Scripts\Activate.ps1
python --version
```

It must also show `Python 3.11.3`.

3. Run the version sanity check:

```powershell
python -c "import tensorflow as tf, keras, numpy as np; print(tf.__version__); print(keras.__version__); print(np.__version__)"
```

Expected:

```text
2.15.0
2.15.0
1.23.5
```

If `keras.__version__` shows `3.x`, stop. The environment was reused or manually modified.

4. If `h5py`, `tables`, or `keras` version mismatches fail:

- delete `.venv`
- create the environment again
- rerun the same install commands exactly in a fresh repo-local environment

```powershell
Remove-Item -Recurse -Force .venv
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python --version
python -m pip install --upgrade pip
python -m pip install -r requirements_win11.txt
python -m pip check
```

If the install still fails:

- share the full error message
- include the line that mentions `keras`, `tensorflow`, `numpy`, `h5py`, or `tables`
- assume the Python version is wrong until proven otherwise

## Trainer Verification

Use this section as the reference-machine checklist before the course.

### Before the course

- confirm that the training machine runs `Python 3.11.3`
- confirm that `python --version` reports `3.11.3`
- confirm that this repo is not using Conda
- confirm that Graphviz is installed and `dot.exe` is on `PATH`

### Reference setup

In the repo folder:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python --version
python -m pip install --upgrade pip
python -m pip install -r requirements_win11.txt
python -m pip check
```

Document these outputs explicitly:

- `python --version` returns `Python 3.11.3`
- `python -m pip check` ends with `No broken requirements found.`

### Notebook smoke test

Start Jupyter:

```powershell
python -m jupyter lab
```

Then open either `day_1/01_Regression_TensorFlow_Keras.ipynb` or `day_1/02_Classification_TensorFlow_Keras.ipynb`, start a fresh kernel, and run:

```python
import tensorflow as tf
import h5py
import tables

print(tf.__version__)
print(h5py.__version__)
print(tables.__version__)
```

Expected example output:

```text
2.15.0
3.10.0
3.8.0
```

### Day 3 Smoke Test

Run this before the CNN / transfer-learning session on a Windows 11 machine. It checks the Day 3 prerequisites that most often fail on first run:

- `MNIST` dataset download/cache
- pretrained `VGG16` weights download/cache
- image-loading support

PowerShell:

```powershell
python --version
python -m pip check
python -c "from tensorflow.keras.datasets import mnist; mnist.load_data(); print('mnist ok')"
python -c "from tensorflow.keras.applications.vgg16 import VGG16; VGG16(weights='imagenet'); print('vgg16 ok')"
python -c "from tensorflow.keras.preprocessing import image; print('image loading ok')"
```

Expected behavior:

- The first successful run may take longer because `MNIST` and `VGG16` weights can be downloaded and cached locally.
- Later runs should be faster on the same machine.
- The transfer-learning notebook saves the trained model as `models/wallet_phone.keras` and creates the `models/` directory automatically when that cell runs.
- If this smoke test passes, the Windows setup is usually stable enough for `day_3`.
