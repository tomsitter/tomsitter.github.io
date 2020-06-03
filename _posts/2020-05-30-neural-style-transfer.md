---
title: "Neural Style Transfer with PyTorch"
date: 2020-06-02
categories:
  - blog
tags:
  - artificial intelligence
  - neural style transfer
  - learning
  - coursera
---

One of the aspects of artificial intelligence that really caught my eye were some images I was seeing online that blended the content of one image with the style of another. Typical examples uses Van Gogh's The Starry Night or a Picasso as the style image. 

{% include figure image_path="/assets/images/gatys-nst.PNG" alt="An Example of Neural Style Transfer published by Gatys et al." caption="An Example of Neural Style Transfer" %}

Initally, it was the incredible images that I wanted to replicate. And fortunately, this was covered in an assignment in Andrew Ng's Deep Learning Specialization. There we implemented the algorithm using TensorFlow and created some simple low resolution images (due to the limited computing power behind the notebooks provided to us). I knew I would want to replicate this on my desktop computer which has a dedicated GPU.

Since I learned the algorithm once in TensorFlow, I figured I should try PyTorch on my own, and was lucky to discover that PyTorch has published [a tutorial](https://pytorch.org/tutorials/advanced/neural_style_tutorial.html) on this algorithm so I was able to get more experience seeing how it works and get more practice using PyTorch. 

The tutorial was written in a Jupyter Notebook, but for the ease of experimenting with many images and parameters easily, I wanted to write a command-line script I can use on my desktop computer. 
The result of that is [this script](https://github.com/tomsitter/pytorch-neural-style-transfer) that I encourage you to download and experiment with. I have tested in on both Windows and Ubuntu Linux using Python 3.7 and 3.8. I've uploaded a few example images to the repository so you can use to easily get started. Check out the readme there for some instructions.

`python main.py --content='./examples/bootsy.jpg' --style='./examples/picasso.jpg' --style_weight=500000 --steps=750 --random_input`

{% include figure image_path="/assets/images/bootsy.png" alt="Neural Style Transfer on my cat Bootsy using a Picasso painting" caption="Neural Style Transfer on my cat Bootsy using a Picasso painting." %}

The thing I find really interesting about neural style transfer is that, in order to extract the "artistic style" of an image, you are peaking into a pre-trained convolutional neural network (in my case, a VGG-19) and seeing the filters that are activated at each layer. These filters are "learned" during the training of the network, with deeper filters looking for the content of the images and shallower layers looking at pixel values. By choosing the layers to include during Neural Style Transfer you can actually see what each of the layers are looking for.


This tutorial is also an example intro to PyTorch since you must create your own loss functions (to tell how far off from the content and style your image is), and you must understand the model architecture since you have to insert your loss functions into the model at the appropriate layers. I could go into details here, but the paper itself is actually quite readable so I'll direct you there (see references below).

Here's another bonus generated image of Bootsy. I've included her picture on GitHub, so you too can enjoy her cute little face.

{% include figure image_path="/assets/images/bonus_bootsy.jpg" alt="Neural Style Transfer on my cat Bootsy using a Picasso painting" caption="Neural Style Transfer on my cat Bootsy using a Picasso painting." class="half" %}


### References

1) Gatys, L., Ecker, A., & Bethge, M. (2016). A Neural Algorithm of Artistic Style. Journal of Vision, 16(12), 326. doi: 10.1167/16.12.326. Retrieved from: https://arxiv.org/pdf/1508.06576.pdf