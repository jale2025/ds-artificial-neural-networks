Here a short summary about some hyperparameters in ANN we touch this afternoon:
- [Important activation functions](https://medium.com/hyunjulie/activation-functions-a-short-summary-8450c1b1d426) and their usage:  
  - step function --> simple but has zero gradient everywhere  
  - linear function --> could be used for scaling but does not provide any non-linearity  
  - sigmoid --> mostly used in classification problems as output layer; suffers from vanishing gradient problem, not zero-centered  
  - tanh --> zero-centered and steeper gradient than sigmoid; mostly used in hidden layers but again vanishing gradient problem  
  - ReLU, leaky ReLU --> standard activation function; ReLU has no gradient for negative inputs  
  - softmax --> used for multiclass output as it sums up to 1 so that each value gives the probability of each class  
  
- [Some optimizers](https://shekhar-banerjee96.medium.com/mastering-gradient-descent-a-deep-dive-into-rmsprop-and-adam-optimizers-c57599b23be3):   
  - mini-bach SGD (stochastic gradient descent) --> uses only several observations to calculate the gradient and thus quite economical  
  - RMSprop --> adjusts the learning rate for each parameter individually: Steep gradients are slowed down, gentle gradients are given a boost  
  - Adam (Adaptive Moment Estimation) --> also uses momentum (portions of previous gradients) AND rmsprop; first choice  

- [Regularization](https://medium.com/ai%C2%B3-theory-practice-business/dropout-early-stopping-188a23beb2f9)  
  - L1/L2 --> well known: ass a penalty to the loss and work on the NN weights  
  - Dropout --> randomly deactivates a fraction of neurons during training, forcing the network to learn more robust features and preventing co-adaptation of neurons, thus reducing overfitting  
  - early stopping --> data is split into a training set and a validation set; Training is halted when the validation error stops improving  

- [Avoid vanishing gradients](https://www.youtube.com/watch?v=ncTHBi8a9uA) (many layers means multiplying many small numbers leading to a vanishing product)  
  - select ReLu instead of sigmoid --> gradient of 1 for positiv inputs.
  - batch normalization --> acts in between the 2 functions of a neuron (summation and activation function) by a kind of standard scaling  
  - weight initialization --> don't initially select weights randomly but with a certain distribution
  - create connections which bridge some layers --> architectural methods 

