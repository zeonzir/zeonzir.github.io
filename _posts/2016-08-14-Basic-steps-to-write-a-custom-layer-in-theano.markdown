---
layout: post
title:  "Basic steps to write a custom layer in theano"
date:   2016-08-29 07:33:11 -0400
categories: jekyll update
---
# Introduction
For the un-initiated, convolutional neural networks may seem like a plug-n-play debug, akin to the usb port, where everything begins to work out perfectly. However, when we begin to delve deeper, we see the cracks appearing in conventional neural network architectures as applied to real-world problems. We begin to expect more and more out of these "black-boxes" without first understanding them.

Fortunately, over the recent years this trend has changed and for the better. As they are being studied in detail, more and more people are beginning to uncover the limits and potential of the neural network architecture and tweaking it to their benefit. 

This post is an effort to help direct the un-initiated towards how to play around with "Theano" in order to maximize the potential of neural network for ones' own purpose. 

# Basic Structure
As mentioned briefly, we will work theano as the programming language of choice and its extension of lasagne. Also, the basic directory structure adopted is as follows,

Main Directory
|                       
|training program.py
|loadData.py
|computeMean.py
|Custom layer directory
    |Custom layer.py
        
For the purposes of this tutorial, we will work on the base [TransformerLayer code][STN] and try to modify it.
                    
# Tools to help in debugging 
One of the most important tools in one's armory when trying to handle modifications are the debugging tools of the framework. Based on their impact, the prototyping time can either be cut in half or increased by the same amount.

Currently, there are three tools I am using to help me debug the custom layer code in theano.

1. 

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
[STN]: https://github.com/skaae/transformer_network
