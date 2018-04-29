## Epochs 
In deep learning, training a network to learn features from scratch takes up a lot of time, and most of the features are not learned in the first pass through the data, just like a child that looks at an image for some time before *learning* its representation.

**_A full pass through all the training data is referred to as one epoch_**, this training data includes the data used to trainour model as well as for validation.

One might summarize this as one iteration through the network while it trains, but that is not the case, because as we know our datasets are large, along with our already **_large expanded network_**, we are left with very little space on our GPU to load our  data at the same time. so we decompose training in batches, and each iteration corresponds to a single training batch.

This leads us to mathematically define an epoch as:
> No of iterations to complete One Epoch = Training data / batch_size  

After every epoch, we check for accuracy on our validation set.
Knowing the above number is crucial because it guides us about:
1. When to check for accuracy 
2. When to save the model, (we may decide to do it after 1 epoch or even half an epoch)

![alt text](https://cdn-images-1.medium.com/max/2000/1*WsYGS4nYq-fEBC9L1UUKiQ.png)

Reference: [Epoch vs Batch Size vs Iterations](https://towardsdatascience.com/epoch-vs-iterations-vs-batch-size-4dfb9c7ce9c9) 


## Filters / Kernels
In layman's terms, a filter is an object placed on another object to change our view of the latter object. Similar is the concept of filters in convolution and neural networks.
A filter is a set of weights that get multiplied to incoming inputs to produce a set of outputs, filters are carefully designed to bring out specific features of the input image.

A specially designed filter to detect top-edges will only fire when top edges are detected, similarly for bottom edge or diagonal edge filters.

Canny Edge Detection:

![alt text](https://upload.wikimedia.org/wikipedia/commons/2/20/%C3%84%C3%A4retuvastuse_n%C3%A4ide.png)

**Convolution**, one of the fundamental techniques in image processing, simply takes a kernel and convolves it over an image, which is to say:
1. The filter starts from the left edge of the image
2. The filter values get multiplied to the image pixel values
3. The filter slides towards the right of the image with  a stride value and multiplies again

If a kernel of the same size is chosen as the input image, a single value output is observed.

One of the finest works in kernel visualization of the hidden layers was done by Matt Zeiler, in his paper he showed us what deeper filters looked like,
here is one of the kernels from his paper:

![alt text](https://i.stack.imgur.com/fsQKd.jpg =500x300)

Filters in an actual network are the weight values that are assigned to the nodes. These values are permanent and are stored at regular intervals, 
because they can be reloaded (reinitialized) to recreate the trained network.    

## Activation Functions
Activation functions are used on top of weights(nodes) in a neural network, these functions give neural networks their most important feature,
their **_non-linearity_**. We know that most of the real world data is non-linear, so for neural networks to learn these features there needs to be a 
way for them to model this non-linearity. Activation function does that.

Some common activation functions:
![alt text](https://www.kdnuggets.com/wp-content/uploads/activation.png)

For over 50 years, **sigmoid** has been the activation function of choice
> f(x) = 1 / 1 + exp(-x)

but because of their:
1. Vanishing Gradient problem
2. Slow convergence
3. Difficulty in optimization

they are being replaced by **tanh** activation functions
>f(x) = 2 / (1 + exp(-2x)) - 1

This helps in optimization as it is zero-centered but still fails for the vanishing gradient problem.

The most commonly used activation function at the moment is the **Rectified Linear Unit (reLU)**

> f(x) = { 0 for x < 0}
> {x for x >= 0}

In one go, it solves the vanishing gradient as well as the convergence problem, which attributes to the recent 
popularity it has received in recent months, reLU is simple and elegant, and a lot of times the simplest answer is the best.