# Coach Checklist Day 3

## Day Goals

- Participants understand the core CNN ideas: convolution, pooling, feature extraction, and spatial structure.
- Participants build and train a simple CNN with Keras on image data.
- Participants understand the difference between training a CNN from scratch and using transfer learning.
- Participants learn why preprocessing and the input pipeline matter especially for pretrained models.

## Check Before the Session

- `tensorflow` and `jupyterlab` work inside the project `.venv`.
- `day_3/cnn/cnn_keras.ipynb` may download `MNIST` on first run if the dataset is not already cached locally.
- `day_3/pretrained_transfer_learning/Pretrained_networks+transfer_learning.ipynb` depends on `day_3/pretrained_transfer_learning/data.zip`.
- `day_3/pretrained_transfer_learning/Pretrained_networks+transfer_learning.ipynb` may also download pretrained `VGG16` weights on first run if they are not cached locally.
- The transfer-learning notebook now extracts `data.zip`, creates `models/` in Python, and saves the trained model as `models/wallet_phone.keras`, which is more stable on Windows than shell magics plus ad hoc save formats.

## Notebook 1: CNN with Keras

File: `cnn/cnn_keras.ipynb`

- Focus: CNN basics, image tensors, training a simple CNN, evaluating predictions.
- Learning goal: understand why images need a different model family than tabular data.
- Learning goal: connect convolution and pooling to feature extraction.
- Learning goal: read training curves, predictions, and the confusion matrix.

### How to Guide Participants Through the Notebook

- Start with the conceptual intro, but keep it short and practical: kernel, stride, padding, pooling.
- Use the diagrams to explain what changes spatially in a CNN, then move quickly to Keras.
- Make the data shape explicit: images are `(samples, width, height, channels)`.
- Explain why label encoding changes from integers to one-hot vectors.
- Build the simple CNN step by step and keep naming the model parts out loud.
- After training, focus on accuracy and loss curves before moving to single-image predictions.
- Use the confusion matrix to talk about systematic mistakes, not just overall accuracy.
- Treat the feature-map section as a bonus, not as the core learning target for everyone.

### If Someone Asks: "What Do We Do Next?"

- "First make sure the input shape is right. CNNs are picky about tensor shape."
- "Now we move from raw images to the model architecture."
- "Before changing hyperparameters, look at the training and validation curves."
- "The next step is not another plot but understanding what the network is predicting."
- "Only after the base CNN works should we spend time on the feature-map bonus."

### Coaching Questions to Watch For

- Why do we need the extra channel dimension for grayscale images?
- Why do we one-hot encode the labels here?
- What does pooling actually help with?
- Why do we look at validation loss and not just accuracy?

### Short Answers

- Why do we need the extra channel dimension for grayscale images?
  Because `Conv2D` expects image tensors with an explicit channel axis, even if there is only one channel.
- Why do we one-hot encode the labels here?
  Because the model uses a `softmax` output with `categorical_crossentropy`, which expects categorical targets in one-hot form.
- What does pooling actually help with?
  It reduces spatial size, lowers computation, and keeps the strongest local signals.
- Why do we look at validation loss and not just accuracy?
  Because loss reacts more sensitively to training problems and overfitting than accuracy alone.

### Stumbling Blocks

- The first half of the notebook is very conceptual. Participants can lose the main thread before the Keras part starts.
- `MNIST` may be downloaded on first run, so the notebook is not fully offline the first time.
- The notebook reshapes the images but does not explicitly normalize pixel values to `[0, 1]`, which is worth pointing out from a best-practice perspective.
- The notebook does not include a clean `model.evaluate(xtest, ytest)` test-set evaluation cell. It relies more on predictions and the confusion matrix.
- The confusion-matrix and prediction cells depend on earlier cells having been run in order.
- The feature-map bonus is interesting, but for many participants it is already beyond the core lesson of the day.

## Notebook 2: Pretrained Networks and Transfer Learning

File: `pretrained_transfer_learning/Pretrained_networks+transfer_learning.ipynb`

- Focus: using a pretrained CNN, model-specific preprocessing, transfer learning, custom image classification.
- Learning goal: understand why pretrained models need the same preprocessing they saw during their original training.
- Learning goal: understand the mechanics of freezing a convolutional base and adding task-specific layers.
- Learning goal: connect data loading, preprocessing, and model persistence to reproducibility.

