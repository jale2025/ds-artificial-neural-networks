# Coach Checklist Day 1

## Day Goals

- Participants understand the difference between regression and classification.
- Participants see the transition from classical ML to Keras/TensorFlow.
- Participants understand why normalization, baseline models, and task-appropriate metrics matter.

## Check Before the Session

- `tensorflow` and `jupyterlab` start correctly inside the project `.venv`.
- `graphviz` is useful for the classification notebook because it uses `plot_model(...)`.
- A separate system HDF5 install is not an obvious Day 1 requirement.
- The regression notebook downloads data from the UCI repository. Without internet access, that notebook can stall.
- The classification notebook imports `termcolor`. On non-Windows setup paths, check the environment if that import fails.

## Notebook 1: Regression

File: `01_Regression_TensorFlow_Keras.ipynb`

- Focus: regression, a `sklearn` baseline, a linear Keras model, then a DNN.
- Learning goal: start with a baseline before judging the value of a neural network.
- Learning goal: understand normalization as a required step for stable training.
- Learning goal: compare a one-feature model with a full-feature model.

### How to Guide Participants Through the Notebook

- Start with the target: `MPG` is a continuous variable, so this is a regression task.
- Check missing values and data types, especially `Horsepower` and `Origin`.
- Encode `Origin` before splitting into train and test.
- Run the `sklearn` baseline on purpose before moving to Keras.
- Then introduce the Keras `Normalization` layer and explain why it is adapted on training data only.
- Build the simple Keras model with only `Horsepower`.
- Then build the linear model with all features.
- Move to the DNN with hidden layers only after that comparison is clear.
- At the end, compare models via the collected metrics rather than intuition.
- Then review predictions, error distribution, and optionally model saving/loading.

### If Someone Asks: "What Do We Do Next?"

- "Do not tune the DNN yet. We still need to finish the simple baseline cleanly."
- "The next step is model comparison, not more feature engineering."
- "Here we want to understand what normalization changes before we add more layers."
- "Now we move from one feature to all features and compare the effect."
- "The jump to the DNN is only useful once the linear model is clear."

### Coaching Questions to Watch For

- Why does the notebook start with `LinearRegression` instead of a DNN?
- Why are `MAE` and `MSE` more useful here than accuracy?
- Why does the `Normalization` layer help?
- What actually changes, conceptually, between a linear model and a DNN?

### Short Answers

- Why does the notebook start with `LinearRegression` instead of a DNN?
  A baseline is the reference point. Without it, nobody can judge whether the DNN is actually better or only more complex.
- Why are `MAE` and `MSE` more useful here than accuracy?
  This is a regression problem. We predict a numeric value, not a class. Accuracy is for discrete labels.
- Why does the `Normalization` layer help?
  The input features live on very different scales. Without normalization, training is less stable and optimization is less efficient.
- What actually changes, conceptually, between a linear model and a DNN?
  The linear model can learn only linear relationships. The DNN can model nonlinear patterns through hidden layers.

### Stumbling Blocks

- The notebook depends on an external UCI data source.
- TensorBoard is useful for a demo but not essential for the core learning goal.
- The notebook now evaluates `dnn_horsepower_model` on the test split, which is the correct behavior to point out when discussing model comparison.

## Notebook 2: Classification

File: `02_Classification_TensorFlow_Keras.ipynb`

- Focus: binary classification with data cleaning, feature engineering, and class weights.
- Learning goal: explain why recall is the relevant metric here.
- Learning goal: recognize imbalanced data and interpret `class_weight`.
- Learning goal: show that most of the work is data preparation, not model architecture.

### How to Guide Participants Through the Notebook

- Start with the target: `RESULT` is a binary classification label.
- Make it explicit that this notebook is mostly about data work, not just building a model.
- Walk through the cleaning steps in order: date, `VEHICLE_AGE`, `VIN`, `GVWR`, `ODOMETER`.
- Then justify the engineered features `MILE_YEAR` and `ENGINE_WEIGHT_RATIO`.
- After that, discuss the final feature selection and the grouping of rare `MAKE` values into `other`.
- After one-hot encoding, split cleanly into train, validation, and test.
- Adapt the `Normalization` layer on the training set only.
- Show the small dense network only after the data pipeline is in place.
- Before training, explain why `class_weight` is used.
- After training, interpret recall, loss, and the confusion matrix together.

### If Someone Asks: "What Do We Do Next?"

- "We are still in data preparation. The model comes next, but the inputs need to be clean first."
- "The next step is to turn the cleaned columns into useful model features."
- "Do not focus on layers yet. We still need a proper split and normalization."
- "From here on, we move from data preparation into modeling."
- "After fitting, we will not look at loss alone. We will focus on recall and the confusion matrix."

### Coaching Questions to Watch For

- Why is `Recall` more important here than plain accuracy?
- Why are `VIN`, `GVWR`, `ODOMETER`, and `MAKE` transformed so heavily?
- Why do we normalize on the training set and not on the full dataset?
- What does the `0.5` threshold mean, and why is it not fixed by nature?

### Short Answers

- Why is `Recall` more important here than plain accuracy?
  The goal is to catch as many problematic vehicles as possible. False negatives are more costly here than a few extra false positives.
- Why are `VIN`, `GVWR`, `ODOMETER`, and `MAKE` transformed so heavily?
  Raw data is rarely ready for modeling. A large part of ML work is turning noisy or awkward raw columns into useful features.
- Why do we normalize on the training set and not on the full dataset?
  To avoid data leakage. Validation and test information must not leak back into training.
- What does the `0.5` threshold mean, and why is it not fixed by nature?
  `0.5` is only a default cutoff for turning probabilities into classes. Depending on the recall/precision tradeoff, another threshold may be better.

### Stumbling Blocks

- This notebook is much more data-heavy than model-heavy, so participants can lose the main thread.
- `plot_model(...)` requires a working Graphviz installation.
- The loss visualization is intentionally left open as an exercise.
- `termcolor` can trigger an import error depending on the setup path.

## Good Questions for the Group

- What is the simplest useful baseline here?
- How do I tell whether a DNN adds value over a simpler model?
- Which metric should I choose if false negatives cost more than false positives?
- Which parts of this workflow are modeling, and which parts are data work?

## Moderation Recommendation

- In the regression notebook, actively name the storyline: "baseline -> normalization -> linear Keras model -> DNN".
- In the classification notebook, moderate more actively because many data-cleaning steps happen back to back.
- If time is tight, spend less time on hyperparameter discussion and more on metrics, data quality, and model comparison.
