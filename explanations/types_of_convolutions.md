

## Dilated Convolution
A dilated convolution is one in which the filter convolves over the input, but with pre-defined gaps.

These gaps are specified by a parameter called the *dilation rate*. A way to understand this would be using a 3x3 filter, and a **dilation rate of 1** the first index of the filter multiplies with the first element of the feature map, but the second value of the filter skips the next pixel value on the feature map and multiplies 
with the adjacent one.

A representation of dilated convolution:

![dilated convolution](https://i.stack.imgur.com/qA0Kx.gif)

The most important advantage gained via dilated convolutions are an increased receptive field, without
an increase in computations, which means that the 3x3 dilated filter is able to see more of the image 
at a single instant, it is better suited for:
1. Gradient detection
2. Edge detection
3. Segmentation

Popular machine learning networks that employ dilated convolutions to help them _see or hear_ better are: 
1. WaveNets -- which employs a Convolutional Neural Network to perform text-to-speech synthesis 
2. ByteNets -- which learns time text translation 

References: [Dilated Convolution - A Blog From Human-engineer-being](http://www.erogol.com/dilated-convolution/)

<br>


## Depthwise Separable Convolution
Depthwise Convolution is used when we need to save resources while training our model. With a fractional loss in accuracy we are able to save a lot of computation power.

Basically what depthwise convolution does is that it splits the channels of a feature map into different images, and then convolves them with respective filters (also split channel wise), then the output feature maps are combined and convolved with _final_channels_requiredx1x1xinput_channels_ filters this gives the same required shape of the tensor as desired, but with less surcharge.

Let us now take an example to demonstrate how it works, and why does it require far fewer parameters:

Let us take a **20x20x8** image and it is convolved with **32x3x3x8** filters, which results in **18x18x32** as the output shape, so the total parameters required are:

$3 * 3 * 8 * 32  = 2304$

Now let us consider how this scenario would change for depthwise convolution, we will first convolve **20x20x8** with **8x3x3x1** kernels, and then use **32x1x1x8** kernels to produce a final output of **18x18x32**, which is the same as above, total parameters required are:

$[8 * 3 * 3 + 32* 1* 1* 8] = 328$

*" A sevenfold reduction in parameters by using this technique. "*

References: [Towards Data Science: Types of Convolutions](https://towardsdatascience.com/types-of-convolutions-in-deep-learning-717013397f4d)

## 1 x 1 convolution

A 1x1 convolution is a *feature merger and a dimensionality reducer*.

What the above statement means is that using a 1x1 kernel we are able to merge the extracted features from a 3x3 filter, suppose by the sixth layer, our network  has extracted the left eyeball as a feature and the right eyeball as another, and the network as a whole has expanded to exorbitant proportions. What we want is now to reduce the number of learned features in such a way that similar features are merged together (such as a node detecting only eyeballs), and also to reduce the overall channels in the feature maps, we can do that via 1x1 convolutions.

![1x1 convolutions](https://raw.githubusercontent.com/iamaaditya/iamaaditya.github.io/master/images/conv_arithmetic/full_padding_no_strides_transposed_small.gif)    

What a 1x1 kernel also offers us is a way to build deeper networks that understand the inputs better without much overhead costs. Interspersing our models with 1x1 convolutions is a very inexpensive way of adding more parameters.

![1x1 convolutions - to make deeper models](https://qph.fs.quoracdn.net/main-qimg-dc463d4d81d488b9a9910a8729dc82d1)

   