### How to Guide Participants Through the Notebook

- Start with the pretrained prediction example and use the wrong initial result as the hook.
- Emphasize that preprocessing is not optional for pretrained models.
- Only then move into the transfer-learning section and explain the five-step workflow.
- Make it explicit that the custom dataset is tiny and the notebook is about the workflow, not about building a production classifier.
- Pause at the generator step and explain how folder structure becomes labels.
- Pause again at `base_model.trainable = False` and explain what is and is not being trained.
- Treat the save step as a normal part of the workflow now that the notebook creates `models/` and saves to `.keras` automatically.

### If Someone Asks: "What Do We Do Next?"

- "First get the pretrained model to predict one image correctly after preprocessing."
- "Now we move from using the model as-is to adapting it for a new task."
- "Before training, check the data folder and class mapping."
- "The key question now is which layers are frozen and which are trainable."
- "The notebook should now create `models/wallet_phone.keras` automatically. If saving still fails, read the exact error before changing formats."

### Coaching Questions to Watch For

- Why does the pretrained model give a bad result before preprocessing?
- What does freezing the convolutional base actually do?
- Is this notebook really doing fine-tuning?
- Why do we save to a `.keras` file here?

### Short Answers

- Why does the pretrained model give a bad result before preprocessing?
  Because the model expects inputs in the same representation used during its original training. Raw resized pixels are not enough.
- What does freezing the convolutional base actually do?
  It keeps the pretrained feature extractor fixed and trains only the new top layers for the custom task.
- Is this notebook really doing fine-tuning?
  Not in the strict sense. The base model is frozen, so this is feature extraction with a custom classifier on top, not true fine-tuning.
- Why do we save to a `.keras` file here?
  Because it matches the current Keras save API, works cleanly in this course setup, and avoids extra friction around legacy HDF5-based saving.

### Stumbling Blocks

- The notebook mixes two ideas: pretrained prediction and transfer learning. Participants can miss where one ends and the other begins.
- The validation set is tiny, so validation accuracy is noisy and easy to over-interpret.
- `batch_size=150` is larger than the effective dataset size, which is acceptable for a demo but unusual for teaching good defaults.
- The notebook reuses `img` across sections, so participants can lose track of which image is being predicted.
- `data.zip` still contains `__MACOSX` and `.DS_Store` artifacts, but the notebook now removes them in Python after extraction.
- The notebook introduces data augmentation, but all augmentation options are commented out, so no real augmentation is being applied.

## Issues to Share with the Group

- `cnn/cnn_keras.ipynb` may download `MNIST` on first run if the dataset is not cached locally.
- `cnn/cnn_keras.ipynb` reshapes the image tensors but does not explicitly normalize pixel values.
- `cnn/cnn_keras.ipynb` does not show a dedicated `model.evaluate(xtest, ytest)` test-step and instead focuses on predictions and the confusion matrix.
- `pretrained_transfer_learning/Pretrained_networks+transfer_learning.ipynb` still needs `data.zip`, but extraction is now handled with Python instead of shell commands.
- The transfer-learning notebook may download pretrained `VGG16` weights on first run if they are not cached locally.
- The notebook talks about data augmentation, but the actual augmentation parameters are commented out.
- The notebook now saves to `models/wallet_phone.keras` and creates `models/` automatically, so participants can usually save without changing the format themselves.
- The notebook uses a frozen base model, so this section demonstrates feature extraction rather than full fine-tuning.
- The validation set in the transfer-learning notebook is extremely small, so reported validation metrics are demo-only and should not be over-interpreted.

## Good Questions for the Group

- Why are CNNs better suited for images than plain dense networks?
- What changes in the data shape when we move from tabular features to images?
- Why must pretrained models use model-specific preprocessing?
- What is the practical difference between feature extraction and fine-tuning?

## Moderation Recommendation

- Keep the CNN notebook moving. The diagrams are useful, but the real learning value starts when the tensor shapes and Keras model appear.
- In the transfer-learning notebook, narrate the transitions very explicitly: pretrained prediction, preprocessing, zipped dataset, generator, frozen base, custom head.
- Expect more setup trouble in the transfer-learning notebook than in the CNN notebook.
- If time is tight, prioritize the pretrained preprocessing example and the frozen-base workflow over the later save and cleanup cells.
